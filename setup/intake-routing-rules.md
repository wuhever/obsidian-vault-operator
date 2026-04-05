# Intake Routing Rules

Heuristics the setup wizard uses to decide where each file in `/_intake/` should go. These are guidance, not absolute — the wizard should combine these with content-awareness and the chosen scheme.

---

## By file extension

| Extension | Default destination | Notes |
|---|---|---|
| `.md` | Depends on content — see content rules below | Read first 20 lines to infer |
| `.pdf` | `09_Reference/` (default) or `05_Papers/` (researcher preset) | Papers with year-stamped names → Papers folder |
| `.docx`, `.doc` | `03_Projects/` or `02_Work/` | Usually work products |
| `.xlsx`, `.csv` | `06_Operations/` or `05_Strategy/` | Data, tracking sheets |
| `.png`, `.jpg`, `.jpeg` | `09_Reference/` or project's folder | If related to a project, put with the project |
| `.canvas` | Keep at vault root or move to topic folder | Visual diagrams usually belong where their content lives |
| `.base` | `06_Operations/` | Database views |
| `.html`, `.htm` | `09_Reference/` | Saved web pages |

---

## By filename patterns

### Papers / research
- `*-YYYY.pdf` or `YYYY-*.pdf` (year-stamped) → `05_Papers/` (researcher) or `09_Reference/` (other)
- `paper-*`, `article-*` → same
- `bib*.md`, `*bibliography*` → alongside papers

### Meetings / calls
- `meeting-*`, `call-*`, `1on1-*`, `standup-*` → `02_Work/{entity}/` if entity is obvious, else `00_Inbox/`

### SOPs / processes
- `sop-*`, `how-to-*`, `workflow-*`, `process-*` → `06_Operations/`

### Ideas / brainstorms
- `idea-*`, `brainstorm-*`, `thought-*` → `07_Ideas/`

### Strategy / planning
- `strategy-*`, `plan-*`, `roadmap-*`, `okrs-*`, `goals-*` → `05_Strategy/` or preset equivalent

### Daily / journal
- `YYYY-MM-DD.md`, `daily-*`, `journal-*` → `00_Inbox/Daily/`

### CV / bio / identity
- `cv*`, `resume*`, `bio*`, `about-*`, `who-am-i*` → `01_Identity/About/`

### Courses / learning
- `course-*`, `lecture-*`, `lesson-*`, `module-*`, `week-*` → `04_Courses/` (student) or `07_Ideas/` (other)

---

## By content (for `.md` files)

Read the first 20 lines of each markdown file. Look for:

### Frontmatter `type` field
If the file already has `type: client` → `02_Work/` / `02_Collaborators/` etc.
If `type: project` → `03_Projects/`
If `type: research` → scope-appropriate research folder
If `type: sop` → `06_Operations/`
If `type: idea` → `07_Ideas/`
If `type: meeting` → scope-appropriate folder or `00_Inbox/`
If `type: daily` → `00_Inbox/Daily/`

### Content signals
- Mentions of a client/company/person name → probably `02_Work/{name}/`
- "Research on", "study of", "analysis of" → research folder for the relevant scope
- Action lists + dates → project or operations
- Questions + open loops → `07_Ideas/`
- Summaries of external content → `09_Reference/` or scope-specific research

---

## By folder structure in intake

If the user's intake already has folders, respect their groupings:

- `intake/clients/AcmeCorp/` → `vault/02_Work/AcmeCorp/` (copy structure)
- `intake/courses/BIO-501/` → `vault/04_Courses/BIO-501/`
- `intake/research/` → scope-appropriate research folders
- `intake/random-notes/` → triage individually (don't preserve this folder name)

Preserve user's subfolder structure when it makes sense. Flatten when the intake folder name is meaningless (like "stuff/" or "misc/").

---

## When you can't decide

If a file doesn't match any rule clearly, route it to `vault/00_Inbox/`. The user can re-triage later with the operator. Don't guess — the inbox exists for ambiguous cases.

Never route to `09_Reference/` unless the file is clearly archival (saved article, textbook PDF, canonical reference). `09_Reference/` is read-only after setup.

---

## Adding frontmatter during routing

When moving a `.md` file that lacks frontmatter, add minimal frontmatter:

```yaml
---
type: note
status: active
created: YYYY-MM-DD  # today's date
---
```

Infer a better `type` if the content makes it obvious (e.g., an SOP-looking file → `type: sop`, an idea-looking file → `type: idea`). If unclear, `note` is always safe.

Don't modify frontmatter that already exists — only add when missing.

---

## PDFs and binary files

Don't add frontmatter to non-markdown files. Just move them.

For PDFs, the filename is the primary metadata. If PDFs are landing in `09_Reference/` or `05_Papers/` and their names are cryptic (e.g., `1711.03938.pdf`), flag this for the user in the setup log — they may want to rename them post-setup.
