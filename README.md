# PAKKO Fulfillment

Responsive marketing website, seller portal and installable PWA using the supplied PAKKO screen reference. A Capacitor configuration is included for packaging the same experience for iOS and Android. No native binaries have been built or submitted.

## Run

Node 20+ required. The web application has no runtime dependencies.

```
npm test
npm run build
npm start
```

Open http://localhost:3000. Deploy `dist/` to a static host; Vercel configuration is included. Hash routing supports direct links on static hosting without rewrite rules. Production HTTPS enables offline service worker and home-screen installation.

## Mobile packaging

Install the declared Capacitor dependencies with `npm install`, then:

```
npm run build
npx cap add android
npx cap add ios
npm run mobile:sync
```

Open the generated projects with Android Studio or Xcode. Native signing, store assets, platform testing and store distribution remain deployment tasks. For production, set the final reverse-domain application ID before first release.

## Routes

- `/`: responsive public website
- `/splash`, `/onboarding`: reference introduction screens
- `/login`, `/signup`, `/forgot-password`: clearly labeled authentication previews
- `/home`: seller dashboard
- `/orders`, `/orders/new`, `/orders/:id`: list, create, detail, item and timeline tabs
- `/inventory`, `/inventory/new`, `/inventory/:id`: searchable inventory and editable products
- `/shipments`, `/tracking`, `/tracking/:id`: shipment list and demo lookup
- `/reports`: workspace totals and CSV export
- `/more`, `/profile`, `/addresses`, `/shipping-settings`, `/payment-methods`, `/notifications`, `/settings`
- `/help`, `/services`, `/privacy`, `/terms`
- Unrecognized routes render a recovery screen.

URLs use `/#/route`.

## What works

Orders validate customer details and reserve stock atomically, including duplicate product lines. Inventory, profile, addresses and shipping preferences persist in browser localStorage. Filters, searches, tracking lookup, detail tabs and CSV export are interactive. The demo can be reset in Settings. Offline application shell is cached by the service worker.

## Production boundary

This is a frontend demo, not a live warehouse system. No backend, real authentication, OAuth, password recovery, multi-user storage, payments, emails or courier APIs are connected. Support requests are saved locally and are not sent. Do not enter real passwords or sensitive customer information. Sample shipment milestones are explicitly labeled. Actual dashboard numbers are calculated from sample records, rather than displaying unsupported counts from the visual reference.

Before production: implement server-side tenant isolation and authorization, durable inventory transactions with idempotency, courier integration and verified webhooks, notifications, billing, audit logging, backup/recovery, rate limits and approved legal policies. Replace the preview auth routes with a configured provider. Inventory reservations currently have no cancellation/release workflow.

## Design assets

`public/assets/reference.jpeg` is the user-supplied visual reference. The PAKKO logos and photographic areas are displayed as CSS crops of that exact image, preserving the supplied artwork rather than inventing a substitute. This source limits sharpness at large desktop sizes. Obtain original logo and licensed full-resolution photographs before commercial launch. The app icon is a complementary package symbol, not a replacement logo.

## Verification

`npm test` covers successful reservation, duplicate-line stock overflow without partial mutation, invalid inputs, stock thresholds and output escaping. `npm run build` produces a dependency-free static web build. Native builds and live integrations are not covered by these tests.
