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
class: py-10
glowSeed: 120
---

# The Thesis: Two Consumers

<span>Every line of code serves two masters</span>

<div mt-16 />

<div flex items-center justify-center gap-16>
  <div
    v-click flex flex-col gap-2 items-center justify-center transition duration-500 ease-in-out
    :class="$clicks < 1 ? 'translate-x--20 opacity-0' : 'translate-x-0 opacity-100'"
  >
    <div flex items-center gap-6>
      <div i-carbon:code text-8xl text-violet-400 />
    </div>
    <span text-2xl mt-4>Developer</span>
    <span text-zinc-400 text-sm>DX</span>
  </div>
  <div
    v-after flex flex-col items-center justify-center transition duration-500 ease-in-out delay-300
    :class="$clicks < 1 ? 'scale-0' : 'scale-100'"
  >
    <div i-carbon:arrows-horizontal text-6xl text-zinc-500 />
  </div>
  <div
    v-after flex flex-col gap-2 items-center justify-center transition duration-500 ease-in-out
    :class="$clicks < 1 ? 'translate-x-20 opacity-0' : 'translate-x-0 opacity-100'"
  >
    <div flex items-center gap-6>
      <div i-carbon:user text-8xl text-sky-400 />
    </div>
    <span text-2xl mt-4>User</span>
    <span text-zinc-400 text-sm>UX</span>
  </div>
</div>

<div v-click mt-16 text-center>
  <div border="2 solid zinc-700" bg="zinc-800/40" rounded-lg px-8 py-4 inline-block>
    <span text-lg>Solve for devs <div i-carbon:arrow-right inline-block translate-y-0.5 mx-2 /> ship better UX faster</span>
  </div>
</div>

<!--
Here's the core idea:

[click] Code has two consumers - developers who write and maintain it, and users who interact with the final product.

[click] When we solve for developer experience first, we ship better user experiences faster. Good DX accelerates UX delivery.
-->

---
class: py-10
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
class: py-10
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
class: py-10
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
class: py-10
glow: bottom
glowSeed: 300
---

# The Layered Flow

<span>The architecture that made it work</span>

<div mt-8 />

<div flex justify-center>
  <div flex flex-col gap-3 w-140>
    <div v-click border="2 solid sky-600" bg="sky-800/30" rounded-lg px-6 py-4 flex items-center gap-4>
      <div i-carbon:link text-2xl text-sky-400 />
      <div flex-1>
        <div font-semibold>URL</div>
        <div text-sm text-zinc-400>Source of truth</div>
      </div>
    </div>
    <div v-click flex justify-center>
      <div i-carbon:arrow-down text-2xl text-zinc-500 />
    </div>
    <div v-click border="2 solid violet-600" bg="violet-800/30" rounded-lg px-6 py-4 flex items-center gap-4>
      <div i-carbon:code text-2xl text-violet-400 />
      <div flex-1>
        <div font-semibold>useUrlTabParams</div>
        <div text-sm text-zinc-400>Decode / Encode layer</div>
      </div>
    </div>
    <div v-click flex justify-center>
      <div i-carbon:arrow-down text-2xl text-zinc-500 />
    </div>
    <div v-click border="2 solid purple-600" bg="purple-800/30" rounded-lg px-6 py-4 flex items-center gap-4>
      <div i-carbon:flow text-2xl text-purple-400 />
      <div flex-1>
        <div font-semibold>SearchPageContext</div>
        <div text-sm text-zinc-400>Actions & state orchestration</div>
      </div>
    </div>
    <div v-click flex justify-center>
      <div i-carbon:arrow-down text-2xl text-zinc-500 />
    </div>
    <div v-click border="2 solid fuchsia-600" bg="fuchsia-800/30" rounded-lg px-6 py-4 flex items-center gap-4>
      <div i-carbon:application text-2xl text-fuchsia-400 />
      <div flex-1>
        <div font-semibold>UI Components</div>
        <div text-sm text-zinc-400>Buttons, filters, cards</div>
      </div>
    </div>
    <div v-click flex justify-center>
      <div i-carbon:arrow-down text-2xl text-zinc-500 />
    </div>
    <div v-click border="2 solid pink-600" bg="pink-800/30" rounded-lg px-6 py-4 flex items-center gap-4>
      <div i-carbon:api text-2xl text-pink-400 />
      <div flex-1>
        <div font-semibold>Infrastructure</div>
        <div text-sm text-zinc-400>React Query / API calls</div>
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
class: py-10
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
class: py-10
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
<SearchPageProvider>
  <UrlSyncProvider>
    <FilterProvider>
      <SearchResults />
    </FilterProvider>
  </UrlSyncProvider>
</SearchPageProvider>
```

</div>

<!--
Why Context over Redux or Zustand?

[click] Context gives us feature-scoped state, natural co-location with URL sync, no extra dependencies, and a natural provider hierarchy.

[click] Global state managers are overkill here - we'd need extra plumbing to sync with URL, and it's global by default when we want feature-scoped.

[click] This is what the provider hierarchy looks like - clean, readable, each provider has a single responsibility.
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
class: py-10
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
class: py-10
glowSeed: 550
---

# The Problem: Manual a11y Doesn't Scale

<span>What 2D grid navigation looks like by hand</span>

<div mt-6 />

<div v-click>

```ts {all|3-6|7-10|11-15}
function handleKeyDown(e: KeyboardEvent) {
  const currentIndex = items.findIndex(item => item.id === focusedId)

  switch (e.key) {
    case 'ArrowRight':
      const nextIndex = currentIndex + 1
      if (nextIndex < items.length)
        setFocusedId(items[nextIndex].id)
      break
    case 'ArrowLeft':
      const prevIndex = currentIndex - 1
      if (prevIndex >= 0)
        setFocusedId(items[prevIndex].id)
      break
    case 'ArrowDown':
      const belowIndex = currentIndex + columnsPerRow
      if (belowIndex < items.length)
        setFocusedId(items[belowIndex].id)
      break
    // ... and 200+ more lines for edge cases
  }
}
```

</div>

<div v-click mt-6>
  <div border="2 solid red-800/50" bg="red-800/20" rounded-lg px-4 py-3>
    <div flex items-center gap-2>
      <div i-carbon:warning text-red-400 />
      <span>Missing: focus management, typeahead, RTL support, screen reader announcements, disabled items...</span>
    </div>
  </div>
</div>

<!--
[click] Here's what manual 2D grid navigation looks like. Just the basics - arrow keys to move around.

[click] Arrow right and left for horizontal movement

[click] Arrow down for vertical movement

[click] And this is just the start. We're missing focus management, typeahead search, RTL support, screen reader announcements, disabled item handling... The list goes on. This doesn't scale.
-->

---
class: py-10
glow: right
glowSeed: 600
---

# The Solution: React Aria Components

<span>Get a11y for free with the right primitives</span>

<div mt-6 />

<div flex gap-6>

<div v-click flex-1>
  <div text-sm font-semibold mb-3 text-zinc-400>Manual implementation needs:</div>
  <div flex flex-col gap-2 text-sm>
    <div flex items-center gap-2>
      <div i-carbon:close-outline text-red-400 />
      <span>Focus refs management</span>
    </div>
    <div flex items-center gap-2>
      <div i-carbon:close-outline text-red-400 />
      <span>Keyboard event handling</span>
    </div>
    <div flex items-center gap-2>
      <div i-carbon:close-outline text-red-400 />
      <span>Screen reader announcements</span>
    </div>
    <div flex items-center gap-2>
      <div i-carbon:close-outline text-red-400 />
      <span>Typeahead search</span>
    </div>
    <div flex items-center gap-2>
      <div i-carbon:close-outline text-red-400 />
      <span>RTL support</span>
    </div>
    <div flex items-center gap-2>
      <div i-carbon:close-outline text-red-400 />
      <span>Disabled item handling</span>
    </div>
    <div flex items-center gap-2>
      <div i-carbon:close-outline text-red-400 />
      <span>Selection management</span>
    </div>
  </div>
</div>

<div v-click flex-1>
  <div text-sm font-semibold mb-3 text-zinc-400>React Aria gives you:</div>

```tsx
<GridList
  aria-label="Search results"
  layout="grid"
  selectionMode="single"
>
  {items.map(item => (
    <GridListItem key={item.id}>
      {item.name}
    </GridListItem>
  ))}
</GridList>
```

  <div mt-4 flex flex-col gap-1 text-sm>
    <div flex items-center gap-2>
      <div i-carbon:checkmark-outline text-green-400 />
      <span>All of the above, free</span>
    </div>
    <div flex items-center gap-2>
      <div i-carbon:checkmark-outline text-green-400 />
      <span>WCAG compliant</span>
    </div>
    <div flex items-center gap-2>
      <div i-carbon:checkmark-outline text-green-400 />
      <span>Tested across browsers</span>
    </div>
  </div>
</div>

</div>

<!--
[click] Manual implementation requires handling all of these - focus management, keyboard events, screen reader announcements, typeahead, RTL, disabled items, selection...

[click] With React Aria, you get all of that with a simple declarative API. GridList with layout="grid" - done. It's WCAG compliant and tested across browsers.
-->

---
class: py-10
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
class: py-10
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
class: py-10
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
class: py-10
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
class: py-10
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

<div text-6xl mb-8>
  Thank You
</div>

<div flex justify-center gap-8 mt-8>
  <div flex items-center gap-2 text-zinc-400>
    <div i-carbon:logo-twitter />
    <span>@omkar_k_</span>
  </div>
  <div flex items-center gap-2 text-zinc-400>
    <div i-carbon:logo-github />
    <span>puresamari</span>
  </div>
</div>

<div mt-16>
  <svg h-8 xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="386" height="98" viewBox="0 0 386 98"><defs><path id="a" d="M0 0h386.538v100H0z"/></defs><g fill="none" fill-rule="evenodd" transform="translate(-1 -1)"><mask id="b" fill="#fff"><use xlink:href="#a"/></mask><path fill="#fff" d="M380.108 46.39c-.147-3.624-3.069-6.816-7.453-6.816-4.823 0-7.6 3.046-8.037 6.815h15.49zm-7.306-12.325c7.89 0 13.736 5.8 13.736 13.776 0 .582 0 1.594-.147 2.03 0 .723-.73 1.306-1.315 1.306h-20.898c0 4.06 3.801 8.12 9.062 8.12 3.507 0 5.552-1.304 7.451-2.463.587-.437 1.172-.583 1.756.144l1.75 2.757c.586.577.733 1.156-.144 2.03-2.193 1.885-6.138 3.77-11.251 3.77-9.209 0-15.052-7.105-15.052-15.664 0-8.555 5.847-15.806 15.052-15.806m-40.914 28.422c-.438-.288-.88-.869-.585-1.596l1.316-2.753c.29-.58 1.168-.868 1.896-.433 1.758 1.013 3.945 2.173 7.452 2.173 2.484 0 3.947-1.163 3.947-2.9 0-2.029-2.339-3.334-6.429-5.22-4.679-2.033-8.182-4.494-8.182-9.426 0-3.773 2.627-8.125 9.935-8.125 4.238 0 7.307 1.306 8.766 2.177.732.579 1.026 1.45.585 2.175l-1.021 2.029c-.438.87-1.316.87-1.901.582-2.044-.87-4.092-1.448-6.429-1.448-2.629 0-3.797 1.302-3.797 2.61 0 1.882 2.187 3.042 5.113 4.351 5.55 2.317 9.792 4.348 9.792 9.859 0 4.641-4.094 8.703-10.817 8.703-4.528.29-7.89-1.595-9.645-2.758zm-21.192-2.32c3.071 0 6.14-2.174 7.018-3.623V51.61c-.44-.29-2.782-1.017-5.553-1.017-3.51 0-6.287 1.89-6.287 4.932.147 2.612 1.757 4.64 4.822 4.64m1.027-14.357c3.065 0 6.134.87 6.134.87.147-4.785-1.021-6.812-4.822-6.812-3.507 0-6.867 1.014-8.473 1.448-.878.143-1.463-.434-1.753-1.305l-.587-2.465c-.144-1.016.294-1.45 1.024-1.744.582-.143 4.823-1.737 10.374-1.737 9.645 0 10.522 5.8 10.522 13.195v15.952a1.566 1.566 0 0 1-1.463 1.452h-2.19c-.588 0-.879-.289-1.173-1.014l-.727-2.032a13.05 13.05 0 0 1-9.352 3.769c-5.7 0-9.792-3.769-9.792-10.003.147-5.367 4.532-9.57 12.278-9.57zm-28.351-11.745c4.679 0 8.184 1.737 10.96 5.217.585.729.434 1.596-.29 2.177l-2.339 2.178c-.878.723-1.463.143-1.902-.292-1.312-1.45-3.798-3.046-6.282-3.046-5.113 0-9.209 4.207-9.209 9.426 0 5.367 3.949 9.572 8.918 9.572 3.945 0 5.551-2.173 7.16-3.77.58-.581 1.315-.581 2.042-.147l2.05 1.598c.728.58 1.02 1.306.58 2.175-2.483 3.769-6.571 6.234-11.832 6.234-8.476 0-15.491-6.669-15.491-15.662.147-8.7 7.306-15.66 15.639-15.66zM253.856 20.72c0-.723.584-1.448 1.46-1.448h3.653a1.565 1.565 0 0 1 1.46 1.448v42.642a1.565 1.565 0 0 1-1.46 1.448h-3.65a1.46 1.46 0 0 1-1.463-1.452zm-16.075 0c0-.723.585-1.448 1.461-1.448h3.654a1.565 1.565 0 0 1 1.46 1.448v42.642a1.565 1.565 0 0 1-1.46 1.448h-3.65a1.46 1.46 0 0 1-1.465-1.452zM215.28 60.166c3.067 0 6.135-2.173 7.012-3.622V51.61c-.436-.29-2.776-1.017-5.553-1.017-3.506 0-6.281 1.89-6.281 4.932 0 2.612 1.606 4.64 4.822 4.64m.878-14.356c3.067 0 6.134.87 6.134.87.147-4.785-1.021-6.812-4.822-6.812-3.505 0-6.865 1.014-8.471 1.448-.88.143-1.465-.434-1.755-1.305l-.587-2.465c-.144-1.016.29-1.45 1.025-1.744.583-.143 4.822-1.737 10.373-1.737 9.645 0 10.668 5.8 10.668 13.195v15.952a1.57 1.57 0 0 1-1.461 1.452h-2.193c-.584 0-.874-.289-1.312-1.014l-.734-2.032a13.05 13.05 0 0 1-9.349 3.769c-5.702 0-9.792-3.769-9.792-10.003.147-5.367 4.53-9.57 12.276-9.57zm-64.295-9.572c0-.725.581-1.448 1.459-1.448h1.46c.731 0 1.173.289 1.316.87l.878 2.609c.581-.723 3.797-4.204 9.645-4.204 4.382 0 7.011 1.737 9.205 4.786.877-.87 4.384-4.786 10.226-4.786 9.21 0 11.547 6.38 11.547 14.212v15.081c0 .801-.656 1.452-1.463 1.452h-3.65c-.878 0-1.465-.58-1.465-1.452V47.987c0-4.786-1.897-7.688-5.989-7.688-4.531 0-6.722 3.046-7.308 3.48.148.581.291 2.466.291 4.062v15.521c0 .72-.583 1.448-1.312 1.448h-3.801c-.878 0-1.459-.58-1.459-1.452V47.987c0-4.932-1.755-7.688-5.994-7.688-4.528 0-6.867 3.338-7.158 4.355v18.704a1.566 1.566 0 0 1-1.462 1.452h-3.65a1.457 1.457 0 0 1-1.463-1.452v-27.12zm-27.62 26.25c-.437-.29-.878-.87-.584-1.597l1.314-2.753c.294-.58 1.172-.868 1.902-.433 1.75 1.013 3.945 2.173 7.45 2.173 2.486 0 3.945-1.163 3.945-2.9 0-2.029-2.337-3.334-6.429-5.22-4.675-2.033-8.182-4.494-8.182-9.426 0-3.773 2.63-8.125 9.936-8.125 4.237 0 7.308 1.306 8.767 2.177.73.579 1.025 1.45.587 2.175l-1.025 2.029c-.436.87-1.312.87-1.899.582-2.042-.87-4.092-1.448-6.43-1.448-2.628 0-3.8 1.302-3.8 2.61 0 1.882 2.193 3.042 5.117 4.351 5.553 2.317 9.788 4.348 9.788 9.859 0 4.641-4.088 8.703-10.815 8.703-4.526.29-7.887-1.595-9.643-2.758m-80.67-49.11 16.803 8.104a1.653 1.653 0 0 1 .773 2.22 1.66 1.66 0 0 1-.743.756l-16.3 8.281a1.74 1.74 0 0 1-1.533 0l-16.801-8.1a1.657 1.657 0 0 1-.032-2.974l16.3-8.283a1.74 1.74 0 0 1 1.532-.003m.12 30.777 39.774-20.208a1.654 1.654 0 0 0-.036-2.97L44 1.965a1.72 1.72 0 0 0-1.526 0L2.7 22.163a1.657 1.657 0 0 0 .034 2.975l39.447 19.01a1.72 1.72 0 0 0 1.511 0zm33.421 14.56c-.3 6.896-4.077 13.178-10.047 16.714-5.536 2.824-10.027-.07-10.023-6.482.296-6.894 4.074-13.18 10.047-16.716 5.535-2.824 10.023.083 10.023 6.48zm11.74 17.348V31.12a1.69 1.69 0 0 0-1.707-1.668 1.7 1.7 0 0 0-.772.189L46.247 50.128c-.56.281-.913.851-.915 1.474v44.944a1.69 1.69 0 0 0 1.707 1.668 1.7 1.7 0 0 0 .771-.188l40.14-20.487a1.66 1.66 0 0 0 .903-1.476M26.799 80.01 8.738 71.334a1.66 1.66 0 0 1-.785-2.217q.053-.103.116-.198l9.04-13.295a1.713 1.713 0 0 1 2.369-.449c.274.185.488.444.615.747l9.043 21.955a1.66 1.66 0 0 1-.857 2.192 1.68 1.68 0 0 1-1.48-.063z" mask="url(#b)"/></g></svg>
</div>

<!--
Thank you! Questions?
-->
