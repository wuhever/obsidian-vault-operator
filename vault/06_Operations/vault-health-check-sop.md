---
type: sop
status: active
created: 2026-01-01
---

# Vault Health Check — Standard Operating Procedure

Run this checklist periodically (weekly recommended, monthly minimum) to keep the vault clean and functional.

## 1. Frontmatter Compliance

- [ ] Every `.md` file has YAML frontmatter with `type`, `status`, and `created`
- [ ] All `type` values match the canonical list: note, client, project, research, idea, sop, task, meeting, reference, system, context, strategy, daily, playbook
- [ ] All `status` values match: draft, active, completed, archived, incomplete, locked
- [ ] No files with `status: draft` older than 30 days (should be promoted or archived)

## 2. File Placement

- [ ] No files at the vault root (except AGENTS.md, CLAUDE.md, README.md, .obsidianignore)
- [ ] No misplaced files (e.g., research notes in `02_Work/`, client docs in `07_Ideas/`)
- [ ] All entity folders in `02_Work/` have a README.md
- [ ] `09_Reference/` contains only files placed by the owner (no agent-created files)

## 3. Inbox Triage

- [ ] `00_Inbox/` checked for unsorted files (excluding `Daily/`)
- [ ] Any unsorted files triaged to correct folders
- [ ] Moved files logged in `vault-operator/changes/`

## 4. Naming Conventions

- [ ] All filenames use kebab-case (no spaces, no camelCase, no PascalCase)
- [ ] No generic filenames (`untitled.md`, `new-note.md`, `test.md`)

## 5. Links and Orphans

- [ ] No broken wikilinks (link targets that don't exist)
- [ ] No orphaned files (files with zero incoming links)
- [ ] Wikilinks used for internal links (not markdown-style links)

## 6. Templates

- [ ] All 8 templates present in `_Templates/`
- [ ] Template frontmatter matches the canonical type/status lists
- [ ] No regular notes accidentally saved in `_Templates/`

## 7. Bases (.base files)

- [ ] All `.base` files open without errors
- [ ] Base filters and formulas return expected results
- [ ] No stale data (completed tasks still showing as active)

## 8. Sync Health

- [ ] Obsidian Sync shows green checkmark (all changes synced)
- [ ] No lingering conflict files (`*sync-conflict*` or `*Conflicted copy*`)
- [ ] `skills/` folder excluded from Sync
- [ ] "Sync all other types" enabled (for .base/.canvas files)

## 9. Personal Space

- [ ] Personal space `_README.md` exists
- [ ] No agent-created files in personal space (unless owner-authorized)

## 10. Protected Content

- [ ] `09_Reference/_READ-ONLY.md` is unchanged
- [ ] No secrets (API keys, passwords, .env content) anywhere in the vault

## After the Check

Log the health check results in `vault-operator/context/` with any issues found and actions taken.
