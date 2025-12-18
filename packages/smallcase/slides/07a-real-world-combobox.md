# Real World: Accessible Combobox

<div class="grid grid-cols-2 gap-8 mt-6">

<div>
<div class="text-sm opacity-50 mb-3">The Challenge</div>

<div class="p-4 rounded-xl bg-red-500/10 border border-red-500/30 mb-4">
  <div class="text-2xl font-bold text-red-300 mb-2">50+</div>
  <div class="text-sm opacity-70">Different interaction patterns to handle correctly</div>
</div>

<div class="text-sm space-y-2">
  <div v-click class="flex items-start gap-2">
    <div class="i-carbon-keyboard text-blue-400 mt-0.5"></div>
    <div>
      <div class="font-semibold text-blue-300">Keyboard Navigation</div>
      <div class="text-xs opacity-60">Arrow keys, Home, End, PageUp/Down, Tab, Escape</div>
    </div>
  </div>

  <div v-click class="flex items-start gap-2">
    <div class="i-carbon-checkmark text-green-400 mt-0.5"></div>
    <div>
      <div class="font-semibold text-green-300">Selection Management</div>
      <div class="text-xs opacity-60">Single/multi-select, clear, highlight, scroll to item</div>
    </div>
  </div>

  <div v-click class="flex items-start gap-2">
    <div class="i-carbon-edit text-purple-400 mt-0.5"></div>
    <div>
      <div class="font-semibold text-purple-300">Input Field State</div>
      <div class="text-xs opacity-60">Typing, filtering, autocomplete, clear button</div>
    </div>
  </div>

  <div v-click class="flex items-start gap-2">
    <div class="i-carbon-view text-yellow-400 mt-0.5"></div>
    <div>
      <div class="font-semibold text-yellow-300">Focus Management</div>
      <div class="text-xs opacity-60">Focus wrapping, restore on close, trap in popover</div>
    </div>
  </div>

  <div v-click class="flex items-start gap-2">
    <div class="i-carbon-time text-orange-400 mt-0.5"></div>
    <div>
      <div class="font-semibold text-orange-300">Async States</div>
      <div class="text-xs opacity-60">Loading, error, empty state, debouncing</div>
    </div>
  </div>

  <div v-click class="flex items-start gap-2">
    <div class="i-carbon-accessibility text-red-400 mt-0.5"></div>
    <div>
      <div class="font-semibold text-red-300">ARIA Attributes</div>
      <div class="text-xs opacity-60">aria-expanded, aria-controls, aria-activedescendant, role</div>
    </div>
  </div>

  <div v-click class="flex items-start gap-2">
    <div class="i-carbon-screen text-pink-400 mt-0.5"></div>
    <div>
      <div class="font-semibold text-pink-300">Screen Reader Support</div>
      <div class="text-xs opacity-60">Announcements, selected count, filter results</div>
    </div>
  </div>

  <div v-click class="flex items-start gap-2">
    <div class="i-carbon-mobile text-teal-400 mt-0.5"></div>
    <div>
      <div class="font-semibold text-teal-300">Touch & Mobile</div>
      <div class="text-xs opacity-60">Virtual keyboard, scroll lock, viewport handling</div>
    </div>
  </div>
</div>

</div>

<div v-click>
<div class="text-sm opacity-50 mb-3">With Downshift</div>

```tsx {*}{maxHeight:'380px'}
import { useCombobox } from 'downshift'

function SearchComboBox({ items, onSelect }) {
  const {
    isOpen,
    getMenuProps,
    getInputProps,
    getItemProps,
    highlightedIndex,
  } = useCombobox({
    items,
    onSelectedItemChange: ({ selectedItem }) => {
      onSelect(selectedItem)
    },
  })

  return (
    <div>
      <label>Search</label>
      <input
        {...getInputProps()}
        placeholder="Type to search..."
      />

      <ul {...getMenuProps()}>
        {isOpen
          && items.map((item, index) => (
            <li
              key={item.id}
              {...getItemProps({ item, index })}
              style={{
                backgroundColor:
                  highlightedIndex === index
                    ? 'lightgray'
                    : 'white',
              }}
            >
              {item.name}
            </li>
          ))}
      </ul>
    </div>
  )
}
```

<div class="mt-4 space-y-2">
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> All 50+ interactions handled
  </div>
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Complete ARIA implementation
  </div>
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Keyboard, mouse, touch support
  </div>
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Screen reader announcements
  </div>
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Focus management & restoration
  </div>
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Flexible styling (no CSS imposed)
  </div>
</div>

</div>

</div>

<div v-click class="mt-6 text-center p-4 rounded-xl bg-purple-500/10 border border-purple-500/30">
  <div class="text-lg font-semibold text-purple-300">
    ~20 lines of code vs ~800 lines with all edge cases
  </div>
</div>

---
