# AI Agent Usage — Downloads

**See, forecast, and break down what your AI coding agents cost — and what they actually ship.**

A native macOS app that reads your local Claude Code, Codex CLI, Cursor, and Gemini CLI session files, turns them into cost + token rollups, and gives you searchable transcripts, ~25 insight cards, and custom Dashboards. Private, on-device, no account needed.

This repo hosts the public DMG downloads, release notes, and privacy policy. The app's source code lives in a separate private repo.

## Download

- **DMG (latest, v1.2.0):** [AI-Agent-Usage.dmg](https://github.com/jziesing/ai-agent-usage-downloads/releases/latest/download/AI-Agent-Usage.dmg)
- **All releases:** [github.com/jziesing/ai-agent-usage-downloads/releases](https://github.com/jziesing/ai-agent-usage-downloads/releases)
- **App Store:** [apps.apple.com/us/app/id6770159263](https://apps.apple.com/us/app/id6770159263) (US + Europe, excluding France)

Requires macOS 15+. On-device LLM narrative cards require macOS 26+.

## What's new in v1.2.0

- **Dashboards** — save named, custom views of any subset of the ~25 insight cards, scoped by project and date. Drag to reorder. Reopens where you left off.
- **One-click GitHub sync** — a single click now pulls all commits and PRs; rate-limit handling is automatic.
- **Refreshed design** — new icon, Insights and Output as separate sidebar tabs, app-wide text-size control.
- **Improved Clear Local Database** — now fully erases usage records, transcripts, the prompt digest, and git data. Saved Dashboards and preferences are kept.

## Live landing page

Feature overview, screenshots, and what's new:

**[jziesing.github.io/ai-agent-usage-downloads](https://jziesing.github.io/ai-agent-usage-downloads/)**

## Privacy

All transcripts, git data, and analytics are stored on your Mac and never leave it. Network requests only happen when you connect a provider Admin API, a GitHub token, or a custom pricing feed — and those go directly from your Mac to the service you authorized.

Read the full [Privacy Policy](https://jziesing.github.io/ai-agent-usage-downloads/privacy.html).
