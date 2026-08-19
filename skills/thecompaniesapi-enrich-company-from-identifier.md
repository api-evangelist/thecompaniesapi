---
name: Enrich a company from a domain, email or social profile
description: Turn any identifier you already hold — a website domain, a work email address, or a LinkedIn/social URL — into a full company profile from The Companies API, without wasting credits.
api: openapi/thecompaniesapi-companies-api-openapi.yml
operations: [fetchCompany, fetchCompanyByEmail, fetchCompanyBySocial, fetchCompanyContext, fetchCompanyEmailPatterns]
generated: '2026-08-14'
method: generated
source: openapi/_original/thecompaniesapi-openapi.yml + https://www.thecompaniesapi.com/api/enrich-company-from-domain
---

# Enrich a company from an identifier

Base URL `https://api.thecompaniesapi.com`. All resources sit under `/v2`.

## Authenticate

Send the API token in the `Authorization` header **with the `Basic ` prefix**:

```
Authorization: Basic MY-API-TOKEN
```

The published OpenAPI declares only `apiKey in header: Authorization` and does not record the prefix. A bare token returns `401 missingApiSecret`. The documented `?token=MY-API-TOKEN` query parameter also works but puts the credential in the URL — use it only for a manual test, never from an agent.

## Pick the right operation

| You hold | Operation | Path |
|---|---|---|
| a domain (`microsoft.com`) | `fetchCompany` | `GET /v2/companies/{domain}` |
| a work email | `fetchCompanyByEmail` | `GET /v2/companies/by-email` |
| a LinkedIn or other social URL | `fetchCompanyBySocial` | `GET /v2/companies/by-social` |

## Spend credits deliberately

`fetchCompany` costs **1 credit**. Two modifiers change that:

- `?simplified=true` — returns a reduced profile and costs **0 credits**. Use this whenever you only need identity fields (name, domain, industry, size). Confirm it satisfies the need before paying for the full record.
- `?refresh=true` — triggers a live crawl of the website and social profiles plus AI enrichment, costing **10 additional credits**. Only use it when freshness genuinely matters (signup-time enrichment, a stale CRM row).

If no company is found, the API returns an empty object and charges nothing. Do not treat an empty object as an error.

## Read the meta envelope every time

Responses carry a `meta` object:

- `meta.cost` — credits this call consumed
- `meta.credits` — credits remaining on the account
- `meta.freeRequest` — true when the call was served free

Credits, not requests, are the binding quota. Stop or escalate when `meta.credits` approaches zero; exhaustion surfaces as `403 noCreditsRemaining`, **not** `429`.

## Go deeper on the same company

- `fetchCompanyContext` — `GET /v2/companies/{domain}/context` returns an AI-generated summary of what the company does and who it serves.
- `fetchCompanyEmailPatterns` — `GET /v2/companies/{domain}/email-patterns` returns observed address patterns with a usage percentage.

## Handle errors

Errors are plain `application/json`. The specification returns `{messages, status, details}` where `messages` is a machine-readable enum; the human docs describe a different `{error: {code, message, type}}` envelope. Read `messages` first and fall back to `error.type`.

| Status | `messages` | What to do |
|---|---|---|
| 401 | `missingApiSecret`, `invalidApiSecret`, `tokenNotFound` | Fix the header (remember `Basic `) or regenerate the token. |
| 403 | `noCreditsRemaining` | Stop. Buying credits or changing plan is a human decision. |
| 404 | `companyNotFound` | The identifier does not resolve. Do not retry. |
| 429 | — | Throttled. Back off exponentially with jitter; no `Retry-After` header is sent. |

There is no idempotency key and no request-id header on this API. Reads are safe to retry; keep your own correlation id.
