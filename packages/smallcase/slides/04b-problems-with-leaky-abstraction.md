# What's Wrong With This?

<div class="mt-8 space-y-3">

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-red-500/10 border border-red-500/30">
  <div class="i-carbon-warning-alt text-2xl text-red-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-red-300 mb-1">Component Does Too Much</div>
    <div class="text-xs opacity-70">Validation, formatting, API calls, analytics, error handling — violates Single Responsibility Principle</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-red-500/10 border border-red-500/30">
  <div class="i-carbon-connection-signal-off text-2xl text-red-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-red-300 mb-1">Tight Coupling</div>
    <div class="text-xs opacity-70">Component knows about uploadService, apiClient, draftsStorage — hard to change any dependency</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-red-500/10 border border-red-500/30">
  <div class="i-carbon-close-filled text-2xl text-red-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-red-300 mb-1">Impossible to Test</div>
    <div class="text-xs opacity-70">Need to mock 16 props for every test — setup takes longer than the actual test</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-red-500/10 border border-red-500/30">
  <div class="i-carbon-deployment-pattern text-2xl text-red-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-red-300 mb-1">Not Reusable</div>
    <div class="text-xs opacity-70">Can't reuse parts — want just the text editor? Too bad, it's buried inside</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-red-500/10 border border-red-500/30">
  <div class="i-carbon-wikis text-2xl text-red-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-red-300 mb-1">Poor Developer Experience</div>
    <div class="text-xs opacity-70">Consumer needs to understand all implementation details — abstraction leaks everywhere</div>
  </div>
</div>

</div>

---
