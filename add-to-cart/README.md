# ShopDemo — Add to Cart UI

A clean, responsive e-commerce product listing and cart interface built with vanilla JavaScript and Bootstrap 5. No frameworks. No build tools. Just HTML, CSS, and JS that works out of the box.

---

## What It Does

ShopDemo is a frontend-only shopping cart demo that showcases real-world UI patterns you'd find in any production e-commerce app — product cards, quantity selectors, a slide-out cart, toast notifications, and a checkout stub — all wired together without a single dependency beyond Bootstrap.

It's intentionally lightweight: open the file in a browser and it just works.

---

## Features

- **Product grid** — six products rendered dynamically from a JavaScript data array, so swapping in real API data is a one-line change
- **Per-card quantity selector** — increment/decrement before adding, resets to 1 after each add
- **Live cart state** — items accumulate correctly; adding the same product multiple times stacks the quantity
- **Offcanvas cart panel** — slides in from the right, lists all items with subtotals, and shows a running total
- **Remove items** — one-click removal updates the total instantly
- **Animated cart badge** — bounces on every add so the user always knows something happened
- **Green "Added!" flash** — the button briefly confirms the action before resetting
- **Toast notifications** — bottom-right toast names the item that was just added
- **Checkout stub** — fires a summary alert and clears the cart, ready to be swapped for a real payment flow
- **Fully responsive** — single column on mobile, two on tablet, three on desktop

---

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 |
| Styling | CSS3 custom properties + Bootstrap 5.3 |
| Icons | Bootstrap Icons 1.11 |
| Logic | Vanilla JavaScript (ES6+) |
| Build tools | None |

---

## Project Structure

```
shopdemo/
└── index.html      # Everything lives here — styles, markup, and script
```

This is a single-file project by design. It's a self-contained demo, easy to share, inspect, and extend.

---

## Getting Started

No install. No terminal. Just open it.

```bash
# Option 1 — open directly
open index.html

# Option 2 — serve locally (avoids any browser file:// quirks)
npx serve .
# then visit http://localhost:3000
```

---

## How the Cart Logic Works

State lives in two plain objects:

```js
let cart = {};       // { productId: { product, qty } }
let quantities = {}; // per-card selector state, separate from cart
```

`cart` tracks what's been added and how many. `quantities` tracks what the user has dialled up on a card *before* clicking Add — these are intentionally separate so adjusting the selector doesn't affect items already in the cart.

When a product is added:

1. If the product is already in the cart, its `qty` is incremented by however many were selected
2. The card's selector resets to 1
3. `updateCartUI()` recalculates the total and re-renders the offcanvas

No libraries, no state management overhead.

---

## Customising the Products

Products are defined in a plain array near the top of the script. Swap in your own data or replace it with a `fetch()` call to any REST API:

```js
const products = [
  { id: 1, name: "Air Max Nairobi", emoji: "👟", price: 8500, desc: "Lightweight everyday runner." },
  // add more here, or replace with: const products = await fetch('/api/products').then(r => r.json())
];
```

Prices are formatted as Kenyan Shillings (`KES`) throughout. Change the currency label in `renderProducts()` and `updateCartUI()` to match your locale.

---

## What's Left to Build (Intentional Stubs)

This demo is designed as a starting point. Here's what a production version would add:

- **Real checkout** — replace the `checkout()` alert with an M-Pesa Daraja STK push or a Stripe/Flutterwave payment call
- **Product images** — swap the emoji placeholders for `<img>` tags pointing to real product photos
- **Backend persistence** — POST the cart to a Node/Express or Django API before checkout
- **Auth** — gate checkout behind a login flow; persist the cart to the user's account
- **Quantity editing in cart** — currently you can only remove items, not adjust qty from the offcanvas
- **Stock validation** — disable Add when qty exceeds available stock

---

## Browser Support

Works in any modern browser. No polyfills needed. Bootstrap 5 drops IE11 support and this project follows suit.

---

## License

MIT — use it, fork it, build on it.
