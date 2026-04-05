# Roadmap

What's planned for future versions. Open an issue to vote on any of these or suggest others.

---

## v0.2 — Scheme preset library

Ship pre-built scheme presets for common vault types, selectable during setup:

- **business** — clients, proposals, operations (current default scheme)
- **researcher** — papers, experiments, thesis chapters, collaborators
- **student** — courses, assignments, readings, projects
- **personal** — journal, ideas, reading list, projects
- **writing** — drafts, research, submissions, published work
- **engineer** — projects, SOPs, references, learning

Each preset would include: folder scheme + a pre-filled `_EXAMPLE-*` demo specific to that use case + routing rules tuned for that content type.

---

## v0.3 — Multi-owner support

Add presets for:
- **two-person** (couple, co-founders, partners): two personal spaces + shared folders
- **family** (3+ owners): N personal spaces + shared
- **agent-only**: no personal spaces, AI-curated knowledge base with human admin

The wizard would ask "how many owners?" and scaffold N `*-space/` folders with proper access rules.

---

## v0.4 — Shell-script fallback

For users without a Claude-capable IDE, ship a `./setup.sh` (and Windows `setup.ps1`) that:
- Reads the same question list as the wizard
- Does find-and-replace on placeholders
- Can't do intelligent scheme adaptation (requires agent), falls back to default scheme
- Prints a message pointing users to run the wizard later for smart reorganization

---

## v0.5 — Automated tests

- Snapshot tests: run `/setup` with fixture `_intake/` contents, verify output matches golden files
- CI checks: no unreplaced placeholders, no dangling wikilinks in templates, all referenced files exist
- Doc drift checks: frontmatter type lists match across `AGENTS.md`, `CLAUDE.md`, `operator-prompt.md`

---

## v1.0 — GitHub Template Repository polish

- Enable the GitHub "Use this template" button (may happen earlier)
- Release notes + versioning
- A polished landing page / demo video
- A curated list of user-submitted scheme presets

---

## Ideas under consideration

- **Optional web UI** for the setup wizard (HTML file that generates config.yaml)
- **Pre-configured `.obsidian/` starter** (plugins, hotkeys, theme choice) as an optional install
- **Integration with n8n / Zapier** for automatic inbox triage on file drops
- **Integration with Readwise / Instapaper** for automatic `09_Reference/` population
- **Voice-activated operator** (dictate changes, operator executes)

---

## Out of scope (probably forever)

- Non-Obsidian vault formats (Logseq, Notion, Roam) — different mental models
- Building a custom Obsidian plugin — out of scope, the repo is markdown-only
- Automatic backups — Obsidian Sync + git handle this
- Multi-language UI — the templates and prompts are English-first

---

## How to influence the roadmap

Open an issue describing your use case. The roadmap is guided by what real users need, not hypothetical features.
