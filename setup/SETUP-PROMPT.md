# Setup Wizard — Master Prompt

> **You are executing the setup wizard for a fresh clone of the `obsidian-vault-operator` template.** Read this entire file before acting. Follow the 5 phases in order. Do not skip phases.

Your job: turn a generic template into a personalized Obsidian vault + operator workspace for this specific user, optionally routing their existing files from `/_intake/` into a scheme designed around their content.

---

## Phase 1 — Orient

Read these files **before asking any questions**:

1. This file (`setup/SETUP-PROMPT.md`) — you're reading it now
2. `setup/placeholders.md` — canonical list of `{{TOKENS}}` you'll replace
3. `setup/scheme-presets.md` — reference schemes (business, researcher, student, personal) to match against intake content
4. `setup/intake-routing-rules.md` — heuristics for routing files by extension and content
5. `setup/setup-log-template.md` — format for the final setup log you'll write

Then scan `/_intake/` to see what the user dropped in:
- List files and folders (use `Glob` or `ls`)
- Read a few small `.md` files to infer content themes
- Note file extensions and counts (how many PDFs, how many markdown files, any nested folders)

If `/_intake/` contains only its own `README.md` and nothing else, mark it as **empty** and skip Phase 3.

---

## Phase 2 — Interview (ask the user 5 questions)

Ask these **one by one** (or batched if your IDE supports it). Do not proceed until you have all 5 answers.

### Questions

1. **Owner name** — "What name should appear as the owner of this vault?" (e.g., "Sarah", "Dad", "Ali")
   - Capture as `{{OWNER_NAME}}`
   - Derive `{{OWNER_SLUG}}` = lowercased, hyphenated (e.g., "Sarah" → "sarah")

2. **Vault name** — "What's the name/slug for this vault?" (e.g., "sarah-phd-vault", "dad-ai-vault")
   - Capture as `{{VAULT_NAME}}`
   - Should be kebab-case, no spaces

3. **Vault purpose** — "What is this vault for, in one sentence?" (e.g., "PhD research on marine biology", "AI engineering notes and project work")
   - Capture as `{{VAULT_PURPOSE}}`
   - Derive `{{ORG_OR_TOPIC}}` = a short version suitable for "Relevance to ___" (e.g., "your research", "your work", "this project")

4. **Vault path on disk** — "Where will this repo live on your computer?" (full path, e.g., `C:\Users\sarah\Documents\sarah-phd-vault` or `/home/sarah/sarah-phd-vault`)
   - Capture as `{{VAULT_PATH}}`
   - Derive `{{VAULT_OPERATOR_PATH}}` = same path + `/vault-operator` (the operator lives inside the repo, not a sibling)
   - Actually, `{{VAULT_PATH}}` = repo path + `/vault`, `{{VAULT_OPERATOR_PATH}}` = repo path + `/vault-operator`

5. **Keep demo content?** — "Should I keep the example/demo files (fictional AcmeCorp client, sample project, sample idea) so you can see the system in action? [y/N]"
   - If no: delete `_EXAMPLE-*` files/folders during Phase 4
   - If yes: keep them — user can delete later

Store all answers. Confirm back to the user before moving on.

---

## Phase 3 — Intake Analysis (skip if `/_intake/` is empty)

Only runs if `/_intake/` contains user files beyond its README.

### Step 3a — Analyze content

Identify themes by looking at:
- File extensions (`.pdf`, `.md`, `.docx`, `.png`, etc.)
- Filename patterns (e.g., "paper-", "lecture-", "meeting-", "proposal-")
- Existing folder structure in intake (e.g., `courses/`, `research/`, `clients/`)
- Sample content from readable `.md` files (read first 20 lines of 3-5 of them)

### Step 3b — Match to a preset

Compare against the 4 presets in `setup/scheme-presets.md`:
- **business** — signals: client folders, proposals, SOPs, retainer docs
- **researcher** — signals: PDF papers, experiments, thesis/chapters, references with years (e.g., "smith-2024.pdf")
- **student** — signals: course folders, lecture notes, assignments, textbook PDFs
- **personal** — signals: journal entries, reading lists, ideas, personal projects

If one preset matches strongly (>60% of content fits), use it as the base.
If multiple match, blend them (e.g., "researcher + student" for a PhD student who also TAs).
If none match, use the **default generic scheme** (`01_Identity`, `02_Work`, `03_Projects`, `05_Strategy`, `06_Operations`, `07_Ideas`, `08_Publishing`, `09_Reference`).

### Step 3c — Propose the scheme + routing

Show the user a scheme proposal like:

```
Based on your intake (40 PDFs, 6 course folders, 1 CV, 12 random notes),
I'm proposing the "researcher" scheme:

Folder scheme:
  00_Inbox/          (ongoing drops)
  01_Identity/       (your CV, bio, goals)
  02_Collaborators/  (advisor, committee, lab mates)
  03_Projects/       (thesis chapters, paper drafts)
  04_Courses/        (6 courses detected — new folder)
  05_Papers/         (40 PDFs detected — renamed from Strategy)
  06_Operations/     (your SOPs, workflows)
  07_Ideas/          (brainstorms)
  09_Reference/      (read-only archive)

File routing (42 files):
  _intake/cv.md                       → vault/01_Identity/About/cv.md
  _intake/courses/bio-501/            → vault/04_Courses/bio-501/
  _intake/papers/smith-2024.pdf       → vault/05_Papers/smith-2024.pdf
  _intake/notes/meeting-advisor.md    → vault/02_Collaborators/meeting-advisor.md
  ... (show 8-12 example rows, then "... and N more")

Keep / Edit / Reject? [K/E/R]
```

### Step 3d — Handle the response

- **Keep:** proceed to Phase 4 with this plan
- **Edit:** ask "what would you change?" Revise plan, re-show, ask again
- **Reject:** fall back to the default scheme, still route files using `intake-routing-rules.md` heuristics

---

## Phase 4 — Execute

Run these steps in order. Log every action — you'll write the full log in Phase 5, but keep notes as you go.

### 4a — Rename folders per approved scheme (if non-default)

Use the scheme from Phase 3. If the default scheme was kept, skip this step.

Example renames:
- `vault/02_Work/` → `vault/02_Collaborators/`
- `vault/05_Strategy/` → `vault/05_Papers/`
- Create new numbered folders if scheme introduces any (e.g., `04_Courses/`)
- Delete unused folders if scheme drops any (only if they're empty)

### 4b — Replace placeholders

Find-and-replace every `{{TOKEN}}` across `vault/`, `vault-operator/`, `setup/`, and repo root files. See `setup/placeholders.md` for the canonical list.

Files known to contain placeholders:
- `vault/AGENTS.md`
- `vault/CLAUDE.md`
- `vault/README.md`
- `vault/Owner-Space/_README.md`
- `vault/_Templates/research-note.md`
- `vault-operator/AGENTS.md`
- `vault-operator/CLAUDE.md`
- `vault-operator/operator-prompt.md`

Do a final grep after replacement: `grep -r "{{" vault/ vault-operator/` should return zero matches (except this file, which is fine).

### 4c — Rename Owner-Space

Rename `vault/Owner-Space/` → `vault/{{OWNER_SLUG}}-space/` (e.g., `vault/sarah-space/`).

Update any references to `Owner-Space/` in docs to use the new name.

### 4d — Delete demo content (if user said no)

Remove:
- `vault/02_Work/_EXAMPLE-AcmeCorp/` (or wherever it landed after folder renames)
- `vault/03_Projects/_EXAMPLE-website-redo.md`
- `vault/07_Ideas/_EXAMPLE-idea.md`

### 4e — Route intake files (if `/_intake/` has content)

For each file in `/_intake/`:
1. Determine destination per the approved routing plan
2. Create destination folder if it doesn't exist
3. If the file is `.md` and lacks frontmatter, add minimal frontmatter:
   ```yaml
   ---
   type: note
   status: active
   created: YYYY-MM-DD  # today's date
   ---
   ```
4. Move the file (don't copy — the backup is the whole `/_intake/` folder)

### 4f — Archive intake

Rename `/_intake/` → `/_intake-backup/`. Do NOT delete.

Verify `/_intake-backup/` is in `.gitignore` (it already is).

### 4g — Self-checks

Before Phase 5, verify:
- [ ] No `{{` tokens remain in `vault/`, `vault-operator/`, or `setup/` (outside this file)
- [ ] `vault/Owner-Space/` no longer exists
- [ ] `vault/{{OWNER_SLUG}}-space/` (with actual slug) does exist
- [ ] If intake was processed, all its files have moved to `vault/` and `/_intake-backup/` is their original location
- [ ] All folders listed in the scheme actually exist
- [ ] Demo files deleted per user's choice

---

## Phase 5 — Log + Handoff

### 5a — Get UTC timestamp

Get the current UTC timestamp in format `YYYY-MM-DD-HHMMSS`:
```bash
date -u +"%Y-%m-%d-%H%M%S"
```

### 5b — Write setup change log

Create `vault-operator/changes/{TIMESTAMP}-initial-setup.md` using the format in `setup/setup-log-template.md`. Include:
- All placeholder replacements (list tokens + values)
- Folder renames (from → to)
- Demo content deletion (yes/no)
- Every intake file moved (source path → dest path)
- Frontmatter added to which files

### 5c — Write setup session log

Create `vault-operator/context/{TIMESTAMP}-initial-setup.md` with:
- User's 5 interview answers
- Scheme chosen (preset name or "default")
- Scheme approval decision (kept / edited / rejected)
- Any issues encountered
- Open items for the user (e.g., "install Obsidian Sync", "review `/_intake-backup/` before deleting")

### 5d — Print the handoff message

Tell the user:

```
✓ Setup complete.

Your vault: {{VAULT_PATH}}/vault/
Your operator: {{VAULT_PATH}}/vault-operator/

Next steps:
  1. Open vault/ in Obsidian (File → Open folder as vault)
  2. Read vault/README.md for day-to-day usage
  3. When you're confident nothing was lost, delete /_intake-backup/
  4. Set up Obsidian Sync → see docs/OBSIDIAN-SYNC.md

Session log: vault-operator/context/{TIMESTAMP}-initial-setup.md
Change log:  vault-operator/changes/{TIMESTAMP}-initial-setup.md
```

---

## Safety rules (never violate)

1. **Never delete `/_intake/`** — always rename to `/_intake-backup/`. The user deletes it when ready.
2. **Never skip the interview.** The 5 questions are mandatory. No placeholders can be filled without them.
3. **Never auto-approve the scheme in Phase 3.** Always show the plan and wait for K/E/R.
4. **Never modify files outside this repo.** Stay within the cloned directory.
5. **If anything is ambiguous, ask.** Don't guess. Re-running setup is expensive.
6. **Write logs before printing the handoff.** If logs aren't written, the operator pattern is broken from day one.
