# Securly

Securly is a K-12 student safety company. Its platform spans web filtering, mobile
device management (MDM), classroom management, and student wellness, self-harm, and
threat monitoring across the web, email, and cloud drives. Securly is deployed by
school districts and integrates deeply with the school technology stack - Google
Workspace, Microsoft 365 / Entra, Apple School Manager, and Student Information
Systems (SIS).

This repository is part of the API Evangelist "all" catalog and documents Securly's
API footprint as an [APIs.json](https://apisjson.org) (0.19) index.

## API access model: gated / district-contract

Securly does **not** publish a public, self-service developer API. There is no
developer portal, no self-signup API key, and no public API reference or OpenAPI.
All Securly capabilities require a school-district contract obtained through Securly
sales. This entry is an **honest gated stub**: it records what is real without
fabricating an endpoint surface.

### What Securly consumes (inbound integration)

Most of Securly's "API" documentation is about connecting Securly *to* the systems a
district already runs. Securly **consumes** these APIs; it does not expose them:

- **Rostering** via OneRoster 1.2, Google Classroom, Schoology, Canvas, ClassLink,
  Securly Sync, or CSV upload. For OneRoster, an admin supplies the SIS's API
  endpoint, Client ID, and Client Secret so Securly can pull roster data.
- **Identity / directory** via Google Workspace and Microsoft 365 / Entra (Azure AD
  OU sync, Office 365 email scanning).
- **Apple device management** via Apple School Manager (ASM), ADE/DEP tokens, and
  VPP content tokens.

### What Securly exposes (the one provider API - gated)

Securly MDM has an **API connections** feature (MDM to Settings to API connections)
that provisions credentials for an approved third-party system to call Securly:

- A **Client ID**, a connection-specific **Password**, an **API URL**, and a
  **Token URL** are issued per tenant for a token-based (OAuth-style) exchange.
- Documented capabilities: pull a **device inventory** (iPads, Macs, Apple TVs) and
  **assign / unassign students** to devices.

These two capabilities are captured in `apis.yml` as:

- `securly:securly-mdm-device-inventory-api`
- `securly:securly-mdm-student-assignment-api`

Both are marked **endpointsModeled** - Securly publishes no endpoint paths, base
URL, or OpenAPI for them, so no specific request/response surface is asserted here.

## WebSocket / real-time

No public WebSocket (`ws://` / `wss://`) or other server-push API is documented
anywhere on Securly's public surface. See `review.yml`.

## Pricing

Securly is sold per student per year under a district contract, tiered by district
size, via contact-sales. Indicative tiers are recorded in
`plans/securly-plans-pricing.yml`. The MDM API connection capability is included
with a district's Securly MDM entitlement rather than sold as a metered API product.

## Files

- `apis.yml` - APIs.json 0.19 index for Securly (two gated, endpoint-modeled MDM APIs).
- `review.yml` - WebSocket / AsyncAPI review and access-model findings.
- `plans/securly-plans-pricing.yml` - indicative per-student, contact-sales pricing.

## Links

- Website: https://www.securly.com/
- Documentation: https://docs.securly.com/
- Support: https://support.securly.com/hc/en-us
- LinkedIn: https://www.linkedin.com/company/securly

## Maintainer

Kin Lane, API Evangelist - kin@apievangelist.com
