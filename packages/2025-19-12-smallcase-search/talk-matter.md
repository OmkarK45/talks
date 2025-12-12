# 🎯 Search Architecture: A Deep Dive

## Building a Search Engine for smallcase

*A technical pitch on architecture decisions, accessibility, and maintainable CSS*

---

## Part 1: Core Principles

---

### 🧠 Philosophy: Two Consumers, One Solution

> **"The code you write has two consumers: developers and users. Solve for developers, and you automatically solve for users."**

When building features, we often think only about the end user. But code has another consumer — the **next developer** who reads, maintains, or extends it.

```
┌─────────────────────────────────────────────────────┐
│                  YOUR CODE                          │
├─────────────────────────────────────────────────────┤
│                                                     │
│    Developer Experience (DX)                        │
│    ├── Clear abstractions                           │
│    ├── Predictable APIs                             │
│    ├── Self-documenting code                        │
│    │                                                │
│    └──────► Accelerates ──────►  User Experience    │
│                                   ├── Fast features │
│                                   ├── Fewer bugs    │
│                                   └── Consistency   │
└─────────────────────────────────────────────────────┘
```

**Tasteful interfaces matter.** When you expose better DX, you accelerate UX delivery.

#### Example from our codebase:

```typescript
// Bad DX → Slow UX iteration
const handleFilterChange = (filterId, value, category, config, currentFilters...) => {
  // Developer has to know 6 parameters
  // Easy to mess up, hard to extend
}

// Good DX → Fast UX iteration
const { onFilterChange } = useSearchPageContext();
onFilterChange('VOLATILITY', 'LOW');
// Developer calls one method. Context handles the rest.
```

The developer doesn't need to know *how* filters work internally. They just call the method. **This is a tasteful interface.**

---

### 🔍 The Vision: smallcase as a Search Engine

What was missing in our existing search?

| Before | After |
|--------|-------|
| Basic text matching | Multi-asset search (stocks, MFs, smallcases) |
| No filtering | Config-driven filters from CMS |
| No sorting | Dynamic sort options |
| Results lost on refresh | URL preserves entire state |
| Mobile = Desktop | Responsive UX (All tab on mobile) |
| No suggestions | Popular + Recent searches |

**The goal:** Make smallcase behave like a search engine where users can:
- Search across asset types
- Apply filters and sorts
- Share exact search states via URL
- Return to their exact search context

---

### 🔗 URL as State Manager

> **"Why does the URL matter so much?"**

The URL is the **only state that survives**:
- Page refreshes
- Copy-paste sharing
- Browser back/forward
- Bookmarks

```
/search/smallcases?q=green&sortBy=RETURNS_1Y&filters.VOLATILITY[]=LOW
```

This URL contains:
- **Mode**: search
- **Category**: smallcases
- **Query**: "green"
- **Sort**: 1-year returns
- **Filter**: Low volatility

**The user can share this link, and the recipient sees the exact same results.**

#### Why layers matter

```
┌─────────────────────────────────────────────────────────────┐
│                         URL                                 │
│            /search/smallcases?sortBy=RETURNS_1Y             │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    useUrlTabParams                          │
│              Decodes URL → { sortBy: 'RETURNS_1Y' }         │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                  SearchPageContext                          │
│              Provides: onSortChange(newSort)                │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                     SortByButton                            │
│              <button onClick={() => onSortChange('...')}>   │
└─────────────────────────────────────────────────────────────┘
```

**The button doesn't care how the URL is updated.** It just calls `onSortChange()`.

This separation means:
- Button component is reusable
- URL logic is centralized
- Testing is easier (mock context, not router)

---

### 🧅 Thinking in Layers

How do you break down complex flows?

#### Simple Example: Making Coffee ☕

```
Layer 1: User Intent      → "I want coffee"
Layer 2: Interface        → Press button on machine
Layer 3: Business Logic   → Grind beans, heat water, brew
Layer 4: Infrastructure   → Electricity, water supply
```

The user doesn't think about electricity. They press a button.

#### Applied to Search:

```
Layer 1: User Intent      → "Show me low volatility smallcases"
Layer 2: Interface        → Click filter checkbox
Layer 3: Business Logic   → Update URL, transform to API params
Layer 4: Infrastructure   → React Query, API calls, caching
```

Each layer has **one job** and communicates through **clear interfaces**.

```typescript
// Layer 2: Interface (Component)
<CheckboxGroupList
  onChange={(value) => onFilterChange('VOLATILITY', value)}
/>

// Layer 3: Business Logic (Context)
const onFilterChange = (key, value) => {
  const updatedFilters = processFilterUpdate({...});
  updateQueryParams({ filters: updatedFilters });
};

// Layer 4: Infrastructure (Hook)
const useDiscoverQuery = (params) => {
  return useInfiniteQuery({
    queryFn: () => getMultiAssetDiscover(params),
    ...
  });
};
```

---

### 🎭 Why Context Made Sense

For this feature, React Context was the right choice over Redux/Zustand:

| Requirement | Context | Redux/Zustand |
|-------------|---------|---------------|
| Scoped to feature | ✅ Natural | ⚠️ Global store |
| URL sync | ✅ Co-located | ❌ Separate middleware |
| SSR hydration | ✅ Simple | ⚠️ Complex setup |
| Bundle size | ✅ Zero | ❌ Additional deps |
| Tab state persistence | ✅ Local state | ⚠️ Overkill |

**Context gives us:**
- Feature-scoped state
- Clear provider boundaries
- No action/reducer boilerplate
- Natural composition with hooks

```tsx
// Clean provider hierarchy
<SearchPageContextProvider>
  {' '}
  {/* State + Actions */}
  <TrackingContextProvider>
    {' '}
    {/* Analytics */}
    <SearchPage />
  </TrackingContextProvider>
</SearchPageContextProvider>
```

---

## Part 2: Accessibility (a11y)

---

### ♿ a11y is for Everyone

> **"Accessibility means your app cares for all users deeply, unbiased."**

Common misconception: a11y is only for disabled users.

**Reality:** a11y improvements help everyone:

| a11y Feature | Helps Users With... | Also Helps... |
|--------------|---------------------|---------------|
| Keyboard navigation | Motor impairments | Power users, broken trackpad |
| Focus indicators | Visual impairments | Everyone in bright sunlight |
| Screen reader labels | Blindness | SEO, testing automation |
| Color contrast | Color blindness | Everyone on cheap monitors |
| Focus traps in modals | Cognitive load | Everyone (prevents confusion) |

**Good a11y is good UX.**

---

### 🎹 The Keyboard Navigation Problem

Let's say you need keyboard navigation in a 2D image grid.

#### ❌ The Manual Approach (Unmaintainable)

```tsx
function ImageGrid({ items }) {
  const [focusedIndex, setFocusedIndex] = useState(0)
  const columns = 3

  const handleKeyDown = (e) => {
    switch (e.key) {
      case 'ArrowRight':
        setFocusedIndex(prev =>
          prev < items.length - 1 ? prev + 1 : prev
        )
        break
      case 'ArrowLeft':
        setFocusedIndex(prev => prev > 0 ? prev - 1 : prev)
        break
      case 'ArrowDown':
        setFocusedIndex(prev =>
          prev + columns < items.length ? prev + columns : prev
        )
        break
      case 'ArrowUp':
        setFocusedIndex(prev =>
          prev - columns >= 0 ? prev - columns : prev
        )
        break
      case 'Home':
        setFocusedIndex(0)
        break
      case 'End':
        setFocusedIndex(items.length - 1)
        break
      case 'Enter':
      case ' ':
        handleSelect(focusedIndex)
        break
    }
  }

  // Now you need to:
  // - Manage focus refs for each item
  // - Handle edge cases (wrapping, empty grid)
  // - Support multi-select
  // - Announce changes to screen readers
  // - Handle disabled items
  // - Support typeahead search
  // ... 200+ more lines
}
```

This is:
- Error-prone
- Hard to test
- Missing edge cases
- Not screen-reader friendly
- A maintenance nightmare

#### ✅ The React Aria Approach (Maintainable)

Using [React Aria Components](https://react-spectrum.adobe.com/react-aria/examples/image-grid.html):

```tsx
import { ListBox, ListBoxItem } from 'react-aria-components'

function ImageGrid({ items }) {
  return (
    <ListBox
      aria-label="Images"
      items={items}
      selectionMode="multiple"
      layout="grid"
    >
      {item => (
        <ListBoxItem textValue={item.name}>
          <img src={item.url} alt={item.alt} />
          <Text slot="label">{item.name}</Text>
        </ListBoxItem>
      )}
    </ListBox>
  )
}
```

**You get for free:**
- ✅ Full keyboard navigation (arrows, home, end, pageup/down)
- ✅ Multi-select with Shift+Click, Cmd+Click
- ✅ Screen reader announcements
- ✅ Focus management
- ✅ Typeahead search
- ✅ RTL support
- ✅ Touch support

**Same outcome. 10x less code. 100x fewer bugs.**

---

### 🎯 Real a11y Use Cases

#### Focus Traps (Modals)

When a modal opens, focus should be **trapped** inside it:

```
┌─────────────────────────────────────────┐
│  Modal                                  │
│  ┌─────────────────────────────────┐    │
│  │  [Input Field]        ← Focus   │    │
│  │  [Submit Button]                │    │
│  │  [Cancel Button]                │    │
│  └─────────────────────────────────┘    │
│                                         │
│  Tab cycles within modal only           │
│  Background is inert                    │
└─────────────────────────────────────────┘
```

Without focus trap:
- User tabs out of modal into invisible background
- Confusing for keyboard + screen reader users

#### Button Outlines (`:focus-visible`)

```css
/* Bad: Removes outlines entirely */
button:focus {
  outline: none; /* ❌ Keyboard users can't see focus */
}

/* Good: Only hide for mouse users */
button:focus:not(:focus-visible) {
  outline: none;
}

button:focus-visible {
  outline: 2px solid var(--color-blue);
  outline-offset: 2px;
}
```

This keeps outlines for keyboard users while hiding them for mouse clicks.

---

## Part 3: Maintainable CSS with Data Attributes

---

### 📊 Data Attributes > Boolean Props

Traditional approach: Pass booleans to components, use ternaries in JSX:

```tsx
// ❌ Unmaintainable: Logic scattered across TSX and CSS
function SearchComboBox() {
  const [isOpen, setIsOpen] = useState(false)
  const [isSticky, setIsSticky] = useState(false)

  return (
    <div
      className={`
        search-container
        ${isOpen ? 'search-container--open' : ''}
        ${isSticky ? 'search-container--sticky' : ''}
        ${isOpen && isSticky ? 'search-container--open-sticky' : ''}
      `}
    >
      <div
        className={`
          search-bar
          ${isOpen ? 'search-bar--open' : ''}
        `}
      >
        <SearchIcon
          className={`
            icon
            ${isSticky ? 'icon--small' : 'icon--large'}
            ${isOpen && isSticky ? 'icon--large' : ''}
          `}
        />
      </div>
    </div>
  )
}
```

**Problems:**
- Class name explosion
- Logic duplicated in TSX and CSS
- Hard to trace which styles apply when
- Merge conflicts in className strings

---

### ✅ The Data Attribute Pattern

```tsx
// ✅ Maintainable: State expressed as data, CSS handles styling
function SearchComboBox() {
  const [isOpen, setIsOpen] = useState(false)

  return (
    <div
      className="search-container"
      data-combobox-open={isOpen}
    >
      <div className="search-bar">
        <SearchIcon className="search-icon" />
      </div>
    </div>
  )
}
```

```css
/* All conditional styling lives in CSS */
.search-container {
  transition: all 0.2s ease;
}

/* When open */
.search-container[data-combobox-open='true'] {
  box-shadow: 0px 0px 24px 0px rgba(var(--color-blue-rgb), 0.24);
}

/* Nested elements respond to parent state */
[data-combobox-open='true'] .search-bar {
  border-color: var(--color-blue);
  border-bottom-radius: 0;
}

/* Compound states */
[data-is-sticky='true'] .search-icon {
  height: 20px;
  width: 20px;
}

[data-is-sticky='true'][data-combobox-open='true'] .search-icon {
  height: 24px;
  width: 24px;
}
```

---

### 🔍 Real Example: SearchComboBox.module.css

From our actual codebase:

```css
/* The container manages the open/closed state */
.search-container[data-combobox-open='true'] {
  box-shadow: 0px 0px 24px 0px rgba(var(--color-blue-rgb), 0.24);
  overflow: visible;
}

/* Child elements respond to parent's data attribute */
[data-combobox-open='true'] .search-bar-container {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.search-container:not([data-combobox-open='true']) .search-bar-container {
  border-radius: 8px;
}

/* No box shadow on hover when panel is open */
[data-combobox-open='true'] [data-search-input]:hover {
  box-shadow: none;
}

/* Sticky + Open compound state */
[data-is-sticky='true'] .search-bar-search-icon {
  height: 20px;
  width: 20px;
}

[data-is-sticky='true'][data-combobox-open='true'] .search-bar-search-icon {
  height: 24px;
  width: 24px;
}
```

**Benefits:**
- **Single source of truth**: All style variants in CSS
- **Readable selectors**: `[data-combobox-open='true']` is self-documenting
- **Easy to trace**: Search for `data-combobox-open` to find all related styles
- **Compound states**: `[data-a][data-b]` naturally expresses AND logic
- **DevTools friendly**: See state directly in Elements panel

---

### 🆚 Comparison

| Aspect | Boolean Props + Ternaries | Data Attributes |
|--------|---------------------------|-----------------|
| TSX complexity | High (class name logic) | Low (just data attrs) |
| CSS complexity | Low (simple classes) | Medium (attribute selectors) |
| Single source of truth | ❌ Split across files | ✅ CSS owns all styling |
| Debugging | Hard (trace through JS) | Easy (visible in DOM) |
| Compound states | Exponential classes | Natural CSS selectors |
| React re-renders | On every state change | Same (but less JS work) |

---

## Part 4: Closing Thoughts

---

### 🏆 What We Built

A search architecture that:

1. **Treats URL as state** — Shareable, bookmarkable, SEO-friendly
2. **Uses config-driven UI** — Filters/sorts from CMS, not hardcoded
3. **Separates concerns cleanly** — Layers for data, state, UI
4. **Prioritizes accessibility** — Keyboard nav, screen readers, focus management
5. **Keeps CSS maintainable** — Data attributes over boolean props

---

### 💡 Key Takeaways

> **For Developers:**

1. **Solve for DX first.** Good abstractions accelerate feature delivery.
2. **URL is your friend.** Make state shareable by default.
3. **Think in layers.** Each layer should have one job.
4. **Don't reinvent a11y.** Use React Aria or similar libraries.
5. **CSS can own conditional styling.** Data attributes are powerful.

> **For Users:**

They don't know any of this. They just experience:
- Fast, responsive search
- Working back button
- Shareable links
- Keyboard navigation that works
- Consistent, polished UI

**That's the goal.**

---

### 🚀 What's Next?

- [ ] Voice search integration
- [ ] AI-powered suggestions
- [ ] Search analytics dashboard
- [ ] Personalized ranking
- [ ] Saved searches

---

## Resources

- [React Aria Components](https://react-spectrum.adobe.com/react-aria/)
- [React Aria Grid Example](https://react-spectrum.adobe.com/react-aria/examples/image-grid.html)
- [Downshift (Combobox)](https://www.downshift-js.com/)
- [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/standards-guidelines/wcag/)

---

*Built with ❤️ by the smallcase frontend team*
