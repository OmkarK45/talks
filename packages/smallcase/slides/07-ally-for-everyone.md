---
layout: center
---

<style>
@keyframes strike {
  0% { width: 0; }
  100% { width: 110%; }
}
.strike-animate {
  animation: strike 0.4s ease-out forwards;
}

@keyframes sparkle-float {
  0%, 100% { transform: translateY(0) scale(1); opacity: 1; }
  50% { transform: translateY(-8px) scale(1.2); opacity: 0.6; }
}
@keyframes sparkle-spin {
  0% { transform: rotate(0deg) scale(1); }
  50% { transform: rotate(180deg) scale(1.3); }
  100% { transform: rotate(360deg) scale(1); }
}
.sparkle-1 { animation: sparkle-float 1.5s ease-in-out infinite; }
.sparkle-2 { animation: sparkle-spin 2s ease-in-out infinite; animation-delay: 0.3s; }
.sparkle-3 { animation: sparkle-float 1.8s ease-in-out infinite; animation-delay: 0.6s; }
.sparkle-4 { animation: sparkle-spin 1.6s ease-in-out infinite; animation-delay: 0.9s; }
</style>

<div class="text-center">

# The Misconception

</div>

<div class="mt-12 flex flex-col items-center">
  <div class="relative max-w-2xl">
    <div class="absolute -left-12 -top-6 text-8xl opacity-20 font-serif">"</div>
    <div class="text-3xl italic opacity-80">
      Accessibility is only for disabled users
    </div>
    <div v-click class="absolute inset-0 flex items-center justify-start -ml-2">
      <div class="strike-animate h-1.5 bg-gradient-to-r from-red-500 via-red-400 to-red-500 rotate-[-2deg] rounded-full shadow-lg shadow-red-500/50"></div>
    </div>
  </div>
  
  <div v-after class="mt-10 relative">
    <span class="sparkle-1 absolute -top-5 -left-8 text-2xl text-yellow-400">✦</span>
    <span class="sparkle-2 absolute -top-3 -right-10 text-xl text-amber-300">✧</span>
    <span class="sparkle-3 absolute -bottom-3 -left-10 text-lg text-yellow-300">✦</span>
    <span class="sparkle-4 absolute -bottom-5 -right-8 text-2xl text-amber-400">✧</span>
    <div class="text-3xl text-green-400 font-semibold">
      Accessibility is for <span class="underline decoration-wavy decoration-green-400">everyone</span>
    </div>
  </div>
</div>

---

# How Users Suffer Without a11y

<div class="grid grid-cols-2 gap-4 mt-6">

<div>
<div class="text-sm opacity-50 mb-3">The Obvious Cases</div>

<div v-click class="flex items-start gap-3 p-3 rounded-lg bg-red-500/10 border border-red-500/20 mb-2">
  <div class="i-carbon-view-off text-red-400 text-xl mt-0.5"></div>
  <div>
    <div class="font-semibold text-red-300 text-sm">Blind users</div>
    <div class="text-xs opacity-60">Can't use the site if screen readers don't work</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-lg bg-red-500/10 border border-red-500/20 mb-2">
  <div class="i-carbon-accessibility text-red-400 text-xl mt-0.5"></div>
  <div>
    <div class="font-semibold text-red-300 text-sm">Motor impairments</div>
    <div class="text-xs opacity-60">Can't click small targets, need keyboard nav</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-lg bg-red-500/10 border border-red-500/20">
  <div class="i-carbon-color-palette text-red-400 text-xl mt-0.5"></div>
  <div>
    <div class="font-semibold text-red-300 text-sm">Color blindness</div>
    <div class="text-xs opacity-60">Info conveyed only through color is lost</div>
  </div>
</div>

</div>

<div>
<div class="text-sm opacity-50 mb-3">Everyone Experiences These</div>

<div v-click class="flex items-start gap-3 p-3 rounded-lg bg-blue-500/10 border border-blue-500/20 mb-2">
  <div class="i-carbon-keyboard text-blue-400 text-xl mt-0.5"></div>
  <div>
    <div class="font-semibold text-blue-300 text-sm">Power user with keyboard</div>
    <div class="text-xs opacity-60">Forced to use mouse for every action</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-lg bg-blue-500/10 border border-blue-500/20 mb-2">
  <div class="i-carbon-light text-blue-400 text-xl mt-0.5"></div>
  <div>
    <div class="font-semibold text-blue-300 text-sm">User in bright sunlight</div>
    <div class="text-xs opacity-60">Can't see low-contrast text</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-lg bg-blue-500/10 border border-blue-500/20 mb-2">
  <div class="i-carbon-user text-blue-400 text-xl mt-0.5"></div>
  <div>
    <div class="font-semibold text-blue-300 text-sm">User holding a baby</div>
    <div class="text-xs opacity-60">One hand occupied, needs keyboard shortcuts</div>
  </div>
</div>

<div v-click class="flex items-start gap-3 p-3 rounded-lg bg-blue-500/10 border border-blue-500/20">
  <div class="i-carbon-mobile text-blue-400 text-xl mt-0.5"></div>
  <div>
    <div class="font-semibold text-blue-300 text-sm">User on mobile</div>
    <div class="text-xs opacity-60">Can't tap 20px buttons with fat fingers</div>
  </div>
</div>

</div>

</div>

---

# The Business Case

<div class="grid grid-cols-2 gap-6 mt-6">

<div>
<div class="text-sm opacity-50 mb-3">The Numbers</div>

<div v-click class="flex items-center gap-4 p-3 rounded-lg bg-blue-500/10 border border-blue-500/20 mb-3">
  <div class="i-carbon-globe text-blue-400 text-3xl"></div>
  <div>
    <div class="text-2xl font-bold text-blue-300">1+ billion</div>
    <div class="text-xs opacity-60">people have disabilities globally (15% of market)</div>
  </div>
</div>

<div v-click class="flex items-center gap-4 p-3 rounded-lg bg-purple-500/10 border border-purple-500/20 mb-3">
  <div class="i-carbon-user-multiple text-purple-400 text-3xl"></div>
  <div>
    <div class="text-2xl font-bold text-purple-300">8%</div>
    <div class="text-xs opacity-60">of men have color vision deficiency</div>
  </div>
</div>

<div v-click class="flex items-center gap-4 p-3 rounded-lg bg-red-500/10 border border-red-500/20 mb-3">
  <div class="i-carbon-chart-line text-red-400 text-3xl"></div>
  <div>
    <div class="text-2xl font-bold text-red-300">70%</div>
    <div class="text-xs opacity-60">of users bounce on inaccessible sites</div>
  </div>
</div>

<div v-click class="flex items-center gap-4 p-3 rounded-lg bg-yellow-500/10 border border-yellow-500/20">
  <div class="i-carbon-money text-yellow-400 text-3xl"></div>
  <div>
    <div class="text-2xl font-bold text-yellow-300">$6.9B</div>
    <div class="text-xs opacity-60">lost annually to poor accessibility</div>
  </div>
</div>

</div>

<div>
<div class="text-sm opacity-50 mb-3">Legal Risk</div>

<div v-click class="p-4 rounded-lg bg-red-500/10 border border-red-500/30 mb-3">
  <div class="flex items-center gap-2 mb-2">
    <div class="i-carbon-warning-alt text-red-400 text-xl"></div>
    <div class="font-semibold text-red-300">SEBI Circular 2025</div>
  </div>
  <div class="text-sm opacity-70">Indian fintech apps now required to follow <span class="text-red-300 font-semibold">WCAG 2.1 AA</span> standards for accessibility compliance</div>
</div>

<div v-click class="p-4 rounded-lg bg-orange-500/10 border border-orange-500/30 mb-3">
  <div class="flex items-center gap-2 mb-2">
    <div class="i-carbon-warning-alt text-orange-400 text-xl"></div>
    <div class="font-semibold text-orange-300">ADA Lawsuits</div>
  </div>
  <div class="text-sm opacity-70">Increased <span class="text-orange-300 font-semibold">400%</span> in US since 2018</div>
</div>

<div v-click class="p-4 rounded-lg bg-amber-500/10 border border-amber-500/30">
  <div class="flex items-center gap-2 mb-2">
    <div class="i-carbon-warning-alt text-amber-400 text-xl"></div>
    <div class="font-semibold text-amber-300">European Accessibility Act</div>
  </div>
  <div class="text-sm opacity-70">Enforcement started <span class="text-amber-300 font-semibold">June 2025</span></div>
</div>

</div>

</div>

---
layout: center
---

<div class="text-center">

# Solving it correctly matters

</div>

<div class="mt-8 flex flex-col items-center">
  <div class="relative max-w-3xl">
    <div class="absolute -left-10 -top-4 text-7xl opacity-15 font-serif text-blue-400">"</div>
    <div class="text-xl italic opacity-90 leading-relaxed">
      Building accessible components from scratch requires 
      <span class="underline decoration-wavy decoration-red-400 text-red-300 font-semibold">deep ARIA expertise</span>. 
      Most developers lack the time to learn these intricacies, leading to 
      <span class="underline decoration-wavy decoration-red-400 text-red-300 font-semibold">inaccessible experiences</span>.
    </div>
    <div class="mt-6 text-sm opacity-60 flex items-center justify-end gap-2">
      <span>—</span>
      <span class="font-semibold">React Aria Team</span>
      <span class="flex items-center gap-1 text-red-400"><svg class="w-4 h-4" viewBox="0 0 32 32" fill="currentColor"><path d="M20.136 2.667H32v26.667zm-8.272 0H0v26.667zM16 12.531l7.469 16.803h-5.068l-2.136-5.333h-5.463z"/></svg>Adobe</span>
    </div>
  </div>
</div>

---

# The ARIA Spec Reality

<div class="grid grid-cols-2 gap-4 mt-8">

<div v-click class="flex items-center gap-4 p-4 rounded-xl bg-red-500/10 border border-red-500/20">
  <div class="i-carbon-document text-red-400 text-3xl"></div>
  <div>
    <div class="text-3xl font-bold text-red-300">200+</div>
    <div class="text-sm opacity-60">pages in ARIA 1.2 spec</div>
  </div>
</div>

<div v-click class="flex items-center gap-4 p-4 rounded-xl bg-orange-500/10 border border-orange-500/20">
  <div class="i-carbon-list text-orange-400 text-3xl"></div>
  <div>
    <div class="text-3xl font-bold text-orange-300">26</div>
    <div class="text-sm opacity-60">different roles with specific requirements</div>
  </div>
</div>

<div v-click class="flex items-center gap-4 p-4 rounded-xl bg-yellow-500/10 border border-yellow-500/20">
  <div class="i-carbon-tag text-yellow-400 text-3xl"></div>
  <div>
    <div class="text-3xl font-bold text-yellow-300">45+</div>
    <div class="text-sm opacity-60">aria attributes with complex interactions</div>
  </div>
</div>

<div v-click class="flex items-center gap-4 p-4 rounded-xl bg-purple-500/10 border border-purple-500/20">
  <div class="i-carbon-warning-alt text-purple-400 text-3xl"></div>
  <div>
    <div class="text-3xl font-bold text-purple-300">∞</div>
    <div class="text-sm opacity-60">browser + screen reader bugs</div>
  </div>
</div>

</div>

<div v-click class="mt-8 text-center text-lg opacity-80">
  Most developers don't have time to become ARIA experts. <span class="text-green-400 font-semibold">And they shouldn't need to.</span>
</div>

---

# Real World Example: 2D Image Gallery

<div class="grid grid-cols-2 gap-8 mt-6">

<div>
  <img src="/gallery.png" class="rounded-xl border border-white/10 shadow-xl" />
</div>

<div>
<div class="text-sm opacity-50 mb-3">Functional Requirements</div>

<div v-click class="flex items-start gap-3 mb-3">
  <div class="i-carbon-grid text-blue-400 text-lg mt-0.5"></div>
  <div class="text-sm">2D grid navigation with <span class="text-blue-300 font-semibold">arrow keys</span></div>
</div>

<div v-click class="flex items-start gap-3 mb-3">
  <div class="i-carbon-checkbox-checked text-green-400 text-lg mt-0.5"></div>
  <div class="text-sm">Multi-select with <span class="text-green-300 font-semibold">Shift + Click</span></div>
</div>

<div v-click class="flex items-start gap-3 mb-3">
  <div class="i-carbon-select-01 text-purple-400 text-lg mt-0.5"></div>
  <div class="text-sm">Select all with <span class="text-purple-300 font-semibold">Cmd/Ctrl + A</span></div>
</div>

<div v-click class="flex items-start gap-3 mb-3">
  <div class="i-carbon-keyboard text-yellow-400 text-lg mt-0.5"></div>
  <div class="text-sm">Focus management & <span class="text-yellow-300 font-semibold">tab navigation</span></div>
</div>

<div v-click class="flex items-start gap-3 mb-3">
  <div class="i-carbon-accessibility text-red-400 text-lg mt-0.5"></div>
  <div class="text-sm">Screen reader announcements with <span class="text-red-300 font-semibold">ARIA</span></div>
</div>

</div>

</div>

---

# Manual Implementation

<div class="grid grid-cols-2 gap-6 mt-4">

<div>
<div class="text-sm opacity-50 mb-2">Keyboard navigation (partial)</div>

```tsx {*}{maxHeight:'320px'}
const handleKeyDown = (e, row, col) => {
  switch (e.key) {
    case 'ArrowRight':
      focusCell(row, Math.min(col + 1, cols - 1));
      break;
    case 'ArrowLeft':
      focusCell(row, Math.max(col - 1, 0));
      break;
    case 'ArrowDown':
      focusCell(Math.min(row + 1, rows - 1), col);
      break;
    case 'ArrowUp':
      focusCell(Math.max(row - 1, 0), col);
      break;
    case ' ':
      e.preventDefault();
      toggleSelection(row, col);
      break;
    case 'a':
      if (e.metaKey || e.ctrlKey) {
        e.preventDefault();
        selectAll();
      }
      break;
    // ... more cases
  }
};
```

</div>

<div v-click>
<div class="text-sm opacity-50 mb-2">And that still doesn't cover...</div>

<div class="space-y-2">
  <div class="flex items-start gap-2 p-2 rounded bg-red-500/10 border border-red-500/20">
    <div class="i-carbon-warning-alt text-red-400 mt-0.5"></div>
    <div class="text-sm">Shift + Arrow for range selection</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-red-500/10 border border-red-500/20">
    <div class="i-carbon-warning-alt text-red-400 mt-0.5"></div>
    <div class="text-sm">Home/End/PageUp/PageDown keys</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-red-500/10 border border-red-500/20">
    <div class="i-carbon-warning-alt text-red-400 mt-0.5"></div>
    <div class="text-sm">ARIA roles & live announcements</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-red-500/10 border border-red-500/20">
    <div class="i-carbon-warning-alt text-red-400 mt-0.5"></div>
    <div class="text-sm">Focus restoration on unmount</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-red-500/10 border border-red-500/20">
    <div class="i-carbon-warning-alt text-red-400 mt-0.5"></div>
    <div class="text-sm">RTL support</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-red-500/10 border border-red-500/20">
    <div class="i-carbon-warning-alt text-red-400 mt-0.5"></div>
    <div class="text-sm">Touch & pointer interactions</div>
  </div>
</div>

</div>

</div>

---

# With React Aria Components

<div class="grid grid-cols-2 gap-6 mt-4">

<div>
<div class="text-sm opacity-50 mb-2">Complete solution</div>

```tsx
import { GridList, GridListItem } from 'react-aria-components';

function ImageGallery({ images }) {
  return (
    <GridList
      aria-label="Image gallery"
      selectionMode="multiple"
      layout="grid"
      items={images}
    >
      {(image) => (
        <GridListItem textValue={image.title}>
          <img src={image.src} alt={image.alt} />
          <span>{image.title}</span>
        </GridListItem>
      )}
    </GridList>
  );
}
```

<div class="mt-3 text-xs text-green-400">✨ ~15 lines. That's it.</div>

</div>

<div v-click>
<div class="text-sm opacity-50 mb-2">What you get for free</div>

<div class="space-y-2">
  <div class="flex items-start gap-2 p-2 rounded bg-green-500/10 border border-green-500/20">
    <div class="text-green-400">✓</div>
    <div class="text-sm">Full 2D keyboard navigation</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-green-500/10 border border-green-500/20">
    <div class="text-green-400">✓</div>
    <div class="text-sm">Multi-select with Shift/Cmd/Ctrl</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-green-500/10 border border-green-500/20">
    <div class="text-green-400">✓</div>
    <div class="text-sm">Complete ARIA implementation</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-green-500/10 border border-green-500/20">
    <div class="text-green-400">✓</div>
    <div class="text-sm">Focus management & restoration</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-green-500/10 border border-green-500/20">
    <div class="text-green-400">✓</div>
    <div class="text-sm">RTL & internationalization</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-green-500/10 border border-green-500/20">
    <div class="text-green-400">✓</div>
    <div class="text-sm">Touch, mouse & keyboard unified</div>
  </div>
  <div class="flex items-start gap-2 p-2 rounded bg-green-500/10 border border-green-500/20">
    <div class="text-green-400">✓</div>
    <div class="text-sm">Battle-tested by Adobe</div>
  </div>
</div>

</div>

</div>

---