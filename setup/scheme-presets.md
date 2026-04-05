# Scheme Presets

Folder schemes the wizard **creates** during setup (not rename). The repo ships with only universal folders (Inbox, Reference, Templates, Owner-Space) — the wizard creates everything else based on the user's chosen vault type.

Each preset is matched to the `{{VAULT_TYPE}}` picked during the interview. Intake content (if any) refines the scheme further.

---

## Universal folders (every vault, every preset)

These are created/preserved in every vault — the wizard does not touch them:

| Folder | Purpose |
|---|---|
| `00_Inbox/` | Catch-all, triaged periodically. `Daily/` subfolder for daily notes. |
| `09_Reference/` | READ-ONLY archive |
| `_Templates/` | Note templates |
| `{owner-slug}-space/` | Owner's personal workspace |

---

## Preset: `student`

**For:** undergraduates, graduate students, anyone doing course-based learning

**Signals:** folders named `courses/`, `lectures/`, `assignments/`, textbook PDFs, syllabus docs, week-numbered files

**Folders to create:**

| Folder | Purpose |
|---|---|
| `01_Identity/` | About you, goals, study plan |
| `02_Courses/` | One folder per course |
| `03_Projects/` | Assignments, term papers, capstones |
| `04_Study-Notes/` | Concept notes, flashcards, summaries |
| `05_Resources/` | Textbooks, cheat sheets, shared readings |
| `06_Operations/` | Study routines, exam prep SOPs |
| `07_Ideas/` | Career ideas, side projects, research interests |

---

## Preset: `researcher`

**For:** PhD students, academic researchers, lab scientists

**Signals:** `.pdf` files with year-stamped names (`smith-2024.pdf`), folders like `papers/`, `experiments/`, `thesis/`, citation keys

**Folders to create:**

| Folder | Purpose |
|---|---|
| `01_Identity/` | CV, bio, research goals |
| `02_Collaborators/` | Advisor, committee, lab mates, co-authors |
| `03_Projects/` | Thesis chapters, paper drafts, grants |
| `04_Experiments/` | Lab notes, datasets, results |
| `05_Papers/` | Reading library, annotated PDFs |
| `06_Operations/` | Writing workflow, submission SOPs |
| `07_Ideas/` | Research questions, hypotheses |
| `08_Publishing/` | Posters, talks, published work |

---

## Preset: `business`

**For:** solo consultants, freelancers, agency operators, service businesses

**Signals:** folders like `clients/`, `proposals/`, `invoices/`, SOPs, contracts, retainer docs

**Folders to create:**

| Folder | Purpose |
|---|---|
| `01_Identity/` | About, brand, positioning (create `01_Identity/Brand/` if brand work applies) |
| `02_Work/` | Clients / engagements (one folder per entity, use `_Entity-Template/`) |
| `03_Projects/` | Active project work |
| `05_Strategy/` | Growth plans, financial models |
| `06_Operations/` | SOPs, processes, task board |
| `07_Ideas/` | Brainstorms, experiments |
| `08_Publishing/` | Social, content, newsletter |

Also create: `02_Work/_Entity-Template/` with `Research/`, `Documents/`, `Workflow/` subfolders + README.

---

## Preset: `hobbyist-builder`

**For:** web designers, app builders, makers, tinkerers, AI enthusiasts building projects

**Signals:** folders like `projects/`, `builds/`, `experiments/`, code snippets, README files, tool lists, tutorials

**Folders to create:**

| Folder | Purpose |
|---|---|
| `01_Identity/` | About you, skills, portfolio notes |
| `02_Tools/` | Stack references, cheat sheets, API notes |
| `03_Projects/` | Active builds (one folder per project) |
| `04_Experiments/` | Prototypes, hacks, half-ideas |
| `05_Learning/` | Tutorials, courses, self-study notes |
| `06_Operations/` | Build SOPs, deployment routines |
| `07_Ideas/` | Project backlog, features-to-add |
| `08_Publishing/` | Blog posts, demos, shared work |

---

## Preset: `personal`

**For:** personal knowledge base, journaling, reading, life admin

**Signals:** journal entries, reading lists, personal projects, no client/course/paper folders

**Folders to create:**

| Folder | Purpose |
|---|---|
| `01_Identity/` | About, goals, values |
| `02_People/` | Relationships, contacts |
| `03_Projects/` | Personal projects, goals in motion |
| `05_Journal/` | Reflections, reviews |
| `06_Operations/` | Routines, habits, SOPs |
| `07_Ideas/` | Thoughts, hunches, questions |
| `08_Reading/` | Books, articles, notes |

---

## Preset: `custom`

If the user picks `custom`, ask them to describe what kind of content they'll hold. Design a 5-8 folder scheme using numbered 01_ through 08_ naming. Present it, let them edit, then create.

Example interactions:

> User: "I want to track my fitness training, nutrition, and sleep."
>
> Wizard proposal:
> ```
> 01_Identity/     Your goals, measurements
> 02_Training/     Programs, sessions, progress
> 03_Nutrition/    Meal plans, recipes, tracking
> 04_Sleep/        Sleep logs, routines
> 06_Operations/   Routines, check-ins
> 07_Ideas/        Things to try
> ```

---

## Blending presets

If intake matches two presets strongly (e.g., PhD student who also freelances), blend them — merge shared folders, add distinctive ones from both, stay under ~9 numbered folders total.

---

## Fallback (user rejects scheme)

Minimal generic scheme:
```
01_Work/
02_Projects/
03_Notes/
04_Ideas/
06_Operations/
```
Safe for any use case, user can expand later via the Vault Operator.

---

## Creating a new preset

Adding a preset for a new use case? Include:

1. Name + one-line description
2. Target user
3. Signals in intake that trigger it
4. Folder scheme (5-8 folders, 00-09 numbering)
5. Rationale for any distinctive folders

Submit via PR — see `CONTRIBUTING.md`.
