# {{VAULT_NAME}} — Agent Instructions

> **Read this file in full before beginning any task.** This is the operating manual for this Obsidian vault. Every AI agent — Claude, Gemini, GPT, Codex, or any other — must follow these rules when working inside this vault.

---

## Vault Identity

**What this is:** The personal Obsidian vault for **{{OWNER_NAME}}**.

**Purpose:** {{VAULT_PURPOSE}}

**Shared via:** Optionally Obsidian Sync (see `docs/OBSIDIAN-SYNC.md` in the repo root).

---

## Folder Structure

```
vault/
├── 00_Inbox/           Quick capture, daily notes, unsorted items
├── 01_Identity/        About, brand, bio, goals
├── 02_Work/            Engagements, clients, collaborators
│   └── _Entity-Template/  Template for new entity folders
├── 03_Projects/        Active projects and deliverables
├── 05_Strategy/        Strategy, growth plans, planning docs
├── 06_Operations/      SOPs, processes, task board
├── 07_Ideas/           Brainstorms, experiments
├── 08_Publishing/      Content, social, newsletter, papers
├── 09_Reference/       READ-ONLY archive
├── {{OWNER_SLUG}}-space/  {{OWNER_NAME}}'s personal workspace
├── _Templates/         Obsidian note templates
├── AGENTS.md           This file
├── CLAUDE.md           Claude-specific instructions
└── README.md           Human guide
```

*(Your folder scheme may differ if you chose a preset during `/setup` — researcher, student, or personal schemes rename some of these folders.)*

---

## Navigation Rules

### Where to create files

| You need to... | Create it in... |
|---|---|
| Capture something quickly | `00_Inbox/` |
| Write about identity, brand, or bio | `01_Identity/` |
| Add information about a client / collaborator / entity | `02_Work/[EntityName]/` |
| Document a project | `03_Projects/` |
| Save research | Inside the scope it relates to — `02_Work/{Entity}/Research/`, `03_Projects/{Project}/Research/`, or `05_Strategy/research/` for cross-cutting research |
| Write strategy or plans | `05_Strategy/` |
| Create an SOP or process doc | `06_Operations/` |
| Brainstorm or capture an idea | `07_Ideas/` |
| Draft publishing content | `08_Publishing/` |
| Store reference material | **DO NOT** — only the owner adds to `09_Reference/` |

### Where NOT to create files

- **Vault root** — never create files at the top level (except by explicit instruction)
- **09_Reference/** — read-only, agents cannot create/modify/delete
- **_Templates/** — only create template files here, never regular notes
- **.obsidian/** — never touch Obsidian configuration

---

## Naming Conventions

### Files
- Use **kebab-case**: `my-research-note.md`, `client-onboarding-sop.md`
- No spaces in filenames
- Use descriptive names, not numbered prefixes (exception: daily notes use date format)

### Frontmatter
Every new `.md` file MUST include YAML frontmatter with at minimum:
```yaml
---
type: [note/client/project/research/idea/sop/task/meeting/reference/system/context/strategy/daily/playbook]
status: [draft/active/completed/archived/incomplete/locked]
created: YYYY-MM-DD
---
```

Additional properties depend on the note type — see `_Templates/` for complete frontmatter schemas.

---

## How to Work in This Vault

These behaviors are expected of every agent in every session:

### Before starting any task
1. **Read existing content in the relevant folder first.** Build on what's already there — don't start from scratch.
2. **Read any identity/brand reference** in `01_Identity/` before writing public-facing or branded content (if the owner has set one up).

### When creating files
3. **Always use a template** when creating a standard note type. Read `_Templates/` to find the right one, copy its structure, fill in the placeholders.
4. **Always add frontmatter** — every `.md` file gets `type`, `status`, and `created` at minimum.
5. **Use wikilinks** to connect related notes across folders: `[[related-note-name]]`.

### When unsure where something goes
6. **Dump it in `00_Inbox/`** — that's what it's for. Don't ask where to put it. Inbox it, add frontmatter, move on. The Vault Operator triages later.

### During the session
7. **Don't create files you don't need.** Prefer adding to existing notes over creating new ones.
8. **Don't reorganize the vault.** Structural changes happen through the `vault-operator/` workspace.

---

## Read-Only Folder: 09_Reference

`09_Reference/` is a **read-only archive**. AI agents:
- **MAY** read any file in this folder freely
- **MUST NOT** create, modify, or delete any file in this folder
- If you need to annotate reference material, create a new note in the appropriate working folder and link back with `[[wikilinks]]`

---

## Personal Space

`{{OWNER_SLUG}}-space/` is {{OWNER_NAME}}'s personal workspace.

- Only the owner (and agents operating on their behalf) should create, modify, or delete files here
- Cross-referencing personal-space content from shared notes is fine

---

## Templates

Use templates from `_Templates/` when creating standard note types:
- `daily-note.md`
- `meeting-note.md`
- `client-folder-README.md` (rename to entity-folder for your preset)
- `research-note.md`
- `idea-note.md`
- `sop.md`
- `project-brief.md`
- `playbook.md`

Copy the template content and fill in placeholders. Do not modify the template files themselves.

**If no template matches your note type:** Use the closest template as a starting point. Always use an approved `type` from the list above — never invent a new one. If nothing fits, use `type: note` with a `subtype` property.

---

## Obsidian Features

This vault uses Obsidian with these features enabled:

- **Wikilinks** — `[[note-name]]` for internal links (preferred over markdown links)
- **Properties** — YAML frontmatter for metadata on every note
- **Bases** — `.base` files for database views (Task-Board, entity trackers)
- **Canvas** — `.canvas` files for visual diagrams

> [!warning] `.base` and `.canvas` files do NOT merge — last-write-wins.
> If two devices edit the same `.base` or `.canvas` file at the same time, the older edit is silently lost. **Only one agent/device should edit these file types at a time.** `.md` files are safe for concurrent editing.

- **Daily notes** — saved in `00_Inbox/Daily/`
- **Tags** — use tags in frontmatter, not inline hashtags
- **Callouts** — use `> [!type] Title` syntax

---

## Prohibitions

1. Never modify `.obsidian/` configuration files
2. Never create files at the vault root
3. Never modify files in `09_Reference/`
4. Never delete personal space content
5. Never store secrets, API keys, or credentials in the vault

---

## Vault Operator

Structural changes to this vault (adding folders, reorganizing, updating templates, modifying this file) are managed through the **`vault-operator/`** workspace at `{{VAULT_OPERATOR_PATH}}`. If you need to suggest structural changes, note them but do not implement them — the Vault Operator handles that.
