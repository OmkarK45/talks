# Real World: 2D Navigation Flyout Menu

<div class="grid grid-cols-2 gap-8 mt-6">

<div>
  <div class="text-sm opacity-50 mb-3">Smallcase All Products Menu</div>
  <div class="border border-white/10 rounded-xl overflow-hidden bg-white/5" style="min-height: 400px;">
    <video src="/products-menu.mov" controls autoplay loop muted class="w-full h-full object-cover"></video>
  </div>
</div>

<div>
<div class="text-sm opacity-50 mb-3">Implementation with React Aria</div>

```tsx {*}{maxHeight:'380px'}
function HeaderAllProductsMenu() {
  const [isOpen, setIsOpen] = useState(false)

  return (
    <DialogTrigger isOpen={isOpen} onOpenChange={setIsOpen}>
      <Button aria-label="See all products">
        All Products
        <IconChevronDown />
      </Button>

      <Popover placement="bottom right">
        <ListBox
          layout="grid"
          orientation="horizontal"
          shouldFocusWrap
          autoFocus
        >
          {/* Investments Section */}
          <ListBoxSection id="invest">
            <Header>Investments</Header>
            <ListBoxItem href="/smallcases">
              Stock & ETF smallcases
            </ListBoxItem>
            <ListBoxItem href="/mutual-funds">
              Mutual Funds
            </ListBoxItem>
            <ListBoxItem href="/stocks">
              Stocks & ETFs
            </ListBoxItem>
          </ListBoxSection>

          {/* Credit Section */}
          <ListBoxSection id="credit">
            <Header>Credit</Header>
            <ListBoxItem href="/loans/mutual-funds">
              Loans against Mutual Funds
            </ListBoxItem>
            <ListBoxItem href="/loans/stocks">
              Loans against Stocks
            </ListBoxItem>
          </ListBoxSection>

          {/* More Section */}
          <ListBoxSection id="other">
            <Header>More</Header>
            <ListBoxItem href="/create">
              Create
            </ListBoxItem>
            <ListBoxItem href="/tickertape">
              Tickertape
            </ListBoxItem>
          </ListBoxSection>
        </ListBox>
      </Popover>
    </DialogTrigger>
  )
}
```

</div>

</div>

<div v-click class="mt-6 grid grid-cols-3 gap-3">
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> 2D arrow key navigation
  </div>
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> Focus management
  </div>
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> Screen reader support
  </div>
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> Keyboard navigation
  </div>
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> Touch & mouse support
  </div>
  <div class="p-3 rounded-lg bg-green-500/10 border border-green-500/30 text-sm">
    <span class="text-green-400">✓</span> RTL support
  </div>
</div>
