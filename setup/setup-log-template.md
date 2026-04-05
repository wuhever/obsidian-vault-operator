# Setup Log Templates

Formats for the two logs the wizard writes at the end of Phase 5.

---

## Change log: `vault-operator/changes/{TIMESTAMP}-initial-setup.md`

```markdown
---
type: change
date: YYYY-MM-DD
operator: [agent name / model]
---

# Change Log — YYYY-MM-DD — Initial Setup

## Summary

Ran `/setup` wizard on fresh template clone. Personalized for owner `{{OWNER_NAME}}`, vault purpose `{{VAULT_PURPOSE}}`. {Preset name or "default"} scheme chosen. {N} files routed from `/_intake/` to vault folders.

## Placeholders Replaced

| Token | Value |
|---|---|
| `{{VAULT_NAME}}` | `sarah-phd-vault` |
| `{{OWNER_NAME}}` | `Sarah` |
| `{{OWNER_SLUG}}` | `sarah` |
| `{{VAULT_PURPOSE}}` | `PhD research on marine biology` |
| `{{ORG_OR_TOPIC}}` | `your research` |
| `{{VAULT_PATH}}` | `C:\Users\sarah\Documents\sarah-phd-vault\vault` |
| `{{VAULT_OPERATOR_PATH}}` | `C:\Users\sarah\Documents\sarah-phd-vault\vault-operator` |

## Folder Renames

| From | To |
|---|---|
| `vault/02_Work/` | `vault/02_Collaborators/` |
| `vault/05_Strategy/` | `vault/05_Papers/` |
| `vault/Owner-Space/` | `vault/sarah-space/` |

## Folders Created

- `vault/04_Courses/`
- `vault/04_Experiments/`

## Demo Content

- Kept / Deleted (list which)

## Files Moved from `/_intake/`

| Source | Destination | Frontmatter added? |
|---|---|---|
| `_intake/cv.md` | `vault/01_Identity/About/cv.md` | no (had frontmatter) |
| `_intake/papers/smith-2024.pdf` | `vault/05_Papers/smith-2024.pdf` | n/a (binary) |
| `_intake/courses/bio-501/notes.md` | `vault/04_Courses/bio-501/notes.md` | yes (added type: note) |
| ... (list every file moved) | | |

## Outstanding

- `/_intake-backup/` exists — user should delete when confident
- {N} PDFs with cryptic filenames flagged for manual rename (see below)
- Install Obsidian Sync → see `docs/OBSIDIAN-SYNC.md`
- Install Obsidian skills: `npx skills add https://github.com/kepano/obsidian-skills.git --yes`

### Files flagged for manual review

- `vault/05_Papers/1711.03938.pdf` — cryptic filename, recommend renaming
```

---

## Session log: `vault-operator/context/{TIMESTAMP}-initial-setup.md`

```markdown
---
type: context
date: YYYY-MM-DD
session: initial-setup
operator: [agent name / model]
participants: [user]
---

# Session — YYYY-MM-DD — Initial Setup

## Context

Fresh clone of `obsidian-vault-operator` template. User ran the `/setup` wizard.

## Interview Answers

| Question | Answer |
|---|---|
| Owner name | Sarah |
| Vault name | sarah-phd-vault |
| Vault purpose | PhD research on marine biology |
| Vault path | C:\Users\sarah\Documents\sarah-phd-vault |
| Keep demo content? | No |

## Intake Analysis

- Intake contained: 40 PDFs, 6 course folders, 1 CV.md, 12 misc notes
- Matched preset: **researcher**
- Confidence: high (dominant signal: year-stamped PDFs + course folders)

## Scheme Decision

Proposed researcher scheme. User responded: **Keep**

Final scheme:
- 00_Inbox, 01_Identity, 02_Collaborators, 03_Projects, 04_Courses, 04_Experiments, 05_Papers, 06_Operations, 07_Ideas, 09_Reference

## Execution Notes

- All placeholders replaced cleanly
- 42 files routed, 31 markdown files received frontmatter
- No errors

## Open Items

- User to verify `/_intake-backup/` before deletion
- User to install Obsidian Sync (optional)
- User to install local Obsidian skills (machine-specific)
- 3 PDFs with cryptic filenames need manual renaming (see change log)

## Next Session

User should run the `vault-operator-audit` skill after using the vault for a week to catch any drift or early issues.
```

---

## Notes

- Use **UTC timestamps** to avoid collisions: `date -u +"%Y-%m-%d-%H%M%S"`
- Store YAML `date` field as absolute date in ISO format (not "today")
- Keep change log focused on **what happened**, session log focused on **what was decided and why**
