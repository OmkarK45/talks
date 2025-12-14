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

---

# Layered Architecture

<div class="grid grid-cols-2 gap-6 mt-6">

<div>
<div class="text-sm opacity-50 mb-3">Benefits</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Fewer files touched</span> — changes stay contained</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Faster onboarding</span> — clear patterns, less tribal knowledge</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Easier testing</span> — mock one layer, not 5 systems</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Fewer bugs</span> — clear boundaries prevent side effects</div>
</div>

<div v-click class="flex items-start gap-2">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Consistent UX</span> — centralized logic = consistent behavior</div>
</div>

</div>

<div>
<div class="text-sm opacity-50 mb-3">When to skip</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-red-400">✗</span>
  <div class="text-sm"><span class="text-red-300 font-semibold">Simple CRUD pages</span> — overkill for basic forms</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-red-400">✗</span>
  <div class="text-sm"><span class="text-red-300 font-semibold">Prototypes/MVPs</span> — adds friction when exploring</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-red-400">✗</span>
  <div class="text-sm"><span class="text-red-300 font-semibold">Isolated components</span> — a date picker doesn't need 4 layers</div>
</div>

<div v-click class="flex items-start gap-2">
  <span class="text-red-400">✗</span>
  <div class="text-sm"><span class="text-red-300 font-semibold">Throwaway code</span> — if deleted in 2 weeks, don't architect it</div>
</div>

</div>

</div>

---

# URL as State Manager

<div class="grid grid-cols-2 gap-6 mt-6">

<div>
<div class="text-sm opacity-50 mb-3">When to use</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Shareable states</span> — users can share links that restore exact view</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Survives refresh</span> — state persists without local storage</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Back/Forward navigation</span> — browser history just works</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">Bookmarkable</span> — users can save specific views</div>
</div>

<div v-click class="flex items-start gap-2">
  <span class="text-green-400">✓</span>
  <div class="text-sm"><span class="text-green-300 font-semibold">SEO friendly</span> — search engines can index different states</div>
</div>

</div>

<div>
<div class="text-sm opacity-50 mb-3">When to skip</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-yellow-400">⚠</span>
  <div class="text-sm"><span class="text-yellow-300 font-semibold">Sensitive data</span> — passwords, tokens shouldn't be in URL</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-yellow-400">⚠</span>
  <div class="text-sm"><span class="text-yellow-300 font-semibold">Ephemeral UI state</span> — modal open, tooltip visible</div>
</div>

<div v-click class="flex items-start gap-2 mb-3">
  <span class="text-yellow-400">⚠</span>
  <div class="text-sm"><span class="text-yellow-300 font-semibold">Large data</span> — URL length limits (~2000 chars)</div>
</div>

<div v-click class="flex items-start gap-2">
  <span class="text-yellow-400">⚠</span>
  <div class="text-sm"><span class="text-yellow-300 font-semibold">High-frequency updates</span> — typing in search box</div>
</div>

</div>

</div>

---
