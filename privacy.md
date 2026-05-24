---
layout: default
title: Privacy Policy — AI Agent Usage
description: Privacy policy for the AI Agent Usage macOS app
---

# Privacy Policy — AI Agent Usage

**Last updated:** 2026-05-23

This is the privacy policy for **AI Agent Usage**, a macOS application that helps you see how much your AI coding agents (Claude Code, OpenAI Codex CLI, Cursor, Google Gemini CLI) are costing you. The app is published by Jack Ziesing as an independent developer.

The short version: **we don't collect anything about you.** Everything the app does runs locally on your Mac. The only network traffic is requests you explicitly authorize (API calls to providers you've connected, and an optional pricing-data refresh from our static feed).

---

## What data we collect

**None.** AI Agent Usage does not collect, store, transmit, sell, or share any personal information, usage data, or telemetry about you or your activity. There is no analytics SDK in the app. There is no account to create. There is no signup. There is no login.

## What the app reads from your Mac

The app reads files you explicitly grant it permission to access, in a sandboxed read-only manner:

- **`~/.claude/projects/`** — local session files written by Claude Code. Read after you grant access via a one-time macOS folder picker.
- **`~/.codex/sessions/`** — local session files written by OpenAI Codex CLI. Read under the same grant.
- **`~/.gemini/tmp/`** — local session files written by Google Gemini CLI. Read under the same grant.

The app uses macOS's security-scoped bookmark system to remember these grants across launches. You can revoke access at any time from **Settings → Re-grant Folder Access** or by deleting the app.

The app has **read-only** entitlement for these folders — it cannot write to or modify your AI session files.

## What the app sends over the network

Network requests only happen for things you explicitly configure:

1. **Provider Admin APIs (optional, opt-in)**: If you paste an Admin API key in Setup for a provider (Anthropic, OpenAI, or Cursor), the app makes HTTPS requests directly to that provider's official API endpoints to fetch your usage and cost data. These requests go from your Mac directly to the provider — they do not pass through any server we operate.
   - Anthropic: `api.anthropic.com`
   - OpenAI: `api.openai.com`
   - Cursor: `api.cursor.com`
2. **Pricing data refresh (optional)**: The app can optionally fetch updated model pricing from a static JSON URL you configure in Settings. This request contains no information about you — it's a plain GET request for a public JSON file.

That's it. No telemetry. No crash reports. No analytics. No "phone home" pings.

## How API keys are stored

When you paste an Admin API key for a provider, it is stored exclusively in the **macOS Keychain** under our app's identifier (`com.aiagentusage.app`). It is never:

- Written to the app's database
- Written to UserDefaults
- Written to any log file
- Transmitted to any party other than the relevant provider when making an authorized API call

You can remove a stored key at any time via **Setup → [Provider] → Disconnect**.

## Where usage data is stored

All usage records, aggregates, and cached pricing data are stored in a local SQLite database inside the app's sandbox container, at:

```
~/Library/Containers/com.aiagentusage.app/Data/Library/Application Support/AIAgentUsage/
```

This data never leaves your Mac. You can wipe it any time via **Settings → Clear Local Database**.

## What providers receive

When you connect a provider Admin API, that provider sees the API request (including your authentication key) as part of their normal API operation. Each provider has its own privacy policy governing how they handle your data:

- [Anthropic Privacy Policy](https://www.anthropic.com/privacy)
- [OpenAI Privacy Policy](https://openai.com/policies/privacy-policy)
- [Cursor Privacy Policy](https://cursor.com/privacy)
- [Google Privacy Policy](https://policies.google.com/privacy) (for Gemini CLI)

We have no control over what providers do with the requests you authorize.

## Children's privacy

This app is not directed at children under 13 and we do not knowingly process any data from children.

## Independence from providers

AI Agent Usage is an independent app. It is not affiliated with, endorsed by, or sponsored by Anthropic, OpenAI, Cursor, or Google. All product names and trademarks are the property of their respective owners.

## Changes to this policy

If the privacy practices ever change (for example, if we add a future optional cloud sync feature), this page will be updated. Material changes will be noted in the app's release notes.

## Contact

For privacy questions or to report a concern:

- GitHub Issues: [github.com/jziesing/ai-agent-usage-downloads/issues](https://github.com/jziesing/ai-agent-usage-downloads/issues)
- Email: [jackappledev@gmail.com](mailto:jackappledev@gmail.com)

---

*This document is also linked from the App Store listing's required Privacy Policy field and is the authoritative privacy statement for the app.*
