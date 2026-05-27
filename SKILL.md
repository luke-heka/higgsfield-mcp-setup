---
name: higgsfield-mcp-setup
description: "[DEPRECATED 2026-05-24] Older Playwright-driven Higgsfield connector. Superseded by `higgsfield-connector` (OAuth-based, no Playwright dependency). Do NOT trigger this skill on 'connect Higgsfield' / 'set up Higgsfield' — route to `higgsfield-connector` instead. Kept on disk for cross-reference only."
allowed-tools: Bash, Read, Write, Edit, WebFetch, mcp__plugin_playwright_playwright__*
metadata:
  category: productivity
  tags: [higgsfield, mcp, workshop, autonomous]
  audience: non-technical business owner
  time-to-complete: 10-15 minutes
  cost-to-user: TBD
  autonomy-bar: "User action = sign in to Higgsfield ONCE. That is it."
  tech-burden: 0
  user-touchpoints: 3
  playwright-required: true
  manual-fallback-forbidden: true
  pack-slug: higgsfield
  pack-version-pin: 0.0.0
  last-verified: 2026-05-19
---

# Higgsfield Setup — Fully Autonomous

> **The standard**: the user signs in to Higgsfield. That is the only thing they do. Playwright drives every click, form fill, scope tick, ID extraction, secret capture, config write, restart prompt, and live verification. Every error is caught and silently recovered. If the agent can't recover, it diagnoses in plain English — never dumps a raw error.
>
> **Applies to**: Selr AI workshop attendees. Non-technical business owners. They should never type a command, paste a value, or edit a file.
>
> **If Playwright MCP isn't available in this session, STOP.** Do not fall back to a manual walkthrough that asks the user to copy-paste credentials. Instead, tell the user: *"I need browser control to set this up hands-off. Let me enable that — give me two minutes."* Then install Playwright MCP in this session and retry. If you genuinely cannot get Playwright working, escalate to support@selrgroup.com.au rather than make the user do manual steps.

---

## Autonomy Bar — What Counts as "User Action"

| User DOES | User DOES NOT |
|---|---|
| Sign in to their own Higgsfield account (email, password, 2FA from their phone) | Click buttons in the developer portal (agent clicks) |
| Confirm in chat when prompted (max 2 yes/no questions in the whole flow) | Fill in form fields (agent fills) |
| Fully quit and reopen Claude Code once (if needed) | Tick scope checkboxes (agent ticks) |
|  | Copy any credential value (agent reads DOM directly) |
|  | Paste anything into chat (agent never asks) |
|  | Run commands, edit config files, restart services (agent does all silently) |
|  | Read error messages (agent translates or handles silently) |

**If at any point you (the agent) are about to ask the user to copy or paste a value, STOP.** You have the Playwright browser in the same session — read the DOM directly.

---

## How This Skill Works

User says any of:
- "Connect my Higgsfield"
- "Set up Higgsfield"
- "connect higgsfield"

Agent runs the 8 phases below. The user experiences a guided conversation with at most 3 touchpoints: sign-in, optional restart, optional yes/no.

---

## Phases

| # | Phase | What happens |
|---|---|---|
| -1 | Self-install (if bootstrapping from zip) | OS-aware unzip into `~/.claude/skills/`. See `install.sh` / `install.ps1`. |
| 0 | Pre-flight | Verify Playwright MCP available. If not → install it. STOP and escalate if cannot. |
| 1 | Safety gate | Confirm with user: country, which Higgsfield account/org to connect, any one-time yes/no. Max 2 questions. |
| 2 | Discovery | Playwright opens vendor developer portal. Identifies what's needed (app creation, scope ticking, etc.) |
| 3 | Auth | Playwright opens sign-in URL. User signs in. Agent waits for the post-signin redirect. |
| 4 | Extract creds | Playwright reads credentials from DOM. Writes via SecretStore: `selrai.higgsfield.<key>`. Never prints to chat. |
| 5 | MCP install | Agent writes the MCP config block into `~/.claude.json`. Restart Claude Code (one user touchpoint). |
| 6 | Verify | Smoke test hits the live API (`scripts/smoke-test.sh`). Confirms HTTP 200. |
| 7 | Handoff | Plain-English summary: "You're connected. Here's what you can do now." Lists 3-5 next-step skills. |

Each phase is documented in `PHASES/0N-<name>.md`. Reference: `~/.claude/skills/xero-mcp-setup/SKILL.md` for the canonical pattern.

---

## Refusal Rules

- **No copy-paste.** If you're about to ask the user to copy a value, STOP. Read the DOM.
- **No manual fallback.** Playwright unavailable → install it, don't degrade to "open the developer portal and click these 7 things."
- **No raw errors.** Translate to plain English. "I need you to add a payment method to your Higgsfield account" is OK. `403 Forbidden {"error":"billing_required"}` is not.
- **No skill rename.** This skill is `higgsfield-mcp-setup`. Don't rename it during refactors; cross-references will break.
- **No fabricated facts.** If the discovery loop can't find the canonical MCP package name, stop and ask the user. Don't guess.

---

## Reference Index — Load on demand

| If you need | Read |
|---|---|
| The exact official connection path | `references/connection.md` |
| What this software does + competitors | `references/discovery.md` |
| Top use cases (the catalogue) | `references/use-cases.md` |
| Smoke test + failure modes | `references/checks.md` |
| When to use MCP vs CLI vs API | `references/runtime.md` |
