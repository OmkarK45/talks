# The Combobox Iceberg: Why We Use Downshift

## The Problem: "It's Just a Search Input, Right?"

A product designer says: _"Can we add autocomplete to the search? Just show suggestions as the user types."_

Sounds simple. Let's see what's actually involved.

---

## How Users Suffer Without Proper Combobox Implementation

- **Keyboard users** can't navigate suggestions without mouse
- **Screen reader users** don't know how many results appeared
- **Fast typers** trigger excessive API calls, see flickering results
- **Mobile users** can't dismiss the dropdown easily
- **Anyone** who clicks outside expects the dropdown to close (but it doesn't)
- **Tab users** accidentally select the wrong item
- **Escape key** doesn't close the panel (or closes the whole modal)

---

## The Manual Implementation Attempt

Let's try building a combobox from scratch. We'll track everything we need to handle.

### Step 1: Basic UI

```tsx
// Looks simple enough...
const SearchCombobox = () => {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div>
      <input
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        onFocus={() => setIsOpen(true)}
      />
      {isOpen && (
        <ul>
          {results.map((item) => (
            <li key={item.id} onClick={() => handleSelect(item)}>
              {item.label}
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};
```

**Status:** Basic structure. **But we're just getting started...**

---

### Step 2: Keyboard Navigation

Users need to navigate with arrow keys. Let's add that.

```tsx
const [highlightedIndex, setHighlightedIndex] = useState(-1);

const handleKeyDown = (e) => {
  switch (e.key) {
    case 'ArrowDown':
      e.preventDefault(); // Stop page scroll
      setHighlightedIndex((prev) =>
        prev < results.length - 1 ? prev + 1 : prev,
      );
      break;
    case 'ArrowUp':
      e.preventDefault();
      setHighlightedIndex((prev) => (prev > 0 ? prev - 1 : prev));
      break;
    case 'Enter':
      if (highlightedIndex >= 0) {
        handleSelect(results[highlightedIndex]);
      }
      break;
    case 'Escape':
      setIsOpen(false);
      break;
  }
};
```

**Wait, we forgot:**

- What if there are no results? Arrow keys shouldn't do anything
- Should Enter submit the form if nothing is highlighted?
- Should Escape clear the input or just close the dropdown?
- What about Home and End keys?
- What about Page Up and Page Down?

**...and we're still not done.**

---

### Step 3: Click Outside to Close

Users expect clicking outside to close the dropdown.

```tsx
const containerRef = useRef(null);

useEffect(() => {
  const handleClickOutside = (event) => {
    if (containerRef.current && !containerRef.current.contains(event.target)) {
      setIsOpen(false);
    }
  };

  document.addEventListener('mousedown', handleClickOutside);
  return () => document.removeEventListener('mousedown', handleClickOutside);
}, []);
```

**Wait, we forgot:**

- What if the click is on a portal/modal that's technically outside?
- What if the user clicks a button that opens another dropdown?
- What about touch events on mobile?
- Memory leak if component unmounts during event

**...and we're still not done.**

---

### Step 4: Focus Management

When dropdown opens, what gets focus? When it closes, where does focus go?

```tsx
const inputRef = useRef(null);
const listRef = useRef(null);

// Focus input on mount
useEffect(() => {
  inputRef.current?.focus();
}, []);

// When dropdown closes, return focus to input
useEffect(() => {
  if (!isOpen) {
    inputRef.current?.focus();
  }
}, [isOpen]);

// Scroll highlighted item into view
useEffect(() => {
  if (highlightedIndex >= 0 && listRef.current) {
    const item = listRef.current.children[highlightedIndex];
    item?.scrollIntoView({ block: 'nearest' });
  }
}, [highlightedIndex]);
```

**Wait, we forgot:**

- What if the input loses focus to a button inside the dropdown?
- What if the user tabs out of the combobox entirely?
- `scrollIntoView` can scroll the whole page, not just the dropdown
- What about virtual scrolling for long lists?

**...and we're still not done.**

---

### Step 5: ARIA Attributes

Screen readers need to understand this is a combobox, not just an input.

```tsx
<div role="combobox" aria-expanded={isOpen} aria-haspopup="listbox">
  <input
    aria-autocomplete="list"
    aria-controls="search-results"
    aria-activedescendant={
      highlightedIndex >= 0 ? `result-${highlightedIndex}` : undefined
    }
  />
  <ul id="search-results" role="listbox" aria-label="Search results">
    {results.map((item, index) => (
      <li
        key={item.id}
        id={`result-${index}`}
        role="option"
        aria-selected={index === highlightedIndex}
      >
        {item.label}
      </li>
    ))}
  </ul>
</div>
```

**Wait, we forgot:**

- Announce result count when results change (`aria-live`)
- Announce when loading (`aria-busy`)
- Announce when selection is made
- What if some items are disabled? (`aria-disabled`)
- What if items are grouped? (`role="group"`)
- Screen reader should announce "X of Y results" when navigating

**...and we're still not done.**

---

### Step 6: Debouncing

We can't make API calls on every keystroke.

```tsx
const [debouncedQuery] = useDebounce(query, 300);

useEffect(() => {
  if (debouncedQuery.length >= 3) {
    fetchResults(debouncedQuery);
  }
}, [debouncedQuery]);
```

**Wait, we forgot:**

- What if user types fast and then deletes? Stale results may appear
- What if requests come back out of order? Race condition
- Should we cancel pending requests?
- What's the right debounce timing? 300ms? 500ms?
- What if user presses Enter before debounce fires?

**...and we're still not done.**

---

### Step 7: Input Value Management

What happens to the input value when user selects an item?

```tsx
const handleSelect = (item) => {
  setQuery(item.label); // Fill input with selected value?
  setSelectedItem(item);
  setIsOpen(false);
};
```

**Wait, we forgot:**

- What if we don't want to fill the input? (search-as-you-type)
- What if the selected value differs from display value?
- Should selecting an item clear the input or keep it?
- What if user edits after selecting? Should selection clear?
- Should we show the selected item differently?

**...and we're still not done.**

---

### Step 8: Edge Cases

Here's what else we haven't handled:

#### Empty States

- No results found
- Query too short
- Error fetching results
- Initial empty state

#### Loading States

- Show spinner while fetching
- Disable keyboard nav while loading?
- What if user keeps typing while loading?

#### Multi-select

- What if user can select multiple items?
- How do we show selected items?
- How do we remove selected items?

#### Groups and Headers

- Results grouped by category
- Headers shouldn't be selectable
- Keyboard nav should skip headers

#### Mobile-Specific

- Virtual keyboard covers dropdown
- Touch scrolling in dropdown
- Touch to select vs scroll

#### Internationalization

- RTL languages (arrow keys reversed)
- Screen reader text localization
- Different IME behaviors (Chinese, Japanese input)

**...and we're STILL not done.**

---

### Step 9: The Tab Key Problem

What happens when user presses Tab?

```tsx
case 'Tab':
  // Option A: Close dropdown, move to next element
  setIsOpen(false);
  break;

  // Option B: Select highlighted item, then move
  if (highlightedIndex >= 0) {
    handleSelect(results[highlightedIndex]);
  }
  setIsOpen(false);
  break;

  // Option C: Tab through items in dropdown
  e.preventDefault();
  setHighlightedIndex(prev => prev + 1);
  break;
```

Which is correct? **It depends on the use case.** Different combobox types have different expected behaviors.

**...and we're STILL not done.**

---

### Step 10: The Highlight Reset Problem

When should `highlightedIndex` reset?

```tsx
// Reset when results change?
useEffect(() => {
  setHighlightedIndex(-1);
}, [results]);

// Reset when query changes?
useEffect(() => {
  setHighlightedIndex(-1);
}, [query]);

// Reset when dropdown opens?
useEffect(() => {
  if (isOpen) setHighlightedIndex(-1);
}, [isOpen]);
```

**Each has different UX implications.** And they interact in subtle ways.

**...and we're STILL not done.**

---

## The Full Checklist (What Downshift Handles)

Here's everything a proper combobox needs:

### Keyboard Navigation

- [ ] Arrow Down — move highlight down
- [ ] Arrow Up — move highlight up
- [ ] Enter — select highlighted item
- [ ] Escape — close dropdown
- [ ] Home — jump to first item
- [ ] End — jump to last item
- [ ] Page Up — jump up by page
- [ ] Page Down — jump down by page
- [ ] Tab — complex behavior depending on context
- [ ] Prevent default on navigation keys
- [ ] Handle when list is empty
- [ ] Handle circular navigation (optional)

### Mouse/Touch Interaction

- [ ] Click item to select
- [ ] Click outside to close
- [ ] Hover to highlight (optional)
- [ ] Touch scroll vs touch select
- [ ] Double-click handling
- [ ] Mouse enter/leave highlighting

### Focus Management

- [ ] Focus input on mount
- [ ] Return focus on close
- [ ] Track focus within component
- [ ] Handle focus loss gracefully
- [ ] Scroll highlighted item into view

### ARIA & Screen Readers

- [ ] `role="combobox"`
- [ ] `role="listbox"`
- [ ] `role="option"`
- [ ] `aria-expanded`
- [ ] `aria-activedescendant`
- [ ] `aria-controls`
- [ ] `aria-autocomplete`
- [ ] `aria-selected`
- [ ] `aria-disabled`
- [ ] `aria-live` for result announcements
- [ ] `aria-busy` during loading
- [ ] Unique IDs for ARIA relationships

### State Management

- [ ] Open/closed state
- [ ] Input value
- [ ] Highlighted index
- [ ] Selected item(s)
- [ ] Loading state
- [ ] Error state

### Input Behavior

- [ ] Controlled vs uncontrolled
- [ ] Debouncing
- [ ] Clear button
- [ ] Placeholder text
- [ ] Min length before search

### Edge Cases

- [ ] Empty results
- [ ] Stale request handling
- [ ] Request cancellation
- [ ] Race conditions
- [ ] IME composition
- [ ] RTL support
- [ ] Disabled items
- [ ] Grouped items
- [ ] Portal rendering

**That's 50+ individual behaviors.** Each one is a potential bug if done wrong.

---

## What Downshift Gives Us

```tsx
import { useCombobox } from 'downshift';

const SearchCombobox = ({ items }) => {
  const {
    isOpen,
    getMenuProps,
    getInputProps,
    getItemProps,
    highlightedIndex,
  } = useCombobox({
    items,
    itemToString: (item) => item?.label ?? '',
    onSelectedItemChange: ({ selectedItem }) => {
      // Handle selection
    },
  });

  return (
    <div>
      <input {...getInputProps()} />
      <ul {...getMenuProps()}>
        {isOpen &&
          items.map((item, index) => (
            <li
              key={item.id}
              {...getItemProps({ item, index })}
              style={{
                backgroundColor: highlightedIndex === index ? '#eee' : 'white',
              }}
            >
              {item.label}
            </li>
          ))}
      </ul>
    </div>
  );
};
```

**That's it.** All 50+ behaviors handled. ARIA attributes injected. Keyboard navigation working. Focus management handled.

---

## The Tradeoff Analysis

| Aspect               | Manual Implementation             | Downshift           |
| -------------------- | --------------------------------- | ------------------- |
| **Initial dev time** | 3-5 days                          | 2-4 hours           |
| **Lines of code**    | 500+                              | 50                  |
| **Bugs to fix**      | Ongoing                           | Near zero           |
| **a11y coverage**    | Whatever you remember             | Complete            |
| **Maintenance**      | Every edge case is yours          | Library maintains   |
| **Bundle size**      | 0 (but your code adds up)         | ~10kb gzipped       |
| **Customization**    | Full control                      | Props and callbacks |
| **Learning curve**   | None (but you learn by suffering) | Read the docs once  |

---

## When NOT to Use Downshift

### Simple cases that don't need it:

- Static dropdown with 5 items (use `<select>`)
- No keyboard navigation required (mobile-first PWA)
- Search without suggestions (just input + submit)

### When you need something different:

- Very custom keyboard behavior
- Non-standard ARIA pattern
- Animation-heavy interactions that fight with the library

---

## Key Takeaways

1. **Combobox is 50+ behaviors** — not "just an input with a dropdown"
2. **Each behavior is a potential bug** — keyboard, mouse, touch, screen reader
3. **ARIA compliance is complex** — experts spent years on the spec
4. **Libraries exist because this is hard** — don't reinvent wheels
5. **10kb of dependency < 500 lines of bugs** — the math is clear
6. **Focus on features, not plumbing** — your users don't care how you built it

---

## Discussion Questions

- What's the most subtle combobox bug you've encountered?
- Are there cases where our combobox doesn't behave as expected?
- Should we audit our other interactive components for similar complexity?

<!--
DIAGRAM PLACEHOLDER:
"The Combobox Iceberg" - top shows simple input/dropdown,
below water shows all the hidden complexity:
- Keyboard handlers
- ARIA attributes
- Focus management
- Race conditions
- Edge cases
-->
