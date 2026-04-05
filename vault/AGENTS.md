# {{VAULT_NAME}} — Agent Instructions

> **Read this file in full before beginning any task.** This is the operating manual for this Obsidian vault. Every AI agent — Claude, Gemini, GPT, Codex, or any other — must follow these rules when working inside this vault.

---

## Vault Identity

**What this is:** The personal Obsidian vault for **{{OWNER_NAME}}**.

**Purpose:** {{VAULT_PURPOSE}}

**Vault type:** {{VAULT_TYPE}}

---

## Folder Structure

This vault's folder scheme was created during setup based on the owner's needs. The current scheme is:

{{SCHEME_TABLE}}

**Universal folders** (present in every vault of this template):

| Folder | Purpose |
|---|---|
| `00_Inbox/` | Catch-all for anything without a clear home. Triaged periodically by the Vault Operator. Contains `Daily/` subfolder for daily notes. |
| `09_Reference/` | READ-ONLY archive. Agents may read but not modify. |
| `_Templates/` | Note templates. Use them when creating standard note types. |
| `{{OWNER_SLUG}}-space/` | {{OWNER_NAME}}'s personal workspace. |

---

## Navigation Rules

### Where to create files

| You need to... | Create it in... |
|---|---|
| Capture something quickly | `00_Inbox/` |
| A note that fits a topical folder | That folder (see scheme table above) |
| Research related to an entity/project | Inside that entity/project folder (scoped colocation) |
| A new idea or experiment | Your ideas folder (see scheme) |
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
- Descriptive names, not numbered prefixes (exception: daily notes use date format)

### Frontmatter
Every new `.md` file MUST include YAML frontmatter with at minimum:
```yaml
---
type: [note/client/project/research/idea/sop/task/meeting/reference/system/context/strategy/daily/playbook]
status: [draft/active/completed/archived/incomplete/locked]
created: YYYY-MM-DD
---
```

See `_Templates/` for complete frontmatter schemas per note type.

---

## How to Work in This Vault

These behaviors are expected of every agent in every session:

### Before starting any task
1. **Read existing content in the relevant folder first.** Build on what's already there.
2. **Read any identity/brand reference** in the identity folder before writing public-facing content (if one exists).

### When creating files
3. **Always use a template** when creating a standard note type. Read `_Templates/`, copy the structure, fill in placeholders.
4. **Always add frontmatter** — every `.md` file gets `type`, `status`, and `created` at minimum.
5. **Use wikilinks** to connect related notes: `[[related-note-name]]`.

### When unsure where something goes
6. **Dump it in `00_Inbox/`** — that's what it's for. Don't ask. Inbox it, add frontmatter, move on. The Vault Operator triages later.

### During the session
7. **Don't create files you don't need.** Prefer adding to existing notes over creating new ones.
8. **Don't reorganize the vault.** Structural changes happen through `vault-operator/`.

---

## Read-Only Folder: 09_Reference

`09_Reference/` is a **read-only archive**. AI agents:
- **MAY** read any file in this folder freely
- **MUST NOT** create, modify, or delete any file in this folder
- To build on reference material, create a new note in the appropriate working folder and link back with `[[wikilinks]]`

---

## Personal Space

`{{OWNER_SLUG}}-space/` is {{OWNER_NAME}}'s personal workspace.

- Only the owner (and agents operating on their behalf) should create, modify, or delete files here
- Cross-referencing personal-space content from shared notes is fine

---

## Templates

8 templates ship in `_Templates/`: `daily-note`, `meeting-note`, `research-note`, `idea-note`, `sop`, `project-brief`, `client-folder-README`, `playbook`.

Copy the template content and fill in placeholders. Do not modify the template files themselves.

**If no template matches your note type:** Use the closest template as a starting point. Always use an approved `type` from the list above — never invent a new one. If nothing fits, use `type: note` with a `subtype` property.

---

## Obsidian Features

This vault uses Obsidian with these features enabled:

- **Wikilinks** — `[[note-name]]` for internal links
- **Properties** — YAML frontmatter for metadata
- **Bases** — `.base` files for database views
- **Canvas** — `.canvas` files for visual diagrams

> [!warning] `.base` and `.canvas` files do NOT merge — last-write-wins.
> Only one agent/device should edit these file types at a time. `.md` files are safe for concurrent editing.

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

Structural changes (adding folders, reorganizing, updating templates, modifying this file) are managed through the **`vault-operator/`** workspace at `{{VAULT_OPERATOR_PATH}}`. If you need to suggest structural changes, note them but do not implement — the Vault Operator handles that.
