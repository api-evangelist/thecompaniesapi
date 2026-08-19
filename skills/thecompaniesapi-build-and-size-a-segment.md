---
name: Build, size and page a company segment
description: Turn a target-market description into a Companies API segmentation, count it before you pay for it, then page the results without burning credits or hitting the per-second limit.
api: openapi/thecompaniesapi-companies-api-openapi.yml
operations: [searchCompaniesByPrompt, promptToSegmentation, countCompanies, countCompaniesPost, searchCompanies, searchCompaniesPost, searchCompaniesByName, searchSimilarCompanies]
generated: '2026-08-14'
method: generated
source: openapi/_original/thecompaniesapi-openapi.yml + https://www.thecompaniesapi.com/api
---

# Build, size and page a company segment

Base URL `https://api.thecompaniesapi.com/v2`. Authenticate with `Authorization: Basic MY-API-TOKEN`.

## 1. Express the target market

Two entry points, depending on what you have:

- **Plain language** — `searchCompaniesByPrompt` (`GET /v2/companies/by-prompt`). Describe the companies you want ("B2B SaaS companies in Germany with fewer than 50 employees").
- **Structured** — `promptToSegmentation` (`POST /v2/prompts/segmentation`) converts a natural-language query into the segmentation array, so you can inspect and edit the filters before running them.

## 2. Understand the query language

A segmentation is an array of conditions, each `{attribute, operator, sign, values}` (`SegmentationCondition` in the specification). The same array is echoed back on every search response as `query`, so you can always read what actually ran rather than what you thought you asked for.

Supporting parameters on `searchCompanies`: `search`, `searchFields`, `sortKey`, `sortFields`, `sortOrder`, `domainsToExclude`, `linkedinToExclude`, `simplified`, `page`, `size`.

Use `searchCompaniesPost` (`POST /v2/companies`) when the segmentation is too large for a query string.

## 3. Count before you page

Call `countCompanies` (`GET /v2/companies/count`) or `countCompaniesPost` (`POST /v2/companies/count`) with the same segmentation **first**. Sizing the segment is how you find out whether paging it is affordable before you spend anything on results.

## 4. Page the results

Paging is page-number based: `page` and `size`. The response envelope is `{companies, meta, query}` and `meta` carries `currentPage`, `firstPage`, `lastPage`, `perPage`, `total`, `cost`, `credits` and `maxScrollResultsReached`.

Rules:

- Stop when `currentPage == lastPage`.
- If `maxScrollResultsReached` is true you have hit the deep-paging ceiling — do not keep incrementing `page`. Narrow the segmentation, or move the job to the Actions queue (see the bulk-export skill).
- Watch `meta.credits` on every page, not just the first.
- Stay under the plan's per-second limit (50 / 250 / 1,000 RPS by tier). No `RateLimit-*` or `Retry-After` headers are returned, so pace yourself and back off exponentially on `429`.

## 5. Adjacent lookups

- `searchCompaniesByName` (`GET /v2/companies/by-name`) — name search, the right operation behind an autocomplete box. Returns `400 companyNameEmpty` on a blank term.
- `searchSimilarCompanies` (`GET /v2/companies/similar`) — lookalikes from one or more seed domains, for expanding a segment from customers you already have.

## 6. Persist what you found

Hand the segment to `createList` (`POST /v2/lists`) to save it, and mark the list dynamic if you want it to keep updating as new matching companies are detected. See the list-management skill.

## Errors

`401 missingApiSecret` / `invalidApiSecret` — auth. `403 noCreditsRemaining` — stop, this is a human decision. `400 companyNameEmpty` — empty name search. `429` — throttled, back off.
