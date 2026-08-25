# PharmD Plus — 3-day PoC / MVP plan

## MVP promise

Customers can browse a small, trusted catalogue, sign in with Google, add products to a cart, pay, view their orders, and open a LINE chat with a pharmacist. Administrators can create, update, archive, price, and restock SKUs.

The included `index.html` is an interactive front-end PoC. Its sign-in, cart, and inventory persistence are deliberately local simulations and are not suitable for real customer or medical data.

## Recommended production architecture

Use **Next.js on Vercel + Supabase + Stripe + LINE Official Account** for the first MVP. It is the shortest reliable path for a small team and leaves clean seams for later replacement.

```text
Browser (customer/admin)
        |
   Next.js app
   /shop /account /admin
        |
  Server/API layer -------- Stripe Checkout + webhook
        |                   LINE Official Account link
  Supabase
  - Google OAuth
  - PostgreSQL
  - Row Level Security
  - product images
```

Never call the database with a service key from the browser. Admin access must be enforced server-side and with database policies; hiding an admin button is not authorization.

## Core data model

| Table | Important fields |
|---|---|
| `profiles` | `id`, `email`, `display_name`, `role` (`customer/admin`), timestamps |
| `products` | `id`, `slug`, `name`, `description`, `status`, timestamps |
| `skus` | `id`, `product_id`, `sku` unique, `price_satang`, `stock_qty`, `active` |
| `orders` | `id`, `user_id`, `status`, `total_satang`, `stripe_session_id`, address snapshot |
| `order_items` | `order_id`, `sku_id`, product/SKU name snapshot, unit price, quantity |
| `inventory_events` | `sku_id`, `delta`, `reason`, `admin_id`, timestamp |

Store prices as integer satang, snapshot order item data, archive rather than delete sold SKUs, and update stock in a database transaction. Do not store symptoms or consultation messages in the commerce database; LINE handles the conversation under its own consent/privacy flow.

## Routes and permissions

- Public: `/`, `/shop`, `/product/[slug]`, LINE handoff.
- Signed in: `/cart`, `/checkout`, `/account/orders`.
- Admin only: `/admin/products`, `/admin/orders`, `/admin/inventory`.
- Server endpoints: Stripe session creation and signed webhook; admin product/SKU mutations.

## Three-day execution

### Day 1 — sellable path

- Lock brand, catalogue fields, delivery rules, return/privacy/terms copy.
- Build responsive shop, product detail, cart, and Google OAuth.
- Create schema, seed 5–10 real SKUs, configure row-level permissions.

### Day 2 — money and operations

- Add Stripe-hosted checkout and webhook-driven order creation.
- Build customer order history and admin product/SKU CRUD.
- Add inventory event log, low-stock state, and LINE Official Account deep link.

### Day 3 — trust and launch

- Test customer/admin permission boundaries, payment success/failure, duplicate webhooks, overselling, and mobile UX.
- Add analytics and error monitoring; finalize Thai PDPA consent, terms, refund, shipping, and health disclaimers with qualified counsel.
- Deploy staging, run one real low-value payment, then release production with a rollback checklist.

## Deliberately out of scope

Prescription dispensing, diagnosis, medical records, insurance, pharmacist chat inside the app, subscriptions, discount engines, multi-warehouse inventory, and marketplace sellers. Any regulated medicine workflow needs a separate legal/compliance design before implementation.

## Definition of done

- A customer completes a mobile purchase and receives confirmation.
- Google sign-in survives refresh and logout revokes the session.
- A non-admin cannot read or mutate admin resources by URL or API.
- Stripe webhook retries do not create duplicate orders.
- Two simultaneous purchases cannot make stock negative.
- Admin can add, archive, reprice, and restock an SKU with an audit trail.
- LINE opens the correct official pharmacist account; privacy and response hours are visible.
