---
name: browser-use-rent-a-cloud-browser
description: >-
  Launch a stealth cloud browser on Browser Use, drive it from your own Playwright/Puppeteer/Selenium
  code over CDP, and stop it so the unused time is refunded. Use when you already own the automation
  and only need managed, un-blocked Chromium.
api: browser-use:browser-use-api-v4
base_url: https://api.browser-use.com/api/v4
operations:
  - create_browser_session_browsers_post
  - get_browser_session_browsers__session_id__get
  - list_browser_sessions_browsers_get
  - update_browser_session_browsers__session_id__patch
  - list_browser_session_downloads_browsers__session_id__downloads_get
  - list_profiles_profiles_get
generated: '2026-08-29'
method: generated
source: >-
  openapi/browser-use-api-v4-openapi.json + https://docs.browser-use.com/cloud/browser/quickstart +
  https://browser-use.com/pricing.md
---

# Rent a Browser Use cloud browser

## 1. Pick a profile, if the site needs a login

`GET /profiles` (`list_profiles_profiles_get`) returns `ProfileView` entries with `cookieDomains`.
Attach the profile id at creation to reuse a logged-in state instead of solving the login again.

## 2. Launch

`POST /browsers` (`create_browser_session_browsers_post`). The response `BrowserSessionView` carries
`cdpUrl` — the endpoint your Playwright/Puppeteer/Selenium client connects to — plus `liveUrl` for a
human view and `timeoutAt`.

Billing starts here at $0.02/browser-hour, metered by the minute. Credits are reserved up front for the
requested timeout. **Keep the returned `id`.** You cannot stop the session with `client.close()`, a
`browser.close()`, or by dropping the CDP connection.

## 3. Work over CDP

Connect your own client to `cdpUrl`. Stealth and CAPTCHA handling are on by default; managed residential
proxies are billed separately at $5/GB, direct or BYO-proxy egress at $0.20/GB. `GET
/browsers/{session_id}/downloads` (`list_browser_session_downloads_browsers__session_id__downloads_get`)
lists anything the browser downloaded.

## 4. Stop it — this is the step that saves money

`PATCH /browsers/{session_id}` (`update_browser_session_browsers__session_id__patch`) with the stop
action. The contract states unused time is automatically refunded; billing rounds up to the nearest
minute with a one-minute minimum. Reserved credits for the unused portion of the timeout are returned.

If you never stop it, it bills until `timeoutAt`.

## Limits

Concurrency is the ceiling, not request rate: 3 sessions on Free, 10 after a top-up, 25 on Dev, 200 on
Business, 500 on Scaleup. Exceeding it returns 429 `TooManyConcurrentActiveSessionsError`. A session
timeout above 4 hours returns 403 `SessionTimeoutLimitExceededError`.
