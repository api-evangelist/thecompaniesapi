---
name: Run bulk work through the Actions queue
description: Estimate, submit, poll and retry long-running enrichment and export jobs instead of bursting synchronous calls against the per-second rate limit.
api: openapi/thecompaniesapi-actions-api-openapi.yml
operations: [requestAction, fetchActions, retryAction, fetchTeam]
generated: '2026-08-14'
method: generated
source: openapi/_original/thecompaniesapi-openapi.yml + https://www.thecompaniesapi.com/api/request-action
---

# Run bulk work through the Actions queue

Base URL `https://api.thecompaniesapi.com/v2`. Authenticate with `Authorization: Basic MY-API-TOKEN`.

Anything large — bulk enrichment, a full-list export, a deep segment that trips `maxScrollResultsReached` — belongs in the Actions queue, not in a loop of synchronous requests. The queue is what keeps a big job from colliding with the per-second rate limit (50 / 250 / 1,000 RPS by plan).

## 1. Estimate first

`requestAction` (`POST /v2/actions`) is documented as "request **or estimate** a new action". Estimate before committing: an `Action` carries a `cost` field, and credits are the binding quota on this API. Check `fetchTeam` (`GET /v2/teams/{teamId}`) for the current `credits` balance and compare.

Required input includes the action `type`; omitting it returns `400 typeMissing`, and an unknown type returns `400 actionTypeInvalid`. When the action targets a saved list, pass a valid `listId` — a bad one returns `400 invalidListId`.

## 2. Submit

Submit the action and keep the returned `id`. The `Action` record carries `id`, `type`, `status`, `attempts`, `cost`, `data`, `result`, `listId`, `promptId`, `teamId`, `createdAt`, `updatedAt`.

**There is no idempotency key on this API.** A retried `POST /v2/actions` queues a *second* job and spends credits again. Record the returned `id` before any retry logic can fire, and never blind-retry a submission on a timeout — poll instead.

## 3. Poll

`fetchActions` (`GET /v2/actions`) lists and filters your actions. Poll on the `status` field with a backoff rather than a tight loop; each poll is a request against the same per-second limit. A list's `unseenActions` array is another place completed jobs surface.

## 4. Or be told

If a webhook is configured in account settings, results are delivered when the operation ends rather than polled. That is the intended path for the "notify me when a new company profile is enriched" pattern. Event names, payload shape, signing and retry behaviour are not published — treat the webhook as a trigger to re-read state through the API rather than as a trusted payload.

## 5. Retry a failure

`retryAction` (`POST /v2/actions/{actionId}/retry`) re-runs a failed action. `400 invalidActionId` means the id is wrong; `400 actionTypeInvalid` means the action's type cannot be retried. Watch `attempts` so you do not loop forever.

## Errors

| Status | `messages` | What to do |
|---|---|---|
| 400 | `typeMissing`, `actionTypeInvalid`, `invalidListId`, `invalidActionId` | Fix the request. Do not retry unchanged. |
| 401 | `missingApiSecret`, `invalidApiSecret`, `tokenNotFound`, `userNotAuthenticated` | Auth. |
| 403 | `invalidPromptId` | The referenced prompt does not belong to this team. |
| 403 | `noCreditsRemaining` | Stop. Buying credits is a human decision. |
| 429 | — | Throttled. Exponential backoff with jitter; no `Retry-After` is returned. |

Health of the service itself is available unauthenticated at `GET /` (`fetchApiHealth`) and on the status page at https://status.thecompaniesapi.com/en/.
