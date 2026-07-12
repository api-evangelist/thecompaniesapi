# The Companies API (thecompaniesapi)

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
