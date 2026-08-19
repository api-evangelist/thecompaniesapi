---
name: Create and maintain saved company lists
description: Save a segment as a list, add and remove companies, keep it updating automatically, and read the analytics attached to it.
api: openapi/thecompaniesapi-lists-api-openapi.yml
operations: [fetchLists, createList, updateList, deleteList, fetchCompaniesInList, fetchCompaniesInListPost, fetchCompanyInList, toggleCompaniesInList, fetchCompaniesAnalytics, exportCompaniesAnalytics]
generated: '2026-08-14'
method: generated
source: openapi/_original/thecompaniesapi-openapi.yml + https://www.thecompaniesapi.com/api/fetch-lists + https://updates.thecompaniesapi.com/changelog
---

# Create and maintain saved company lists

Base URL `https://api.thecompaniesapi.com/v2`. Authenticate with `Authorization: Basic MY-API-TOKEN`.

A list is per-team state, keyed by a numeric `id`, owned by `teamId`. Lists are the persistence layer for the search surface.

## Operations

| Do | Operation | Path |
|---|---|---|
| See what exists | `fetchLists` | `GET /v2/lists` |
| Create one | `createList` | `POST /v2/lists` |
| Rename / reconfigure | `updateList` | `PATCH /v2/lists/{listId}` |
| Delete | `deleteList` | `DELETE /v2/lists/{listId}` |
| Read members | `fetchCompaniesInList` | `GET /v2/lists/{listId}/companies` |
| Read members with a big segmentation | `fetchCompaniesInListPost` | `POST /v2/lists/{listId}/companies` |
| Check one member | `fetchCompanyInList` | `GET /v2/lists/{listId}/companies/{domain}` |
| Add or remove members | `toggleCompaniesInList` | `PATCH /v2/lists/{listId}/companies/toggle` |

## Dynamic lists

Set `dynamic` on the list and it keeps updating in real time as newly detected companies match its criteria. Pair it with a webhook (configured in account settings) to act on each new match — push to a CRM, trigger an internal workflow, alert on a technology adoption. The event names and payload shape are not published; they are only visible in the dashboard.

Other fields worth reading on `List`: `query` (the saved segmentation), `querySimilar`, `maxCompanies`, `processActive` / `processInitialized` / `processingAt` / `processMessage` (the background job state), `unseenActions` (queued actions attached to the list), `analytics`, `exporting` / `exportingAt`.

## Toggle is a toggle, not an append

`toggleCompaniesInList` flips membership. Read the current state with `fetchCompanyInList` before toggling if you need a deterministic add or remove — there is no idempotency key on this API, so a retried toggle will undo itself.

Adding the same company twice costs nothing and creates no duplicate: a company cannot belong to a list twice.

## Analytics on a list

`fetchCompaniesAnalytics` (`GET /v2/companies/analytics`) aggregates any list or segmentation — group by industry, technology stack, social presence, traffic range, company size, NAICS/SIC. Up to 10,000 companies in a single call, documented as free to use.

`exportCompaniesAnalytics` (`POST /v2/companies/analytics/export`) exports the same aggregate as CSV, JSON or XLS.

## Errors

| Status | `messages` | Meaning |
|---|---|---|
| 400 | `listNotFound` | The `listId` does not exist. Note this arrives as **400**, not 404. |
| 400 | `invalidListId` | Malformed id. |
| 403 | `userCurrentTeamIsNotInstanceOwner` | The list belongs to another team. Do not retry. |
| 404 | `companyNotFound` | The domain does not resolve. |
| 401 | `missingApiSecret` / `invalidApiSecret` / `tokenNotFound` | Auth. |
