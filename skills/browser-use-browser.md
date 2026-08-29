---
name: Browser
description: Use when building AI agents that automate browser tasks, scrape websites, fill forms, handle authentication, extract data, or perform multi-step workflows. Agents work with any LLM (Claude, GPT, Gemini, etc.) and run locally or in the cloud.
metadata:
    mintlify-proj: browser
    version: "1.0"
---

# Browser Use

## Product summary

Browser Use is a Python library and cloud service for AI-driven browser automation. Agents receive natural language tasks, autonomously navigate websites, interact with pages, and extract data. The library supports 15+ LLM providers (Claude, GPT, Gemini, etc.) and runs locally or via Browser Use Cloud. Key files: `Agent` class (core), `Browser` class (browser config), `Tools` registry (custom actions). CLI: `browser-use install` (setup), `browser-use --mcp` (MCP server). Primary docs: https://docs.browser-use.com

## When to use

Reach for Browser Use when:
- Building agents that need to navigate websites, click buttons, fill forms, or extract data
- Automating multi-step workflows (login → search → extract → save)
- Handling authentication flows (2FA, cookies, profiles)
- Scraping dynamic content that requires JavaScript execution
- Creating follow-up tasks in the same browser session (keep_alive sessions)
- Needing structured output from web data (use Pydantic schemas)
- Running tasks locally with your own LLM or via Browser Use Cloud
- Integrating with coding assistants (Claude Code, Cursor) via MCP

Do not use for: simple HTTP requests (use requests library), static HTML parsing (use BeautifulSoup), or tasks that don't require browser interaction.

## Quick reference

### Core Agent Setup

| Task | Code |
|------|------|
| Create basic agent | `Agent(task="...", llm=ChatBrowserUse())` |
| Run agent | `await agent.run(max_steps=100)` |
| Set browser config | `Browser(headless=False, window_size={'width': 1000, 'height': 700})` |
| Use custom LLM | `Agent(task="...", llm=ChatOpenAI(model="gpt-5"))` |
| Get results | `history = await agent.run()` then `history.final_result()` |

### Built-in Tools (Actions)

| Tool | Purpose |
|------|---------|
| `click` | Click elements by index |
| `input` | Type text into form fields |
| `scroll` | Scroll page up/down |
| `navigate` | Go to URL |
| `search` | Search via DuckDuckGo/Google/Bing |
| `extract` | Extract data using LLM |
| `evaluate` | Execute custom JavaScript |
| `send_keys` | Send keyboard shortcuts (Tab, Enter, etc.) |
| `upload_file` | Upload files to inputs |
| `screenshot` | Request screenshot for visual confirmation |
| `done` | Complete task |

### Environment Variables

```bash
# Required for cloud features
BROWSER_USE_API_KEY=your_key

# LLM providers (choose one)
OPENAI_API_KEY=...
ANTHROPIC_API_KEY=...
GOOGLE_API_KEY=...
```

### Key Parameters

| Parameter | Default | Purpose |
|-----------|---------|---------|
| `task` | Required | Natural language task description |
| `llm` | Required | LLM instance (ChatBrowserUse, ChatOpenAI, etc.) |
| `max_steps` | 100 | Max agent steps before stopping |
| `browser` | Auto | Browser config (headless, proxy, profile) |
| `use_vision` | "auto" | Screenshot mode: "auto", True, or False |
| `max_actions_per_step` | 4 | Max parallel actions per step |
| `output_model_schema` | None | Pydantic model for structured output |
| `extend_system_message` | None | Add custom instructions to prompt |

## Decision guidance

### When to use Cloud vs Local

| Scenario | Use Cloud | Use Local |
|----------|-----------|-----------|
| Production deployment | ✓ | |
| Authentication with cookies | ✓ | |
| Geo-targeted browsing (proxies) | ✓ | |
| CAPTCHA solving | ✓ | |
| Development/testing | | ✓ |
| Cost-sensitive (free tier) | | ✓ |
| Custom LLM integration | | ✓ |

### When to use Vision (Screenshots)

| Scenario | Setting | Reason |
|----------|---------|--------|
| Visual elements, complex layouts | `use_vision=True` | Always include screenshots |
| Occasional visual confirmation | `use_vision="auto"` | Agent decides when needed |
| Text-only extraction | `use_vision=False` | Skip screenshots, faster |

### When to use Structured Output

| Scenario | Approach |
|----------|----------|
| Extract typed data (JSON, CSV) | Use `output_model_schema` with Pydantic model |
| Free-form text result | Return `history.final_result()` as string |
| Cloud API (V4) | Request JSON in task, validate client-side (no schema support) |

### When to use Keep-Alive Sessions

| Scenario | Use Keep-Alive |
|----------|----------------|
| Single task | No (default) |
| Follow-up tasks in same browser | Yes (`keep_alive=True`) |
| Preserve cookies/auth state | Yes |
| Cost optimization (cache page state) | Yes |

## Workflow

### 1. Set up environment
- Install: `pip install browser-use` (local) or `pip install browser-use-sdk` (cloud)
- Create `.env` with API key (BROWSER_USE_API_KEY or LLM provider key)
- Load env: `from dotenv import load_dotenv; load_dotenv()`

### 2. Choose LLM and initialize agent
- Pick LLM: ChatBrowserUse (recommended), ChatOpenAI, ChatAnthropic, ChatGoogle, etc.
- Create agent: `agent = Agent(task="...", llm=llm_instance)`
- Configure browser if needed: `browser = Browser(headless=False); agent = Agent(..., browser=browser)`

### 3. Write effective task description
- Be specific: "Go to example.com, search for 'Python', click first result, extract title"
- Name actions: "Use search action to find X, then use click to open result"
- Handle errors: "If page times out, use go_back and try alternative approach"
- Avoid: vague tasks like "make money" or "do something useful"

### 4. Run and capture results
- Execute: `history = await agent.run(max_steps=100)`
- Access results: `history.final_result()`, `history.urls()`, `history.extracted_content()`
- Check success: `history.is_done()`, `history.has_errors()`
- Get metadata: `history.number_of_steps()`, `history.total_duration_seconds()`

### 5. For structured output
- Define Pydantic model: `class Result(BaseModel): title: str; price: float`
- Pass to agent: `Agent(..., output_model_schema=Result)`
- Access: `history.structured_output` (returns parsed model instance)

### 6. For follow-up tasks (cloud)
- Create session with `keep_alive=True`
- Send follow-up task to same session ID
- Browser state, cookies, and memory persist across tasks

## Common gotchas

- **Parameter name mismatch in custom tools**: Use `browser_session: BrowserSession` (not `browser: Browser`). Agent injects by name matching; wrong names fail silently.
- **Vision overhead**: `use_vision=True` always includes screenshots, increasing cost. Use `use_vision="auto"` to let agent decide.
- **Closing browser doesn't stop cloud session**: Call `client.browsers.stop(browser.id)` or PATCH `/api/v4/browsers/{id}` with `{"action":"stop"}` explicitly.
- **Credentials in prompts**: Never put passwords or TOTP secrets in task text. Use 1Password vault, profile sync, or custom tools instead.
- **Max steps reached silently**: Agent stops at `max_steps` without error. Increase if task is incomplete.
- **Timeouts on slow networks**: Increase `step_timeout` (default 120s) or `llm_timeout` (default 90s) via environment variables.
- **Structured output in Cloud V4**: V4 API doesn't accept `output_schema`. Request JSON in task, validate client-side.
- **Flash mode disables thinking**: `flash_mode=True` skips reasoning steps for speed; use only for simple tasks.
- **Proxy country codes**: Set `proxy_country_code` in session settings; defaults to US. Some sites block certain regions.
- **Screenshot detail level**: `vision_detail_level='high'` increases cost. Use `'auto'` or `'low'` for most tasks.

## Verification checklist

Before submitting work:

- [ ] Task description is specific and action-oriented (not vague)
- [ ] LLM API key is set and valid (test with simple task first)
- [ ] Browser config matches requirements (headless, proxy, profile)
- [ ] `max_steps` is sufficient for task complexity (increase if hitting limit)
- [ ] Custom tools use correct parameter names (`browser_session`, not `browser`)
- [ ] Credentials are not in task text (use 1Password, profiles, or tools)
- [ ] Structured output schema (if used) matches expected data
- [ ] Error handling is in place (fallback LLM, retry logic)
- [ ] Session is stopped after use (especially cloud sessions)
- [ ] Cost tracking is enabled if needed (`calculate_cost=True`)
- [ ] Results are extracted correctly (`history.final_result()`, `history.structured_output`)

## Resources

- **Comprehensive navigation**: https://docs.browser-use.com/llms.txt — Full page-by-page reference for agents
- **Open Source Quickstart**: https://docs.browser-use.com/open-source/quickstart — Install, run first agent, choose LLM
- **Cloud Quickstart**: https://docs.browser-use.com/cloud/quickstart — Run hosted agents or cloud browsers
- **Agent Configuration**: https://docs.browser-use.com/open-source/customize/agent/all-parameters — All parameters, timeouts, environment variables
- **Prompting Guide**: https://docs.browser-use.com/open-source/customize/agent/prompting-guide — Write effective task descriptions
- **Available Tools**: https://docs.browser-use.com/open-source/customize/tools/available — Full list of built-in actions
- **Custom Tools**: https://docs.browser-use.com/open-source/customize/tools/add — Add API calls, file operations, custom logic
- **Supported Models**: https://docs.browser-use.com/open-source/supported-models — 15+ LLM providers with examples
- **Authentication Guide**: https://docs.browser-use.com/cloud/guides/authentication — 2FA, 1Password, profile sync

---

> For additional documentation and navigation, see: https://docs.browser-use.com/llms.txt