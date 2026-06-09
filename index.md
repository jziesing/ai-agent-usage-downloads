---
layout: default
title: Downloads — AI Agent Usage
description: Track AI agent usage AND understand what your AI is actually doing for you — with insights cards tailored to individuals and managers.
---

# AI Agent Usage

**Track AI agent usage AND understand what your AI is actually doing for you** — with insights cards tailored to individuals and managers.

A native macOS app that reads your local Claude Code, Codex CLI, Cursor, and Gemini CLI session files, turns them into cost + token rollups, and — new in v1.1.1 — gives you searchable transcripts and a grid of insights cards that surface patterns in how you work with AI.

<p>
  <a href="https://github.com/jziesing/ai-agent-usage-downloads/releases/latest/download/AI-Agent-Usage.dmg"><strong>Download the DMG (v1.1.1)</strong></a>
  &nbsp;·&nbsp;
  <a href="https://apps.apple.com/us/app/id6770159263">Get it on the App Store</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/jziesing/ai-agent-usage-downloads/releases">All releases</a>
</p>

*Requires macOS 15+. The on-device LLM narrative cards (Apple Foundation Models) require macOS 26+.*

---

## What is this?

AI Agent Usage is a reflective tool for people and teams who use AI coding assistants every day and want to understand — not just measure — what's coming out of that spend.

- **For individuals:** see exactly what your AI is doing for you, step by step. Read your past sessions, search them, and spot where you're learning vs. where you're delegating the same question over and over.
- **For managers and budget owners:** translate token spend into concrete work shapes. Not "we spent $50k" — but "here's the mix of work that produced, the per-artifact economics, and where the exploratory time went."
- **On-device by default:** transcripts, git data, and analytics never leave your Mac. No account, no telemetry, no cloud sync. Optional connections to provider Admin APIs and GitHub are user-initiated and use keys you paste in yourself.

---

## What's in v1.1.1 (DMG)

The DMG ships ahead of the App Store build. v1.1.1 adds a full transcript layer and an Insights grid on top of the cost/token tracking that's already on the App Store.

### Session transcripts + search

- **Session Transcripts** — a chat-bubble view of every prompt and response in a past session, with copy buttons per turn. Tool output is stored under a tiered policy (Bash/WebFetch capped at 8 KB, file Reads skipped because that content is already on disk, web searches kept in full) so you keep the substance without bloating disk.
- **Transcript Search** — a Search tab backed by SQLite full-text search. Type a past question or a snippet of an answer and jump straight to the session that produced it, with the matched text highlighted.
- **Session Categorization** — sessions are sorted into categories (debug, feature, refactor, explain, test, docs, DevOps, data analysis, report generation, document drafting, API integration, ops workflow, and more) using heuristic rules, then refined by an on-device LLM where macOS 26+ is available.

### Insights cards — individual view

- **Repeat Prompts** — the questions you've asked AI two or more times, clustered together. A nudge toward where self-learning might pay off.
- **Skill Areas Decreased** — categories where you're doing less AI-assisted work over time. A signal you've grown into them.
- **Confidence Trends** — how your HIGH / MEDIUM / LOW confidence sessions shift across categories from period to period.
- **Tasks You Could Learn** — an on-demand, on-device LLM summary of concrete techniques you're currently delegating, with a "Generate" button so you decide when inference runs.

### Insights cards — manager view

- **Output by Category** — what shapes of work the team's AI spend is producing, with session count and token spend per category.
- **Cost per Shipped Artifact** — per-feature and per-bug-fix economics, using local + GitHub commit signal (by time proximity) to detect what shipped near a session.
- **Session Patterns** — a non-judgmental, side-by-side contrast of focused sessions vs. exploratory sessions, so you can see where time is going without ranking people.
- **Budget Narrative** — an on-device LLM drafts a short, honest justification of the team's AI spend that you can copy into a budget review.

### Storage controls + consent

- **Settings → Transcripts** — live storage stats (MB, sessions, turns), a toggle to stop capturing new transcripts, "Purge older than 90 days," "Clear transcripts" (all or per-project), and a "Compact database" (VACUUM) button.
- **One-time consent dialog** — transcript capture is on by default; on first launch you get a clear, one-time prompt explaining it and letting you turn it off on the spot.

Everything above is **on-device** — see the [Privacy Policy](privacy.html) for exactly what is stored and where.

---

## App Store version

The App Store build covers the core cost-and-tokens experience: local session ingestion across Claude Code, Codex CLI, Cursor, and Gemini CLI, plus optional Admin API connections for authoritative billing data. It's currently available in the US and Europe (excluding France).

The transcript layer, Search tab, and Insights grid described above land first via the DMG on this page, then roll into the App Store build on the next review cycle. If you want stability and automatic updates, take the App Store build. If you want the newest insights work, grab the DMG.

---

## Screenshots

<!-- Screenshots are added to assets/screenshots/ before publishing. Until then,
     these references resolve once the PNGs are dropped in (see that folder's README). -->

![Usage overview showing per-provider cost and tokens](assets/screenshots/01-usage-overview.png)

![Output tab showing the Insights grid spanning individual and manager views](assets/screenshots/02-insights-grid.png)

![Repeat Prompts card expanded into a modal with clusters and session drilldown](assets/screenshots/03-repeat-prompts-card.png)

![Tasks You Could Learn card showing the on-device LLM narrative](assets/screenshots/04-tasks-you-could-learn.png)

![Search tab with a full-text query, snippet preview, and session result](assets/screenshots/05-search-tab.png)

![Settings → Transcripts with storage stats, toggle, purge, and compact controls](assets/screenshots/06-settings-transcripts.png)

---

## How it works

- **Reads what's already on your Mac.** AI Agent Usage tails the local session files that Claude Code, Codex CLI, Cursor, and Gemini CLI already write — `~/.claude/projects`, `~/.codex/sessions`, `~/.gemini/tmp`, and Cursor's local store — using security-scoped folder access you grant once.
- **Stores everything locally in SQLite.** Usage events, git activity (via libgit2 and an optional GitHub token), session metadata, and the new transcript + full-text-search layer all live in one on-device database. Admin API keys and the GitHub token live in the macOS Keychain, never in the database.
- **Surfaces patterns, not metrics for their own sake.** The Insights grid is built around two questions: *as an individual, what is my AI actually doing for me?* and *as a manager, what shape of work are we getting from this spend?* Cards that draw on the on-device LLM (Apple Foundation Models, macOS 26+) only run when you click Generate.

---

## Privacy

Transcripts, git data, and analytics are stored on your Mac and never leave it. The app only makes network requests when you explicitly connect a provider Admin API, a GitHub token, or a custom pricing-data feed URL — and those requests go directly from your Mac to the service you authorized.

Read the full [Privacy Policy](privacy.html).

---

## Source + releases

The Mac app source lives in a private repo for now. This downloads repo, the DMG, and the release notes here are public and will stay that way.

- **Latest release + previous DMGs:** [github.com/jziesing/ai-agent-usage-downloads/releases](https://github.com/jziesing/ai-agent-usage-downloads/releases)
- **Privacy policy:** [privacy.html](privacy.html)
- **App Store listing:** [apps.apple.com/us/app/id6770159263](https://apps.apple.com/us/app/id6770159263)
