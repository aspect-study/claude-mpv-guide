# Claude Desktop Triad — MVP Solo Developer Guide

A set of standalone HTML guides on using Claude Desktop's three surfaces — **Chat**, **Code**, and **Cowork** — as a coordinated workflow for shipping an MVP solo.

No build step, no npm, no framework. Every page is a single self-contained HTML file styled with Tailwind via CDN. Clone it and open a file in a browser, or serve the folder as a static site.

---

## The core idea

The guide's argument is that the three Claude surfaces are not interchangeable, and treating them as such is the main way solo developers waste time. Each gets a distinct role:

| Surface | Role | Where it runs |
|---|---|---|
| **Chat** | Strategist & PM — scoping, PRD, architecture, UI flow | Claude Desktop GUI, cloud sandbox |
| **Code** | Full-stack developer — writes code, runs tests, handles Git | Local terminal, mapped to your project root |
| **Cowork** | Operations agent — browser tasks, file organization, data seeding | Claude Desktop GUI with local folder + browser access |

These are used **sequentially**, not in parallel: scope in Chat → build in Code → seed and automate in Cowork. The premise behind it is that solo devs spend roughly 30% of their time writing code and 70% on setup, debugging, docs, data population, and admin — and the triad is aimed at that 70%.

---

## Pages

| File | What it covers |
|---|---|
| `index.html` | The main guide. Three parts: the 5Ws of the setup, a three-phase execution flow with tabbed blueprints, and an automation blueprint for scheduled routines. Includes 5 copy-to-clipboard prompt templates. |
| `optimize-tokens.html` | Token optimization companion. An 8-framework playbook covering intentional prompting, context management, local memory systems, model stacking, tool splitting, pricing reality, Skills, and subscription strategy. Ends with a 10-rule quick reference. |
| `openrouter-getting-started-guide.html` | OpenRouter onboarding — account setup, API key generation, and request examples in 15+ languages and frameworks (cURL, Python, JS, TypeScript, Next.js App Router, React, Spring Boot, Laravel, .NET, C++, Kotlin, Swift, Flutter, React Native, OpenAI SDK). |
| `playwright-claude-mcp.html` | Short three-step setup for adding the Playwright MCP server to Claude and starting an agent session. |
| `qa-summary-report.html` | A worked example of QA output — a full release-readiness report for the LessonForge MVP. 59 test cases across seven risk-ordered sections, 5 defects found and closed, Go recommendation. |

`COWORK_INSTRUCTIONS.md` holds the Project Instructions block to paste into Claude Cowork when working on this repo, along with the styling rules, color system, and the exact markup patterns for adding prompt blocks and blueprint tabs.

---

## Viewing it

Open any `.html` file directly in a browser. That's it — no server required.

If you want a local server anyway (useful for consistent relative-link behavior):

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

The repo is set up for GitHub Pages deployment from `main`. Push to `main` and the site goes live in roughly two minutes at `https://aspect-study.github.io/claude-mpv-guide/`, assuming Pages is enabled in repository settings.

---

## How it's built

- **Tailwind CSS v4** via the browser CDN (`@tailwindcss/browser@4`) — utility classes only, no config file, no compilation
- **Font Awesome** via CDN for icons
- **Vanilla JS** for the interactive bits: `switchTab()` drives the blueprint tabs, `copyPrompt()` handles clipboard copy on prompt blocks
- **Dark theme** on a slate palette (`slate-950` → `slate-700`), with a color-per-surface convention: indigo for Chat, emerald for Code, amber for Cowork, purple for Automation, cyan for the token guide, orange for warnings
- **Responsive** from a 375px base up through `sm:` (640px) and `lg:` (1024px), with separate desktop-sidebar and mobile-pill navigation for the tab system

---

## Contributing / editing

Read `COWORK_INSTRUCTIONS.md` first. The important constraints:

- Never split `index.html` into multiple files
- Never introduce a build step, `package.json`, or `node_modules`
- Keep CSS inside the existing `<style>` block in `<head>`
- Don't change the `switchTab()` or `copyPrompt()` signatures
- Adding a blueprint tab requires exactly four coordinated changes — the `tabConfig` entry, the desktop button, the mobile pill, and the content panel. Miss one and tab switching breaks silently.
- Conventional commits: `feat:`, `fix:`, `docs:`, `style:`, `refactor:`

---

## Known gaps

Documenting these rather than leaving them for the next person to trip over:

**The repository name is misspelled.** It reads `claude-mpv-guide`, but every page inside says **MVP**. Renaming on GitHub leaves a redirect for the git remote, but it changes the GitHub Pages URL and any existing links to it.

**Three pages are orphaned.** Only `index.html` and `optimize-tokens.html` link to each other. `openrouter-getting-started-guide.html`, `playwright-claude-mcp.html`, and `qa-summary-report.html` have no inbound links from anywhere — you can only reach them by typing the URL. A small nav or index section would fix it.

**`COWORK_INSTRUCTIONS.md` is out of date.** It describes a two-page project and doesn't mention the three newer files at all. Anyone following it as ground truth will have an incomplete picture.

**The canonical source files aren't in the repo.** `COWORK_INSTRUCTIONS.md` names `guide document/guide.txt` as the source of truth that HTML text must match, but `.gitignore` excludes `guide document/`. The documented sync workflow can't be run from a fresh clone.

**Dependency versions drift across pages.** Font Awesome appears at three versions (6.4.0, 6.4.2, and a 4.7.0 fork), and `playwright-claude-mcp.html` loads Tailwind from the v3 play CDN (`cdn.tailwindcss.com`) while the other pages use the v4 browser CDN. Worth standardizing — the class names differ between v3 and v4 in ways that will bite during a future edit.

**Section numbering is out of order** in the OpenRouter guide: 4.15 (Response Structure) appears after 4.16 and 4.17.

**`qa-summary-report.html` is topically separate.** It's a LessonForge deliverable rather than Claude workflow guidance. Reasonable to keep as a worked example of what the workflow produces, but that framing isn't stated anywhere on the page.

**No license file.** Anyone finding this has no stated terms for reuse.

---

## License

None specified.
