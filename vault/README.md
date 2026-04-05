# {{VAULT_NAME}}

Personal Obsidian vault for **{{OWNER_NAME}}** — {{VAULT_PURPOSE}}.

---

## Quick Reference

| Folder | Purpose |
|---|---|
| `00_Inbox/` | Quick capture, daily notes, unsorted items |
| `01_Identity/` | About, brand, bio, goals |
| `02_Work/` | Engagements, clients, collaborators |
| `03_Projects/` | Active projects and deliverables |
| `05_Strategy/` | Strategy, growth plans, planning |
| `06_Operations/` | SOPs, internal processes, task board |
| `07_Ideas/` | Brainstorms, experiments |
| `08_Publishing/` | Content, social, newsletter, papers |
| `09_Reference/` | Read-only archive |
| `{{OWNER_SLUG}}-space/` | {{OWNER_NAME}}'s personal workspace |
| `_Templates/` | Note templates |

*Your folder names may differ if you chose a preset (researcher, student, personal) during `/setup`.*

---

## How to Add a New Entity (Client / Collaborator)

1. Copy `02_Work/_Entity-Template/` and rename to the entity's name
2. Fill in the entity folder's `README.md` with details
3. Use subfolders: `Research/`, `Documents/`, `Workflow/`

## How to Capture an Idea

1. Quick capture: drop in `00_Inbox/` or today's daily note
2. When ready to develop: move to `07_Ideas/` using the idea template
3. When actionable: promote to `03_Projects/` with a project brief

## How to Create a Daily Note

Obsidian's Daily Notes plugin auto-saves to `00_Inbox/Daily/` using the `_Templates/daily-note.md` template.

---

## 09_Reference is Read-Only

This folder is an archive. Nothing inside gets modified. If you want to build on a reference, create a note in the scoped working folder and link back with `[[wikilinks]]`.

---

## Research Notes Go Inside Their Scope

No top-level research folder. Research notes live inside what they're about:

- Entity research → `02_Work/{Entity}/Research/`
- Project research → `03_Projects/{Project}/Research/`
- Cross-cutting research → `05_Strategy/research/`

When in doubt, drop it in `00_Inbox/` and the Vault Operator will route it.

---

## Using AI Agents in This Vault

Any AI agent (Claude, Gemini, GPT) can work inside this vault:

- Claude reads `CLAUDE.md` automatically
- Other agents should be pointed to `AGENTS.md`
- Both files explain folder structure, naming rules, and content guidelines

---

## What Syncs (Obsidian Sync)

**Syncs:** all folders visible in Obsidian — notes, PDFs, images, `.base`, `.canvas`, templates.

**Does NOT sync** (excluded by `.obsidianignore`):
- `.agents/`, `.claude/`, `skills/` — agent infrastructure is per-machine
- Install skills locally: `npx skills add https://github.com/kepano/obsidian-skills.git --yes`

---

## Vault Operations

Structural changes (adding folders, reorganizing, updating templates) go through the **`vault-operator/`** workspace at `{{VAULT_OPERATOR_PATH}}`. Don't restructure manually — use the Vault Operator so everything stays tracked and consistent.
