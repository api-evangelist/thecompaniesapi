# The Companies API (thecompaniesapi)

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

The Companies API is a company data and enrichment platform offering programmatic access to firmographic, technographic, and web-intelligence data on 50M+ companies. Its REST API (base `https://api.thecompaniesapi.com`, all resources under `/v2`) covers company search and segmentation, company enrichment by domain, email, or social profile, similar-company lookup, industry and technology reference data, location reference data, saved lists, and asynchronous bulk actions. Requests are authenticated with an API token in the `Authorization` header, billing is credit-based, and the full OpenAPI 3.1 description is published at `GET /v2/openapi`.

**Access model (be honest):** The Companies API is a proprietary, hosted commercial service - not open source or self-hostable. Open-source *client SDKs* (TypeScript/JavaScript, Python, Go) are published under [github.com/thecompaniesapi](https://github.com/thecompaniesapi), but the data platform and API are closed and reached only over the hosted endpoints. New accounts receive **500 free credits** (no credit card required) for evaluation; beyond that, usage is billed against a credit-based monthly plan (Startup / Scaleup / Enterprise). There is no documented public WebSocket/streaming API - long-running and bulk work is handled by an asynchronous Actions job queue that is polled over REST.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/thecompaniesapi/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/thecompaniesapi/refs/heads/main/apis.yml)

## Tags

- Company Data
- Data Enrichment
- Firmographics
- Web Intelligence
- B2B Data
- Reference Data
- Company Search

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### The Companies API Company Search API

Search and segment the 50M+ company database with structured segmentation queries, natural-language prompts, or company name. Endpoints include `GET`/`POST /v2/companies`, `GET /v2/companies/by-name`, `GET /v2/companies/by-prompt`, `GET`/`POST /v2/companies/count`, and `GET /v2/companies/similar`.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Company Search
- Firmographics
- B2B Data
- Segmentation

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/thecompaniesapi.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/thecompaniesapi.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### The Companies API Company Enrichment API

Retrieve 100+ data points on a single company by its domain, a work email, or a social-media profile. Endpoints include `GET /v2/companies/{domain}`, `GET /v2/companies/by-email`, `GET /v2/companies/by-social`, `GET /v2/companies/{domain}/context`, `GET /v2/companies/{domain}/email-patterns`, and `POST /v2/companies/{domain}/ask`.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Data Enrichment
- Company Data
- Web Intelligence
- Firmographics

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/thecompaniesapi.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/thecompaniesapi.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### The Companies API Company Analytics API

Aggregate analytics over search segmentations and saved lists for market sizing and firmographic distribution. Endpoints include `GET /v2/companies/analytics` and `POST /v2/companies/analytics/export`.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Analytics
- Firmographics
- B2B Data

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### The Companies API Industries API

Reference data for industry classification used across the company dataset. Endpoints include `GET /v2/industries` and `GET /v2/industries/similar` for building and normalizing segmentation filters.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Industries
- Reference Data
- Classification

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### The Companies API Technologies API

Reference data for the technologies (technographics) detected on company websites, used to build technology-based segments. Endpoint `GET /v2/technologies`.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Technographics
- Reference Data
- Web Intelligence

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### The Companies API Locations API

Geographic reference data for normalizing and filtering companies by location. Endpoints include `GET /v2/locations/cities`, `/v2/locations/counties`, `/v2/locations/states`, `/v2/locations/countries`, and `/v2/locations/continents`.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Reference Data
- Locations
- Geographic

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### The Companies API Lists API

Create and manage saved lists of companies for building and maintaining target datasets. Endpoints include `GET`/`POST /v2/lists`, `PATCH`/`DELETE /v2/lists/{listId}`, `GET`/`POST /v2/lists/{listId}/companies`, `PATCH /v2/lists/{listId}/companies/toggle`, and `GET /v2/lists/{listId}/companies/{domain}`.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Lists
- Data Management
- B2B Data

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### The Companies API Actions API

Queue, estimate, and track asynchronous jobs for bulk enrichment and search workloads. Endpoints include `GET /v2/actions`, `POST /v2/actions`, and `POST /v2/actions/{actionId}/retry`.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Async
- Bulk Enrichment
- Jobs

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### The Companies API Job Titles Enrichment API

Normalize and enrich raw job titles into structured seniority and department signals. Endpoint `GET /v2/job-titles/enrich`.

- **Human URL:** [https://www.thecompaniesapi.com/api](https://www.thecompaniesapi.com/api)
- **Base URL:** `https://api.thecompaniesapi.com/v2`

#### Tags

- Data Enrichment
- Job Titles
- Reference Data

#### Properties

- [Documentation](https://www.thecompaniesapi.com/api)
- [API Reference](https://thecompaniesapi.dev/api)
- [OpenAPI](openapi/thecompaniesapi-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Authentication](authentication/thecompaniesapi-authentication.yml)
- [GitHub Organization](https://github.com/thecompaniesapi)
- [LinkedIn](https://www.linkedin.com/company/thecompaniesapi)
- [Website](https://www.thecompaniesapi.com)
- [Documentation](https://www.thecompaniesapi.com/api)
- [Plans](plans/thecompaniesapi-plans-pricing.yml)
- [Rate Limits](rate-limits/thecompaniesapi-rate-limits.yml)
- [Fin Ops](finops/thecompaniesapi-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
