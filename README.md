# Leafly (leafly)

Leafly is a cannabis discovery marketplace where consumers research strains, read reviews, and browse and order from licensed dispensaries and brands. For retailers and point-of-sale (POS) providers, Leafly exposes a documented **Menu Integration API** that keeps a dispensary's Leafly menu in near-real-time sync with its system of record - pushing item data, variants, inventory, pricing, strain, and cannabinoid information - and a partner-gated **Order (Reservations) API** that lets a POS system receive and manage online orders placed on Leafly.

## Access Model (read this first)

Leafly's APIs are **not a self-serve public developer platform** and there is **no consumer-facing strain/dispensary data API**. Using the APIs requires:

- A **paid Leafly for Retailers subscription** (quoted by sales; tiered by market, product selection, and service level).
- A **Leafly-issued `menu_integration_key`** that scopes every request to one dispensary.
- For POS / system-of-record providers, **onboarding through Partner Ops** (`partners@leafly.com`). Technical questions go to `api-support@leafly.com`.

The **Menu Integration API is publicly documented** via ReDoc/OpenAPI (V1, V1.1, V2). The **Order API's machine-readable specification is behind Cloudflare Access** and is available to onboarded partners only, so it is cataloged here at the capability level - no endpoint surface is fabricated.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/leafly/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/leafly/refs/heads/main/apis.yml)

## Tags

- Cannabis
- Dispensary
- Menu Sync
- POS Integration
- Retail
- Marketplace
- Strains
- Ecommerce

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## APIs

### Leafly Menu Integration API

Near-real-time menu synchronization for dispensaries and their POS / system-of-record providers. The retailer's system pushes menu items - name, type, brand, description, strain, cannabinoid values, per-variant inventory and pricing, images, and pickup availability - so the public Leafly menu stays current.

- **Human URL:** [https://docs.leafly.io/menu-integration-docs/v2.html](https://docs.leafly.io/menu-integration-docs/v2.html)
- **Base URL (V2 production):** `https://api.leafly.com/v2/menu_integration`
- **Base URL (V2 sandbox):** `https://api-sandbox.leafly.io/v2/menu_integration`
- **Auth:** OAuth2 client credentials (V2); API key (V1)

Documented endpoints:

- `GET    /{menu_integration_key}/menu` — read the current menu
- `POST   /{menu_integration_key}/menu/items` — full menu synchronization
- `PUT    /{menu_integration_key}/menu/items` — upsert items
- `DELETE /{menu_integration_key}/menu/items` — delete items
- `GET    /{menu_integration_key}/status` — integration status/health

Updates are processed asynchronously (up to ~2.5 min sandbox, ~5 min production). Recommended sync profile: a full `POST` once per day plus batched `PUT`/`DELETE` as items change.

#### Properties

- [Documentation](https://docs.leafly.io/menu-integration-docs/v2.html)
- [API Reference](https://docs.leafly.io/menu-integration-docs/v2.html)
- [OpenAPI](openapi/leafly-menu-integration-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Leafly Order API (Reservations)

Lets any cannabis POS provider integrate Leafly online orders into its own system. Launched in beta in 2023; requires the retailer to already run V2 of the Menu Integration API. The full reference is published via ReDoc, but the machine-readable spec is behind Cloudflare Access (partner-gated), so endpoints are documented at the capability level only.

- **Human URL:** [https://docs.leafly.io/reservations-api/order-api/](https://docs.leafly.io/reservations-api/order-api/)
- **Access:** partner onboarding via `partners@leafly.com`

#### Properties

- [Documentation](https://docs.leafly.io/reservations-api/order-api/)
- [Announcement](https://www.businesswire.com/news/home/20230926705189/en/Leafly-Announces-New-API-for-Order-Integration)

## Common Properties

- [Website](https://www.leafly.com)
- [Documentation](https://docs.leafly.io/menu-integration-docs/v2.html)
- [LinkedIn](https://www.linkedin.com/company/leafly)
- [Signup (Leafly for Retailers)](https://success.leafly.com/retail)
- [Support (Developer FAQs)](https://help.leafly.com/hc/en-us/categories/20959505132051-Developer-FAQs)
- [Plans](plans/leafly-plans-pricing.yml)
- [Rate Limits](rate-limits/leafly-rate-limits.yml)
- [Fin Ops](finops/leafly-finops.yml)

## WebSocket Review

Does Leafly expose a documented public WebSocket API? **No.** Leafly's documented API surface is request/response REST over HTTPS - a push-by-HTTP Menu Integration API and a partner-gated Order API. No WebSocket (`ws://`/`wss://`) or SSE endpoint is documented. See [review.yml](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
