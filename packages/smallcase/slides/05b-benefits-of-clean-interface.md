# Why This Works Better

<div class="mt-8 space-y-3">

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-green-500/10 border border-green-500/30">
  <div class="i-carbon-checkmark-filled text-2xl text-green-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-green-300 mb-1">Single Responsibility</div>
    <div class="text-xs opacity-70">Each component does one thing well — TextEditor edits, AttachmentPicker picks files, useMessages handles API</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-green-500/10 border border-green-500/30">
  <div class="i-carbon-plug text-2xl text-green-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-green-300 mb-1">Loose Coupling</div>
    <div class="text-xs opacity-70">Components communicate through clear interfaces — swap CustomGifPicker without touching other parts</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-green-500/10 border border-green-500/30">
  <div class="i-carbon-task-complete text-2xl text-green-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-green-300 mb-1">Easy to Test</div>
    <div class="text-xs opacity-70">Test each piece independently — mock one thing at a time, not 16 props</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-green-500/10 border border-green-500/30">
  <div class="i-carbon-cube text-2xl text-green-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-green-300 mb-1">Highly Reusable</div>
    <div class="text-xs opacity-70">Use TextEditor anywhere — in comments, posts, reviews. Components are like LEGO blocks</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-xl bg-green-500/10 border border-green-500/30">
  <div class="i-carbon-development text-2xl text-green-400 flex-shrink-0"></div>
  <div>
    <div class="text-base font-semibold text-green-300 mb-1">Great Developer Experience</div>
    <div class="text-xs opacity-70">Consumer doesn't need to know internals — just compose what you need, extend when you want</div>
  </div>
</div>

</div>

---
