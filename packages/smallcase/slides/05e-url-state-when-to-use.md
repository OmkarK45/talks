# URL as State Manager: When to Use

<div class="grid grid-cols-2 gap-4 mt-6">

<div>
<div class="text-lg font-semibold text-green-300 mb-3 flex items-center gap-2">
  <div class="i-carbon-checkmark-filled text-xl"></div>
  <span>Use It For</span>
</div>

<div class="space-y-2">
  <div v-click class="p-2 rounded-lg bg-green-500/10 border border-green-500/30">
    <div class="font-semibold text-green-300 text-xs mb-1">Search & Filters</div>
    <div class="text-xs opacity-70">Users want to share filtered views</div>
    <div class="text-xs mt-1 font-mono text-green-400">/products?q=laptop&min=500</div>
  </div>

  <div v-click class="p-2 rounded-lg bg-green-500/10 border border-green-500/30">
    <div class="font-semibold text-green-300 text-xs mb-1">Pagination & Sorting</div>
    <div class="text-xs opacity-70">Navigate back to previous results</div>
    <div class="text-xs mt-1 font-mono text-green-400">/users?page=3&sort=name</div>
  </div>

  <div v-click class="p-2 rounded-lg bg-green-500/10 border border-green-500/30">
    <div class="font-semibold text-green-300 text-xs mb-1">Tab/View Selection</div>
    <div class="text-xs opacity-70">Deep link to specific sections</div>
    <div class="text-xs mt-1 font-mono text-green-400">/dashboard?view=analytics</div>
  </div>

  <div v-click class="p-2 rounded-lg bg-green-500/10 border border-green-500/30">
    <div class="font-semibold text-green-300 text-xs mb-1">Modal/Dialog State</div>
    <div class="text-xs opacity-70">Share links that open specific modals</div>
    <div class="text-xs mt-1 font-mono text-green-400">/products/123?modal=reviews</div>
  </div>

  <div v-click class="p-2 rounded-lg bg-green-500/10 border border-green-500/30">
    <div class="font-semibold text-green-300 text-xs mb-1">Feature Flags</div>
    <div class="text-xs opacity-70">Enable features via URL for testing</div>
    <div class="text-xs mt-1 font-mono text-green-400">?debug=true&beta=new-ui</div>
  </div>
</div>

</div>

<div>
<div class="text-lg font-semibold text-red-300 mb-3 flex items-center gap-2">
  <div class="i-carbon-close-filled text-xl"></div>
  <span>Skip It For</span>
</div>

<div class="space-y-2">
  <div v-click class="p-2 rounded-lg bg-red-500/10 border border-red-500/30">
    <div class="font-semibold text-red-300 text-xs mb-1">Large Complex Objects</div>
    <div class="text-xs opacity-70">Deeply nested data structures</div>
    <div class="text-xs mt-1 opacity-60">URLs have length limits (2048 chars)</div>
  </div>

  <div v-click class="p-2 rounded-lg bg-red-500/10 border border-red-500/30">
    <div class="font-semibold text-red-300 text-xs mb-1">Transient UI State</div>
    <div class="text-xs opacity-70">Dropdown open/closed, hover states</div>
    <div class="text-xs mt-1 opacity-60">Use local component state</div>
  </div>

  <div v-click class="p-2 rounded-lg bg-red-500/10 border border-red-500/30">
    <div class="font-semibold text-red-300 text-xs mb-1">Form Draft Data</div>
    <div class="text-xs opacity-70">Unsaved form contents (use localStorage)</div>
    <div class="text-xs mt-1 opacity-60">Too much data for URL</div>
  </div>

  <div v-click class="p-2 rounded-lg bg-red-500/10 border border-red-500/30">
    <div class="font-semibold text-red-300 text-xs mb-1">Computed State</div>
    <div class="text-xs opacity-70">Values derived from other state</div>
    <div class="text-xs mt-1 opacity-60">Derive on-the-fly instead</div>
  </div>

  <div v-click class="p-2 rounded-lg bg-red-500/10 border border-red-500/30">
    <div class="font-semibold text-red-300 text-xs mb-1">Frequently Changing State</div>
    <div class="text-xs opacity-70">Slider dragging, scroll position</div>
    <div class="text-xs mt-1 opacity-60">Creates messy browser history</div>
  </div>
</div>

</div>

</div>

---
