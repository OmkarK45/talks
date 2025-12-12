---
layout: center
highlighter: shiki
css: unocss
colorSchema: dark
transition: fade-out
title: In Search for DX - Building for two consumers
exportFilename: smallcase Search Architecture - A Deep Dive
lineNumbers: false
drawings:
  persist: false
mdc: true
clicks: 0
preload: false
glowSeed: 228
routerMode: hash
theme: geist
---

# In Search for DX <span text-violet-400>*</span> Building for two consumers

Omkar Kulkarni

<div w-full absolute bottom-0 left-0 flex items-center transform="translate-x--10 translate-y--10">
  <div w-full flex items-center justify-end gap-4>
    <svg h-6 xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="386" height="98" viewBox="0 0 386 98"><defs><path id="a" d="M0 0h386.538v100H0z"/></defs><g fill="none" fill-rule="evenodd" transform="translate(-1 -1)"><mask id="b" fill="#fff"><use xlink:href="#a"/></mask><path fill="#fff" d="M380.108 46.39c-.147-3.624-3.069-6.816-7.453-6.816-4.823 0-7.6 3.046-8.037 6.815h15.49zm-7.306-12.325c7.89 0 13.736 5.8 13.736 13.776 0 .582 0 1.594-.147 2.03 0 .723-.73 1.306-1.315 1.306h-20.898c0 4.06 3.801 8.12 9.062 8.12 3.507 0 5.552-1.304 7.451-2.463.587-.437 1.172-.583 1.756.144l1.75 2.757c.586.577.733 1.156-.144 2.03-2.193 1.885-6.138 3.77-11.251 3.77-9.209 0-15.052-7.105-15.052-15.664 0-8.555 5.847-15.806 15.052-15.806m-40.914 28.422c-.438-.288-.88-.869-.585-1.596l1.316-2.753c.29-.58 1.168-.868 1.896-.433 1.758 1.013 3.945 2.173 7.452 2.173 2.484 0 3.947-1.163 3.947-2.9 0-2.029-2.339-3.334-6.429-5.22-4.679-2.033-8.182-4.494-8.182-9.426 0-3.773 2.627-8.125 9.935-8.125 4.238 0 7.307 1.306 8.766 2.177.732.579 1.026 1.45.585 2.175l-1.021 2.029c-.438.87-1.316.87-1.901.582-2.044-.87-4.092-1.448-6.429-1.448-2.629 0-3.797 1.302-3.797 2.61 0 1.882 2.187 3.042 5.113 4.351 5.55 2.317 9.792 4.348 9.792 9.859 0 4.641-4.094 8.703-10.817 8.703-4.528.29-7.89-1.595-9.645-2.758zm-21.192-2.32c3.071 0 6.14-2.174 7.018-3.623V51.61c-.44-.29-2.782-1.017-5.553-1.017-3.51 0-6.287 1.89-6.287 4.932.147 2.612 1.757 4.64 4.822 4.64m1.027-14.357c3.065 0 6.134.87 6.134.87.147-4.785-1.021-6.812-4.822-6.812-3.507 0-6.867 1.014-8.473 1.448-.878.143-1.463-.434-1.753-1.305l-.587-2.465c-.144-1.016.294-1.45 1.024-1.744.582-.143 4.823-1.737 10.374-1.737 9.645 0 10.522 5.8 10.522 13.195v15.952a1.566 1.566 0 0 1-1.463 1.452h-2.19c-.588 0-.879-.289-1.173-1.014l-.727-2.032a13.05 13.05 0 0 1-9.352 3.769c-5.7 0-9.792-3.769-9.792-10.003.147-5.367 4.532-9.57 12.278-9.57zm-28.351-11.745c4.679 0 8.184 1.737 10.96 5.217.585.729.434 1.596-.29 2.177l-2.339 2.178c-.878.723-1.463.143-1.902-.292-1.312-1.45-3.798-3.046-6.282-3.046-5.113 0-9.209 4.207-9.209 9.426 0 5.367 3.949 9.572 8.918 9.572 3.945 0 5.551-2.173 7.16-3.77.58-.581 1.315-.581 2.042-.147l2.05 1.598c.728.58 1.02 1.306.58 2.175-2.483 3.769-6.571 6.234-11.832 6.234-8.476 0-15.491-6.669-15.491-15.662.147-8.7 7.306-15.66 15.639-15.66zM253.856 20.72c0-.723.584-1.448 1.46-1.448h3.653a1.565 1.565 0 0 1 1.46 1.448v42.642a1.565 1.565 0 0 1-1.46 1.448h-3.65a1.46 1.46 0 0 1-1.463-1.452zm-16.075 0c0-.723.585-1.448 1.461-1.448h3.654a1.565 1.565 0 0 1 1.46 1.448v42.642a1.565 1.565 0 0 1-1.46 1.448h-3.65a1.46 1.46 0 0 1-1.465-1.452zM215.28 60.166c3.067 0 6.135-2.173 7.012-3.622V51.61c-.436-.29-2.776-1.017-5.553-1.017-3.506 0-6.281 1.89-6.281 4.932 0 2.612 1.606 4.64 4.822 4.64m.878-14.356c3.067 0 6.134.87 6.134.87.147-4.785-1.021-6.812-4.822-6.812-3.505 0-6.865 1.014-8.471 1.448-.88.143-1.465-.434-1.755-1.305l-.587-2.465c-.144-1.016.29-1.45 1.025-1.744.583-.143 4.822-1.737 10.373-1.737 9.645 0 10.668 5.8 10.668 13.195v15.952a1.57 1.57 0 0 1-1.461 1.452h-2.193c-.584 0-.874-.289-1.312-1.014l-.734-2.032a13.05 13.05 0 0 1-9.349 3.769c-5.702 0-9.792-3.769-9.792-10.003.147-5.367 4.53-9.57 12.276-9.57zm-64.295-9.572c0-.725.581-1.448 1.459-1.448h1.46c.731 0 1.173.289 1.316.87l.878 2.609c.581-.723 3.797-4.204 9.645-4.204 4.382 0 7.011 1.737 9.205 4.786.877-.87 4.384-4.786 10.226-4.786 9.21 0 11.547 6.38 11.547 14.212v15.081c0 .801-.656 1.452-1.463 1.452h-3.65c-.878 0-1.465-.58-1.465-1.452V47.987c0-4.786-1.897-7.688-5.989-7.688-4.531 0-6.722 3.046-7.308 3.48.148.581.291 2.466.291 4.062v15.521c0 .72-.583 1.448-1.312 1.448h-3.801c-.878 0-1.459-.58-1.459-1.452V47.987c0-4.932-1.755-7.688-5.994-7.688-4.528 0-6.867 3.338-7.158 4.355v18.704a1.566 1.566 0 0 1-1.462 1.452h-3.65a1.457 1.457 0 0 1-1.463-1.452v-27.12zm-27.62 26.25c-.437-.29-.878-.87-.584-1.597l1.314-2.753c.294-.58 1.172-.868 1.902-.433 1.75 1.013 3.945 2.173 7.45 2.173 2.486 0 3.945-1.163 3.945-2.9 0-2.029-2.337-3.334-6.429-5.22-4.675-2.033-8.182-4.494-8.182-9.426 0-3.773 2.63-8.125 9.936-8.125 4.237 0 7.308 1.306 8.767 2.177.73.579 1.025 1.45.587 2.175l-1.025 2.029c-.436.87-1.312.87-1.899.582-2.042-.87-4.092-1.448-6.43-1.448-2.628 0-3.8 1.302-3.8 2.61 0 1.882 2.193 3.042 5.117 4.351 5.553 2.317 9.788 4.348 9.788 9.859 0 4.641-4.088 8.703-10.815 8.703-4.526.29-7.887-1.595-9.643-2.758m-80.67-49.11 16.803 8.104a1.653 1.653 0 0 1 .773 2.22 1.66 1.66 0 0 1-.743.756l-16.3 8.281a1.74 1.74 0 0 1-1.533 0l-16.801-8.1a1.657 1.657 0 0 1-.032-2.974l16.3-8.283a1.74 1.74 0 0 1 1.532-.003m.12 30.777 39.774-20.208a1.654 1.654 0 0 0-.036-2.97L44 1.965a1.72 1.72 0 0 0-1.526 0L2.7 22.163a1.657 1.657 0 0 0 .034 2.975l39.447 19.01a1.72 1.72 0 0 0 1.511 0zm33.421 14.56c-.3 6.896-4.077 13.178-10.047 16.714-5.536 2.824-10.027-.07-10.023-6.482.296-6.894 4.074-13.18 10.047-16.716 5.535-2.824 10.023.083 10.023 6.48zm11.74 17.348V31.12a1.69 1.69 0 0 0-1.707-1.668 1.7 1.7 0 0 0-.772.189L46.247 50.128c-.56.281-.913.851-.915 1.474v44.944a1.69 1.69 0 0 0 1.707 1.668 1.7 1.7 0 0 0 .771-.188l40.14-20.487a1.66 1.66 0 0 0 .903-1.476M26.799 80.01 8.738 71.334a1.66 1.66 0 0 1-.785-2.217q.053-.103.116-.198l9.04-13.295a1.713 1.713 0 0 1 2.369-.449c.274.185.488.444.615.747l9.043 21.955a1.66 1.66 0 0 1-.857 2.192 1.68 1.68 0 0 1-1.48-.063z" mask="url(#b)"/></g></svg>
  </div>
</div>

<!--
Hi everyone!

Today I want to share some learnings from building the search experience at smallcase, and how thinking about "two consumers" shaped our architecture decisions.
-->

---
layout: intro
class: px-24
glowSeed: 205
---

# Agenda

<span>Two acts of building for DX and UX</span>

<div mt-10/>

<div flex items-center gap-4>
<v-clicks>
  <div
    :class="$clicks < 1 ? 'translate-x--20' : 'translate-x-0'"
    rounded-lg
    border="2 solid violet-800" bg="violet-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-16 flex items-center justify-center>
      <div i-carbon:search h-20 w-20 />
    </div>
    <div bg="violet-800/30" w-full px-4 py-2 h="5rem" flex items-center justify-center text-center>
      <span>Search Architecture</span>
    </div>
  </div>
  <div
    :class="$clicks < 2 ? 'translate-x--20' : 'translate-x-0'"
    rounded-lg
    border="2 solid purple-800" bg="purple-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-16 flex items-center justify-center>
      <div i-carbon:accessibility h-20 w-20 />
    </div>
    <div bg="purple-800/30" w-full px-4 py-2 h="5rem" flex items-center justify-center text-center>
      <span>Accessibility that scales</span>
    </div>
  </div>
</v-clicks>
</div>

<!--
We'll cover two main areas today:

[click] First, the search project and architectural learnings around state management, layered design, and why URL-as-state matters.

[click] Second, how we approached accessibility in a way that scales without becoming a maintenance nightmare.
-->

---
glowSeed: 120
---

# The Thesis: Two Consumers

<span>A search page is built by developers, used by customers</span>

<div mt-6 />

<div flex gap-6>
  <div v-click flex-1 border="2 solid violet-800/50" rounded-lg overflow-hidden>
    <div bg="violet-800/30" px-4 py-2 font-semibold flex items-center gap-2>
      <div i-carbon:code text-violet-400 />
      Developer Experience (DX)
    </div>
    <div bg="violet-800/10" px-4 py-3>
      <div text-sm flex flex-col gap-2>
        <div>When adding a new filter takes <span text-green-400>30 minutes</span> not 3 days</div>
        <div>When debugging is <span text-green-400>straightforward</span> not archeology</div>
        <div>When new team members <span text-green-400>onboard quickly</span></div>
      </div>
    </div>
  </div>
  <div flex items-center>
    <div i-carbon:arrow-right text-3xl text-zinc-500 />
  </div>
  <div v-click flex-1 border="2 solid sky-800/50" rounded-lg overflow-hidden>
    <div bg="sky-800/30" px-4 py-2 font-semibold flex items-center gap-2>
      <div i-carbon:user text-sky-400 />
      User Experience (UX)
    </div>
    <div bg="sky-800/10" px-4 py-3>
      <div text-sm flex flex-col gap-2>
        <div>Features ship <span text-green-400>faster</span></div>
        <div>Fewer bugs reach <span text-green-400>production</span></div>
        <div>Consistent behavior <span text-green-400>builds trust</span></div>
      </div>
    </div>
  </div>
</div>

<div v-click mt-6 text-center>
  <div border="2 solid zinc-700" bg="zinc-800/40" rounded-lg px-8 py-4 inline-block>
    <span text-lg>Good DX <div i-carbon:arrow-right inline-block translate-y-0.5 mx-2 /> Good UX, faster</span>
  </div>
</div>

<!--
A search page is built by developers and used by customers.

[click] Good DX means adding a filter takes 30 minutes not 3 days, debugging is straightforward, and new team members onboard quickly.

[click] This leads to better UX - features ship faster, fewer bugs reach production, and consistent behavior builds trust.

[click] Good DX leads to good UX, faster.
-->

---
glowSeed: 130
---

# What Slows Teams Down?

<span>Common patterns that hurt velocity</span>

<div mt-6 />

<div flex flex-col gap-3>

<v-clicks>

<div border="2 solid red-800/50" rounded-lg>
  <div flex items-center bg="red-800/30" px-3 py-2 text-red-300>
    <div i-carbon:misuse text-sm mr-2 />
    <div text-xs><em>Leaky abstractions</em></div>
  </div>
  <div bg="red-800/10" px-4 py-3>
    <div>Components need to know about URL encoding, API pagination, analytics tracking</div>
    <div text-xs flex gap-2 mt-1 text-zinc-400>
      <div>Hard to reuse</div>
      <div>Hard to test</div>
      <div>Hard to refactor</div>
    </div>
  </div>
</div>

<div border="2 solid orange-800/50" rounded-lg>
  <div flex items-center bg="orange-800/30" px-3 py-2 text-orange-300>
    <div i-carbon:arrows-horizontal text-sm mr-2 />
    <div text-xs><em>Scattered state</em></div>
  </div>
  <div bg="orange-800/10" px-4 py-3>
    <div>Filter state in Redux, sort state in URL, pagination in component state</div>
    <div text-xs flex gap-2 mt-1 text-zinc-400>
      <div>Hard to debug</div>
      <div>Hard to sync</div>
      <div>Race conditions</div>
    </div>
  </div>
</div>

<div border="2 solid yellow-800/50" rounded-lg>
  <div flex items-center bg="yellow-800/30" px-3 py-2 text-yellow-300>
    <div i-carbon:document-unknown text-sm mr-2 />
    <div text-xs><em>Tribal knowledge</em></div>
  </div>
  <div bg="yellow-800/10" px-4 py-3>
    <div>"Ask John how filters work" - patterns exist only in people's heads</div>
    <div text-xs flex gap-2 mt-1 text-zinc-400>
      <div>Onboarding takes months</div>
      <div>Knowledge silos</div>
      <div>Bus factor risk</div>
    </div>
  </div>
</div>

</v-clicks>

</div>

<!--
What slows teams down?

[click] Leaky abstractions - when components need to know about URL encoding, API pagination, and analytics

[click] Scattered state - when filter state is in Redux, sort in URL, and pagination in component state

[click] Tribal knowledge - when patterns exist only in people's heads
-->

---

# What "Tasteful Interface" Means

<span>The DX lens on API design</span>

<div mt-10 />

<div flex gap-8>

<div v-click flex-1>
  <div border="2 solid red-800/50" rounded-lg overflow-hidden>
    <div flex items-center bg="red-800/30" px-3 py-2 text-red-300>
      <div i-carbon:close text-sm mr-2 />
      <span text-sm>Leaky abstraction</span>
    </div>
    <div bg="red-800/10" px-4 py-3>

```ts
handleFilterChange(
  filterType,
  value,
  shouldUpdateUrl,
  shouldRefetch,
  debounceMs,
  trackingPayload
)
```

</div>
  </div>
</div>

<div v-click flex-1>
  <div border="2 solid green-800/50" rounded-lg overflow-hidden>
    <div flex items-center bg="green-800/30" px-3 py-2 text-green-300>
      <div i-carbon:checkmark text-sm mr-2 />
      <span text-sm>Clean interface</span>
    </div>
    <div bg="green-800/10" px-4 py-3>

```ts
const { onFilterChange } = useSearchPageContext()

onFilterChange({ type: 'sort', value: 'returns' })
```

</div>
  </div>
</div>

</div>

<div v-click mt-8>
  <div border="2 solid zinc-700" bg="zinc-800/20" rounded-lg px-4 py-3>
    <div flex items-center gap-2>
      <div i-carbon:idea text-yellow-400 />
      <span>The component shouldn't care about URL updates, refetching, or tracking</span>
    </div>
  </div>
</div>

<!--
What does "tasteful" actually mean in code?

[click] This is what a leaky abstraction looks like - 6 arguments, implementation details exposed everywhere.

[click] This is what we aimed for - the consumer just says what changed. Everything else is handled by the layer below.

[click] The key insight: a button shouldn't know about URL encoding or API calls.
-->

---
glow: right
glowSeed: 180
---

# Why Software Principles Matter

<span>The fundamentals that guided our decisions</span>

<div mt-6 />

### These aren't new ideas...

<br>

<v-clicks depth="2">

- <span text-violet-400>Single Responsibility</span> - each function, hook, or component does one thing well
  - A filter button handles clicks, not URL updates
  - A context provides state, not UI
- <span text-purple-400>Separation of Concerns</span> - different layers handle different responsibilities
  - URL encoding is separate from business logic
  - API calls are separate from state management
- <span text-fuchsia-400>Dependency Inversion</span> - depend on abstractions, not implementations
  - Components call `onFilterChange()`, not `router.push()`
  - Testing becomes trivial with mock contexts
- <span text-pink-400>Information Hiding</span> - each layer hides its complexity from the one above
  - The button doesn't know about debouncing or analytics
  - The context doesn't know about React Query internals

</v-clicks>

<!--
These aren't new ideas - they're classic software principles:

[click] Single Responsibility - each function, hook, or component does one thing well

[click] Separation of Concerns - different layers handle different responsibilities

[click] Dependency Inversion - depend on abstractions, not implementations

[click] Information Hiding - each layer hides its complexity from the one above
-->

---
glow: right
glowSeed: 200
---

# The Vision: smallcase as a Search Engine

<span>What users were missing, what search should feel like</span>

<div mt-8 />

<div flex flex-col gap-4>

<v-clicks>

<div border="2 solid zinc-700/50" rounded-lg overflow-hidden>
  <div grid grid-cols-3 text-sm>
    <div bg="zinc-800/40" px-4 py-3 font-semibold border-r="1 solid zinc-700/50">Problem</div>
    <div bg="zinc-800/40" px-4 py-3 font-semibold border-r="1 solid zinc-700/50">Before</div>
    <div bg="zinc-800/40" px-4 py-3 font-semibold>After</div>
  </div>
  <div grid grid-cols-3 text-sm border-t="1 solid zinc-700/50">
    <div px-4 py-3 border-r="1 solid zinc-700/50" flex items-center gap-2>
      <div i-carbon:link text-violet-400 />
      State persistence
    </div>
    <div px-4 py-3 border-r="1 solid zinc-700/50" text-zinc-400>Lost on refresh</div>
    <div px-4 py-3 text-green-400>URL as state</div>
  </div>
  <div grid grid-cols-3 text-sm border-t="1 solid zinc-700/50">
    <div px-4 py-3 border-r="1 solid zinc-700/50" flex items-center gap-2>
      <div i-carbon:share text-violet-400 />
      Shareability
    </div>
    <div px-4 py-3 border-r="1 solid zinc-700/50" text-zinc-400>Not possible</div>
    <div px-4 py-3 text-green-400>Link sharing works</div>
  </div>
  <div grid grid-cols-3 text-sm border-t="1 solid zinc-700/50">
    <div px-4 py-3 border-r="1 solid zinc-700/50" flex items-center gap-2>
      <div i-carbon:search text-violet-400 />
      Asset types
    </div>
    <div px-4 py-3 border-r="1 solid zinc-700/50" text-zinc-400>Single type</div>
    <div px-4 py-3 text-green-400>Multi-asset</div>
  </div>
  <div grid grid-cols-3 text-sm border-t="1 solid zinc-700/50">
    <div px-4 py-3 border-r="1 solid zinc-700/50" flex items-center gap-2>
      <div i-carbon:settings text-violet-400 />
      Configuration
    </div>
    <div px-4 py-3 border-r="1 solid zinc-700/50" text-zinc-400>Hardcoded</div>
    <div px-4 py-3 text-green-400>Config-driven</div>
  </div>
</div>

</v-clicks>

</div>

<!--
[click] Here's what we were solving for. The table shows the before and after - from state that disappears on refresh to URL-persisted state, from unshareable searches to link sharing, from single asset type to multi-asset, and from hardcoded logic to configuration-driven behavior.
-->

---
glowSeed: 250
---

# URL as State Manager

<span>Why it's non-negotiable for search</span>

<div mt-10 />

<div flex items-center gap-4>

<v-clicks>
  <div
    :class="$clicks < 1 ? 'translate-y-10 opacity-0' : 'translate-y-0 opacity-100'"
    rounded-lg
    border="2 solid violet-800" bg="violet-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:restart h-16 w-16 />
    </div>
    <div bg="violet-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Survives refresh</span>
    </div>
  </div>
  <div
    :class="$clicks < 2 ? 'translate-y-10 opacity-0' : 'translate-y-0 opacity-100'"
    rounded-lg
    border="2 solid purple-800" bg="purple-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:share h-16 w-16 />
    </div>
    <div bg="purple-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Shareable</span>
    </div>
  </div>
  <div
    :class="$clicks < 3 ? 'translate-y-10 opacity-0' : 'translate-y-0 opacity-100'"
    rounded-lg
    border="2 solid fuchsia-800" bg="fuchsia-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:undo h-16 w-16 />
    </div>
    <div bg="fuchsia-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Back/Forward works</span>
    </div>
  </div>
  <div
    :class="$clicks < 4 ? 'translate-y-10 opacity-0' : 'translate-y-0 opacity-100'"
    rounded-lg
    border="2 solid pink-800" bg="pink-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:bookmark h-16 w-16 />
    </div>
    <div bg="pink-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Bookmarkable</span>
    </div>
  </div>
</v-clicks>

</div>

<div v-click mt-10 flex justify-center>
  <div bg="zinc-800/60" border="1 solid zinc-700" rounded-full px-6 py-2 font-mono text-sm>
    /discover?tab=smallcases&sort=returns&filters=equity,thematic
  </div>
</div>

<!--
Why URL as state? Four reasons:

[click] Survives refresh - no lost state

[click] Shareable - send someone your exact search

[click] Back/Forward navigation works correctly

[click] Bookmarkable - save for later

[click] This is what a search URL looks like - everything encoded, everything restorable.
-->

---
glow: right
glowSeed: 280
---

# When URL State Doesn't Fit

<span>Not everything belongs in the URL</span>

<div mt-6 />

<div flex flex-col gap-3>

<v-clicks>

<div flex items-center gap-3 border="1 solid yellow-800/50" bg="yellow-800/10" rounded-lg px-4 py-3>
  <div i-carbon:password text-2xl text-yellow-400 />
  <div>
    <div font-semibold>Sensitive data</div>
    <div text-sm text-zinc-400>Passwords, tokens, PII - never in URLs (browser history, logs, referrers)</div>
  </div>
</div>

<div flex items-center gap-3 border="1 solid yellow-800/50" bg="yellow-800/10" rounded-lg px-4 py-3>
  <div i-carbon:time text-2xl text-yellow-400 />
  <div>
    <div font-semibold>Ephemeral UI state</div>
    <div text-sm text-zinc-400>Modal open/closed, dropdown expanded, tooltip visible - too noisy for URL</div>
  </div>
</div>

<div flex items-center gap-3 border="1 solid yellow-800/50" bg="yellow-800/10" rounded-lg px-4 py-3>
  <div i-carbon:data-volume text-2xl text-yellow-400 />
  <div>
    <div font-semibold>Large data sets</div>
    <div text-sm text-zinc-400>Selected items array, form drafts - URLs have length limits (~2000 chars)</div>
  </div>
</div>

<div flex items-center gap-3 border="1 solid yellow-800/50" bg="yellow-800/10" rounded-lg px-4 py-3>
  <div i-carbon:flash text-2xl text-yellow-400 />
  <div>
    <div font-semibold>High-frequency updates</div>
    <div text-sm text-zinc-400>Scroll position, cursor location, animation state - would thrash history</div>
  </div>
</div>

<div flex items-center gap-3 border="1 solid yellow-800/50" bg="yellow-800/10" rounded-lg px-4 py-3>
  <div i-carbon:user-profile text-2xl text-yellow-400 />
  <div>
    <div font-semibold>User-specific preferences</div>
    <div text-sm text-zinc-400>Theme, collapsed sections - better in localStorage or user settings</div>
  </div>
</div>

</v-clicks>

</div>

<!--
Not everything belongs in the URL:

[click] Sensitive data - passwords, tokens, PII should never be in URLs

[click] Ephemeral UI state - modals, dropdowns, tooltips are too noisy

[click] Large data sets - URLs have length limits around 2000 characters

[click] High-frequency updates - scroll position would thrash browser history

[click] User-specific preferences - theme, collapsed sections belong in localStorage
-->

---
glow: bottom
glowSeed: 300
---

# The Layered Flow

<span>The architecture that made it work</span>

<div mt-4 />

<div flex justify-center>
  <div flex flex-col gap-1 w-120>
    <div v-click border="1 solid sky-600" bg="sky-800/30" rounded px-4 py-2 flex items-center gap-3>
      <div i-carbon:link text-lg text-sky-400 />
      <div flex-1>
        <div font-semibold text-sm>URL</div>
        <div text-xs text-zinc-400>Source of truth</div>
      </div>
    </div>
    <div v-click flex justify-center>
      <div i-carbon:arrow-down text-lg text-zinc-500 />
    </div>
    <div v-click border="1 solid violet-600" bg="violet-800/30" rounded px-4 py-2 flex items-center gap-3>
      <div i-carbon:code text-lg text-violet-400 />
      <div flex-1>
        <div font-semibold text-sm>useUrlTabParams</div>
        <div text-xs text-zinc-400>Decode / Encode layer</div>
      </div>
    </div>
    <div v-click flex justify-center>
      <div i-carbon:arrow-down text-lg text-zinc-500 />
    </div>
    <div v-click border="1 solid purple-600" bg="purple-800/30" rounded px-4 py-2 flex items-center gap-3>
      <div i-carbon:flow text-lg text-purple-400 />
      <div flex-1>
        <div font-semibold text-sm>SearchPageContext</div>
        <div text-xs text-zinc-400>Actions & state orchestration</div>
      </div>
    </div>
    <div v-click flex justify-center>
      <div i-carbon:arrow-down text-lg text-zinc-500 />
    </div>
    <div v-click border="1 solid fuchsia-600" bg="fuchsia-800/30" rounded px-4 py-2 flex items-center gap-3>
      <div i-carbon:application text-lg text-fuchsia-400 />
      <div flex-1>
        <div font-semibold text-sm>UI Components</div>
        <div text-xs text-zinc-400>Buttons, filters, cards</div>
      </div>
    </div>
    <div v-click flex justify-center>
      <div i-carbon:arrow-down text-lg text-zinc-500 />
    </div>
    <div v-click border="1 solid pink-600" bg="pink-800/30" rounded px-4 py-2 flex items-center gap-3>
      <div i-carbon:api text-lg text-pink-400 />
      <div flex-1>
        <div font-semibold text-sm>Infrastructure</div>
        <div text-xs text-zinc-400>React Query / API calls</div>
      </div>
    </div>
  </div>
</div>

<!--
Here's the layered architecture:

[click] URL is the source of truth at the top

[click] Arrow down

[click] useUrlTabParams handles encoding and decoding

[click] Arrow down

[click] SearchPageContext orchestrates actions and state

[click] Arrow down

[click] UI components just consume and emit actions

[click] Arrow down

[click] Infrastructure layer handles API calls with React Query

The key: each layer only talks to adjacent layers. A button doesn't know about URLs.
-->

---
glowSeed: 320
---

# Why Layers Matter

<span>The button doesn't care how the URL is updated</span>

<div mt-4 />

<div flex gap-6>

<div v-click flex-1>

```tsx
// Layer 2: Interface (Component)
<CheckboxGroupList
  onChange={(value) => onFilterChange('VOLATILITY', value)}
/>

// Layer 3: Business Logic (Context)
const onFilterChange = (key, value) => {
  const updatedFilters = processFilterUpdate({...})
  updateQueryParams({ filters: updatedFilters })
}

// Layer 4: Infrastructure (Hook)
const useDiscoverQuery = (params) => {
  return useInfiniteQuery({
    queryFn: () => getMultiAssetDiscover(params),
  })
}
```

</div>

<div v-click flex-1 flex flex-col gap-3>
  <div text-sm font-semibold text-zinc-400>This separation means:</div>
  <div border="1 solid green-800/50" bg="green-800/10" rounded px-3 py-2 text-sm flex items-center gap-2>
    <div i-carbon:checkmark-outline text-green-400 />
    <span>Button component is reusable</span>
  </div>
  <div border="1 solid green-800/50" bg="green-800/10" rounded px-3 py-2 text-sm flex items-center gap-2>
    <div i-carbon:checkmark-outline text-green-400 />
    <span>URL logic is centralized</span>
  </div>
  <div border="1 solid green-800/50" bg="green-800/10" rounded px-3 py-2 text-sm flex items-center gap-2>
    <div i-carbon:checkmark-outline text-green-400 />
    <span>Testing is easier (mock context, not router)</span>
  </div>
  <div v-click mt-4 border="2 solid zinc-700" bg="zinc-800/20" rounded-lg px-3 py-2>
    <div flex items-center gap-2 text-sm>
      <div i-carbon:idea text-yellow-400 />
      <span>It just calls <code text-violet-300>onSortChange()</code></span>
    </div>
  </div>
</div>

</div>

<!--
[click] Each layer has one job. The component calls onChange, the context processes the filter update, and the infrastructure handles the API call.

[click] This separation means the button is reusable, URL logic is centralized, and testing is easier.

[click] The button just calls onSortChange() - it doesn't care about URLs or APIs.
-->

---
glowSeed: 350
---

# Thinking in Layers

<span>An analogy to make it concrete</span>

<div mt-8 />

<div flex gap-12 items-start>

<div v-click flex-1>
  <div text-lg font-semibold mb-4 flex items-center gap-2>
    <div i-carbon:cafe text-amber-400 />
    Coffee Machine
  </div>
  <div flex flex-col gap-2>
    <div border="1 solid zinc-700" bg="zinc-800/40" rounded px-4 py-2 text-sm>
      <span text-amber-300>Intent:</span> "I want coffee"
    </div>
    <div border="1 solid zinc-700" bg="zinc-800/40" rounded px-4 py-2 text-sm>
      <span text-amber-300>Interface:</span> Press button
    </div>
    <div border="1 solid zinc-700" bg="zinc-800/40" rounded px-4 py-2 text-sm>
      <span text-amber-300>Logic:</span> Grind, heat, brew
    </div>
    <div border="1 solid zinc-700" bg="zinc-800/40" rounded px-4 py-2 text-sm>
      <span text-amber-300>Infra:</span> Pump, heater, grinder
    </div>
  </div>
</div>

<div v-click flex-1>
  <div text-lg font-semibold mb-4 flex items-center gap-2>
    <div i-carbon:search text-violet-400 />
    Search Page
  </div>
  <div flex flex-col gap-2>
    <div border="1 solid zinc-700" bg="zinc-800/40" rounded px-4 py-2 text-sm>
      <span text-violet-300>Intent:</span> "Filter by returns"
    </div>
    <div border="1 solid zinc-700" bg="zinc-800/40" rounded px-4 py-2 text-sm>
      <span text-violet-300>Interface:</span> Click filter chip
    </div>
    <div border="1 solid zinc-700" bg="zinc-800/40" rounded px-4 py-2 text-sm>
      <span text-violet-300>Logic:</span> Update URL, refetch
    </div>
    <div border="1 solid zinc-700" bg="zinc-800/40" rounded px-4 py-2 text-sm>
      <span text-violet-300>Infra:</span> React Query, API
    </div>
  </div>
</div>

</div>

<div v-click mt-8>
  <div border="2 solid zinc-700" bg="zinc-800/20" rounded-lg px-4 py-3>
    <div flex items-center gap-2>
      <div i-carbon:idea text-yellow-400 />
      <span>You don't think about the pump when you want coffee. Components shouldn't think about APIs.</span>
    </div>
  </div>
</div>

<!--
[click] Think of a coffee machine - you express intent, interact with an interface, logic handles the brewing, and infrastructure does the physical work.

[click] Same for search - intent is "filter by returns", interface is clicking a chip, logic updates URL and triggers refetch, infrastructure makes the API call.

[click] The insight: you don't think about the pump when you want coffee. Components shouldn't think about APIs when they want to filter.
-->

---
glow: right
glowSeed: 380
---

# Benefits of This Architecture

<span>What we gained from layered design</span>

<div mt-6 />

### This architecture gives us...

<br>

<v-clicks depth="2">

- <span text-violet-400>Testability</span> - each layer can be tested in isolation
  - Mock the context to test components
  - Mock the API to test the context
- <span text-purple-400>Reusability</span> - components work in any context that provides the same interface
  - FilterChip works on search page, discover page, anywhere
  - No hardcoded dependencies on specific URLs or APIs
- <span text-fuchsia-400>Maintainability</span> - changes are localized to one layer
  - Change URL encoding? Only touch the URL layer
  - Switch from REST to GraphQL? Only touch infrastructure
- <span text-pink-400>Debuggability</span> - clear boundaries make bugs easier to find
  - Is the URL wrong? Check the URL layer
  - Is the API call wrong? Check infrastructure

</v-clicks>

<!--
This architecture gives us:

[click] Testability - each layer can be tested in isolation

[click] Reusability - components work in any context that provides the same interface

[click] Maintainability - changes are localized to one layer

[click] Debuggability - clear boundaries make bugs easier to find
-->

---
glow: right
glowSeed: 400
---

# Why Context Made Sense

<span>A decision slide for the architecture nerds</span>

<div mt-8 />

<div flex gap-8>

<div v-click flex-1>
  <div border="2 solid green-800/50" rounded-lg overflow-hidden>
    <div flex items-center bg="green-800/30" px-3 py-2 text-green-300>
      <div i-carbon:checkmark text-sm mr-2 />
      <span text-sm>React Context</span>
    </div>
    <div bg="green-800/10" px-4 py-4>
      <div flex flex-col gap-2 text-sm>
        <div flex items-center gap-2>
          <div i-carbon:checkmark-outline text-green-400 />
          <span>Feature-scoped</span>
        </div>
        <div flex items-center gap-2>
          <div i-carbon:checkmark-outline text-green-400 />
          <span>Co-located with URL sync</span>
        </div>
        <div flex items-center gap-2>
          <div i-carbon:checkmark-outline text-green-400 />
          <span>No extra dependencies</span>
        </div>
        <div flex items-center gap-2>
          <div i-carbon:checkmark-outline text-green-400 />
          <span>Natural provider hierarchy</span>
        </div>
      </div>
    </div>
  </div>
</div>

<div v-click flex-1>
  <div border="2 solid yellow-800/50" rounded-lg overflow-hidden>
    <div flex items-center bg="yellow-800/30" px-3 py-2 text-yellow-300>
      <div i-carbon:warning text-sm mr-2 />
      <span text-sm>Redux / Zustand</span>
    </div>
    <div bg="yellow-800/10" px-4 py-4>
      <div flex flex-col gap-2 text-sm>
        <div flex items-center gap-2>
          <div i-carbon:close-outline text-yellow-400 />
          <span>Global by default</span>
        </div>
        <div flex items-center gap-2>
          <div i-carbon:close-outline text-yellow-400 />
          <span>Extra URL sync plumbing</span>
        </div>
        <div flex items-center gap-2>
          <div i-carbon:close-outline text-yellow-400 />
          <span>Additional dependency</span>
        </div>
        <div flex items-center gap-2>
          <div i-carbon:close-outline text-yellow-400 />
          <span>Overkill for feature state</span>
        </div>
      </div>
    </div>
  </div>
</div>

</div>

<div v-click mt-8>

```tsx
// Clean provider hierarchy
<SearchPageContextProvider>
  {/* State + Actions */}
  <TrackingContextProvider>
    {/* Analytics */}
    <SearchPage />
  </TrackingContextProvider>
</SearchPageContextProvider>
```

</div>

<!--
Why Context over Redux or Zustand?

[click] Context gives us feature-scoped state, natural co-location with URL sync, no extra dependencies, and a natural provider hierarchy.

[click] Global state managers are overkill here - we'd need extra plumbing to sync with URL, and it's global by default when we want feature-scoped.

[click] This is the actual provider hierarchy - clean, readable, each provider has a single responsibility. State and actions in one, analytics in another.
-->

---
layout: center
class: text-center
glowSeed: 450
---

<div text-4xl mb-8>Part 2</div>

<h1 flex items-center justify-center gap-4>
  <div i-carbon:accessibility text-6xl text-purple-400 />
  <span>Accessibility</span>
</h1>

<div mt-4 text-zinc-400>
  If DX accelerates UX, a11y is UX for everyone
</div>

<!--
Let's shift to Part 2 - Accessibility.

If DX accelerates UX, then accessibility is UX for everyone.
-->

---
glowSeed: 500
---

# Accessibility is for Everyone

<span>Not just for users with disabilities</span>

<div mt-8 />

<div grid grid-cols-2 gap-4>

<v-clicks>

<div border="2 solid violet-800/50" rounded-lg overflow-hidden>
  <div flex items-center bg="violet-800/30" px-3 py-3>
    <div i-carbon:keyboard text-xl mr-3 text-violet-400 />
    <span font-semibold>Keyboard Navigation</span>
  </div>
  <div bg="violet-800/10" px-4 py-3 text-sm text-zinc-300>
    <div>Power users prefer keyboard</div>
    <div text-zinc-500 mt-1>Also: broken trackpad, RSI, efficiency</div>
  </div>
</div>

<div border="2 solid purple-800/50" rounded-lg overflow-hidden>
  <div flex items-center bg="purple-800/30" px-3 py-3>
    <div i-carbon:view text-xl mr-3 text-purple-400 />
    <span font-semibold>Focus Indicators</span>
  </div>
  <div bg="purple-800/10" px-4 py-3 text-sm text-zinc-300>
    <div>Know where you are</div>
    <div text-zinc-500 mt-1>Also: bright environments, fatigue</div>
  </div>
</div>

<div border="2 solid fuchsia-800/50" rounded-lg overflow-hidden>
  <div flex items-center bg="fuchsia-800/30" px-3 py-3>
    <div i-carbon:tag text-xl mr-3 text-fuchsia-400 />
    <span font-semibold>Semantic Labels</span>
  </div>
  <div bg="fuchsia-800/10" px-4 py-3 text-sm text-zinc-300>
    <div>Screen reader support</div>
    <div text-zinc-500 mt-1>Also: automation, testing, SEO</div>
  </div>
</div>

<div border="2 solid pink-800/50" rounded-lg overflow-hidden>
  <div flex items-center bg="pink-800/30" px-3 py-3>
    <div i-carbon:touch-1 text-xl mr-3 text-pink-400 />
    <span font-semibold>Touch Targets</span>
  </div>
  <div bg="pink-800/10" px-4 py-3 text-sm text-zinc-300>
    <div>Motor impairments</div>
    <div text-zinc-500 mt-1>Also: mobile users, cold hands</div>
  </div>
</div>

</v-clicks>

</div>

<!--
Accessibility isn't just for users with disabilities:

[click] Keyboard navigation - power users prefer it, but also helps with broken trackpads, RSI, or just efficiency

[click] Focus indicators - essential for knowing where you are, but also helps in bright environments or when fatigued

[click] Semantic labels - screen readers need them, but so does automation, testing, and SEO

[click] Touch targets - motor impairments need them, but so do mobile users and anyone with cold hands
-->

---
glow: right
glowSeed: 530
---

# The a11y Mindset

<span>How to think about accessibility</span>

<div mt-6 />

### Accessibility is a spectrum, not a checkbox...

<br>

<v-clicks depth="2">

- <span text-violet-400>Progressive enhancement</span> - start with semantic HTML, enhance with ARIA
  - A `<button>` is already accessible, a `<div onClick>` is not
  - Add ARIA only when native elements aren't enough
- <span text-purple-400>Focus on interactions</span> - if you can click it, you should be able to keyboard it
  - Every interactive element needs a focus state
  - Every action needs a keyboard equivalent
- <span text-fuchsia-400>Announce changes</span> - users need to know what happened
  - Filter applied? Announce the new count
  - Error occurred? Announce the message
- <span text-pink-400>Test with real tools</span> - use screen readers and keyboard-only navigation
  - VoiceOver on Mac, NVDA on Windows
  - Tab through your entire app without touching the mouse

</v-clicks>

<!--
Accessibility is a spectrum, not a checkbox:

[click] Progressive enhancement - start with semantic HTML, enhance with ARIA

[click] Focus on interactions - if you can click it, you should be able to keyboard it

[click] Announce changes - users need to know what happened

[click] Test with real tools - use screen readers and keyboard-only navigation
-->

---
glow: right
glowSeed: 550
---

# What Manual a11y Looks Like

<span>Just the basics for 2D grid navigation</span>

<div mt-4 />

<div flex gap-4>

<div flex-1>

```ts
function handleKeyDown(e: KeyboardEvent) {
  const idx = items.findIndex(
    item => item.id === focusedId
  )

  switch (e.key) {
    case 'ArrowRight':
      if (idx + 1 < items.length)
        setFocusedId(items[idx + 1].id)
      break
    case 'ArrowLeft':
      if (idx - 1 >= 0)
        setFocusedId(items[idx - 1].id)
      break
    case 'ArrowDown':
      if (idx + cols < items.length)
        setFocusedId(items[idx + cols].id)
      break
    // ... 200+ more lines
  }
}
```

</div>

<div v-click flex-1 flex flex-col justify-center>
  <div border="2 solid red-800/50" bg="red-800/20" rounded-lg px-4 py-3>
    <div font-semibold text-red-300 mb-2>And this is just arrow keys!</div>
    <div text-sm text-zinc-400>
      Still missing: Home/End, Page Up/Down, typeahead, focus restoration, disabled items, RTL, screen reader announcements...
    </div>
  </div>
</div>

</div>

<!--
Here's what manual 2D grid navigation looks like - just the arrow keys.

[click] And this is just arrow keys! We're still missing Home/End, Page Up/Down, typeahead, focus restoration, disabled items, RTL support, screen reader announcements...
-->

---
glowSeed: 555
---

# Why manual a11y doesn't scale

<span>What goes wrong when you build it yourself</span>

<div mt-6 />

### For keyboard navigation in a 2D grid...

<br>

<v-clicks depth="2">

- You need to handle <span text-red-400>arrow key navigation</span> in all four directions
- You need to track <span text-violet-400>focus state</span> across potentially hundreds of items
- You need to handle <span text-purple-400>edge cases</span> like:
  - First/last item wrapping
  - Row boundaries
  - Disabled items
- You need to implement <span text-fuchsia-400>typeahead search</span> for quick item selection
- You need to support <span text-pink-400>RTL layouts</span> where arrow directions are reversed
- You need to add <span text-sky-400>screen reader announcements</span> for every state change

</v-clicks>

<!--
For keyboard navigation in a 2D grid...

[click] You need to handle arrow key navigation in all four directions

[click] You need to track focus state across potentially hundreds of items

[click] You need to handle edge cases like first/last item wrapping, row boundaries, and disabled items

[click] You need to implement typeahead search for quick item selection

[click] You need to support RTL layouts where arrow directions are reversed

[click] And you need to add screen reader announcements for every state change
-->

---
glowSeed: 560
---

# The cost of manual a11y

<span>Why this approach fails at scale</span>

<div mt-6 />

### This manual approach is...

<br>

<v-clicks depth="2">

- <span text-red-400>Error-prone</span> - one missed edge case breaks the entire experience for keyboard users
- <span text-red-400>Hard to test</span> - how do you even write tests for "focus moves correctly"?
- <span text-red-400>Missing edge cases</span> - you will forget something (everyone does)
- <span text-red-400>Not screen-reader friendly</span> - announcing state changes requires aria-live regions, role management
- <span text-red-400>A maintenance nightmare</span> - 200+ lines of code just for arrow keys, and it grows with features
- <span text-red-400>Not future-proof</span> - new requirements mean rewriting fragile logic

</v-clicks>

<!--
This manual approach is...

[click] Error-prone - one missed edge case breaks the entire experience for keyboard users

[click] Hard to test - how do you even write tests for "focus moves correctly"?

[click] Missing edge cases - you will forget something, everyone does

[click] Not screen-reader friendly - announcing state changes requires aria-live regions and role management

[click] A maintenance nightmare - 200+ lines of code just for arrow keys, and it grows with every feature

[click] Not future-proof - new requirements mean rewriting fragile logic
-->

---
glowSeed: 580
---

<div flex>
  <div flex-1>
    <h1 mb="0!">a11y in the Real World</h1>
    <span text="sm white/50 nowrap">What the industry says about accessibility</span>
  </div>
  <div flex items-center>
    <div i-simple-icons:adobe text-4xl text-red-500 mr-2 />
  </div>
</div>

<div v-click border-l="4 solid violet-500" bg="violet-900/20" pl-4 py-2 mt-4 rounded-r>

**Adobe's accessibility research:**

Building accessible components from scratch requires <span v-mark="{ at: 2, color: 'rgb(144, 200, 255)', type: 'underline' }">deep ARIA expertise</span>. Most developers lack the time to learn these intricacies, leading to <span v-mark="{ at: 3, color: 'rgb(144, 200, 255)', type: 'underline' }">inaccessible experiences</span>.

</div>

<div v-click="4" border-l="4 solid purple-500" bg="purple-900/20" pl-4 py-2 mt-4 rounded-r>

**The business case:**

Over <span v-mark="{ at: 5, color: 'rgb(144, 200, 255)', type: 'underline' }">1 billion people</span> worldwide have disabilities. Inaccessible websites don't just fail morally - they <span v-mark="{ at: 6, color: 'rgb(144, 200, 255)', type: 'underline' }">lose customers</span> and face legal risk.

</div>

<div v-click="7" border-l="4 solid fuchsia-500" bg="fuchsia-900/20" pl-4 py-2 mt-4 rounded-r>

**The solution:**

React Aria provides <span v-mark="{ at: 8, color: 'rgb(144, 200, 255)', type: 'underline' }">accessibility primitives</span> that handle the hard parts, letting developers focus on <span v-mark="{ at: 9, color: 'rgb(144, 200, 255)', type: 'underline' }">building features</span>.

</div>

<!--
Adobe's accessibility research shows:

[click] Building accessible components from scratch requires deep ARIA expertise.

[click] Most developers lack time to learn these, leading to inaccessible experiences.

[click] The business case is clear - over 1 billion people have disabilities.

[click] Inaccessible websites lose customers and face legal risk.

[click] React Aria provides accessibility primitives.

[click] This lets developers focus on building features.
-->

---
glowSeed: 600
---

# React Aria Features

<span>What you get out of the box</span>

<div mt-8 />

<div flex items-center gap-4>

<v-clicks>
  <div
    :class="$clicks < 1 ? 'translate-x--20' : 'translate-x-0'"
    rounded-lg
    border="2 solid purple-800" bg="purple-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:keyboard h-16 w-16 />
    </div>
    <div bg="purple-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Full keyboard navigation</span>
    </div>
  </div>
  <div
    :class="$clicks < 2 ? 'translate-x--20' : 'translate-x-0'"
    rounded-lg
    border="2 solid violet-800" bg="violet-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:center-to-fit h-16 w-16 />
    </div>
    <div bg="violet-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Focus management</span>
    </div>
  </div>
  <div
    :class="$clicks < 3 ? 'translate-x--20' : 'translate-x-0'"
    rounded-lg
    border="2 solid indigo-800" bg="indigo-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:accessibility h-16 w-16 />
    </div>
    <div bg="indigo-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Screen reader support</span>
    </div>
  </div>
  <div
    :class="$clicks < 4 ? 'translate-x--20' : 'translate-x-0'"
    rounded-lg
    border="2 solid blue-800" bg="blue-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:text-selection h-16 w-16 />
    </div>
    <div bg="blue-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Selection patterns</span>
    </div>
  </div>
  <div
    :class="$clicks < 5 ? 'translate-x--20' : 'translate-x-0'"
    rounded-lg
    border="2 solid sky-800" bg="sky-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-12 flex items-center justify-center>
      <div i-carbon:globe h-16 w-16 />
    </div>
    <div bg="sky-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>RTL & i18n</span>
    </div>
  </div>
</v-clicks>

</div>

<!--
What does React Aria give you out of the box?

[click] Full keyboard navigation - arrow keys, Tab, Enter, Escape, all handled correctly

[click] Focus management - focus trapping in modals, focus restoration, roving tabindex

[click] Screen reader support - proper ARIA attributes, live announcements, semantic structure

[click] Selection patterns - single, multiple, none - all with correct keyboard and mouse behavior

[click] RTL and internationalization - right-to-left layouts just work, no extra code
-->

---
glow: right
glowSeed: 620
---

# How React Aria Works

<span>The mental model for using primitives</span>

<div mt-6 />

### React Aria follows a simple pattern...

<br>

<v-clicks depth="2">

- <span text-violet-400>Hooks for behavior</span> - `useButton`, `useListBox`, `useComboBox` handle all the logic
  - Keyboard events, focus management, ARIA attributes
  - You bring your own styling and DOM structure
- <span text-purple-400>Components for convenience</span> - pre-built components when you want less control
  - `<Button>`, `<ListBox>`, `<ComboBox>` work out of the box
  - Still fully styleable with CSS
- <span text-fuchsia-400>State hooks for complex patterns</span> - `useListState`, `useSelectState` manage collections
  - Selection, disabled items, virtualization
  - Works with any data shape
- <span text-pink-400>Composition over configuration</span> - build complex UIs from simple primitives
  - Combine `useSearchField` + `useListBox` for autocomplete
  - Each piece is independently testable

</v-clicks>

<!--
React Aria follows a simple pattern:

[click] Hooks for behavior - useButton, useListBox handle all the logic, you bring styling

[click] Components for convenience - pre-built when you want less control

[click] State hooks for complex patterns - manage collections, selection, virtualization

[click] Composition over configuration - build complex UIs from simple primitives
-->

---
glowSeed: 650
---

# Concrete a11y Wins

<span>What we actually implemented</span>

<div mt-6 />

<div grid grid-cols-3 gap-4>

<div v-click border="2 solid violet-800/50" rounded-lg overflow-hidden>
  <div flex items-center bg="violet-800/30" px-3 py-3>
    <div i-carbon:center-to-fit text-xl mr-2 text-violet-400 />
    <span font-semibold text-sm>Focus Trap</span>
  </div>
  <div bg="violet-800/10" px-4 py-3 text-sm>
    <div text-zinc-300>Modal & drawer focus cycling</div>
    <div mt-2 font-mono text-xs bg="zinc-900" rounded px-2 py-1>
      Tab cycles within modal
    </div>
    <div mt-2 text-xs text-zinc-500>
      Without: focus escapes to background
    </div>
  </div>
</div>

<div v-click border="2 solid purple-800/50" rounded-lg overflow-hidden>
  <div flex items-center bg="purple-800/30" px-3 py-3>
    <div i-carbon:keyboard text-xl mr-2 text-purple-400 />
    <span font-semibold text-sm>:focus-visible</span>
  </div>
  <div bg="purple-800/10" px-4 py-3 text-sm>
    <div text-zinc-300>Keyboard-only outlines</div>
    <div mt-2 font-mono text-xs bg="zinc-900" rounded px-2 py-1>
      :focus-visible { outline: 2px }
    </div>
    <div mt-2 text-xs text-zinc-500>
      Without: outlines on mouse click
    </div>
  </div>
</div>

<div v-click border="2 solid fuchsia-800/50" rounded-lg overflow-hidden>
  <div flex items-center bg="fuchsia-800/30" px-3 py-3>
    <div i-carbon:view-off text-xl mr-2 text-fuchsia-400 />
    <span font-semibold text-sm>Inert Background</span>
  </div>
  <div bg="fuchsia-800/10" px-4 py-3 text-sm>
    <div text-zinc-300>aria-hidden on backdrop</div>
    <div mt-2 font-mono text-xs bg="zinc-900" rounded px-2 py-1>
      inert attribute on body
    </div>
    <div mt-2 text-xs text-zinc-500>
      Without: screen reader reads bg
    </div>
  </div>
</div>

</div>

<div v-click mt-6>
  <div border="2 solid zinc-700" bg="zinc-800/20" rounded-lg px-4 py-3>
    <div flex items-center gap-2>
      <div i-carbon:idea text-yellow-400 />
      <span>React Aria handles all of this. We just use the components correctly.</span>
    </div>
  </div>
</div>

<!--
Here are three concrete wins:

[click] Focus trap - when a modal opens, Tab cycles within it. Without this, focus escapes to the background.

[click] Focus-visible - outlines only appear on keyboard navigation, not mouse clicks. Cleaner UX for mouse users, still accessible for keyboard users.

[click] Inert background - when a modal is open, the background is marked inert. Screen readers won't read background content.

[click] The best part: React Aria handles all of this. We just use the components correctly.
-->

---
glowSeed: 700
---

# What We Built

<span>Bringing it all together</span>

<div mt-10 />

<div flex items-center gap-4>

<v-clicks>
  <div
    :class="$clicks < 1 ? 'translate-y-10 opacity-0' : 'translate-y-0 opacity-100'"
    rounded-lg
    border="2 solid violet-800" bg="violet-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-10 flex items-center justify-center>
      <div i-carbon:link h-12 w-12 />
    </div>
    <div bg="violet-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>URL as state</span>
    </div>
  </div>
  <div
    :class="$clicks < 2 ? 'translate-y-10 opacity-0' : 'translate-y-0 opacity-100'"
    rounded-lg
    border="2 solid purple-800" bg="purple-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-10 flex items-center justify-center>
      <div i-carbon:layers h-12 w-12 />
    </div>
    <div bg="purple-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Layered architecture</span>
    </div>
  </div>
  <div
    :class="$clicks < 3 ? 'translate-y-10 opacity-0' : 'translate-y-0 opacity-100'"
    rounded-lg
    border="2 solid fuchsia-800" bg="fuchsia-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-10 flex items-center justify-center>
      <div i-carbon:accessibility h-12 w-12 />
    </div>
    <div bg="fuchsia-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>a11y via primitives</span>
    </div>
  </div>
  <div
    :class="$clicks < 4 ? 'translate-y-10 opacity-0' : 'translate-y-0 opacity-100'"
    rounded-lg
    border="2 solid pink-800" bg="pink-800/20"
    backdrop-blur
    flex-1 h-full
    transition duration-500 ease-in-out
  >
    <div px-5 py-10 flex items-center justify-center>
      <div i-carbon:api h-12 w-12 />
    </div>
    <div bg="pink-800/30" w-full px-4 py-2 h="4rem" flex items-center justify-center text-center text-sm>
      <span>Clean interfaces</span>
    </div>
  </div>
</v-clicks>

</div>

<div v-click mt-10 flex justify-center>
  <div border="2 solid zinc-700" bg="zinc-800/40" rounded-lg px-8 py-4>
    <span text-lg>DX-first interfaces <div i-carbon:arrow-right inline-block translate-y-0.5 mx-2 /> accelerate UX delivery</span>
  </div>
</div>

<!--
So what did we actually build?

[click] URL as the source of truth - shareable, bookmarkable, survives refresh

[click] Layered architecture - each layer has single responsibility, easy to reason about

[click] Accessibility through primitives - React Aria does the heavy lifting

[click] Clean interfaces - components don't care about implementation details

[click] The through line: DX-first interfaces accelerate UX delivery.
-->

---
glow: right
glowSeed: 750
---

# Key Takeaways

<span>What to remember from this talk</span>

<div mt-8 />

<div flex flex-col gap-4>

<v-clicks>

<div border="2 solid violet-800/50" rounded-lg>
  <div bg="violet-800/10" px-4 py-4 flex items-start gap-4>
    <div i-carbon:number-1 text-2xl text-violet-400 mt-1 />
    <div>
      <div font-semibold>Code has two consumers</div>
      <div text-sm text-zinc-400 mt-1>Developers and users. Solve for devs to ship better UX faster.</div>
    </div>
  </div>
</div>

<div border="2 solid purple-800/50" rounded-lg>
  <div bg="purple-800/10" px-4 py-4 flex items-start gap-4>
    <div i-carbon:number-2 text-2xl text-purple-400 mt-1 />
    <div>
      <div font-semibold>URL is your friend for search</div>
      <div text-sm text-zinc-400 mt-1>Shareable, bookmarkable, survives refresh, back/forward works.</div>
    </div>
  </div>
</div>

<div border="2 solid fuchsia-800/50" rounded-lg>
  <div bg="fuchsia-800/10" px-4 py-4 flex items-start gap-4>
    <div i-carbon:number-3 text-2xl text-fuchsia-400 mt-1 />
    <div>
      <div font-semibold>Layers reduce cognitive load</div>
      <div text-sm text-zinc-400 mt-1>Each layer talks only to adjacent layers. Components don't know about APIs.</div>
    </div>
  </div>
</div>

<div border="2 solid pink-800/50" rounded-lg>
  <div bg="pink-800/10" px-4 py-4 flex items-start gap-4>
    <div i-carbon:number-4 text-2xl text-pink-400 mt-1 />
    <div>
      <div font-semibold>Use primitives for a11y</div>
      <div text-sm text-zinc-400 mt-1>React Aria gives you WCAG compliance. Don't reinvent focus management.</div>
    </div>
  </div>
</div>

</v-clicks>

</div>

<!--
Four key takeaways:

[click] Code has two consumers - developers and users. Solve for devs to ship better UX faster.

[click] URL is your friend for search - it's shareable, bookmarkable, survives refresh, and back/forward works.

[click] Layers reduce cognitive load - each layer talks only to adjacent layers.

[click] Use primitives for accessibility - React Aria gives you WCAG compliance out of the box.
-->

---
glowSeed: 800
---

# What's Next

<span>Where we're heading</span>

<div mt-12 />

<div flex justify-center gap-8>

<v-clicks>

<div border="2 solid violet-800/50" rounded-lg w-60>
  <div px-5 py-8 flex flex-col items-center justify-center text-center>
    <div i-carbon:machine-learning-model text-4xl text-violet-400 mb-4 />
    <span font-semibold>AI Suggestions</span>
    <span text-sm text-zinc-400 mt-2>Smart query completions</span>
  </div>
</div>

<div border="2 solid purple-800/50" rounded-lg w-60>
  <div px-5 py-8 flex flex-col items-center justify-center text-center>
    <div i-carbon:analytics text-4xl text-purple-400 mb-4 />
    <span font-semibold>Search Analytics</span>
    <span text-sm text-zinc-400 mt-2>Understand user intent</span>
  </div>
</div>

<div border="2 solid fuchsia-800/50" rounded-lg w-60>
  <div px-5 py-8 flex flex-col items-center justify-center text-center>
    <div i-carbon:bookmark text-4xl text-fuchsia-400 mb-4 />
    <span font-semibold>Saved Searches</span>
    <span text-sm text-zinc-400 mt-2>Return to your queries</span>
  </div>
</div>

</v-clicks>

</div>

<!--
What's next for search at smallcase?

[click] AI suggestions - smart query completions based on context

[click] Search analytics - understanding user intent at scale

[click] Saved searches - let users return to their favorite queries
-->

---
glowSeed: 850
---

# Resources

<span>Links and references</span>

<div mt-10 />

<div flex flex-col gap-4>

<div border="2 solid zinc-700/50" rounded-lg>
  <div bg="zinc-800/20" px-4 py-3 flex items-center gap-4>
    <div i-carbon:book text-xl text-violet-400 />
    <div>
      <div font-semibold>React Aria Components</div>
      <div text-sm text-zinc-400>react-spectrum.adobe.com/react-aria</div>
    </div>
  </div>
</div>

<div border="2 solid zinc-700/50" rounded-lg>
  <div bg="zinc-800/20" px-4 py-3 flex items-center gap-4>
    <div i-carbon:accessibility text-xl text-purple-400 />
    <div>
      <div font-semibold>WCAG Guidelines</div>
      <div text-sm text-zinc-400>w3.org/WAI/standards-guidelines/wcag</div>
    </div>
  </div>
</div>

<div border="2 solid zinc-700/50" rounded-lg>
  <div bg="zinc-800/20" px-4 py-3 flex items-center gap-4>
    <div i-carbon:code text-xl text-fuchsia-400 />
    <div>
      <div font-semibold>Downshift (alternative)</div>
      <div text-sm text-zinc-400>github.com/downshift-js/downshift</div>
    </div>
  </div>
</div>

</div>

<div mt-10 text-center>
  <div border="2 solid zinc-700" bg="zinc-800/40" rounded-lg px-6 py-3 inline-block>
    <span>Two consumers: </span>
    <span text-violet-400><div i-carbon:code inline-block translate-y-0.5 mr-1 />Developer</span>
    <span mx-2>+</span>
    <span text-sky-400><div i-carbon:user inline-block translate-y-0.5 mr-1 />User</span>
  </div>
</div>

<!--
Some resources if you want to dive deeper:

React Aria Components for accessible UI primitives, WCAG guidelines for the standards, and Downshift as an alternative approach for comboboxes.

Remember the thesis: two consumers - developer and user. Solve for both.
-->

---
layout: center
class: text-center
glowSeed: 900
---

<h1 text-6xl mb-8>
  Thank You!
</h1>

<div flex justify-center gap-8 mt-8>
  <div flex items-center gap-2 text-zinc-400>
    <div i-carbon:logo-twitter />
    <span>@omkar_k45</span>
  </div>
  <div flex items-center gap-2 text-zinc-400>
    <div i-carbon:logo-github />
    <span>OmkarK45</span>
  </div>
</div>

<div mt-16>
  <svg h-8 xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="386" height="98" viewBox="0 0 386 98"><defs><path id="a" d="M0 0h386.538v100H0z"/></defs><g fill="none" fill-rule="evenodd" transform="translate(-1 -1)"><mask id="b" fill="#fff"><use xlink:href="#a"/></mask><path fill="#fff" d="M380.108 46.39c-.147-3.624-3.069-6.816-7.453-6.816-4.823 0-7.6 3.046-8.037 6.815h15.49zm-7.306-12.325c7.89 0 13.736 5.8 13.736 13.776 0 .582 0 1.594-.147 2.03 0 .723-.73 1.306-1.315 1.306h-20.898c0 4.06 3.801 8.12 9.062 8.12 3.507 0 5.552-1.304 7.451-2.463.587-.437 1.172-.583 1.756.144l1.75 2.757c.586.577.733 1.156-.144 2.03-2.193 1.885-6.138 3.77-11.251 3.77-9.209 0-15.052-7.105-15.052-15.664 0-8.555 5.847-15.806 15.052-15.806m-40.914 28.422c-.438-.288-.88-.869-.585-1.596l1.316-2.753c.29-.58 1.168-.868 1.896-.433 1.758 1.013 3.945 2.173 7.452 2.173 2.484 0 3.947-1.163 3.947-2.9 0-2.029-2.339-3.334-6.429-5.22-4.679-2.033-8.182-4.494-8.182-9.426 0-3.773 2.627-8.125 9.935-8.125 4.238 0 7.307 1.306 8.766 2.177.732.579 1.026 1.45.585 2.175l-1.021 2.029c-.438.87-1.316.87-1.901.582-2.044-.87-4.092-1.448-6.429-1.448-2.629 0-3.797 1.302-3.797 2.61 0 1.882 2.187 3.042 5.113 4.351 5.55 2.317 9.792 4.348 9.792 9.859 0 4.641-4.094 8.703-10.817 8.703-4.528.29-7.89-1.595-9.645-2.758zm-21.192-2.32c3.071 0 6.14-2.174 7.018-3.623V51.61c-.44-.29-2.782-1.017-5.553-1.017-3.51 0-6.287 1.89-6.287 4.932.147 2.612 1.757 4.64 4.822 4.64m1.027-14.357c3.065 0 6.134.87 6.134.87.147-4.785-1.021-6.812-4.822-6.812-3.507 0-6.867 1.014-8.473 1.448-.878.143-1.463-.434-1.753-1.305l-.587-2.465c-.144-1.016.294-1.45 1.024-1.744.582-.143 4.823-1.737 10.374-1.737 9.645 0 10.522 5.8 10.522 13.195v15.952a1.566 1.566 0 0 1-1.463 1.452h-2.19c-.588 0-.879-.289-1.173-1.014l-.727-2.032a13.05 13.05 0 0 1-9.352 3.769c-5.7 0-9.792-3.769-9.792-10.003.147-5.367 4.532-9.57 12.278-9.57zm-28.351-11.745c4.679 0 8.184 1.737 10.96 5.217.585.729.434 1.596-.29 2.177l-2.339 2.178c-.878.723-1.463.143-1.902-.292-1.312-1.45-3.798-3.046-6.282-3.046-5.113 0-9.209 4.207-9.209 9.426 0 5.367 3.949 9.572 8.918 9.572 3.945 0 5.551-2.173 7.16-3.77.58-.581 1.315-.581 2.042-.147l2.05 1.598c.728.58 1.02 1.306.58 2.175-2.483 3.769-6.571 6.234-11.832 6.234-8.476 0-15.491-6.669-15.491-15.662.147-8.7 7.306-15.66 15.639-15.66zM253.856 20.72c0-.723.584-1.448 1.46-1.448h3.653a1.565 1.565 0 0 1 1.46 1.448v42.642a1.565 1.565 0 0 1-1.46 1.448h-3.65a1.46 1.46 0 0 1-1.463-1.452zm-16.075 0c0-.723.585-1.448 1.461-1.448h3.654a1.565 1.565 0 0 1 1.46 1.448v42.642a1.565 1.565 0 0 1-1.46 1.448h-3.65a1.46 1.46 0 0 1-1.465-1.452zM215.28 60.166c3.067 0 6.135-2.173 7.012-3.622V51.61c-.436-.29-2.776-1.017-5.553-1.017-3.506 0-6.281 1.89-6.281 4.932 0 2.612 1.606 4.64 4.822 4.64m.878-14.356c3.067 0 6.134.87 6.134.87.147-4.785-1.021-6.812-4.822-6.812-3.505 0-6.865 1.014-8.471 1.448-.88.143-1.465-.434-1.755-1.305l-.587-2.465c-.144-1.016.29-1.45 1.025-1.744.583-.143 4.822-1.737 10.373-1.737 9.645 0 10.668 5.8 10.668 13.195v15.952a1.57 1.57 0 0 1-1.461 1.452h-2.193c-.584 0-.874-.289-1.312-1.014l-.734-2.032a13.05 13.05 0 0 1-9.349 3.769c-5.702 0-9.792-3.769-9.792-10.003.147-5.367 4.53-9.57 12.276-9.57zm-64.295-9.572c0-.725.581-1.448 1.459-1.448h1.46c.731 0 1.173.289 1.316.87l.878 2.609c.581-.723 3.797-4.204 9.645-4.204 4.382 0 7.011 1.737 9.205 4.786.877-.87 4.384-4.786 10.226-4.786 9.21 0 11.547 6.38 11.547 14.212v15.081c0 .801-.656 1.452-1.463 1.452h-3.65c-.878 0-1.465-.58-1.465-1.452V47.987c0-4.786-1.897-7.688-5.989-7.688-4.531 0-6.722 3.046-7.308 3.48.148.581.291 2.466.291 4.062v15.521c0 .72-.583 1.448-1.312 1.448h-3.801c-.878 0-1.459-.58-1.459-1.452V47.987c0-4.932-1.755-7.688-5.994-7.688-4.528 0-6.867 3.338-7.158 4.355v18.704a1.566 1.566 0 0 1-1.462 1.452h-3.65a1.457 1.457 0 0 1-1.463-1.452v-27.12zm-27.62 26.25c-.437-.29-.878-.87-.584-1.597l1.314-2.753c.294-.58 1.172-.868 1.902-.433 1.75 1.013 3.945 2.173 7.45 2.173 2.486 0 3.945-1.163 3.945-2.9 0-2.029-2.337-3.334-6.429-5.22-4.675-2.033-8.182-4.494-8.182-9.426 0-3.773 2.63-8.125 9.936-8.125 4.237 0 7.308 1.306 8.767 2.177.73.579 1.025 1.45.587 2.175l-1.025 2.029c-.436.87-1.312.87-1.899.582-2.042-.87-4.092-1.448-6.43-1.448-2.628 0-3.8 1.302-3.8 2.61 0 1.882 2.193 3.042 5.117 4.351 5.553 2.317 9.788 4.348 9.788 9.859 0 4.641-4.088 8.703-10.815 8.703-4.526.29-7.887-1.595-9.643-2.758m-80.67-49.11 16.803 8.104a1.653 1.653 0 0 1 .773 2.22 1.66 1.66 0 0 1-.743.756l-16.3 8.281a1.74 1.74 0 0 1-1.533 0l-16.801-8.1a1.657 1.657 0 0 1-.032-2.974l16.3-8.283a1.74 1.74 0 0 1 1.532-.003m.12 30.777 39.774-20.208a1.654 1.654 0 0 0-.036-2.97L44 1.965a1.72 1.72 0 0 0-1.526 0L2.7 22.163a1.657 1.657 0 0 0 .034 2.975l39.447 19.01a1.72 1.72 0 0 0 1.511 0zm33.421 14.56c-.3 6.896-4.077 13.178-10.047 16.714-5.536 2.824-10.027-.07-10.023-6.482.296-6.894 4.074-13.18 10.047-16.716 5.535-2.824 10.023.083 10.023 6.48zm11.74 17.348V31.12a1.69 1.69 0 0 0-1.707-1.668 1.7 1.7 0 0 0-.772.189L46.247 50.128c-.56.281-.913.851-.915 1.474v44.944a1.69 1.69 0 0 0 1.707 1.668 1.7 1.7 0 0 0 .771-.188l40.14-20.487a1.66 1.66 0 0 0 .903-1.476M26.799 80.01 8.738 71.334a1.66 1.66 0 0 1-.785-2.217q.053-.103.116-.198l9.04-13.295a1.713 1.713 0 0 1 2.369-.449c.274.185.488.444.615.747l9.043 21.955a1.66 1.66 0 0 1-.857 2.192 1.68 1.68 0 0 1-1.48-.063z" mask="url(#b)"/></g></svg>
</div>

<!--
Thank you! Questions?
-->
