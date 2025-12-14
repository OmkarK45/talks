# Embracing React Aria Components

## The Problem: a11y Expertise is Rare

### How Users Suffer When Developers Lack ARIA Knowledge

- Components look right but **don't work with screen readers**
- Keyboard users get **trapped** in modals they can't escape
- Focus **jumps unpredictably** after interactions
- Custom widgets are **invisible to assistive technology**
- Users with disabilities **abandon your product** for competitors

---

## Adobe's Research on Developer a11y Skills

### The Findings:

> "Building accessible components from scratch requires **deep ARIA expertise**. Most developers lack the time to learn these intricacies, leading to **inaccessible experiences**."
> — React Aria Team, Adobe

### Why ARIA is Hard:

| ARIA Concept | What Developers Think | What It Actually Requires |
|--------------|----------------------|---------------------------|
| `role="button"` | "Just add this to make it a button" | Needs keyboard handlers, focus styling, disabled state management |
| `aria-expanded` | "True when open, false when closed" | Must coordinate with `aria-controls`, announce state changes |
| `aria-live` | "Add it for dynamic updates" | Needs correct politeness level, debouncing, no repetition |
| Focus management | "Just call `.focus()`" | Restore focus on close, trap focus in modals, handle portals |

### The ARIA Spec Reality:

- **ARIA 1.2 spec** is 200+ pages
- **26 different roles** with specific requirements
- **45+ aria attributes** with complex interactions
- **Design patterns** differ by role (listbox vs combobox vs menu vs tree)
- **Browser/screen reader combinations** have bugs and inconsistencies

**Most developers don't have time to become ARIA experts.** And they shouldn't need to.

---

## The Business Case for Accessibility

### The Numbers:

| Statistic | Source |
|-----------|--------|
| **1.3 billion people** worldwide have significant disabilities | WHO |
| **15% of the global population** | That's your market |
| **71% of users with disabilities** will leave inaccessible sites | WebAIM |
| **$6.9 billion** in annual e-commerce lost to poor accessibility | Air360 |
| **2,387 web accessibility lawsuits** filed in US in 2023 | UsableNet |

### What Disability Looks Like:

| Category | Examples | % of Population |
|----------|----------|-----------------|
| Visual | Blindness, low vision, color blindness | 2.2% |
| Motor | Paralysis, tremors, limited mobility | 4.3% |
| Cognitive | Learning disabilities, ADHD, autism | 5.2% |
| Hearing | Deafness, hard of hearing | 1.5% |
| **Temporary/Situational** | Broken arm, holding baby, bright sunlight | **Everyone, sometimes** |

### The Moral Argument:

> "The power of the Web is in its universality. Access by everyone regardless of disability is an essential aspect."
> — Tim Berners-Lee, W3C Director

Building inaccessible websites is like building a store with stairs-only entrance. It's:
- Exclusionary by design
- Losing customers
- Potentially illegal
- Fixable with intentional effort

---

## What Were the Options?

| Approach | Description | Reality |
|----------|-------------|---------|
| **Ignore it** | Ship without a11y | Legal risk, lost users, ethical failure |
| **Audit & fix** | Hire a11y consultant, remediate | Expensive, doesn't prevent new issues |
| **Manual ARIA** | Learn spec, implement yourself | Time-consuming, error-prone, maintenance burden |
| **Accessibility overlays** | Third-party "fix" widgets | [Don't work](https://overlayfactsheet.com/), create legal liability |
| **Headless primitives** | React Aria, Radix, Headless UI | Correct a11y built-in, you control styling |

---

## What Was Chosen: React Aria Components

### Why React Aria:

1. **Built by Adobe's accessibility team** — years of expertise
2. **WAI-ARIA patterns implemented correctly** — spec compliance
3. **Cross-browser testing** — handles browser/screen reader bugs
4. **Hooks-first architecture** — use what you need, style how you want
5. **Zero styling opinions** — full visual control
6. **Active maintenance** — evolves with specs

### React Aria Architecture:

```
┌─────────────────────────────────────────────────────────────┐
│                    Your Component                           │
│                   (Styling, Layout)                         │
└─────────────────────────────────────────────────────────────┘
                            │ uses
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                  React Aria Hooks                           │
│        useButton, useListBox, useComboBox, useDialog        │
│     (Behavior, Keyboard, Focus, ARIA attributes)            │
└─────────────────────────────────────────────────────────────┘
                            │ uses
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                   React Stately                             │
│                  (State Management)                         │
└─────────────────────────────────────────────────────────────┘
```

---

## Example: Poorly Designed Component

### The Problem: Custom Dropdown

```tsx
// ❌ Inaccessible dropdown
const Dropdown = ({ options, onSelect }) => {
  const [isOpen, setIsOpen] = useState(false);
  
  return (
    <div className="dropdown">
      <div 
        className="dropdown-trigger"
        onClick={() => setIsOpen(!isOpen)}
      >
        Select an option
      </div>
      {isOpen && (
        <div className="dropdown-menu">
          {options.map(option => (
            <div 
              key={option.id}
              className="dropdown-item"
              onClick={() => {
                onSelect(option);
                setIsOpen(false);
              }}
            >
              {option.label}
            </div>
          ))}
        </div>
      )}
    </div>
  );
};
```

### What's Wrong:

| Issue | Impact |
|-------|--------|
| `<div>` instead of `<button>` | Not focusable, can't activate with keyboard |
| No `role` attributes | Screen reader doesn't know it's a dropdown |
| No `aria-expanded` | User doesn't know if menu is open |
| No keyboard navigation | Can't Arrow Up/Down through options |
| No focus management | Focus doesn't move to menu when opened |
| No Escape to close | Keyboard users are trapped |
| No `aria-selected` | Selected option not announced |
| No focus trap | Tab key escapes to random place |

**Screen reader experience:** "Select an option. Clickable."  
**User thinks:** "What is this? How do I interact with it?"

---

## Example: React Aria Select

```tsx
// ✅ Accessible with React Aria
import { useSelectState } from 'react-stately';
import { 
  useSelect, 
  useButton, 
  useListBox, 
  useOption 
} from 'react-aria';

const Select = ({ label, options }) => {
  const state = useSelectState({ items: options });
  const ref = useRef(null);
  const { labelProps, triggerProps, valueProps, menuProps } = useSelect(
    { label, items: options },
    state,
    ref
  );

  return (
    <div className="select-wrapper">
      <label {...labelProps}>{label}</label>
      <button {...triggerProps} ref={ref}>
        <span {...valueProps}>
          {state.selectedItem?.label ?? 'Select...'}
        </span>
      </button>
      {state.isOpen && (
        <ul {...menuProps} className="options-menu">
          {[...state.collection].map(item => (
            <Option key={item.key} item={item} state={state} />
          ))}
        </ul>
      )}
    </div>
  );
};

const Option = ({ item, state }) => {
  const ref = useRef(null);
  const { optionProps, isSelected, isFocused } = useOption(
    { key: item.key },
    state,
    ref
  );

  return (
    <li {...optionProps} ref={ref} className={`option ${isFocused ? 'focused' : ''}`}>
      {item.label}
      {isSelected && <CheckIcon />}
    </li>
  );
};
```

### What You Get:

| Feature | Automatically Handled |
|---------|----------------------|
| **Keyboard** | Space/Enter to open, Arrow keys to navigate, Escape to close |
| **ARIA** | Correct roles, states, and properties |
| **Focus** | Moves to menu on open, returns on close |
| **Screen reader** | "Select an option, combobox, expanded, 5 options, Option 1 selected" |
| **Type-ahead** | Type "ban" to jump to "Banana" |
| **Touch** | Works correctly on mobile |
| **RTL** | Arrow keys reverse in RTL languages |

---

## Complex Example: 2D Image Gallery

### The Challenge:

Build an image gallery with:
- Grid layout (4 columns)
- Keyboard navigation (Arrow keys in 2D)
- Multi-select support (Shift+Click, Cmd+Click)
- Screen reader announcements
- Focus management

### Manual Implementation:

```tsx
// ❌ Manual 2D keyboard navigation
const ImageGallery = ({ images }) => {
  const [selectedIds, setSelectedIds] = useState(new Set());
  const [focusedIndex, setFocusedIndex] = useState(0);
  const columns = 4;
  const itemRefs = useRef([]);
  
  const handleKeyDown = (e) => {
    const currentRow = Math.floor(focusedIndex / columns);
    const currentCol = focusedIndex % columns;
    
    switch (e.key) {
      case 'ArrowRight':
        e.preventDefault();
        if (currentCol < columns - 1 && focusedIndex + 1 < images.length) {
          setFocusedIndex(focusedIndex + 1);
        }
        break;
        
      case 'ArrowLeft':
        e.preventDefault();
        if (currentCol > 0) {
          setFocusedIndex(focusedIndex - 1);
        }
        break;
        
      case 'ArrowDown':
        e.preventDefault();
        if (focusedIndex + columns < images.length) {
          setFocusedIndex(focusedIndex + columns);
        }
        break;
        
      case 'ArrowUp':
        e.preventDefault();
        if (focusedIndex - columns >= 0) {
          setFocusedIndex(focusedIndex - columns);
        }
        break;
        
      case 'Home':
        e.preventDefault();
        if (e.ctrlKey) {
          setFocusedIndex(0); // First item overall
        } else {
          setFocusedIndex(currentRow * columns); // First in row
        }
        break;
        
      case 'End':
        e.preventDefault();
        if (e.ctrlKey) {
          setFocusedIndex(images.length - 1); // Last item overall
        } else {
          const rowEnd = Math.min((currentRow + 1) * columns - 1, images.length - 1);
          setFocusedIndex(rowEnd); // Last in row
        }
        break;
        
      case 'PageDown':
        e.preventDefault();
        // Jump down multiple rows
        const nextPageIndex = Math.min(focusedIndex + columns * 3, images.length - 1);
        setFocusedIndex(nextPageIndex);
        break;
        
      case 'PageUp':
        e.preventDefault();
        const prevPageIndex = Math.max(focusedIndex - columns * 3, 0);
        setFocusedIndex(prevPageIndex);
        break;
        
      case ' ':
      case 'Enter':
        e.preventDefault();
        handleSelect(images[focusedIndex].id, e.shiftKey, e.metaKey || e.ctrlKey);
        break;
        
      case 'a':
        if (e.metaKey || e.ctrlKey) {
          e.preventDefault();
          // Select all
          setSelectedIds(new Set(images.map(img => img.id)));
        }
        break;
    }
  };
  
  const handleSelect = (id, isShift, isCtrl) => {
    if (isShift && lastSelectedId) {
      // Range select: find indices, select all between
      const startIdx = images.findIndex(img => img.id === lastSelectedId);
      const endIdx = images.findIndex(img => img.id === id);
      const [min, max] = startIdx < endIdx ? [startIdx, endIdx] : [endIdx, startIdx];
      const rangeIds = images.slice(min, max + 1).map(img => img.id);
      setSelectedIds(new Set([...selectedIds, ...rangeIds]));
    } else if (isCtrl) {
      // Toggle select
      const newSelected = new Set(selectedIds);
      if (newSelected.has(id)) {
        newSelected.delete(id);
      } else {
        newSelected.add(id);
      }
      setSelectedIds(newSelected);
    } else {
      // Single select
      setSelectedIds(new Set([id]));
    }
    setLastSelectedId(id);
  };
  
  // Focus management
  useEffect(() => {
    itemRefs.current[focusedIndex]?.focus();
  }, [focusedIndex]);
  
  // Scroll into view
  useEffect(() => {
    itemRefs.current[focusedIndex]?.scrollIntoView({
      block: 'nearest',
      behavior: 'smooth'
    });
  }, [focusedIndex]);
  
  return (
    <div
      role="grid"
      aria-label="Image gallery"
      aria-multiselectable="true"
      onKeyDown={handleKeyDown}
    >
      {Array.from({ length: Math.ceil(images.length / columns) }).map((_, rowIndex) => (
        <div key={rowIndex} role="row">
          {images.slice(rowIndex * columns, (rowIndex + 1) * columns).map((image, colIndex) => {
            const index = rowIndex * columns + colIndex;
            return (
              <div
                key={image.id}
                ref={el => itemRefs.current[index] = el}
                role="gridcell"
                tabIndex={index === focusedIndex ? 0 : -1}
                aria-selected={selectedIds.has(image.id)}
                onClick={(e) => handleSelect(image.id, e.shiftKey, e.metaKey)}
                className={`
                  gallery-item
                  ${selectedIds.has(image.id) ? 'selected' : ''}
                  ${index === focusedIndex ? 'focused' : ''}
                `}
              >
                <img src={image.url} alt={image.alt} />
              </div>
            );
          })}
        </div>
      ))}
    </div>
  );
  
  // Still missing:
  // - Screen reader announcements for selection changes
  // - aria-live region for "X items selected"
  // - Disabled items handling
  // - Typeahead search
  // - RTL support (arrows reversed)
  // - Touch gestures for mobile
  // - Drag-to-select support
  // - Focus visible styling
  // - Roving tabindex management
  // - ... and more
};
```

**That's 150+ lines** and it's still incomplete. Every edge case is a potential bug.

---

### React Aria GridList Solution:

```tsx
// ✅ React Aria handles everything
import { GridList, GridListItem } from 'react-aria-components';

const ImageGallery = ({ images }) => {
  const [selectedKeys, setSelectedKeys] = useState(new Set());
  
  return (
    <GridList
      aria-label="Image gallery"
      items={images}
      selectionMode="multiple"
      selectedKeys={selectedKeys}
      onSelectionChange={setSelectedKeys}
      layout="grid"
      className="gallery-grid"
    >
      {(image) => (
        <GridListItem textValue={image.alt} className="gallery-item">
          <img src={image.url} alt={image.alt} />
          <span className="image-label">{image.name}</span>
        </GridListItem>
      )}
    </GridList>
  );
};

// CSS handles the grid layout
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
}

.gallery-item {
  &[data-focused] {
    outline: 2px solid blue;
  }
  
  &[data-selected] {
    background: lightblue;
  }
}
```

### What React Aria Provides:

| Feature | Manual Effort | React Aria |
|---------|---------------|------------|
| 2D arrow navigation | 50 lines | Built-in |
| Home/End/PageUp/Down | 20 lines | Built-in |
| Shift+Click range select | 15 lines | Built-in |
| Cmd+Click toggle | 10 lines | Built-in |
| Ctrl+A select all | 5 lines | Built-in |
| Roving tabindex | 10 lines | Built-in |
| Screen reader announcements | 20 lines | Built-in |
| Focus management | 15 lines | Built-in |
| RTL support | 20 lines | Built-in |
| Typeahead search | 30 lines | Built-in |
| **Total** | **200+ lines** | **15 lines** |

---

## React Aria Features Summary

### What You Get Out of the Box:

| Category | Features |
|----------|----------|
| **Keyboard** | Full navigation, shortcuts, typeahead |
| **Focus** | Management, restoration, trapping |
| **ARIA** | Correct roles, states, properties |
| **Selection** | Single, multiple, none, controlled/uncontrolled |
| **Interactions** | Press, hover, focus, long press |
| **Accessibility** | Screen reader tested across platforms |
| **International** | RTL, locale-aware, collation |
| **Touch** | Mobile-optimized interactions |

### Available Components:

- **Buttons:** Button, ToggleButton, Menu, MenuTrigger
- **Collections:** ListBox, GridList, Table, Tree
- **Date/Time:** Calendar, DatePicker, TimeField
- **Forms:** TextField, NumberField, SearchField, Select
- **Navigation:** Link, Tabs, Breadcrumbs
- **Overlays:** Dialog, Modal, Popover, Tooltip
- **Status:** ProgressBar, Meter, Switch

---

## The Tradeoff Summary

| Factor | Manual Implementation | React Aria |
|--------|----------------------|------------|
| **Development time** | Days to weeks | Hours |
| **a11y compliance** | Whatever you know | Full WCAG |
| **Bugs** | Continuous discovery | Near-zero |
| **Bundle size** | 0 base (but grows) | ~15-30kb |
| **Customization** | Unlimited | Very flexible |
| **Learning curve** | ARIA spec + trial/error | Library docs |
| **Maintenance** | Forever yours | Library maintains |
| **Browser testing** | You do it | They did it |

---

## When NOT to Use React Aria

### Situations where manual might be better:

1. **Very simple components** — a single button doesn't need a library
2. **Non-standard interactions** — if the spec doesn't cover your use case
3. **Extreme bundle size constraints** — embedded widgets with <10kb budget
4. **Learning purposes** — building from scratch teaches ARIA deeply
5. **Existing mature solutions** — don't migrate working accessible code

### But ask yourself:

- Will you remember all ARIA requirements in 6 months?
- Will new team members understand your custom implementation?
- Can you maintain browser compatibility as things change?

---

## Key Takeaways

1. **ARIA is complex** — 200+ page spec, 45+ attributes, countless edge cases
2. **Most developers aren't ARIA experts** — and that's okay, use primitives
3. **1+ billion people need accessibility** — it's not a niche concern
4. **Primitives provide correct behavior** — let experts handle the hard parts
5. **15 lines vs 200 lines** — the math is clear
6. **Focus on features, not plumbing** — React Aria handles the plumbing

---

## Resources

- [React Aria Documentation](https://react-spectrum.adobe.com/react-aria/)
- [React Aria Components](https://react-spectrum.adobe.com/react-aria/components.html)
- [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
- [WebAIM Million Analysis](https://webaim.org/projects/million/)
- [Overlay Fact Sheet](https://overlayfactsheet.com/)

---

## Discussion Questions

- What components in our app could benefit from React Aria?
- Are there any custom widgets we built that might have a11y issues?
- Should we create a component library with React Aria as the foundation?

<!--
DIAGRAM PLACEHOLDER:
Side-by-side comparison:
Left: Manual implementation (tall code block, many lines)
Right: React Aria (short code block)
Both with checkmarks showing what features are included
-->

