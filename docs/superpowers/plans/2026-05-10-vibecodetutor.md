# vibecodetutor Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-file static web guide that walks a non-technical adult through setting up Claude Code with the `superpowers` and `gstack` plugins, including basic prompting and feedback practices. Hosted free on GitHub Pages.

**Architecture:** One self-contained `index.html` file with embedded `<style>` and `<script>`. No build step, no runtime dependencies. CSS variables for theming. Vanilla JS for checklist persistence (localStorage), platform toggle, copy-to-clipboard, and smooth scrolling. Static assets in `assets/screenshots/`.

**Tech Stack:** HTML5, CSS3 (custom properties + flexbox + grid), vanilla JS (no framework). Deployed via GitHub Pages on `main` branch root.

**Spec reference:** [docs/superpowers/specs/2026-05-10-vibecodetutor-design.md](../specs/2026-05-10-vibecodetutor-design.md)

---

## Conventions and constraints

**Commits and pushes require explicit user permission each time.** This plan includes `git commit` and `git push` steps for traceability, but the executing agent must pause and ask the user before running them. Never push to `main` without confirmation.

**Verification is manual, not automated.** Each task ends with a "Verify in browser" step listing concrete things to check by opening `index.html` (or the live URL once deployed). No test framework is being introduced — the spec's zero-dependency rule wins.

**Working directory:** `C:\Users\baranmcl\Code\vibecodetutor` (absolute) or relative paths from there.

**Live URL after Task 1 push:** `https://baranmcl.github.io/vibecodetutor/`

---

## Task 1: Skeleton + first GitHub Pages deploy

Get a minimal `index.html` deployed so the rest of the work has a live target to verify against.

**Files:**
- Create: `index.html`

- [ ] **Step 1: Write the minimal index.html**

Path: `index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>vibecodetutor — Get started with Claude Code</title>
  <meta name="description" content="A friendly, step-by-step guide to setting up Claude Code, even if you've never coded before.">
</head>
<body>
  <h1>vibecodetutor</h1>
  <p>Coming soon — a friendly guide to getting started with Claude Code.</p>
</body>
</html>
```

- [ ] **Step 2: Verify locally**

Open `index.html` in a browser by double-clicking the file. Expected: page shows the title and one-line description.

- [ ] **Step 3: Stage and commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: initial index.html skeleton"
```

- [ ] **Step 4: Push to main (ASK USER FIRST)**

```bash
git push origin main
```

- [ ] **Step 5: Enable GitHub Pages (USER ACTION REQUIRED)**

Tell the user: "Go to https://github.com/baranmcl/vibecodetutor/settings/pages, set Source to `Deploy from a branch`, Branch to `main`, folder to `/ (root)`, and click Save. Then wait ~1 minute and open https://baranmcl.github.io/vibecodetutor/."

- [ ] **Step 6: Verify live deploy**

Expected: `https://baranmcl.github.io/vibecodetutor/` shows the skeleton page.

---

## Task 2: Design tokens, base styles, and page header

Establish the visual foundation: CSS custom properties for colors and spacing, system font stack, the off-white background, and a styled page header (title + subtitle).

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add `<style>` block with design tokens and base resets**

Add inside `<head>`, after the `<meta name="description">` line:

```html
<style>
  :root {
    --color-bg: #fafbff;
    --color-surface: #ffffff;
    --color-border: #e0e7ff;
    --color-text: #1e1b4b;
    --color-text-muted: #4b5563;
    --color-text-faint: #9ca3af;
    --color-primary: #6366f1;
    --color-primary-soft: #eef2ff;
    --color-primary-dark: #4f46e5;
    --color-success: #10b981;
    --color-success-soft: #d1fae5;
    --color-warning: #f59e0b;
    --color-warning-soft: #fef3c7;
    --color-code-bg: #1e1b4b;
    --color-code-text: #e0e7ff;

    --radius-sm: 6px;
    --radius-md: 12px;
    --radius-lg: 16px;
    --radius-pill: 999px;

    --shadow-card: 0 4px 16px rgba(99, 102, 241, 0.08);
    --shadow-card-hover: 0 8px 24px rgba(99, 102, 241, 0.12);

    --space-1: 4px;
    --space-2: 8px;
    --space-3: 12px;
    --space-4: 16px;
    --space-5: 24px;
    --space-6: 32px;
    --space-8: 48px;
    --space-10: 64px;

    --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    --font-mono: "SF Mono", "Cascadia Code", Menlo, Consolas, monospace;
  }

  * { box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    margin: 0;
    font-family: var(--font-sans);
    background: var(--color-bg);
    color: var(--color-text);
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
  }

  .container {
    max-width: 760px;
    margin: 0 auto;
    padding: var(--space-6) var(--space-5);
  }

  .page-header {
    text-align: center;
    padding: var(--space-10) var(--space-5) var(--space-6);
  }

  .page-header h1 {
    font-size: 40px;
    font-weight: 800;
    letter-spacing: -0.5px;
    margin: 0 0 var(--space-3);
  }

  .page-header .lede {
    font-size: 18px;
    color: var(--color-text-muted);
    max-width: 560px;
    margin: 0 auto;
  }
</style>
```

- [ ] **Step 2: Replace body content with the styled header**

Replace the current `<body>` contents with:

```html
<body>
  <header class="page-header">
    <h1>vibecodetutor</h1>
    <p class="lede">A friendly, step-by-step guide to setting up Claude Code — even if you've never coded before.</p>
  </header>
  <main class="container">
    <!-- sections will land here in later tasks -->
  </main>
</body>
```

- [ ] **Step 3: Verify in browser**

Reload `index.html`. Expected:
- Soft off-white background (`#fafbff`)
- Centered title in dark indigo, large and bold
- Subtitle in muted gray below it
- Page reads as visually polished, not raw HTML

- [ ] **Step 4: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add design tokens and styled page header"
```

---

## Task 3: JS state foundation (loadState, saveState, stubs)

Add the script block with the core state utilities. Wire it up to a single dummy checkbox to confirm persistence works before adding real content.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add `<script>` block at the end of `<body>`**

Add just before `</body>`:

```html
<script>
  const STATE_KEY = "vibecodetutor:v1";
  const PLATFORM_KEY = "vibecodetutor:platform";

  function loadState() {
    try {
      return JSON.parse(localStorage.getItem(STATE_KEY)) || {};
    } catch {
      return {};
    }
  }

  function saveState(state) {
    localStorage.setItem(STATE_KEY, JSON.stringify(state));
  }

  function wireCheckboxes() {
    const state = loadState();
    document.querySelectorAll("input.task-check[data-id]").forEach(box => {
      const id = box.dataset.id;
      box.checked = !!state[id];
      box.addEventListener("change", () => {
        const s = loadState();
        if (box.checked) s[id] = true;
        else delete s[id];
        saveState(s);
        updateProgress();
      });
    });
  }

  function updateProgress() {
    // overall + per-section progress bars are wired in later tasks
  }

  function applyPlatform(platform) {
    document.querySelectorAll("[data-platform]").forEach(el => {
      el.style.display = (el.dataset.platform === platform) ? "" : "none";
    });
    document.querySelectorAll(".platform-text").forEach(el => {
      el.textContent = (platform === "mac") ? el.dataset.mac : el.dataset.win;
    });
  }

  function wirePlatformToggle() {
    let platform = localStorage.getItem(PLATFORM_KEY);
    if (!platform) {
      const p = (navigator.platform || "").toLowerCase();
      platform = p.includes("mac") ? "mac" : "win";
    }
    applyPlatform(platform);
    document.querySelectorAll(".platform-btn").forEach(btn => {
      btn.addEventListener("click", () => {
        platform = btn.dataset.platform;
        localStorage.setItem(PLATFORM_KEY, platform);
        document.querySelectorAll(".platform-btn").forEach(b => {
          b.classList.toggle("is-active", b.dataset.platform === platform);
        });
        applyPlatform(platform);
      });
    });
    document.querySelectorAll(".platform-btn").forEach(b => {
      b.classList.toggle("is-active", b.dataset.platform === platform);
    });
  }

  function wireCopyButtons() {
    document.querySelectorAll(".code-block").forEach(block => {
      const btn = block.querySelector(".copy-btn");
      const code = block.querySelector("pre code") || block.querySelector("pre");
      if (!btn || !code) return;
      btn.addEventListener("click", async () => {
        const text = code.innerText;
        try {
          await navigator.clipboard.writeText(text);
          btn.textContent = "Copied!";
          btn.classList.add("is-copied");
        } catch {
          const range = document.createRange();
          range.selectNode(code);
          window.getSelection().removeAllRanges();
          window.getSelection().addRange(range);
          btn.textContent = "Press Ctrl/⌘+C";
        }
        setTimeout(() => {
          btn.textContent = "Copy";
          btn.classList.remove("is-copied");
        }, 1200);
      });
    });
  }

  function wireResetButton() {
    const btn = document.getElementById("reset-progress");
    if (!btn) return;
    btn.addEventListener("click", e => {
      e.preventDefault();
      if (!confirm("Reset all checklist progress? This can't be undone.")) return;
      localStorage.removeItem(STATE_KEY);
      document.querySelectorAll("input.task-check").forEach(b => { b.checked = false; });
      updateProgress();
    });
  }

  document.addEventListener("DOMContentLoaded", () => {
    wirePlatformToggle();
    wireCheckboxes();
    wireCopyButtons();
    wireResetButton();
    updateProgress();
  });
</script>
```

- [ ] **Step 2: Add a dummy test checkbox to `<main>`**

Replace the `<!-- sections will land here in later tasks -->` placeholder with:

```html
<p style="margin: 24px 0;">
  <label>
    <input type="checkbox" class="task-check" data-id="test-persistence">
    Test checkbox (will be removed in Task 4)
  </label>
</p>
```

- [ ] **Step 3: Verify in browser**

1. Reload page. Check the test checkbox. Reload again. Expected: checkbox stays checked.
2. Uncheck. Reload. Expected: checkbox stays unchecked.
3. Open DevTools Application → Local Storage. Expected: `vibecodetutor:v1` key holds `{"test-persistence": true}` when checked.

- [ ] **Step 4: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add JS state foundation with localStorage persistence"
```

---

## Task 4: Platform toggle UI

Build the Windows | Mac toggle bar at the top of the page and remove the dummy checkbox from Task 3.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add platform toggle CSS**

Append inside the `<style>` block, before the closing `</style>`:

```css
.platform-toggle {
  display: inline-flex;
  background: var(--color-primary-soft);
  border-radius: var(--radius-pill);
  padding: 4px;
  gap: 4px;
  margin: var(--space-4) auto var(--space-6);
}
.platform-toggle-wrap { display: flex; justify-content: center; }
.platform-btn {
  border: none;
  background: transparent;
  color: var(--color-text-muted);
  font-family: inherit;
  font-size: 14px;
  font-weight: 600;
  padding: 8px 20px;
  border-radius: var(--radius-pill);
  cursor: pointer;
  transition: background 120ms, color 120ms;
}
.platform-btn.is-active {
  background: var(--color-primary);
  color: white;
}
```

- [ ] **Step 2: Add platform toggle markup**

Replace the dummy checkbox `<p>` block from Task 3 with:

```html
<div class="platform-toggle-wrap">
  <div class="platform-toggle" role="tablist" aria-label="Operating system">
    <button class="platform-btn" data-platform="win" role="tab">Windows</button>
    <button class="platform-btn" data-platform="mac" role="tab">Mac</button>
  </div>
</div>

<p style="margin: 24px 0; text-align: center;">
  Showing instructions for:
  <strong data-platform="win">Windows</strong>
  <strong data-platform="mac">Mac</strong>
</p>
```

- [ ] **Step 3: Verify in browser**

1. Reload. Expected: pill-shaped toggle visible, Windows or Mac selected based on your OS, "Showing instructions for: Windows" (or Mac) shown.
2. Click the other platform. Expected: pill highlight moves, text below updates.
3. Reload. Expected: choice persists.

- [ ] **Step 4: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add Windows/Mac platform toggle"
```

---

## Task 5: Prerequisites checklist + sticky overall progress bar

Add the "What you need before starting" panel and the sticky progress bar at the top of the page. This is the first real persistent checklist.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add CSS for prereq panel and sticky progress bar**

Append inside `<style>`:

```css
.progress-sticky {
  position: sticky;
  top: 0;
  z-index: 10;
  background: rgba(250, 251, 255, 0.92);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--color-border);
}
.progress-sticky-inner {
  max-width: 760px;
  margin: 0 auto;
  padding: 10px var(--space-5);
  display: flex;
  align-items: center;
  gap: var(--space-3);
  font-size: 13px;
  color: var(--color-text-muted);
}
.progress-bar {
  flex: 1;
  height: 6px;
  background: var(--color-primary-soft);
  border-radius: var(--radius-pill);
  overflow: hidden;
}
.progress-bar-fill {
  height: 100%;
  background: var(--color-primary);
  border-radius: var(--radius-pill);
  width: 0%;
  transition: width 240ms ease;
}

.prereq {
  background: var(--color-warning-soft);
  border: 1px solid #fde68a;
  border-radius: var(--radius-md);
  padding: var(--space-5);
  margin: var(--space-6) 0;
}
.prereq h2 {
  margin: 0 0 var(--space-2);
  font-size: 18px;
  color: #92400e;
}
.prereq ul {
  list-style: none;
  padding: 0;
  margin: var(--space-3) 0 0;
  display: grid;
  gap: var(--space-2);
}
.prereq label {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  cursor: pointer;
  font-size: 15px;
}
.task-check {
  width: 18px;
  height: 18px;
  accent-color: var(--color-primary);
  flex-shrink: 0;
}
```

- [ ] **Step 2: Insert sticky bar above `<header>` and prereq panel inside `<main>`**

Replace the body's opening (everything from `<body>` through the existing platform-toggle-wrap section) so the structure becomes:

```html
<body>
  <div class="progress-sticky" id="overall-progress" aria-label="Overall progress">
    <div class="progress-sticky-inner">
      <span id="overall-progress-label">0% complete</span>
      <div class="progress-bar"><div class="progress-bar-fill" id="overall-progress-fill"></div></div>
    </div>
  </div>

  <header class="page-header">
    <h1>vibecodetutor</h1>
    <p class="lede">A friendly, step-by-step guide to setting up Claude Code — even if you've never coded before.</p>
  </header>

  <main class="container">
    <div class="platform-toggle-wrap">
      <div class="platform-toggle" role="tablist" aria-label="Operating system">
        <button class="platform-btn" data-platform="win" role="tab">Windows</button>
        <button class="platform-btn" data-platform="mac" role="tab">Mac</button>
      </div>
    </div>

    <section class="prereq">
      <h2>Before you start</h2>
      <p style="margin: 0; color: #92400e; font-size: 14px;">You'll need these four things. Check them off as you go — your progress is saved automatically.</p>
      <ul>
        <li><label><input type="checkbox" class="task-check" data-id="prereq-computer"> A computer (running <strong data-platform="win">Windows 10 or newer</strong><strong data-platform="mac">macOS Big Sur or newer</strong>)</label></li>
        <li><label><input type="checkbox" class="task-check" data-id="prereq-internet"> A working internet connection</label></li>
        <li><label><input type="checkbox" class="task-check" data-id="prereq-time"> About 30 minutes</label></li>
        <li><label><input type="checkbox" class="task-check" data-id="prereq-card"> A credit or debit card (Claude requires a paid plan — we'll cover costs below)</label></li>
      </ul>
    </section>

    <!-- numbered sections will land here in Task 6+ -->
  </main>
```

- [ ] **Step 3: Update `updateProgress()` in the script**

Replace the empty `updateProgress()` function with:

```javascript
function updateProgress() {
  const all = document.querySelectorAll("input.task-check");
  const done = document.querySelectorAll("input.task-check:checked");
  const pct = all.length === 0 ? 0 : Math.round((done.length / all.length) * 100);
  const fill = document.getElementById("overall-progress-fill");
  const label = document.getElementById("overall-progress-label");
  if (fill) fill.style.width = pct + "%";
  if (label) label.textContent = pct + "% complete";
  // section-level progress wired in Task 6
}
```

- [ ] **Step 4: Verify in browser**

1. Reload. Expected: sticky progress bar at top says "0% complete" with empty bar.
2. Check one of the four prereq boxes. Expected: bar fills to 25%, label says "25% complete".
3. Reload. Expected: state persists, bar still at 25%.
4. Toggle platform Windows/Mac. Expected: "Windows 10 or newer" / "macOS Big Sur or newer" swap correctly in the first prereq line.

- [ ] **Step 5: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add prerequisites checklist and sticky progress bar"
```

---

## Task 6: Section card component + Section 1 (Accounts)

Build the reusable section-card pattern with its per-section progress, then use it to implement Section 1.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add CSS for section cards and step rows**

Append inside `<style>`:

```css
.section {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  padding: var(--space-6);
  margin: var(--space-6) 0;
  box-shadow: var(--shadow-card);
}
.section-header {
  display: flex;
  align-items: flex-start;
  gap: var(--space-4);
  margin-bottom: var(--space-4);
}
.section-num {
  flex-shrink: 0;
  width: 40px;
  height: 40px;
  background: var(--color-primary);
  color: white;
  border-radius: var(--radius-md);
  font-family: var(--font-mono);
  font-weight: 700;
  font-size: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  letter-spacing: -1px;
}
.section-title-wrap { flex: 1; }
.section h2 {
  margin: 0 0 4px;
  font-size: 24px;
  font-weight: 700;
  letter-spacing: -0.3px;
  display: flex;
  align-items: center;
  gap: 10px;
}
.section h2 .check-done {
  color: var(--color-success);
  font-size: 18px;
  opacity: 0;
  transition: opacity 200ms;
}
.section.is-complete h2 .check-done { opacity: 1; }
.section .section-meta {
  font-size: 13px;
  color: var(--color-text-faint);
}
.section .progress-bar {
  margin-top: var(--space-3);
}

.step {
  display: flex;
  gap: var(--space-4);
  padding: var(--space-4) 0;
  border-top: 1px solid var(--color-border);
}
.step:first-of-type { border-top: none; padding-top: var(--space-3); }
.step-badge {
  flex-shrink: 0;
  width: 28px;
  height: 28px;
  background: var(--color-primary-soft);
  color: var(--color-primary-dark);
  border-radius: var(--radius-sm);
  font-family: var(--font-mono);
  font-weight: 700;
  font-size: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.step-body { flex: 1; }
.step-body h3 {
  margin: 0 0 var(--space-2);
  font-size: 17px;
  font-weight: 600;
}
.step-body p { margin: 0 0 var(--space-3); color: var(--color-text-muted); }
.step-body p:last-child { margin-bottom: 0; }
.step-body a { color: var(--color-primary-dark); }

.callout {
  background: var(--color-primary-soft);
  border-left: 3px solid var(--color-primary);
  padding: var(--space-3) var(--space-4);
  border-radius: var(--radius-sm);
  margin: var(--space-3) 0;
  font-size: 14px;
}
.callout.callout-cost {
  background: var(--color-warning-soft);
  border-left-color: var(--color-warning);
}
.callout strong { color: var(--color-text); }

.step-check {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  margin-top: var(--space-3);
  padding: var(--space-3);
  background: var(--color-primary-soft);
  border-radius: var(--radius-sm);
  font-size: 14px;
  cursor: pointer;
}
.step-check input { margin: 0; }

.btn-primary {
  display: inline-block;
  background: var(--color-primary);
  color: white;
  padding: 10px 20px;
  border-radius: var(--radius-sm);
  text-decoration: none;
  font-weight: 600;
  font-size: 14px;
  transition: background 120ms;
}
.btn-primary:hover { background: var(--color-primary-dark); }
```

- [ ] **Step 2: Add Section 1 markup**

Replace the comment `<!-- numbered sections will land here in Task 6+ -->` with:

```html
<section class="section" id="section-accounts" data-section="accounts">
  <div class="section-header">
    <div class="section-num">1</div>
    <div class="section-title-wrap">
      <h2>Set up your accounts <span class="check-done">✓</span></h2>
      <div class="section-meta">About 10 minutes</div>
      <div class="progress-bar"><div class="progress-bar-fill section-progress-fill"></div></div>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">1</div>
    <div class="step-body">
      <h3>Make a GitHub account</h3>
      <p>Think of GitHub like <strong>Dropbox for code</strong> — a place online where your projects live so you don't lose them, and so you can share them.</p>
      <p><a href="https://github.com/signup" target="_blank" rel="noopener" class="btn-primary">Open github.com/signup →</a></p>
      <p>Pick a username (this will be public — many people use a version of their real name), enter your email, and choose a password. GitHub will email you a code to verify your address.</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="accounts-github"> I created my GitHub account and verified my email</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">2</div>
    <div class="step-body">
      <h3>Make a Claude account</h3>
      <p>Claude is the AI you'll be talking to. <strong>Anthropic</strong> is the company that makes Claude.</p>
      <p><a href="https://console.anthropic.com/" target="_blank" rel="noopener" class="btn-primary">Open console.anthropic.com →</a></p>
      <p>Sign up using your email or Google account. You'll get a verification email — click the link to confirm.</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="accounts-anthropic"> I created my Anthropic account</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">3</div>
    <div class="step-body">
      <h3>Pick a plan and add payment</h3>
      <p>Claude Code needs a paid plan. There are two ways to pay:</p>
      <p><strong>Claude Pro / Max subscription</strong> (recommended for most beginners) — a flat monthly fee, with a generous usage limit that resets every few hours. Predictable cost.</p>
      <p><strong>API pay-as-you-go</strong> — you load credit and pay per use. Cheaper if you only use Claude occasionally, but harder to predict.</p>
      <div class="callout callout-cost"><strong>💰 What to expect:</strong> Plan prices are shown on the Anthropic site when you sign up. Most beginners start with the lower subscription tier and upgrade only if they hit the limits. <em>(Exact prices verified at implementation time — see Task 13.)</em></div>
      <p>Add a payment method, choose your plan, and confirm.</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="accounts-plan"> I picked a plan and added payment</label>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Extend `updateProgress()` for section-level progress**

Replace `updateProgress()` with:

```javascript
function updateProgress() {
  const all = document.querySelectorAll("input.task-check");
  const done = document.querySelectorAll("input.task-check:checked");
  const pct = all.length === 0 ? 0 : Math.round((done.length / all.length) * 100);
  const fill = document.getElementById("overall-progress-fill");
  const label = document.getElementById("overall-progress-label");
  if (fill) fill.style.width = pct + "%";
  if (label) label.textContent = pct + "% complete";

  document.querySelectorAll(".section[data-section]").forEach(section => {
    const sAll = section.querySelectorAll("input.task-check");
    const sDone = section.querySelectorAll("input.task-check:checked");
    const sPct = sAll.length === 0 ? 0 : Math.round((sDone.length / sAll.length) * 100);
    const sFill = section.querySelector(".section-progress-fill");
    if (sFill) sFill.style.width = sPct + "%";
    section.classList.toggle("is-complete", sPct === 100 && sAll.length > 0);
  });
}
```

- [ ] **Step 4: Verify in browser**

1. Reload. Expected: Section 1 card visible with header "1 — Set up your accounts", three numbered steps, three checkboxes.
2. Check the three step checkboxes one by one. Expected: per-section progress bar advances 33% → 66% → 100%, then green ✓ appears next to title. Sticky overall progress bar also advances.
3. Reload. Expected: state persists.

- [ ] **Step 5: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add section card component and Section 1 (accounts)"
```

---

## Task 7: Section 2 — Install your tools

Add Section 2 with platform-specific install instructions and the first code blocks with copy buttons.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add CSS for code blocks**

Append inside `<style>`:

```css
.code-block {
  position: relative;
  margin: var(--space-3) 0;
}
.code-block pre {
  background: var(--color-code-bg);
  color: var(--color-code-text);
  padding: var(--space-4);
  padding-right: 80px;
  border-radius: var(--radius-sm);
  overflow-x: auto;
  margin: 0;
  font-family: var(--font-mono);
  font-size: 14px;
  line-height: 1.5;
}
.copy-btn {
  position: absolute;
  top: 8px;
  right: 8px;
  background: rgba(255, 255, 255, 0.1);
  color: var(--color-code-text);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: var(--radius-sm);
  padding: 4px 12px;
  font-size: 12px;
  font-family: inherit;
  font-weight: 600;
  cursor: pointer;
  transition: background 120ms;
}
.copy-btn:hover { background: rgba(255, 255, 255, 0.2); }
.copy-btn.is-copied {
  background: var(--color-success);
  border-color: var(--color-success);
  color: white;
}
```

- [ ] **Step 2: Add Section 2 markup**

Insert after the `</section>` closing Section 1:

```html
<section class="section" id="section-install" data-section="install">
  <div class="section-header">
    <div class="section-num">2</div>
    <div class="section-title-wrap">
      <h2>Install your tools <span class="check-done">✓</span></h2>
      <div class="section-meta">About 15 minutes</div>
      <div class="progress-bar"><div class="progress-bar-fill section-progress-fill"></div></div>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">1</div>
    <div class="step-body">
      <h3>Install VSCode</h3>
      <p>VSCode is a free code editor from Microsoft. Think of it like <strong>Microsoft Word, but for code</strong>. It's where you'll talk to Claude.</p>
      <p><a href="https://code.visualstudio.com/" target="_blank" rel="noopener" class="btn-primary">Open code.visualstudio.com →</a></p>
      <div data-platform="win">
        <p>Click the big blue "Download for Windows" button. Once the download finishes, double-click the installer and accept the defaults — the only setting worth changing is checking <em>"Add to PATH"</em> if it's not already checked (this lets other tools find VSCode).</p>
      </div>
      <div data-platform="mac">
        <p>Click the big blue "Download Mac Universal" button. Once the .zip finishes downloading, double-click it to unzip. Drag the <em>Visual Studio Code</em> icon into your Applications folder.</p>
      </div>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="install-vscode"> VSCode is installed and I can open it</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">2</div>
    <div class="step-body">
      <h3>Install Claude Code</h3>
      <p>Claude Code is the actual AI assistant that runs inside VSCode. It can read your files, write code, and run commands for you.</p>
      <div data-platform="win">
        <p>Claude Code on Windows needs <strong>Node.js</strong> first (a tool that lets other programs run). Download and install it from <a href="https://nodejs.org/" target="_blank" rel="noopener">nodejs.org</a> — pick the "LTS" version, run the installer, accept defaults.</p>
        <p>Then open <strong>PowerShell</strong> (press the Windows key, type "PowerShell", press Enter) and paste this command:</p>
        <div class="code-block">
          <pre><code>npm install -g @anthropic-ai/claude-code</code></pre>
          <button class="copy-btn">Copy</button>
        </div>
        <p>Press Enter. Wait for it to finish (usually under a minute). <em>(Exact install command verified at implementation time — see Task 13.)</em></p>
      </div>
      <div data-platform="mac">
        <p>Open <strong>Terminal</strong> (press Cmd+Space, type "Terminal", press Enter). Paste this command:</p>
        <div class="code-block">
          <pre><code>npm install -g @anthropic-ai/claude-code</code></pre>
          <button class="copy-btn">Copy</button>
        </div>
        <p>If your Mac says "command not found: npm", you need Node.js first. Install it from <a href="https://nodejs.org/" target="_blank" rel="noopener">nodejs.org</a> (pick the "LTS" version), then try the command again. <em>(Exact install command verified at implementation time — see Task 13.)</em></p>
      </div>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="install-claude-code"> Claude Code is installed</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">3</div>
    <div class="step-body">
      <h3>Install the Claude Code VSCode extension</h3>
      <p>This is the panel inside VSCode where you'll actually chat with Claude.</p>
      <p>Open VSCode. On the left sidebar, click the <strong>Extensions</strong> icon (it looks like four squares). In the search box, type <em>Claude Code</em>. Find the one published by Anthropic and click <strong>Install</strong>.</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="install-extension"> Extension installed</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">4</div>
    <div class="step-body">
      <h3>Sign in</h3>
      <p>After install, you'll see a Claude icon on the left sidebar — click it to open the Claude Code panel. The panel will prompt you to sign in. Click <strong>Sign in</strong>; a browser tab opens; sign in with your Anthropic account; the tab closes and the panel says you're connected.</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="install-signin"> I'm signed in</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">5</div>
    <div class="step-body">
      <h3>Say hello to Claude</h3>
      <p>In the Claude Code panel, type this and press Enter:</p>
      <div class="code-block">
        <pre><code>Hello! Can you tell me what you can help with?</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
      <p>You should see Claude reply within a few seconds. Congrats — you're set up.</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="install-hello"> Claude said hi back</label>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

1. Reload. Expected: Section 2 visible with five steps.
2. Switch platform toggle Windows/Mac. Expected: install step text swaps between Windows (PowerShell, "Download for Windows") and Mac (Terminal, "Download Mac Universal").
3. Click "Copy" on one of the code blocks. Expected: button flashes green and says "Copied!" for ~1.2s, then returns to "Copy". Paste into a text editor to confirm the command copied.
4. Check the five checkboxes. Expected: per-section progress bar fills, ✓ appears at 100%.

- [ ] **Step 4: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add Section 2 (install your tools) with copy buttons"
```

---

## Task 8: Section 3 — Add superpowers

Section 3 covers installing the `superpowers` and `gstack` plugins.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Section 3 markup**

Insert after the `</section>` closing Section 2:

```html
<section class="section" id="section-skills" data-section="skills">
  <div class="section-header">
    <div class="section-num">3</div>
    <div class="section-title-wrap">
      <h2>Add superpowers <span class="check-done">✓</span></h2>
      <div class="section-meta">About 5 minutes</div>
      <div class="progress-bar"><div class="progress-bar-fill section-progress-fill"></div></div>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">1</div>
    <div class="step-body">
      <h3>What are "skills"?</h3>
      <p>Skills are <strong>expansion packs for Claude</strong>. Each one teaches Claude a new way of working — like how to brainstorm before coding, or how to use a real browser to test a website.</p>
      <p>You'll install two skill packs now. Both are free.</p>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">2</div>
    <div class="step-body">
      <h3>Install superpowers (by Jesse Vincent / "obra")</h3>
      <p>This adds careful planning, debugging, and code review skills. In the Claude Code panel, paste each of these one at a time:</p>
      <div class="code-block">
        <pre><code>/plugin marketplace add obra/superpowers-marketplace</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
      <div class="code-block">
        <pre><code>/plugin install superpowers@superpowers-marketplace</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
      <p><em>(Exact commands verified at implementation time — see Task 13.)</em></p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="skills-superpowers"> superpowers installed</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">3</div>
    <div class="step-body">
      <h3>Install gstack (by Garry Tan)</h3>
      <p>This adds testing, deployment, and design-review skills — handy when you want Claude to actually try the website it just built. Paste these in the Claude Code panel:</p>
      <div class="code-block">
        <pre><code>/plugin marketplace add garrytan/gstack</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
      <div class="code-block">
        <pre><code>/plugin install gstack@gstack</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
      <p><em>(Exact commands verified at implementation time — see Task 13.)</em></p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="skills-gstack"> gstack installed</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">4</div>
    <div class="step-body">
      <h3>Try one</h3>
      <p>In the Claude Code panel, type:</p>
      <div class="code-block">
        <pre><code>/brainstorm I want to build a small website about my favorite hobby</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
      <p>Claude should now walk you through a structured brainstorming conversation before writing any code. That's superpowers in action.</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="skills-tried"> I tried a skill</label>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Verify in browser**

1. Reload. Expected: Section 3 visible with four steps, four code blocks each with copy buttons.
2. Click each copy button. Expected: copies the command correctly.
3. Check the three checkboxes. Expected: per-section progress fills to 100% and ✓ appears.

- [ ] **Step 3: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add Section 3 (skill plugin installs)"
```

---

## Task 9: Section 4 — Use Claude Code well

Prompting + feedback + basic git, with ❌/✅ examples.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add CSS for prompt example pairs**

Append inside `<style>`:

```css
.prompt-pair {
  display: grid;
  gap: var(--space-3);
  margin: var(--space-3) 0;
}
.prompt-example {
  border-radius: var(--radius-sm);
  padding: var(--space-3) var(--space-4);
  font-size: 14px;
  border-left: 3px solid;
}
.prompt-bad {
  background: #fef2f2;
  border-left-color: #ef4444;
  color: #7f1d1d;
}
.prompt-good {
  background: var(--color-success-soft);
  border-left-color: var(--color-success);
  color: #064e3b;
}
.prompt-example .tag {
  font-weight: 700;
  margin-right: 8px;
}
```

- [ ] **Step 2: Add Section 4 markup**

Insert after the `</section>` closing Section 3:

```html
<section class="section" id="section-use-well" data-section="use-well">
  <div class="section-header">
    <div class="section-num">4</div>
    <div class="section-title-wrap">
      <h2>Use Claude Code well <span class="check-done">✓</span></h2>
      <div class="section-meta">About 10 minutes — read through, no installs</div>
      <div class="progress-bar"><div class="progress-bar-fill section-progress-fill"></div></div>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">1</div>
    <div class="step-body">
      <h3>Describe the goal, not the keystrokes</h3>
      <p>Claude is better at the "what" than the "how". Tell it the outcome you want, not the exact steps.</p>
      <div class="prompt-pair">
        <div class="prompt-example prompt-bad"><span class="tag">❌</span>Open file.txt, go to line 3, change "hello" to "hi", save.</div>
        <div class="prompt-example prompt-good"><span class="tag">✅</span>In file.txt, replace every "hello" with "hi".</div>
      </div>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="well-goal"> Got it</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">2</div>
    <div class="step-body">
      <h3>Give context first</h3>
      <p>Claude can't see what's on your screen or in your head. Tell it what you're working on before you ask for help.</p>
      <div class="prompt-pair">
        <div class="prompt-example prompt-bad"><span class="tag">❌</span>Make it faster.</div>
        <div class="prompt-example prompt-good"><span class="tag">✅</span>The Python script `analyze.py` reads a 50MB CSV and takes 2 minutes to finish. Can you help me figure out which part is slow and speed it up?</div>
      </div>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="well-context"> Got it</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">3</div>
    <div class="step-body">
      <h3>Show, don't tell</h3>
      <p>If you can show an example — a screenshot, a sample, a piece of code you like — Claude will mimic it better than it can imagine it.</p>
      <div class="prompt-pair">
        <div class="prompt-example prompt-bad"><span class="tag">❌</span>Make my website look more professional.</div>
        <div class="prompt-example prompt-good"><span class="tag">✅</span>Make my website look more like stripe.com — clean white background, sharp typography, lots of whitespace.</div>
      </div>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="well-show"> Got it</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">4</div>
    <div class="step-body">
      <h3>Be specific about the output</h3>
      <p>Tell Claude what format you want back. Otherwise you'll get whatever it guesses.</p>
      <div class="prompt-pair">
        <div class="prompt-example prompt-bad"><span class="tag">❌</span>Give me ideas for a startup.</div>
        <div class="prompt-example prompt-good"><span class="tag">✅</span>Give me 5 startup ideas in fintech for people in their 60s. For each: a one-line pitch, the main customer, and the biggest risk. Format as a numbered list.</div>
      </div>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="well-output"> Got it</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">5</div>
    <div class="step-body">
      <h3>Giving feedback mid-task</h3>
      <p>You don't have to wait for Claude to finish. While it's working, you can:</p>
      <p><strong>Type a new message</strong> to redirect — Claude reads it and adjusts.</p>
      <p><strong>Press Escape</strong> to stop a run that's going sideways.</p>
      <p>If a conversation has wandered far from what you wanted, it's often faster to <strong>start a fresh conversation</strong> than to try to steer the old one back.</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="well-feedback"> Got it</label>
    </div>
  </div>

  <div class="step">
    <div class="step-badge">6</div>
    <div class="step-body">
      <h3>The four git commands worth knowing</h3>
      <p>You don't need to be a git expert. Just these four, in this order:</p>
      <div class="code-block">
        <pre><code>git status      # What files have I changed?
git add .       # Stage all my changes
git commit -m "what I did"   # Save a snapshot
git push        # Send the snapshot to GitHub</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
      <p>Run these in PowerShell (Windows) or Terminal (Mac) from inside your project folder. Claude can also run them for you — just ask "commit and push my changes".</p>
      <label class="step-check"><input type="checkbox" class="task-check" data-id="well-git"> Got it</label>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

1. Reload. Expected: Section 4 visible with six steps, four red/green prompt example pairs, and the git command block.
2. Check all six step boxes. Expected: per-section progress fills, ✓ appears.

- [ ] **Step 4: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add Section 4 (prompting, feedback, basic git)"
```

---

## Task 10: Section 5 — Starter projects

Four starter project cards, each with a description and a copy-paste prompt.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add CSS for project cards grid**

Append inside `<style>`:

```css
.projects {
  display: grid;
  grid-template-columns: 1fr;
  gap: var(--space-4);
  margin-top: var(--space-4);
}
@media (min-width: 600px) {
  .projects { grid-template-columns: 1fr 1fr; }
}
.project-card {
  border: 1px solid var(--color-border);
  border-radius: var(--radius-sm);
  padding: var(--space-4);
  background: var(--color-bg);
}
.project-card h4 {
  margin: 0 0 var(--space-2);
  font-size: 16px;
  font-weight: 700;
  display: flex;
  align-items: center;
  gap: 8px;
}
.project-card .emoji { font-size: 20px; }
.project-card p {
  margin: 0 0 var(--space-3);
  font-size: 14px;
  color: var(--color-text-muted);
}
```

- [ ] **Step 2: Add Section 5 markup**

Insert after the `</section>` closing Section 4:

```html
<section class="section" id="section-projects" data-section="projects">
  <div class="section-header">
    <div class="section-num">5</div>
    <div class="section-title-wrap">
      <h2>Try your first project <span class="check-done">✓</span></h2>
      <div class="section-meta">About 5 minutes to kick one off</div>
      <div class="progress-bar"><div class="progress-bar-fill section-progress-fill"></div></div>
    </div>
  </div>

  <p style="color: var(--color-text-muted); margin-top: 0;">Pick one and paste the prompt into Claude Code. Each takes 5–20 minutes for Claude to do — you mostly just watch and answer the occasional question.</p>

  <div class="projects">
    <div class="project-card">
      <h4><span class="emoji">🌐</span> A personal website</h4>
      <p>One-page site about you. Deployed to the internet, free.</p>
      <div class="code-block">
        <pre><code>Build me a one-page personal website about me. Include my name, a short bio, and a way to contact me. Deploy it to GitHub Pages.</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
    </div>

    <div class="project-card">
      <h4><span class="emoji">🐍</span> A Python tool</h4>
      <p>A small script that does a useful thing.</p>
      <div class="code-block">
        <pre><code>Write a Python script that organizes the files in my Downloads folder by file type (PDFs in one folder, images in another, etc.).</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
    </div>

    <div class="project-card">
      <h4><span class="emoji">📊</span> A PowerPoint deck</h4>
      <p>Yes — Claude can generate real .pptx files.</p>
      <div class="code-block">
        <pre><code>Make a 5-slide PowerPoint introducing me to my new team. Use a clean modern design.</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
    </div>

    <div class="project-card">
      <h4><span class="emoji">📈</span> An Excel spreadsheet</h4>
      <p>A working .xlsx with formulas you can edit.</p>
      <div class="code-block">
        <pre><code>Build a monthly budget spreadsheet with categories for rent, food, transportation, and savings. Include formulas that show how much I have left.</code></pre>
        <button class="copy-btn">Copy</button>
      </div>
    </div>
  </div>

  <label class="step-check" style="margin-top: var(--space-4);"><input type="checkbox" class="task-check" data-id="projects-tried"> I kicked off my first project</label>
</section>
```

- [ ] **Step 3: Verify in browser**

1. Reload. Expected: Section 5 visible with four project cards in a 2×2 grid on desktop, single column on mobile.
2. Click the copy buttons. Expected: each copies the corresponding prompt.
3. Check the single "I kicked off my first project" box. Expected: section progress goes to 100%, ✓ appears.
4. Resize browser window narrow. Expected: cards stack vertically.

- [ ] **Step 4: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add Section 5 (starter project ideas)"
```

---

## Task 11: Footer — troubleshooting, help, reset

Add the page footer with common-gotcha troubleshooting list, help links, and the reset checklist button.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add footer CSS**

Append inside `<style>`:

```css
.page-footer {
  margin: var(--space-10) 0 var(--space-8);
  padding-top: var(--space-6);
  border-top: 1px solid var(--color-border);
  color: var(--color-text-muted);
  font-size: 14px;
}
.page-footer h2 {
  color: var(--color-text);
  font-size: 20px;
  margin-bottom: var(--space-3);
}
.page-footer h3 {
  color: var(--color-text);
  font-size: 15px;
  margin: var(--space-4) 0 var(--space-2);
}
.faq details {
  border-top: 1px solid var(--color-border);
  padding: var(--space-3) 0;
}
.faq summary {
  font-weight: 600;
  color: var(--color-text);
  cursor: pointer;
}
.faq summary::marker { color: var(--color-primary); }
.faq details[open] summary { margin-bottom: var(--space-2); }
.reset-link {
  color: #b91c1c;
  background: transparent;
  border: none;
  font: inherit;
  cursor: pointer;
  padding: 0;
  text-decoration: underline;
}
```

- [ ] **Step 2: Add footer markup**

Insert after the `</section>` closing Section 5, still inside `<main class="container">`:

```html
<footer class="page-footer">
  <h2>Troubleshooting</h2>
  <div class="faq">
    <details>
      <summary>"command not found" when I run npm or claude-code</summary>
      <p>Close and reopen PowerShell/Terminal — installs only take effect in new windows. If still broken, reinstall Node.js from <a href="https://nodejs.org/" target="_blank" rel="noopener">nodejs.org</a> and try again.</p>
    </details>
    <details>
      <summary>The Claude Code panel says "Sign in failed"</summary>
      <p>Sign out completely (click the gear icon in the panel → Sign out), close VSCode, reopen it, and sign in again. If you have multiple Anthropic accounts, make sure you're signing in with the one that has a plan.</p>
    </details>
    <details>
      <summary>Claude says "rate limit reached" or "usage limit"</summary>
      <p>You hit your plan's limit for the current window. Either wait (it resets every few hours on most plans) or upgrade.</p>
    </details>
    <details>
      <summary>I installed a plugin but the slash commands don't work</summary>
      <p>Reload VSCode (Ctrl/⌘+Shift+P → "Reload Window"). Plugins are picked up on startup.</p>
    </details>
    <details>
      <summary>My checklist progress disappeared</summary>
      <p>Progress is saved in your browser. If you switched browsers, used a private/incognito window, or cleared site data, the progress won't carry over.</p>
    </details>
  </div>

  <h3>Where to get more help</h3>
  <ul>
    <li><a href="https://docs.anthropic.com/" target="_blank" rel="noopener">Anthropic docs</a> — official guides for Claude and Claude Code</li>
    <li><a href="https://support.anthropic.com/" target="_blank" rel="noopener">Anthropic support</a> — for account or billing issues</li>
    <li><a href="https://github.com/anthropics/claude-code/discussions" target="_blank" rel="noopener">Claude Code discussions on GitHub</a> — community Q&amp;A</li>
  </ul>

  <h3>Start over</h3>
  <p><button id="reset-progress" class="reset-link">Reset my checklist progress</button></p>

  <p style="margin-top: var(--space-6); font-size: 12px; color: var(--color-text-faint);">
    Built with Claude Code. Source on <a href="https://github.com/baranmcl/vibecodetutor" target="_blank" rel="noopener">GitHub</a>. Open an issue if anything is wrong or out of date.
  </p>
</footer>
```

- [ ] **Step 3: Verify in browser**

1. Reload. Expected: footer visible with collapsed FAQ items, three help links, and reset button.
2. Click an FAQ item. Expected: expands inline.
3. Check at least one checkbox somewhere on the page, then click "Reset my checklist progress". Expected: confirm dialog appears; if you confirm, all boxes uncheck, progress bars go to 0%, ✓ disappears from any complete sections.
4. Click again and cancel the confirm. Expected: nothing happens.

- [ ] **Step 4: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add footer with troubleshooting, help, and reset"
```

---

## Task 12: Sticky TOC nav with smooth scroll

Add a sticky table of contents to the right of the sticky progress bar for quick section jumps.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add TOC CSS**

Append inside `<style>`:

```css
.toc {
  display: none;
}
@media (min-width: 980px) {
  .toc {
    display: block;
    position: fixed;
    top: 80px;
    right: max(20px, calc((100vw - 760px) / 2 - 220px));
    width: 200px;
    font-size: 13px;
  }
  .toc h4 {
    margin: 0 0 var(--space-2);
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: var(--color-text-faint);
  }
  .toc ul { list-style: none; padding: 0; margin: 0; }
  .toc li { margin: 0; }
  .toc a {
    display: block;
    padding: 6px 10px;
    color: var(--color-text-muted);
    text-decoration: none;
    border-radius: var(--radius-sm);
    border-left: 2px solid transparent;
  }
  .toc a:hover { background: var(--color-primary-soft); color: var(--color-primary-dark); }
  .toc a.is-active {
    background: var(--color-primary-soft);
    color: var(--color-primary-dark);
    border-left-color: var(--color-primary);
    font-weight: 600;
  }
}
```

- [ ] **Step 2: Add TOC markup**

Insert just after the closing `</header>` and before `<main class="container">`:

```html
<nav class="toc" aria-label="Sections">
  <h4>Contents</h4>
  <ul>
    <li><a href="#section-accounts">1. Accounts</a></li>
    <li><a href="#section-install">2. Install</a></li>
    <li><a href="#section-skills">3. Skills</a></li>
    <li><a href="#section-use-well">4. Use well</a></li>
    <li><a href="#section-projects">5. Projects</a></li>
  </ul>
</nav>
```

- [ ] **Step 3: Wire scrollspy in JS**

Add this new function inside `<script>`, before the `DOMContentLoaded` listener:

```javascript
function wireScrollspy() {
  const sections = document.querySelectorAll(".section[id]");
  const links = document.querySelectorAll(".toc a");
  if (sections.length === 0 || links.length === 0) return;
  const observer = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const id = entry.target.id;
        links.forEach(a => {
          a.classList.toggle("is-active", a.getAttribute("href") === "#" + id);
        });
      }
    });
  }, { rootMargin: "-30% 0px -60% 0px" });
  sections.forEach(s => observer.observe(s));
}
```

Then add `wireScrollspy();` to the `DOMContentLoaded` handler so it becomes:

```javascript
document.addEventListener("DOMContentLoaded", () => {
  wirePlatformToggle();
  wireCheckboxes();
  wireCopyButtons();
  wireResetButton();
  wireScrollspy();
  updateProgress();
});
```

- [ ] **Step 4: Verify in browser**

1. Reload at desktop width (≥ 980px). Expected: TOC visible at the right of the page, sticky as you scroll.
2. Scroll down. Expected: active TOC item highlights and follows as you reach each section.
3. Click a TOC item. Expected: smooth scroll to that section. URL hash updates (e.g., `#section-skills`).
4. Open `index.html#section-projects` in a new tab. Expected: page loads scrolled to Section 5.
5. Resize browser narrow (< 980px). Expected: TOC hides.

- [ ] **Step 5: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "feat: add sticky TOC with scrollspy"
```

---

## Task 13: Verification research pass

Verify exact install commands and pricing against current public docs, then update any inaccurate copy in Sections 2, 3, and 1's pricing callout.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Look up the current Claude Code install instructions**

Use WebFetch on `https://docs.anthropic.com/en/docs/claude-code/quickstart` (or the current quickstart URL — search if that path 404s) and confirm the install command for both Windows and Mac. Note any standalone installer if Anthropic now ships one.

- [ ] **Step 2: Look up the current Anthropic plan pricing**

Use WebFetch on `https://www.anthropic.com/pricing` and confirm the current Pro / Max / Team plan prices that apply to Claude Code users. Note tier names exactly as Anthropic writes them.

- [ ] **Step 3: Look up the current superpowers install commands**

Use WebFetch on `https://github.com/obra/superpowers-marketplace` (or whatever the current canonical repo is — search GitHub if that's moved) and confirm the exact `/plugin marketplace add` and `/plugin install` strings.

- [ ] **Step 4: Look up the current gstack install commands**

Use WebFetch on `https://github.com/gstackio/gstack` or search for "garrytan gstack claude code plugin marketplace" — confirm the canonical install commands.

- [ ] **Step 5: Update Section 2 install commands**

If the commands differ from what's in the plan, update both the Windows and Mac code blocks in Section 2 step 2. Remove the `<em>(Exact install command verified at implementation time...)</em>` note once verified.

- [ ] **Step 6: Update Section 3 plugin install commands**

If the commands differ, update the four code blocks (two for superpowers, two for gstack). Remove the `<em>(Exact commands verified...)</em>` notes.

- [ ] **Step 7: Update Section 1 pricing callout**

Replace the generic "Plan prices are shown on the Anthropic site" callout with a concrete price reference based on what you found. Keep the `💰` icon and warning styling. Example replacement:

```html
<div class="callout callout-cost"><strong>💰 What to expect:</strong> Claude Pro is $X/month and works well for most beginners. Claude Max is $Y/month for heavier users. The API pay-as-you-go option starts at $5 in credits.</div>
```

(Fill in actual values from Step 2.)

- [ ] **Step 8: Verify in browser**

Reload. Spot-check that:
- The Section 1 pricing callout shows real numbers, not "verified at implementation time"
- All the "verified at implementation time" italic notes are gone
- Section 2's install commands match what's in the docs you fetched
- Section 3's plugin install commands match the repos you fetched

- [ ] **Step 9: Commit (ASK USER FIRST)**

```bash
git add index.html
git commit -m "fix: replace placeholder install commands and pricing with verified values"
```

---

## Task 14: Capture screenshots

Capture the five screenshots from the spec and embed them. This step requires the user to capture screenshots from their own machine — the agent guides but doesn't operate the user's GUI.

**Files:**
- Create: `assets/screenshots/vscode-download.webp`
- Create: `assets/screenshots/vscode-extensions.webp`
- Create: `assets/screenshots/claude-code-panel.webp`
- Create: `assets/screenshots/first-auth.webp`
- Create: `assets/screenshots/plugin-install.webp`
- Modify: `index.html`

- [ ] **Step 1: Add screenshot CSS**

Append inside `<style>`:

```css
.screenshot {
  margin: var(--space-3) 0;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-sm);
  overflow: hidden;
}
.screenshot img {
  display: block;
  width: 100%;
  height: auto;
}
.screenshot-caption {
  padding: var(--space-2) var(--space-3);
  background: var(--color-bg);
  font-size: 12px;
  color: var(--color-text-muted);
  border-top: 1px solid var(--color-border);
}
```

- [ ] **Step 2: Create the assets directory**

```bash
mkdir -p assets/screenshots
```

- [ ] **Step 3: Tell the user what to capture (USER ACTION REQUIRED)**

Tell the user verbatim:

> Please capture five screenshots and save them in `assets/screenshots/` with these exact filenames. Each should be roughly 1200–1600 pixels wide.
>
> 1. **`vscode-download.webp`** — the code.visualstudio.com homepage with the big blue "Download" button visible. Try to fit just the hero section.
> 2. **`vscode-extensions.webp`** — VSCode with the Extensions sidebar open, "Claude Code" typed in the search box, and the Anthropic extension visible in the results.
> 3. **`claude-code-panel.webp`** — VSCode with the Claude Code panel open and a sample message visible (something innocuous like "Hello"). This shows what "success" looks like.
> 4. **`first-auth.webp`** — the browser tab that opens when you first sign in to Claude Code. Capture just before clicking the final "Authorize" button.
> 5. **`plugin-install.webp`** — the Claude Code panel mid-way through typing `/plugin install` so the autocomplete is visible.
>
> You can use Windows Snipping Tool (Win+Shift+S) or Mac's Cmd+Shift+4. Save as PNG, then convert to WEBP at https://squoosh.app/ for smaller file size. If WEBP is too fiddly, .png is fine — just update the filenames in the next step to match.

- [ ] **Step 4: Embed screenshots in their respective sections**

In Section 2 step 1 (Install VSCode), inside both `data-platform` divs (or just below the Open button — pick whichever placement feels right), insert:

```html
<figure class="screenshot">
  <img src="assets/screenshots/vscode-download.webp" alt="The VSCode download page with the blue download button highlighted." loading="lazy">
  <figcaption class="screenshot-caption">Click the big blue download button.</figcaption>
</figure>
```

In Section 2 step 3 (Install the extension), just before the closing `</div>` of the `step-body`:

```html
<figure class="screenshot">
  <img src="assets/screenshots/vscode-extensions.webp" alt="VSCode Extensions panel with Claude Code search results visible." loading="lazy">
  <figcaption class="screenshot-caption">The Extensions panel — search for "Claude Code".</figcaption>
</figure>
```

In Section 2 step 4 (Sign in), before its closing `</div>`:

```html
<figure class="screenshot">
  <img src="assets/screenshots/first-auth.webp" alt="The first-time Claude Code sign-in screen in a browser tab." loading="lazy">
  <figcaption class="screenshot-caption">The sign-in tab that opens automatically.</figcaption>
</figure>
```

In Section 2 step 5 (Say hello), before its closing `</div>`:

```html
<figure class="screenshot">
  <img src="assets/screenshots/claude-code-panel.webp" alt="The Claude Code panel open inside VSCode with a sample conversation visible." loading="lazy">
  <figcaption class="screenshot-caption">Success looks like this — Claude Code panel open and replying.</figcaption>
</figure>
```

In Section 3 step 2 (Install superpowers), before its closing `</div>`:

```html
<figure class="screenshot">
  <img src="assets/screenshots/plugin-install.webp" alt="The Claude Code panel showing the /plugin install command autocomplete." loading="lazy">
  <figcaption class="screenshot-caption">Paste each slash command into the Claude Code panel.</figcaption>
</figure>
```

- [ ] **Step 5: Verify in browser**

1. Confirm all five files exist in `assets/screenshots/`.
2. Reload `index.html`. Expected: each section shows its screenshot inline.
3. Check DevTools Network. Expected: each `.webp` (or `.png`) loads with status 200 and is under 200 KB.
4. If any file is missing, the `<img>` will show a broken icon — capture it and re-save.

- [ ] **Step 6: Commit (ASK USER FIRST)**

```bash
git add assets/screenshots/ index.html
git commit -m "feat: add 5 screenshots to install + skills sections"
```

---

## Task 15: README + final polish

Write a README that explains what this is for visitors who land on the GitHub repo, and do one final polish pass.

**Files:**
- Create: `README.md`
- Modify: `index.html`

- [ ] **Step 1: Write README.md**

Path: `README.md`

```markdown
# vibecodetutor

A friendly, step-by-step guide to setting up Claude Code — even if you've never coded before.

**Live site:** https://baranmcl.github.io/vibecodetutor/

## What this is

A single-page interactive guide that walks a non-technical adult through:

1. Creating GitHub and Anthropic accounts
2. Installing VSCode and Claude Code (Windows + Mac)
3. Installing the `superpowers` (by obra) and `gstack` (by Garry Tan) skill plugins
4. Prompting and feedback best practices
5. Four starter project ideas to try

It uses checkboxes that save to your browser, a Windows/Mac platform toggle, and copy-to-clipboard buttons for every terminal command.

## How it's built

One self-contained `index.html` file with embedded CSS and JavaScript. No build step, no npm, no dependencies. You can open the source in any text editor.

## To run locally

Just open `index.html` in any browser. No server needed.

## To fork and customize

1. Click "Fork" on GitHub.
2. Edit `index.html` directly — the file is small enough to read end to end.
3. In your fork's Settings → Pages, set Source to `main` branch, `/ (root)`, and Save.
4. Your customized version is live at `https://<your-username>.github.io/vibecodetutor/`.

## Maintenance notes

Two things go stale faster than the rest of the content:

- **Install commands** (Section 2, Section 3) — re-verify against the current Anthropic docs and plugin repos.
- **Screenshots** (`assets/screenshots/`) — recapture after any major Claude Code UI update.

## License

See [LICENSE](LICENSE).
```

- [ ] **Step 2: Polish — minor copy and styling tweaks**

Open `index.html` and skim every section as if you were a non-tech reader. Look for:
- Sentences that assume knowledge (e.g., "PATH variable", "shell", "directory") — replace with everyday wording.
- Awkward phrases or run-on sentences.
- Any remaining placeholder/TBD text.
- Inconsistent capitalization (e.g., "GitHub" vs "Github" — should always be GitHub; "VSCode" vs "VS Code" — pick one and use it everywhere; this plan uses "VSCode" throughout).

Apply small edits as needed.

- [ ] **Step 3: Verify in browser**

1. Reload `index.html`. Read it top to bottom out loud. Anything jarring or confusing?
2. Resize the window from 360px wide to 1400px wide. Expected: layout stays readable at every width, no horizontal scrolling, no overlapping elements.
3. Try it in a different browser (Firefox or Safari). Expected: identical behavior.
4. Open DevTools → Lighthouse → Run audit. Expected: Performance ≥ 95, Accessibility ≥ 95, Best Practices ≥ 95, SEO ≥ 90.

- [ ] **Step 4: Commit (ASK USER FIRST)**

```bash
git add README.md index.html
git commit -m "docs: add README and polish copy"
```

---

## Task 16: Final deploy verification

End-to-end check on the live site.

**Files:** none

- [ ] **Step 1: Push everything (ASK USER FIRST)**

```bash
git push origin main
```

- [ ] **Step 2: Wait for Pages to redeploy**

GitHub Pages usually takes 30–90 seconds. The user can watch the deploy under the repo's Actions tab.

- [ ] **Step 3: Verify on live URL**

Open `https://baranmcl.github.io/vibecodetutor/` in an incognito/private window (so localStorage is empty — that's a realistic first-visit experience). Verify:
- Page loads without console errors (DevTools Console clean)
- Platform toggle auto-detects correctly
- Checking a few boxes persists across reload
- Copy buttons work
- All five screenshots load (no broken images)
- TOC is visible at desktop width, hidden at mobile width
- Reset link works
- All external links open in new tabs and load real pages

- [ ] **Step 4: Run a Lighthouse audit on the live URL**

In Chrome DevTools → Lighthouse → analyze the live URL. Expected: same scores as local (Performance ≥ 95, Accessibility ≥ 95, Best Practices ≥ 95, SEO ≥ 90).

- [ ] **Step 5: Smoke test on mobile**

Open the live URL on a phone (or use DevTools device emulation at iPhone width). Verify:
- Text is readable without zooming
- Buttons and checkboxes are easy to tap (no overlapping touch targets)
- Code blocks scroll horizontally when too wide instead of breaking the layout
- TOC is hidden

- [ ] **Step 6: Announce done**

The guide is live at `https://baranmcl.github.io/vibecodetutor/`. Share the URL with one non-technical person and watch them go through it — that's the real test.

---

## Self-review notes

After writing this plan, I checked it against the spec:

- **Spec coverage:** All five content sections map to Tasks 6, 7, 8, 9, 10. Page chrome (header, sticky progress, prereq, platform toggle) maps to Tasks 2, 4, 5. Footer + reset maps to Task 11. TOC maps to Task 12. Screenshots map to Task 14. README + polish maps to Task 15. Deploy verification maps to Tasks 1 and 16.
- **Verification placeholders:** Section 1 pricing, Section 2 install commands, and Section 3 plugin commands are all marked `(Exact ... verified at implementation time — see Task 13.)` and explicitly cleaned up in Task 13.
- **Screenshots are user-assisted.** Task 14 Step 3 hands a clear capture list to the user; the rest of the task only runs once files exist.
- **Type/name consistency:** `STATE_KEY = "vibecodetutor:v1"` and `PLATFORM_KEY = "vibecodetutor:platform"` defined in Task 3, referenced consistently in `loadState`/`saveState`/`wirePlatformToggle`/`wireResetButton`. Section ids (`section-accounts`, `section-install`, `section-skills`, `section-use-well`, `section-projects`) match between the section markup tasks and the TOC links in Task 12. Checkbox `data-id` values are unique across the page.
- **No TDD test framework.** The spec is a static HTML page with no testable backend; introducing Playwright would conflict with the "no dependencies" rule. Each task ends with a manual browser-verification step that catches the same regressions a unit test would.
