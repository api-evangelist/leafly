# Leafly (leafly)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
