# URL as State Manager

<div class="grid grid-cols-2 gap-8 mt-8">

<div>
<div class="text-sm opacity-50 mb-3">Traditional Approach</div>

```tsx {*}{maxHeight:'280px'}
function ProductList() {
  const [filters, setFilters] = useState({
    category: '',
    minPrice: 0,
    maxPrice: 1000,
    sortBy: 'popular'
  })
  const [page, setPage] = useState(1)
  const [searchTerm, setSearchTerm] = useState('')

  // User applies filters...
  // Then shares the link 🔗
  // Recipient sees default state 😢

  return (
    <div>
      <SearchBar
        value={searchTerm}
        onChange={setSearchTerm}
      />
      <Filters
        filters={filters}
        onChange={setFilters}
      />
      <Products
        filters={filters}
        search={searchTerm}
        page={page}
      />
    </div>
  )
}
```

<div v-click class="mt-3 p-3 rounded-lg bg-red-500/10 border border-red-500/30 text-sm">
  <span class="text-red-400">✗</span> State is lost on refresh
</div>

</div>

<div v-click>
<div class="text-sm opacity-50 mb-3">URL as State</div>

```tsx {*}{maxHeight:'280px'}
function ProductList() {
  const [searchParams] = useSearchParams()

  const filters = {
    category: searchParams.get('category') ?? '',
    minPrice: searchParams.get('min') ?? 0,
    maxPrice: searchParams.get('max') ?? 1000,
    sortBy: searchParams.get('sort') ?? 'popular'
  }
  const page = searchParams.get('page') ?? 1
  const searchTerm = searchParams.get('q') ?? ''

  // User applies filters...
  // URL: /products?q=laptop&min=500&sort=price
  // Share link → Perfect! ✨

  return (
    <div>
      <SearchBar
        value={searchTerm}
        onChange={q => setSearchParams({ ...filters, q })}
      />
      <Filters
        filters={filters}
        onChange={f => setSearchParams({ ...f, page: 1 })}
      />
      <Products
        filters={filters}
        search={searchTerm}
        page={page}
      />
    </div>
  )
}
```

<div class="mt-3 grid grid-cols-2 gap-2">
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Shareable
  </div>
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Bookmarkable
  </div>
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Browser back/forward
  </div>
  <div class="p-2 rounded-lg bg-green-500/10 border border-green-500/30 text-xs">
    <span class="text-green-400">✓</span> Survives refresh
  </div>
</div>

</div>

</div>

---
