# Setup Wizard — Master Prompt

> **You are executing the setup wizard for a fresh clone of the `obsidian-vault-operator` template.** Read this entire file before acting. Follow the 5 phases in order. Do not skip phases.

Your job: turn a minimal template scaffold into a personalized Obsidian vault + operator workspace designed around THIS specific user's needs. The scaffold ships with only universal essentials (Inbox, Reference, Templates, Owner-Space). You CREATE the topical folders based on the user's vault type and optional intake content.

---

## Phase 1 — Orient

Read these files **before asking any questions**:

1. This file (`setup/SETUP-PROMPT.md`)
2. `setup/placeholders.md` — canonical list of `{{TOKENS}}`
3. `setup/scheme-presets.md` — preset schemes (student, researcher, business, hobbyist-builder, personal) you'll create folders from
4. `setup/intake-routing-rules.md` — heuristics for routing files
5. `setup/setup-log-template.md` — format for the final logs

Then scan the repo:
- List `/_intake/` contents (use `Glob` or `ls`)
- If intake has files beyond its own README, read a few small `.md` files to infer content themes
- Note: if `/_intake/` contains only its own `README.md`, mark it as **empty** and skip intake analysis

---

## Phase 2 — Interview

Ask the user these questions. Don't proceed until you have all answers.

### Q1 — Rename the vault directory?

> "The vault folder is currently called `vault/`. Would you like to rename it to something else (like `my-vault/`, `phd-vault/`, `notes/`)? Just press Enter to keep `vault/`."

- Capture as `{{VAULT_DIR}}` (default: `vault`)
- Must be filesystem-safe (no spaces, no special chars, kebab-case recommended)

### Q2 — Owner name

> "What name should appear as the owner of this vault?"

- Capture as `{{OWNER_NAME}}` (e.g., "Sarah", "Dad", "Ali")
- Derive `{{OWNER_SLUG}}` = lowercased, hyphenated (e.g., "Sarah Smith" → "sarah-smith")

### Q3 — Vault name / slug

> "What's the name/slug for this vault? (e.g., sarah-phd-vault, dad-ai-vault)"

- Capture as `{{VAULT_NAME}}` (kebab-case, no spaces)

### Q4 — Vault purpose

> "What is this vault for, in one sentence? (e.g., 'PhD research on marine biology', 'Learning web development', 'Running my consulting business')"

- Capture as `{{VAULT_PURPOSE}}`
- Derive `{{ORG_OR_TOPIC}}` = short phrase for "Relevance to ___" context (e.g., "your research", "your projects", "your work")

### Q5 — Vault type

> "What type of vault is this? Pick the closest match:
>   1) student (courses, lectures, assignments, study notes)
>   2) researcher (papers, experiments, thesis, grants)
>   3) business (clients, proposals, SOPs, operations)
>   4) hobbyist-builder (projects, tools, learning, experiments)
>   5) personal (journal, reading, ideas, life admin)
>   6) custom (I'll describe it and you design it)"

- Capture as `{{VAULT_TYPE}}` (one of: `student`, `researcher`, `business`, `hobbyist-builder`, `personal`, `custom`)
- If **custom**: ask follow-up — "Describe what kind of content this vault will hold. Give me a few categories and I'll design a scheme."

If `/_intake/` has content: still ask this, but note intake signals for cross-checking. You can tell the user "Your intake looks like a researcher vault — confirm?" and let them override.

### Q6 — Vault path on disk

> "Where will this repo live on your computer? (full absolute path)"

- Capture as repo root path
- Derive `{{VAULT_PATH}}` = repo_root + "/" + `{{VAULT_DIR}}`
- Derive `{{VAULT_OPERATOR_PATH}}` = repo_root + "/vault-operator"

### Q7 — Install demo content?

> "Should I install demo content so you can see the system in action? It's a fictional AcmeCorp entity + sample project + sample idea (3 files total). You can delete them later. [y/N]"

- If yes: during Phase 4, copy files from `examples/demo-content/` into appropriate numbered folders the wizard creates

Store all 7 answers. Confirm back to the user before proceeding.

---

## Phase 3 — Scheme Design

### Step 3a — Pick the base scheme

From `setup/scheme-presets.md`, select the preset matching `{{VAULT_TYPE}}`:
- `student` → student preset
- `researcher` → researcher preset
- `business` → business preset
- `hobbyist-builder` → hobbyist-builder preset
- `personal` → personal preset
- `custom` → design a scheme from the user's description

### Step 3b — Refine with intake (if intake has files)

If `/_intake/` has content:
1. Analyze file extensions, filename patterns, folder structure, sample content
2. Adjust the preset scheme if intake reveals specific needs:
   - 40 PDFs with year-stamped names → ensure `05_Papers/` or similar exists
   - 6 course folders → ensure `04_Courses/` or similar exists
   - Distinctive content types → propose a new numbered folder
3. Present a file-routing plan showing which file goes to which folder

### Step 3c — Present the plan

Show the user:

```
Your scheme ({{VAULT_TYPE}} preset):

  00_Inbox/          (universal)
  01_Identity/       (your bio, goals)
  02_Courses/        (6 courses detected)
  03_Projects/       (assignments, term papers)
  04_Study-Notes/    (flashcards, summaries)
  05_Resources/      (textbooks, cheat sheets)
  06_Operations/     (study routines, SOPs)
  07_Ideas/          (thoughts, side projects)
  09_Reference/      (universal — read-only)

File routing (if intake has files):
  _intake/cv.md                       → 01_Identity/About/cv.md
  _intake/courses/bio-501/            → 02_Courses/bio-501/
  _intake/papers/smith-2024.pdf       → 05_Resources/smith-2024.pdf
  ... (show 8-12 example rows if many)

Keep / Edit / Reject? [K/E/R]
```

### Step 3d — Handle response

- **Keep:** proceed to Phase 4
- **Edit:** ask "what would you change?", revise, re-show, ask again
- **Reject:** fall back to a minimal generic scheme (just `01_Work/`, `02_Projects/`, `03_Notes/`, `04_Ideas/`) and still route files

---

## Phase 4 — Execute

Run these steps in order. Keep notes of every action for Phase 5 logging.

### 4a — Rename the vault directory (if user renamed it)

If `{{VAULT_DIR}}` is not `vault`:
```bash
mv vault {{VAULT_DIR}}
```

### 4b — Create scheme folders

For each folder in the approved scheme, create it inside `{{VAULT_DIR}}/`:
```bash
mkdir -p "{{VAULT_DIR}}/01_Identity"
mkdir -p "{{VAULT_DIR}}/01_Identity/About"
mkdir -p "{{VAULT_DIR}}/02_Courses"
# ... etc
```

If the scheme includes an entity template pattern (business, researcher), also create:
```bash
mkdir -p "{{VAULT_DIR}}/02_Work/_Entity-Template/Research"
mkdir -p "{{VAULT_DIR}}/02_Work/_Entity-Template/Documents"
mkdir -p "{{VAULT_DIR}}/02_Work/_Entity-Template/Workflow"
```

Create an `_Entity-Template/README.md` inside from the template in the repo (or write a minimal one).

### 4c — Replace placeholders

Find-and-replace every `{{TOKEN}}` across these files:
- `{{VAULT_DIR}}/AGENTS.md`
- `{{VAULT_DIR}}/CLAUDE.md`
- `{{VAULT_DIR}}/README.md`
- `{{VAULT_DIR}}/Owner-Space/_README.md`
- `{{VAULT_DIR}}/_Templates/research-note.md`
- `vault-operator/AGENTS.md`
- `vault-operator/CLAUDE.md`
- `vault-operator/operator-prompt.md`

Placeholders to replace: see `setup/placeholders.md`.

### 4d — Generate and insert {{SCHEME_TABLE}}

Build a markdown table of the created scheme:

```markdown
| Folder | Purpose |
|---|---|
| `01_Identity/` | Your bio, goals, positioning |
| `02_Courses/` | One folder per course |
| `03_Projects/` | Assignments, term papers, capstones |
| `04_Study-Notes/` | Concept notes, flashcards, summaries |
| `05_Resources/` | Textbooks, cheat sheets |
| `06_Operations/` | Study routines, exam prep SOPs |
| `07_Ideas/` | Career ideas, side projects |
```

Insert this table wherever `{{SCHEME_TABLE}}` appears:
- `{{VAULT_DIR}}/AGENTS.md`
- `{{VAULT_DIR}}/README.md`
- `vault-operator/operator-prompt.md`

### 4e — Rename Owner-Space

```bash
mv "{{VAULT_DIR}}/Owner-Space" "{{VAULT_DIR}}/{{OWNER_SLUG}}-space"
```

### 4f — Install demo content (if user said yes)

Copy from `examples/demo-content/` into appropriate folders:
- AcmeCorp entity → the entity-holding folder (e.g., `02_Work/` or `02_Courses/` or wherever fits)
- Sample project → the projects folder
- Sample idea → the ideas folder

If the scheme doesn't naturally accommodate demo content (e.g., pure research vault has no "entity" concept), skip incompatible files and note it.

If user said **no** to demo content: do nothing; examples/ stays in the repo (user can delete later).

### 4g — Route intake files (if intake has content)

For each file in `/_intake/`:
1. Determine destination per the approved routing plan
2. Create destination folder if it doesn't exist
3. If `.md` file lacks frontmatter, add minimal:
   ```yaml
   ---
   type: note
   status: active
   created: YYYY-MM-DD
   ---
   ```
4. Move the file (don't copy)

### 4h — Archive intake

```bash
mv _intake _intake-backup
```

Verify `_intake-backup/` is in `.gitignore` (it is).

### 4i — Self-checks

Before Phase 5, verify:
- [ ] No `{{` tokens remain in `{{VAULT_DIR}}/`, `vault-operator/` (grep check)
- [ ] `Owner-Space/` renamed
- [ ] All scheme folders exist
- [ ] `{{SCHEME_TABLE}}` was replaced everywhere
- [ ] If intake processed, files moved + `/_intake-backup/` exists

---

## Phase 5 — Log + Handoff

### 5a — Get UTC timestamp

```bash
date -u +"%Y-%m-%d-%H%M%S"
```

### 5b — Write setup change log

Create `vault-operator/changes/{TIMESTAMP}-initial-setup.md` per `setup/setup-log-template.md`. Include:
- Placeholder replacements
- Folders created (full scheme list)
- Vault directory rename (if done)
- Owner-Space rename
- Demo content installed (which files, where)
- Intake files moved (source → dest)
- Frontmatter added to which files

### 5c — Write setup session log

Create `vault-operator/context/{TIMESTAMP}-initial-setup.md` with:
- All 7 interview answers
- Vault type chosen
- Scheme decision (preset / custom / rejected-fallback)
- Issues encountered
- Open items for the user

### 5d — Print handoff

```
✓ Setup complete.

Vault: {{VAULT_PATH}}
Operator: {{VAULT_OPERATOR_PATH}}

Next steps:
  1. Open {{VAULT_DIR}}/ in Obsidian (File → Open folder as vault)
  2. Read {{VAULT_DIR}}/README.md for day-to-day usage
  3. Delete /_intake-backup/ when you're confident nothing was lost
  4. Set up Obsidian Sync (optional) → docs/OBSIDIAN-SYNC.md
  5. Install Obsidian skills: npx skills add https://github.com/kepano/obsidian-skills.git --yes

Session log: vault-operator/context/{TIMESTAMP}-initial-setup.md
Change log:  vault-operator/changes/{TIMESTAMP}-initial-setup.md
```

---

## Safety rules (never violate)

1. **Never delete `/_intake/`** — always rename to `/_intake-backup/`.
2. **Never skip the interview.** All 7 questions are mandatory.
3. **Never auto-approve the scheme.** Always show plan, wait for K/E/R.
4. **Never modify files outside this repo.**
5. **If anything is ambiguous, ask.** Don't guess.
6. **Write logs before printing handoff.**
