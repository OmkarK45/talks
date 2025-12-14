# What Slows Teams Down?

<div class="grid grid-cols-3 gap-6 mt-12">
  <div v-click class="p-6 rounded-xl bg-red-500/10 border border-red-500/30">
    <div class="i-carbon-warning-alt text-3xl text-red-400 mb-4"></div>
    <div class="text-lg font-semibold text-red-300 mb-2">Leaky Abstractions</div>
    <div class="text-sm opacity-70">Components know too much — URL encoding, Redux, analytics, API calls all in one place</div>
  </div>

  <div v-click class="p-6 rounded-xl bg-red-500/10 border border-red-500/30">
    <div class="i-carbon-scatter-matrix text-3xl text-red-400 mb-4"></div>
    <div class="text-lg font-semibold text-red-300 mb-2">Scattered State</div>
    <div class="text-sm opacity-70">Filters in Redux, sort in URL, pagination in component state — sync bugs everywhere</div>
  </div>

  <div v-click class="p-6 rounded-xl bg-red-500/10 border border-red-500/30">
    <div class="i-carbon-user-speaker text-3xl text-red-400 mb-4"></div>
    <div class="text-lg font-semibold text-red-300 mb-2">Tribal Knowledge</div>
    <div class="text-sm opacity-70">New team members take months to understand — patterns live in people's heads, not code</div>
  </div>
</div>

---
