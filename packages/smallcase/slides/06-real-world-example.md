# Real World Example: Search Page

<div class="grid grid-cols-2 gap-8">

<div>
<div class="text-sm opacity-60 mb-2">The component</div>

```tsx
const FilterButton = ({ filterId, value, label }) => {
  const { onFilterChange } = useSearchPageContext();

  return (
    <button onClick={() => onFilterChange(filterId, value)}>
      {label}
    </button>
  );
};
```

</div>

<div v-click>
<div class="text-sm opacity-60 mb-2">Usage</div>

```tsx
<FilterButton 
  filterId="marketCap" 
  value="large" 
  label="Large Cap" 
/>

<FilterButton 
  filterId="returns" 
  value="1Y" 
  label="1 Year Returns" 
/>

// Clean, simple, just works ✨
```

</div>

</div>

<v-click>

<div class="mt-6 text-center text-sm opacity-60">
  But how does <code>onFilterChange</code> actually work? →
</div>

</v-click>

---

# Real World Example: Search Page


<div class="flex justify-center mt-2">
<div class="text-left font-mono text-xs">

<div v-click class="px-3 py-1.5 rounded-lg bg-blue-500/20 border border-blue-500/40 flex items-center gap-3">
  <div class="i-carbon-link text-blue-400 text-lg"></div>
  <div class="w-56">
    <div class="text-blue-300 font-semibold text-sm">URL</div>
    <div class="opacity-50 text-2xs">/search?sortBy=RETURNS_1Y</div>
  </div>
  <div class="w-px h-6 bg-white/20"></div>
  <span class="opacity-40 text-2xs pl-2 w-32">Source of truth</span>
</div>

<div v-click class="flex justify-center text-xs opacity-30">↓</div>

<div v-click class="px-3 py-1.5 rounded-lg bg-purple-500/20 border border-purple-500/40 flex items-center gap-3">
  <div class="i-carbon-code text-purple-400 text-lg"></div>
  <div class="w-56">
    <div class="text-purple-300 font-semibold text-sm">useUrlTabParams</div>
    <div class="opacity-50 text-2xs">decode(url) → params</div>
  </div>
  <div class="w-px h-6 bg-white/20"></div>
  <span class="opacity-40 text-2xs pl-2 w-32">URL ↔ structured data</span>
</div>

<div v-click class="flex justify-center text-xs opacity-30">↓</div>

<div v-click class="px-3 py-1.5 rounded-lg bg-green-500/20 border border-green-500/40 flex items-center gap-3">
  <div class="i-carbon-flow-data text-green-400 text-lg"></div>
  <div class="w-56">
    <div class="text-green-300 font-semibold text-sm">SearchPageContext</div>
    <div class="opacity-50 text-2xs">onFilterChange(), onSortChange()</div>
  </div>
  <div class="w-px h-6 bg-white/20"></div>
  <span class="opacity-40 text-2xs pl-2 w-32">State orchestration</span>
</div>

<div v-click class="flex justify-center text-xs opacity-30">↓</div>

<div v-click class="px-3 py-1.5 rounded-lg bg-yellow-500/20 border border-yellow-500/40 flex items-center gap-3">
  <div class="i-carbon-application text-yellow-400 text-lg"></div>
  <div class="w-56">
    <div class="text-yellow-300 font-semibold text-sm">UI Components</div>
    <div class="opacity-50 text-2xs">FilterChip, SortDropdown</div>
  </div>
  <div class="w-px h-6 bg-white/20"></div>
  <span class="opacity-40 text-2xs pl-2 w-32">User interaction only</span>
</div>

<div v-click class="flex justify-center text-xs opacity-30">↓</div>

<div v-click class="px-3 py-1.5 rounded-lg bg-red-500/20 border border-red-500/40 flex items-center gap-3">
  <div class="i-carbon-cloud text-red-400 text-lg"></div>
  <div class="w-56">
    <div class="text-red-300 font-semibold text-sm">Infrastructure</div>
    <div class="opacity-50 text-2xs">useDiscoverQuery</div>
  </div>
  <div class="w-px h-6 bg-white/20"></div>
  <span class="opacity-40 text-2xs pl-2 w-32">Data fetching</span>
</div>

</div>
</div>

