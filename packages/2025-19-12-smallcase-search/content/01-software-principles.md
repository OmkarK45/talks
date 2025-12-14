# Software Principles & Layered Architecture

## The Problem: How Users (and Developers) Suffer

### Without Clear Architecture:

- **New team members** take months to understand the codebase
- **Adding a simple filter** requires touching 6+ files across unrelated directories
- **Debugging** becomes archaeology — tracing through spaghetti code to find where state lives
- **State synchronization bugs** — filters in Redux, sort in URL, pagination in component state
- **Regression risk** — changing one thing breaks three others because everything is coupled

### Real-World Example (Bad):

```tsx
// ❌ Component knows too much
const FilterButton = ({ filterId, value }) => {
  const router = useRouter();
  const dispatch = useDispatch();
  const analytics = useAnalytics();
  const { refetch } = useQuery(...);

  const handleClick = () => {
    // Component knows about URL encoding
    const encoded = encodeURIComponent(JSON.stringify({ [filterId]: value }));
    router.push(`/search?filters=${encoded}`);

    // Component knows about Redux structure
    dispatch({ type: 'UPDATE_FILTER', payload: { filterId, value } });

    // Component knows about analytics payload shape
    analytics.track('filter_applied', {
      filter_id: filterId,
      filter_value: value,
      timestamp: Date.now()
    });

    // Component knows about data fetching
    refetch();
  };

  return <button onClick={handleClick}>Apply</button>;
};
```

**Problems with this approach:**

- 6 parameters of implicit knowledge required
- Cannot reuse this button elsewhere without carrying all dependencies
- Testing requires mocking router, Redux, analytics, and React Query
- Any change to URL encoding requires updating every component that touches URLs

---

## What Were the Options?

| Option                  | Description                            | Pros                                                  | Cons                                                                   |
| ----------------------- | -------------------------------------- | ----------------------------------------------------- | ---------------------------------------------------------------------- |
| **Redux/Zustand**       | Global state management                | Centralized state, DevTools                           | Global by default, URL sync requires middleware, additional dependency |
| **Component State**     | Local useState/useReducer              | Simple, no dependencies                               | State lost on unmount, no URL persistence, prop drilling               |
| **URL Only**            | Query params as state                  | Shareable, survives refresh                           | Complex encoding, no derived state                                     |
| **React Context + URL** | Feature-scoped context synced with URL | Scoped state, URL as source of truth, zero extra deps | Requires thoughtful design, provider hierarchy                         |

---

## What Was Chosen: Layered Architecture with Context

### The Architecture:

```
┌─────────────────────────────────────────────────────────────┐
│                         URL                                 │
│            /search/smallcases?sortBy=RETURNS_1Y             │
│                    (Source of Truth)                        │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    useUrlTabParams                          │
│              Decode / Encode layer                          │
│     (Transforms URL ↔ structured params)                    │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                  SearchPageContext                          │
│         Actions: onFilterChange, onSortChange               │
│         State: current filters, sort, category              │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                     UI Components                           │
│         FilterChip, SortDropdown, SearchInput               │
│           (Know nothing about URL or API)                   │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    Infrastructure                           │
│              React Query / API Calls                        │
└─────────────────────────────────────────────────────────────┘
```

### Real-World Example (Good):

```tsx
// ✅ Component knows only what it needs
const FilterButton = ({ filterId, value, label }) => {
  const { onFilterChange } = useSearchPageContext();

  return (
    <button onClick={() => onFilterChange(filterId, value)}>{label}</button>
  );
};

// The context handles everything else:
// - URL encoding/updating
// - Analytics tracking
// - Data refetching
// - Tab state persistence
```

**Why this is better:**

- Component has a single responsibility: respond to clicks
- Reusable anywhere that provides the context
- Testing is trivial: mock the context
- URL encoding changes require updating ONE file

---

## The Software Principles at Play

### 1. Single Responsibility Principle

Each layer has ONE job:

- `useUrlTabParams` → URL encoding/decoding
- `SearchPageContext` → State orchestration
- `FilterButton` → UI interaction

### 2. Separation of Concerns

| Layer           | Concern          | Doesn't Know About    |
| --------------- | ---------------- | --------------------- |
| URL             | Persistence      | React, Components     |
| URL Params Hook | Encoding         | Business logic, API   |
| Context         | Orchestration    | URL format, API shape |
| Components      | User interaction | URL, API, Analytics   |
| Infrastructure  | Data fetching    | UI, URL               |

### 3. Dependency Inversion

Components depend on **abstractions** (context methods), not **implementations** (router, API client).

```tsx
// Bad: Depends on implementation
const handleClick = () => router.push(`/search?sort=${value}`);

// Good: Depends on abstraction
const handleClick = () => onSortChange(value);
```

### 4. Information Hiding

Each layer hides its complexity:

- Button doesn't know about debouncing
- Context doesn't know about React Query internals
- URL layer doesn't know about filter validation rules

---

## Benefits Achieved

### For Developers:

| Metric                          | Before          | After          |
| ------------------------------- | --------------- | -------------- |
| Time to add new filter          | 2-3 days        | 30 minutes     |
| Files touched for filter change | 6+ files        | 1-2 files      |
| Onboarding time                 | Months          | Days           |
| Test setup complexity           | Mock 5+ systems | Mock 1 context |

### For Users:

- **Faster feature delivery** — less time fighting architecture
- **Fewer bugs** — clear boundaries prevent unintended side effects
- **Better UX consistency** — centralized logic means consistent behavior

### For the Business:

- **Lower maintenance cost** — easier to understand, easier to change
- **Reduced bus factor** — patterns are documented in code, not people's heads
- **Faster iteration** — product can experiment more with less dev time

---

## When Does Layered Architecture Make Sense?

### ✅ Good Fit:

- **Complex state interactions** — multiple pieces of state that affect each other
- **URL-driven features** — search, filters, pagination, tabs
- **Shareable states** — users need to share links that restore exact state
- **Team collaboration** — multiple developers working on the same feature
- **Long-lived features** — features that will be maintained and extended over time

### ❌ Poor Fit:

- **Simple CRUD pages** — overkill for a basic form
- **Prototypes/MVPs** — adds friction when you're still figuring out the feature
- **Isolated components** — a standalone date picker doesn't need 4 layers
- **Performance-critical hot paths** — layers add (minimal) indirection overhead
- **Throwaway code** — if it's getting deleted in 2 weeks, don't architect it

---

## The Tradeoff Triangle

```
                    Simplicity
                        △
                       / \
                      /   \
                     /     \
                    /       \
                   /  Choose  \
                  /   two      \
                 /_______________\
          Flexibility         Performance
```

**Our choice:** We optimized for **Simplicity** and **Flexibility** because:

- This is a long-lived, core feature
- Multiple developers contribute
- Requirements change frequently (new filters, new sort options)
- Performance cost of abstraction is negligible for this use case

---

## Key Takeaways

1. **Leaky abstractions slow teams down** — when components know too much, everything becomes harder
2. **URL as state is powerful** — for shareable, persistent features
3. **Layers work when responsibilities are clear** — each layer should have one obvious job
4. **Context beats Redux for feature-scoped state** — no global store pollution, no extra dependencies
5. **Good DX → Good UX** — faster iteration, fewer bugs, happier users

---

## Discussion Questions

- Where else in our codebase would this pattern help?
- What features are too simple for this approach?
- How do we balance architecture investment vs shipping speed?

<!--
DIAGRAM PLACEHOLDER:
Could add a flowchart showing a user action (click filter)
flowing through layers and back up with updated UI
-->
