# {{VAULT_NAME}}

Personal Obsidian vault for **{{OWNER_NAME}}** — {{VAULT_PURPOSE}}.

**Vault type:** {{VAULT_TYPE}}

---

## Your Folder Scheme

{{SCHEME_TABLE}}

**Universal folders** (every vault has these):

| Folder | Purpose |
|---|---|
| `00_Inbox/` | Quick capture, daily notes, unsorted items |
| `09_Reference/` | Read-only archive |
| `{{OWNER_SLUG}}-space/` | {{OWNER_NAME}}'s personal workspace |
| `_Templates/` | Note templates |

---

## Common Workflows

### Capture something quickly
Drop it in `00_Inbox/` or today's daily note. Don't worry about where it "should" go — the Vault Operator triages later.

### Create a daily note
Obsidian's Daily Notes plugin auto-saves to `00_Inbox/Daily/` using `_Templates/daily-note.md`.

### Add research
Research notes live **inside the scope** they relate to (entity folder, project folder, etc.) — never in a generic top-level research folder. When in doubt, drop in `00_Inbox/`.

### Use templates
When creating a standard note type (research, idea, meeting, SOP, project brief, entity, playbook), copy from `_Templates/` and fill in.

---

## 09_Reference is Read-Only

This folder is an archive. Nothing inside gets modified. To build on a reference, create a note elsewhere and link back with `[[wikilinks]]`.

---

## Using AI Agents

Any AI agent (Claude, Gemini, GPT) can work in this vault:

- Claude auto-reads `CLAUDE.md`
- Other agents should be pointed to `AGENTS.md`

Both files explain folder structure, naming rules, and content guidelines.

---

## What Syncs (Obsidian Sync)

**Syncs:** all folders visible in Obsidian — notes, PDFs, images, `.base`, `.canvas`, templates.

**Does NOT sync** (via `.obsidianignore`):
- `.agents/`, `.claude/`, `skills/` — installed per-machine
- Install locally: `npx skills add https://github.com/kepano/obsidian-skills.git --yes`

---

## Vault Operations

Structural changes go through the **`vault-operator/`** workspace at `{{VAULT_OPERATOR_PATH}}`. Don't restructure manually — use the Vault Operator to keep everything tracked and consistent.
