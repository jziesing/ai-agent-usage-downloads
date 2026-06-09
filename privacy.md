---
layout: default
title: Privacy Policy — AI Agent Usage
description: Privacy policy for the AI Agent Usage macOS app
---

# Privacy Policy — AI Agent Usage

**Last updated:** 2026-06-09

This is the privacy policy for **AI Agent Usage**, a macOS application that helps you see how much your AI coding agents (Claude Code, OpenAI Codex CLI, Cursor, Google Gemini CLI) are costing you — and, as of v1.1, understand what those agents are actually doing for you through on-device transcripts and insights. The app is published by Jack Ziesing as an independent developer.

The short version: **we don't collect anything about you.** Everything the app does — including reading your session transcripts and generating insights — runs locally on your Mac. Nothing about your prompts, your code, your commits, or your activity is ever sent to a server we operate. The only network traffic is requests you explicitly authorize: API calls to providers you've connected, GitHub if you connect it, and an optional pricing-data refresh from a static feed.

When you connect a provider Admin API or a GitHub token, the app talks **directly** to that provider on your behalf (see *What the app sends over the network*). It never routes through us.

---

## What data we collect

**None.** AI Agent Usage does not collect, store, transmit, sell, or share any personal information, usage data, or telemetry about you or your activity. There is no analytics SDK in the app. There is no account to create. There is no signup. There is no login.

## What the app reads from your Mac

The app reads files you explicitly grant it permission to access, in a sandboxed read-only manner:

- **`~/.claude/projects/`** — local session files written by Claude Code. Read after you grant access via a one-time macOS folder picker.
- **`~/.codex/sessions/`** — local session files written by OpenAI Codex CLI. Read under the same grant.
- **`~/.gemini/tmp/`** — local session files written by Google Gemini CLI. Read under the same grant.
- **Local git repositories you add** — if you use the AI-to-shipped-code features, the app reads commit metadata (author, date, message subject, branch, diff statistics) from local git repositories you explicitly add, via the libgit2 library. It does not read or store the contents of your source files.

Inside those session files, the app parses and locally stores not just token counts but the substance of each session: the **verbatim text of your prompts**, the AI's responses, and tool activity such as the **file paths edited, bash commands run, and web searches performed**. This is what powers the transcript viewer, full-text search, and the Insights cards. All of it stays on your Mac (see *What gets stored on your Mac*).

The app uses macOS's security-scoped bookmark system to remember these grants across launches. You can revoke access at any time from **Settings → Re-grant Folder Access** or by deleting the app.

The app has **read-only** entitlement for these folders — it cannot write to or modify your AI session files or git repositories.

## What gets stored on your Mac

All data the app derives from your sessions is stored in a local SQLite database inside the app's sandbox container, at:

```
~/Library/Containers/com.aiagentusage.app/Data/Library/Application Support/AIAgentUsage/
```

**This database never leaves your Mac.** There is no cloud sync, no backup to our servers, no replication. (Like any file in your home folder, it may be included in your own Time Machine or iCloud backups if you have those enabled — that's your backup, under your control, not ours.)

What's in it:

- **Usage records & aggregates** — per-request token counts, model, timestamp, estimated cost, and daily rollups, parsed from your session files.
- **Authoritative cost data** — if you connect a provider Admin API, the daily billed-cost figures it returns are cached here.
- **Session metadata & summaries** — for each session, a cached digest including the verbatim text of your first and last prompts and a concatenation of your prompt text, the file paths touched, the bash commands run, web searches performed, a heuristic + (where available) on-device-LLM category, and a one-sentence summary. *This digest is what the Insights tab reads, and it is stored whenever the app scans your sessions — it is independent of the transcript toggle described below.*
- **Full session transcripts** *(v1.1+, controlled by the transcript toggle)* — a turn-by-turn record of each session: your prompts, the AI's text responses, and tool calls. Tool **results** are stored under a tiered policy to keep the substance without bloating disk: file Read/Edit/Write results are skipped (that content already lives in your files), Bash and WebFetch output is capped at 8 KB, results from other tools (e.g. MCP) are capped at 4 KB, and web-search/grep/glob results are kept in full. Wrapper artifacts that some agents inject into the prompt stream are filtered out at parse time.
- **Full-text search index** *(v1.1+)* — a SQLite FTS5 index over your transcript text so the Search tab can find past prompts and answers instantly. It indexes the same transcript content described above.
- **Git activity & correlations** — if you use the AI-to-shipped-code features: commit/PR metadata from your local repos and (if connected) GitHub, plus correlation rows that link AI sessions to nearby commits by time proximity. These link sessions to commits; they do **not** claim the AI authored any code.
- **Internal housekeeping** — small cursor tables tracking which session and git files have already been parsed, plus your app preferences.

## On-device intelligence (no cloud inference)

Some Insights — session categorization, the "Tasks you could learn" card, and the "Budget narrative" card — use a language model to summarize your activity. This runs **entirely on your Mac** using Apple's on-device **Foundation Models** framework (available on macOS 26 and later). Your prompts, transcripts, and summaries are **not** sent to Apple, to us, or to any cloud service for this. On macOS versions without Foundation Models, these specific cards are simply unavailable and a non-LLM heuristic is used for categorization instead.

Categorization runs automatically in the background in batches so the Insights tab populates without you waiting. It is on-device and uses the data already described above.

## What the app sends over the network

Network requests only happen for things you explicitly configure:

1. **Provider Admin APIs (optional, opt-in)**: If you paste an Admin API key in Setup for a provider (Anthropic, OpenAI, or Cursor), the app makes HTTPS requests directly to that provider's official API endpoints to fetch your usage and cost data. These requests go from your Mac directly to the provider — they do not pass through any server we operate.
   - Anthropic: `api.anthropic.com`
   - OpenAI: `api.openai.com`
   - Cursor: `api.cursor.com`
2. **GitHub (optional, opt-in)**: If you connect a GitHub personal access token, the app makes HTTPS requests directly to `api.github.com` to fetch your own commit and pull-request metadata, used to correlate AI sessions with shipped code. Direct from your Mac to GitHub.
3. **Pricing data refresh (optional)**: The app can optionally fetch updated model pricing from a static JSON URL you configure in Settings. The request body contains no information about you — it's a plain GET for a public JSON file. (As with any HTTPS request, the host necessarily sees your IP address.)

That's it. No telemetry. No crash reports. No analytics. No "phone home" pings.

## How API keys and tokens are stored

When you paste an Admin API key or a GitHub token, it is stored exclusively in the **macOS Keychain** under our app's identifier (`com.aiagentusage.app`). It is never:

- Written to the app's database
- Written to UserDefaults
- Written to any log file
- Transmitted to any party other than the relevant provider when making an authorized API call

You can remove a stored key at any time via **Setup → [Provider] → Disconnect**.

## Your controls

You're in charge of what's stored, and you can clear it at any time:

- **Settings → Transcripts → "Capture session transcripts" toggle** — turns the full-transcript capture (the turn-by-turn record and its search index) on or off. **It is on by default**, so the transcript viewer and Search work out of the box. On first launch you'll see a one-time dialog ("Capture session transcripts?") that explains this and lets you turn it off immediately if you'd rather not store transcript text. You can flip it any time here. *(Note: turning this off stops new transcript capture, but the session-metadata digest described above — including your first/last prompt text — is still maintained for the Insights tab. To remove that as well, use Clear Local Database.)*
- **Settings → Transcripts → Storage used** — shows how much disk the transcripts occupy (megabytes, session count, turn count).
- **Settings → Transcripts → Purge older than 90 days** — deletes transcript turns older than 90 days.
- **Settings → Transcripts → Clear transcripts** — clears all transcript turns, or just the ones for projects you choose.
- **Settings → Transcripts → Compact database** — runs a SQLite VACUUM to reclaim disk space after a large delete.
- **Settings → Clear Local Database** — wipes everything the app has stored locally *from your data*: usage records, parse cursors, cached authoritative cost data, the session-metadata digest (including your first/last prompt text), all captured transcripts and their search index, and git correlation data. Your saved dashboards and app preferences are kept (those are configuration, not data). A re-scan rebuilds everything from the on-disk source files.
- **Settings → Re-grant / revoke Folder Access** — controls which folders the app may read.

## What providers receive

When you connect a provider Admin API or GitHub, that service sees the API request (including your authentication key) as part of their normal API operation. Each has its own privacy policy governing how they handle your data:

- [Anthropic Privacy Policy](https://www.anthropic.com/privacy)
- [OpenAI Privacy Policy](https://openai.com/policies/privacy-policy)
- [Cursor Privacy Policy](https://cursor.com/privacy)
- [Google Privacy Policy](https://policies.google.com/privacy) (for Gemini CLI)
- [GitHub Privacy Statement](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement)

We have no control over what providers do with the requests you authorize.

## Children's privacy

This app is not directed at children under 13 and we do not knowingly process any data from children.

## Independence from providers

AI Agent Usage is an independent app. It is not affiliated with, endorsed by, or sponsored by Anthropic, OpenAI, Cursor, Google, Apple, or GitHub. All product names and trademarks are the property of their respective owners.

## Changes to this policy

If the privacy practices ever change (for example, if we add a future optional cloud sync feature), this page will be updated. Material changes will be noted in the app's release notes.

**What changed in this update (2026-06-09):** disclosed the v1.1 transcript layer — on-device storage of session transcripts, the full-text search index, the session-metadata digest (including verbatim prompt text), git/commit correlation data, and the on-device Foundation Models categorization. Clarified exactly which "Clear" control removes which data. No data is collected or transmitted as a result of these features; they are entirely on-device.

## Contact

For privacy questions or to report a concern:

- GitHub Issues: [github.com/jziesing/ai-agent-usage-downloads/issues](https://github.com/jziesing/ai-agent-usage-downloads/issues)
- Email: [jackappledev@gmail.com](mailto:jackappledev@gmail.com)

---

*This document is also linked from the App Store listing's required Privacy Policy field and is the authoritative privacy statement for the app.*
