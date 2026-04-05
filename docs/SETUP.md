# Setup — Detailed Walkthrough

Full guide to running the `/setup` wizard.

---

## Prerequisites

- Git installed
- An AI coding IDE with an agent: Claude Code, Cursor, Copilot CLI, Antigravity, or similar
- Obsidian installed (free) if you want to actually use the vault after setup

No other dependencies. No shell scripts to run. No npm/pip installs.

---

## Step 1 — Clone

```bash
git clone https://github.com/wuhever/obsidian-vault-operator.git my-vault
cd my-vault
```

Rename `my-vault` to whatever you want — this is the repo directory, not your vault name. The wizard will ask for your vault name separately.

---

## Step 2 — Drop files into `/_intake/` (optional)

If you have existing files — notes, PDFs, course materials, research papers, anything — copy them into `/_intake/`. The agent will analyze them and design a folder scheme around what you've got.

You can drop:
- Individual files: `cv.md`, `paper-draft.pdf`
- Whole folders: a `research/` folder, a `courses/` folder with subfolders

If you're starting completely fresh, leave `/_intake/` empty. The wizard will use the default scheme.

---

## Step 3 — Open in your IDE

Open the repo folder in your AI coding IDE:

- **Claude Code:** `cd my-vault && claude`
- **Cursor:** File → Open Folder → `my-vault`
- **Copilot CLI:** `cd my-vault && gh copilot`
- **Antigravity:** Open project → `my-vault`

---

## Step 4 — Trigger the wizard

Tell the agent:

```
Run the setup wizard in setup/SETUP-PROMPT.md
```

The agent reads the prompt and takes over.

---

## Step 5 — Answer the interview questions

The agent asks 7 short questions:

| # | Question | Example answer |
|---|---|---|
| 1 | Rename the `vault/` folder? | `phd-vault` (or Enter to keep `vault`) |
| 2 | Owner name | `Sarah` |
| 3 | Vault name / slug | `sarah-phd-vault` |
| 4 | Vault purpose | `PhD research on marine biology` |
| 5 | Vault type | `researcher` (or student/business/hobbyist-builder/personal/custom) |
| 6 | Vault path on disk | `C:\Users\sarah\Documents\sarah-phd-vault` |
| 7 | Install demo content? | `n` (or `y` to see the system in action) |

---

## Step 6 — Review the proposed scheme (if intake has files)

The agent shows you a table like:

```
Proposed folder scheme (researcher):
  00_Inbox/
  01_Identity/      (your CV, bio)
  02_Collaborators/ (advisor, committee, lab mates)
  03_Projects/      (thesis chapters, paper drafts)
  04_Courses/       (6 courses detected in intake)
  05_Papers/        (40 PDFs detected)
  06_Operations/
  07_Ideas/
  09_Reference/

Proposed file routing (42 files):
  intake/papers/smith-2024.pdf        → vault/05_Papers/smith-2024.pdf
  intake/courses/bio-501/notes.md     → vault/04_Courses/bio-501/notes.md
  intake/cv.md                        → vault/01_Identity/About/cv.md
  ...

Keep / Edit / Reject? [K/E/R]
```

- **Keep (K)** — agent executes the plan as shown
- **Edit (E)** — you tell the agent what to change ("move the course folder into 03_Projects instead")
- **Reject (R)** — agent falls back to the default generic scheme

---

## Step 7 — Agent executes

The agent will:

1. Rename the `vault/` directory if you chose a new name
2. Create the topical folders (01-08) based on your vault type
3. Replace all `{{PLACEHOLDER}}` tokens across the repo
4. Insert the generated scheme table into AGENTS.md, CLAUDE.md, README.md
5. Rename `Owner-Space/` → `sarah-space/` (or whatever your owner slug is)
6. Install demo content into the created folders (if you said yes)
7. Move files from `/_intake/` to their destinations, adding frontmatter
8. Rename `/_intake/` → `/_intake-backup/`
9. Write setup logs to `vault-operator/context/` and `vault-operator/changes/`

---

## Step 8 — Verify and open Obsidian

1. Check `vault-operator/changes/*.md` — the newest file lists everything the agent did
2. **Install Obsidian and configure it** — see [OBSIDIAN-SETUP.md](OBSIDIAN-SETUP.md) for the ~10-minute one-time app setup (core plugins, Daily Notes, Templates)
3. Open Obsidian → Open folder as vault → pick your `vault/` directory
4. Read `vault/README.md`
5. Start using it

When you're confident nothing was lost, delete `/_intake-backup/`.

---

## Troubleshooting

**Wizard left placeholders unreplaced.** Run `grep -r "{{" vault/ vault-operator/` to find them. Either fix manually or re-run the wizard (see re-run section below).

**Files got routed to the wrong folder.** The `vault-operator/changes/` log shows what moved where. You can move files manually in Obsidian — wikilinks update automatically.

**Agent crashes or loses context mid-setup.** Safe to restart: tell the new agent "continue the setup wizard, read vault-operator/changes/ for what's already done."

**Re-running `/setup`.** The wizard detects if placeholders are already replaced. To fully reset, `git reset --hard origin/main` (⚠️ loses all your intake work) then re-clone.

---

## Next steps

- Install & configure Obsidian → [OBSIDIAN-SETUP.md](OBSIDIAN-SETUP.md)
- Set up Obsidian Sync across devices → [OBSIDIAN-SYNC.md](OBSIDIAN-SYNC.md)
- Customize folders, add SOPs, tweak operator prompt → [CUSTOMIZATION.md](CUSTOMIZATION.md)
