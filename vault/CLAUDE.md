# {{VAULT_NAME}} — Claude Instructions

> Read `AGENTS.md` first for full vault context, folder structure, and content rules. This file covers Claude-specific capabilities.

---

## Vault Context

This is the Obsidian vault for **{{OWNER_NAME}}**, purpose: {{VAULT_PURPOSE}}. See `AGENTS.md` for the complete folder map, naming conventions, and prohibitions.

---

## Session Behavior

Before the user tells you what to do, you already know:

1. **Read existing content first.** Before creating anything in a folder, read what's already there.
2. **Use templates automatically.** When creating a research note, idea, meeting note, SOP, project brief, client/entity folder, or playbook — use the matching template from `_Templates/`.
3. **Read any identity/brand reference** in `01_Identity/` before writing public-facing content.
4. **Wikilink related notes.** If your work connects to other notes, link them: `[[note-name]]`.
5. **Use `00_Inbox/` for anything without a clear home.** Don't ask. Inbox it, add frontmatter, move on.
6. **Only use approved frontmatter types:** `note`, `client`, `project`, `research`, `idea`, `sop`, `task`, `meeting`, `reference`, `system`, `context`, `strategy`, `daily`, `playbook`. Never invent a new type.

---

## Installed Obsidian Skills

Five Obsidian skills are available from `kepano/obsidian-skills`:

| Task | Skill to use |
|---|---|
| Creating/editing `.md` notes (wikilinks, embeds, callouts, properties) | `obsidian-markdown` |
| Creating/editing `.base` database views (tables, boards, filters, formulas) | `obsidian-bases` |
| Creating/editing `.canvas` visual diagrams | `json-canvas` |
| CLI interaction with the Obsidian app | `obsidian-cli` |
| Extracting clean markdown from a web URL | `defuddle` |

### Installing / Updating Skills

Skills are per-machine (they don't sync). Install locally:

```bash
npx skills add https://github.com/kepano/obsidian-skills.git --yes
npx skills add https://github.com/kepano/obsidian-skills.git --yes --global
```

---

## Obsidian Syntax Reminders

```markdown
# Internal links
[[note-name]]
[[note-name|display text]]
[[note-name#heading]]

# Embeds
![[note-name]]
![[image.png]]

# Callouts
> [!info] Title
> Content

> [!warning] Important
> Warning content

# Frontmatter
---
type: note
status: active
created: 2026-01-15
tags: [topic, area]
---
```

---

## Inbox (`00_Inbox/`)

The vault's catch-all folder. When you need to save something but aren't sure which folder it belongs in, put it here.

- Read `[[_README]]` in `00_Inbox/` for full triage rules
- `00_Inbox/Daily/` is for daily notes only — do not triage or move those
- The Vault Operator periodically scans and sorts unsorted files from this folder

---

## Vault Operator

Structural changes are managed through `vault-operator/` at `{{VAULT_OPERATOR_PATH}}`. If you need to suggest structural changes, note them but do not implement — the Vault Operator handles that.
