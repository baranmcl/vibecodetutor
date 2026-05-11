# vibecodetutor

**👉 Live site: [baranmcl.github.io/vibecodetutor](https://baranmcl.github.io/vibecodetutor/)**

A friendly, step-by-step guide to setting up Claude Code — even if you've never coded before.

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
