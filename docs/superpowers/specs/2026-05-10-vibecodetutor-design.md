# vibecodetutor — Design Spec

**Date:** 2026-05-10
**Status:** Approved, ready for implementation plan

## Purpose

An interactive web guide that walks a non-technical adult from zero to running Claude Code productively, including installing community skill plugins (obra's `superpowers`, Garry Tan's `gstack`) and basic prompting/feedback practices. The guide is shareable publicly via GitHub Pages.

## Audience

General non-technical public. Assume the reader has never used GitHub, VSCode, or any programming language, has a personal computer with internet, has ~30 minutes, and has a credit card available for the Claude subscription.

## Success criteria

- A reader who follows the guide end-to-end has: a GitHub account, an Anthropic account on an appropriate plan, VSCode installed, Claude Code installed and authenticated, the `superpowers` and `gstack` plugins installed, and has successfully run at least one prompt.
- A reader can resume mid-guide on the same browser without losing progress.
- The source is approachable enough that a reader who completes the guide could plausibly fork it and edit the content.

## Scope

**In scope:**
- Pre-flight checklist (what you need)
- GitHub account creation
- Anthropic account creation + plan selection (with cost/billing transparency)
- VSCode install (Windows + Mac)
- Claude Code install (Windows + Mac)
- VSCode extension setup + first prompt
- Installing `superpowers` plugin
- Installing `gstack` plugin
- Prompting best practices (3–4 patterns with ❌/✅ examples)
- Feedback best practices (mid-task correction, stop, fresh start)
- Basic git workflow: `status`, `add`, `commit`, `push` in plain English
- 4 starter project ideas with copy-paste prompts (website, Python script, PowerPoint, Excel)
- Troubleshooting (3–5 common gotchas)

**Out of scope:**
- Linux installation paths
- Quizzes
- Video content
- Server-side state (no accounts, no sync across browsers)
- Analytics, tracking, cookies
- Teaching programming concepts beyond what's needed to use Claude Code

## Distribution

GitHub Pages on the `main` branch of `baranmcl/vibecodetutor`, root path. Public URL: `https://baranmcl.github.io/vibecodetutor/`. No GitHub Actions workflow — Pages serves the static files directly. Every push to `main` auto-deploys.

## Architecture

Single self-contained `index.html` file with embedded `<style>` and `<script>`. No build step, no npm, no runtime dependencies. Total page weight target: under 100 KB excluding screenshots.

### File layout

```
vibecodetutor/
├── index.html                  # the entire guide
├── assets/
│   └── screenshots/            # 5 PNG/WEBP screenshots
├── README.md                   # what this is, how to fork, link to live site
├── LICENSE                     # existing
└── .gitignore                  # existing
```

## Page structure

Top-of-page elements (in order):
1. Title and one-paragraph intro ("what you're about to learn")
2. "What you need before starting" mini-checklist (computer, internet, ~30 min, credit card)
3. Global **Windows | Mac** platform toggle
4. Sticky overall progress bar (% of total checklist items complete)

Body — five section cards in order, each with its own header (numbered badge + title), description, internal checklist, and per-section progress bar:

### Section 1 — Set up your accounts (~10 min)
- What GitHub is (analogy: "Dropbox for code")
- Create a GitHub account, verify email
- What Anthropic / Claude is
- Create an Anthropic account, pick a plan (cost & billing explanation lives here)

### Section 2 — Install your tools (~15 min)
- What VSCode is (analogy: "Microsoft Word, but for code")
- Download & install VSCode — platform-specific
- What Claude Code is, why it lives inside VSCode
- Install Claude Code — platform-specific
- Install the VSCode extension, sign in
- Run your first prompt ("Say hello to Claude")

### Section 3 — Add superpowers (~5 min)
- What skills/plugins are (analogy: "expansion packs for Claude")
- Install `superpowers` (obra's plugin) — install commands shown with copy buttons (exact commands verified at implementation time)
- Install `gstack` (Garry Tan's plugin) — install commands shown with copy buttons (exact commands verified at implementation time)
- One sentence each on what they unlock

### Section 4 — Use Claude Code well (~10 min)
- Prompting best practices: 3–4 concrete patterns, each with ❌ bad / ✅ good example
  - Describe the goal, not the keystrokes
  - Give context first
  - Show, don't tell (paste examples in)
  - Be specific about output format
- Giving feedback: how to correct Claude mid-task, when to use "stop", when to start fresh
- Basic git: `status`, `add`, `commit`, `push` — what each does in plain English. Why you'd want to. Kept minimal.

### Section 5 — Try your first project (~5 min)
4 starter project cards, each with a one-line description and a copy-to-clipboard prompt:
- **A personal website** — "Build me a one-page personal website about [me]. Deploy it to GitHub Pages."
- **A Python tool** — "Write a Python script that organizes the files in my Downloads folder by file type."
- **A PowerPoint deck** — "Make a 5-slide PowerPoint introducing me to my new team."
- **An Excel spreadsheet** — "Build a monthly budget spreadsheet with categories for rent, food, and savings."

### Footer
- Troubleshooting: 3–5 common gotchas (e.g., "Claude Code says my API key is invalid", "VSCode can't find the Claude Code extension")
- Where to get help (Anthropic support, GitHub Discussions, etc.)
- "Reset checklist" link (with confirm prompt)

## Visual design system

- **Palette:**
  - Primary accent: indigo `#6366f1`
  - Body text: `#1e1b4b`
  - Background: `#fafbff`
  - Card surface: pure white with 1px `#e0e7ff` border
  - Success: green `#10b981` (completed states)
  - Warning: amber `#f59e0b` (cost/heads-up callouts)
- **Type:** system font stack (SF Pro on Mac, Segoe UI on Windows). Body 16px. Section titles 28px bold. Numbered badge digits in tabular monospace.
- **Step badges:** 28×28px rounded indigo squares with white numerals, used to label each step within a section.
- **Cards:** 12px border radius, 24–32px padding, `box-shadow: 0 4px 16px rgba(99, 102, 241, 0.08)`.
- **Buttons:** filled indigo for primary actions; outlined for secondary. Code blocks dark-themed with copy button in top-right.
- **Progress bars:** 6px indigo fill on light indigo track. Used at top (overall) and inside each section card.
- **Motion:** subtle — checkbox checks animate in, copy buttons flash green for 1s on click, smooth scroll between section anchors. No scroll-triggered animations.
- **Voice:** second person ("You'll create…"), encouraging but not condescending. Analogies for any jargon term.

## Interactivity behaviors

All client-side vanilla JS, no dependencies.

### Checklist persistence
- Each checkbox has a stable `data-id` (e.g., `github-create-account`)
- State stored in `localStorage` under key `vibecodetutor:v1` as a JSON object: `{ [id: string]: true }`
- Missing ids are silently ignored on load (no migration needed when content changes)
- Reset link in footer clears the key after a `confirm()`

### Progress bars
- Overall (top, sticky) and per-section (in each card header)
- Recomputed on every checkbox change event
- When a section hits 100%, its header shows a green ✓ next to the title

### Platform toggle (Windows | Mac)
- Single global toggle at the top
- Stored in `localStorage` under key `vibecodetutor:platform` (`"win"` or `"mac"`)
- On first visit: auto-detects via `navigator.platform`, defaults to Windows on unknown values
- Two presentation patterns:
  - Multi-line blocks: `<div data-platform="win">…</div>` / `<div data-platform="mac">…</div>` — JS toggles `display`
  - Inline tokens: `<span class="platform-text" data-win="Ctrl" data-mac="⌘"></span>` — JS swaps text content

### Copy-to-clipboard
- Every `<pre>` code block gets a copy button (top-right)
- Uses `navigator.clipboard.writeText`
- Success: button flashes green and shows "Copied!" for 1 second
- Failure (insecure context, etc.): falls back to selecting the text and showing "Press Ctrl+C / ⌘C"

### Smooth scroll & deep links
- Each section and step has an `id`
- Sticky TOC links scroll smoothly to anchors
- URL hash updates on click so deep links are shareable

### Non-features (intentional)
- No server sync — localStorage is per-browser
- No "mark all complete" shortcut — friction is the point
- No analytics, no cookies, no third-party scripts

## Screenshots

Five screenshots in `assets/screenshots/`, captured at standard 16:10 resolution and exported as WEBP (with PNG fallback if WEBP encoding isn't available):
1. **VSCode download page** — arrow overlay on the correct big blue button
2. **VSCode Extensions panel** — Extensions icon location + Claude Code extension card
3. **Claude Code panel open in VSCode** — sidebar + input box (what "success" looks like)
4. **First-time auth screen** — browser tab opened for sign-in
5. **`/plugin install` in action** — the slash command interface as you type it

Screenshots are loaded with `loading="lazy"` and a `max-width: 100%` container with a subtle rounded border.

## Verification needed at implementation time

These items will be checked against current docs as a single research pass before writing install-section copy:
- Exact Windows Claude Code install command (npm vs standalone installer)
- Exact Mac Claude Code install command (Homebrew cask vs npm)
- Exact `/plugin marketplace add` commands for `superpowers` and `gstack`
- Current Anthropic subscription tiers and prices

## Maintenance considerations

Documented in the README so future contributors know what to update:
- Claude Code install commands change occasionally — re-verify on each annual review
- Screenshots go stale faster than text — recapture after any major Claude Code UI update
- Plugin install commands may change as the marketplace evolves

## Component boundaries

The implementation has three internal components that can be reasoned about independently:

1. **Content** — the marked-up HTML body. Pure structure, no behavior.
2. **Style sheet** — CSS variables at the top, then component styles. One place to change colors and spacing.
3. **Behavior script** — five small functions: `loadState()`, `saveState()`, `applyPlatform()`, `wireCheckboxes()`, `wireCopyButtons()`. Each touches a well-defined set of selectors. Adding a new checkbox or code block requires no script change.

A new section can be added to the page by writing its HTML alone — the script picks up checkboxes by class and copy buttons by `pre` tag automatically.
