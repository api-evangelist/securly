# Securly

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
