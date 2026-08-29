---
name: browser-use-run-a-web-task
description: >-
  Give Browser Use Cloud a natural-language web task, watch it run, and collect the result. Use when an
  agent needs a live website interacted with rather than merely read.
api: browser-use:browser-use-api-v4
base_url: https://api.browser-use.com/api/v4
operations:
  - create_run_runs_post
  - get_run_status_runs__run_id__status_get
  - get_run_events_runs__run_id__events_get
  - get_run_runs__run_id__get
  - cancel_run_runs__run_id__cancel_post
generated: '2026-08-29'
method: generated
source: openapi/browser-use-api-v4-openapi.json + https://docs.browser-use.com/cloud/agent/quickstart
---

# Run a web task on Browser Use Cloud

## Before you start

Authenticate with `X-Browser-Use-API-Key`. Keys are prefixed `bu_` and are minted at
https://cloud.browser-use.com/settings?tab=api-keys&new=1. There is no OAuth path for the REST API —
OAuth (`mcp` scope) covers the MCP resource only.

## 1. Start the run

`POST /runs` (`create_run_runs_post`). The only required field is `task`. Useful optional fields from
`RunCreateRequest`: `model`, `sessionId` (continue an existing conversation), `workspaceId` (persist
files), `browserSettings` (proxy country, profile), `secretBindings`, `judge`, and `maxCostUsd`.

Set `maxCostUsd`. It is the only spend guard the contract offers, and there is no dry-run mode.

```
POST https://api.browser-use.com/api/v4/runs
X-Browser-Use-API-Key: bu_...
{"task": "Find the top Hacker News story and return its title", "model": "gpt-5.6-luna", "maxCostUsd": 0.50}
```

**This call is not retry-safe.** Browser Use publishes no idempotency key. If the response is lost, do
not blindly resend — call `list_runs_runs_get` and look for your task first.

## 2. Poll

`GET /runs/{run_id}/status` (`get_run_status_runs__run_id__status_get`) is the cheap poll. Use
`GET /runs/{run_id}/events` (`get_run_events_runs__run_id__events_get`) when you need step detail;
events are ordered and incremental, so pass the last id you saw. The `browser.ready` event carries
`live_view_url` — embed it if a human may need to take over.

## 3. Read the result

`GET /runs/{run_id}` (`get_run_runs__run_id__get`) returns `RunSummary`: `result`, `error`,
`judgement`, `totalInputTokens`, `totalOutputTokens`, `totalCostUsd`.

## 4. Stop it if you must

`POST /runs/{run_id}/cancel` (`cancel_run_runs__run_id__cancel_post`) works any time before the run is
terminal, and is idempotent on a run that already finished. Once cancelled, the gateway refuses further
model calls, so the project cannot be billed further.

## Errors to expect

| Status | Meaning | Do this |
|---|---|---|
| 402 | Project has no credits | Top up; this is the quota wall, not 429 |
| 403 | Zero Data Retention is enabled (V4 unsupported) | Use v3/v2 or disable ZDR — this is declared on 15 v4 operations |
| 409 | Session already has an active run | Wait or cancel before starting another in the same session |
| 422 | Validation error | Read `detail[].loc` |
| 429 | Too many concurrent active sessions | Concurrency, not request rate. Read `concurrentSessionLimit` from `GET /api/v3/billing/account` |
| 502 | Control plane unreachable | Retry with backoff |

No `Retry-After` or `RateLimit-*` headers are returned. Back off on your own clock.
