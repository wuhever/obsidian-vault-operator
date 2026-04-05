# Customization — Post-Setup Tweaks

After `/setup` runs, the vault is personalized and ready. This guide covers common customizations you might want over time.

---

## Adding a new top-level folder

Decide the number (use next available, e.g., `04_` if unused) and add it to:

1. Create the folder in `vault/`
2. Update the folder table in `vault/AGENTS.md` (navigation rules)
3. Update the folder table in `vault/README.md`
4. Update the folder list in `vault-operator/operator-prompt.md`
5. Log the change: `vault-operator/changes/YYYY-MM-DD-HHMMSS-added-folder-X.md`

If you use an agent, just tell it: *"Add a new top-level folder called 04_Courses for tracking class materials. Update the docs and log the change."*

---

## Adding a new frontmatter `type`

The canonical types are hardcoded in several places for consistency. If you need a new one:

1. Edit the type list in `vault/AGENTS.md`
2. Edit the type list in `vault/CLAUDE.md`
3. Edit the type list in `vault-operator/operator-prompt.md`
4. Add a matching template in `vault/_Templates/` if the new type needs one
5. Log the change

**Alternative:** instead of adding a type, use `type: note` with a `subtype: your-thing` property. No doc changes needed.

---

## Adding a new template

1. Create `vault/_Templates/your-template.md` with YAML frontmatter and placeholder sections
2. Follow the pattern of existing templates (see `_Templates/research-note.md`, `_Templates/sop.md`)
3. Add it to the template list in `vault/AGENTS.md` and `vault/CLAUDE.md`
4. Log the change

---

## Editing the operator's behavior

The operator's rules live in `vault-operator/operator-prompt.md`. Common edits:

- Tighten or loosen what it can modify
- Add new operational patterns (e.g., "weekly review SOP")
- Add/remove read-only folders
- Change logging conventions

Whenever you edit `operator-prompt.md`, write a change log explaining what changed and why — future sessions need that context.

---

## Renaming folders

Obsidian wikilinks resolve by filename, not path, so **moving files between folders** doesn't break links. But **renaming folders** requires updating:

1. The folder itself
2. Any hardcoded path references in `AGENTS.md`, `CLAUDE.md`, `operator-prompt.md`, `README.md`
3. Base files (`.base`) that filter by folder path

Use the operator to do this safely — it'll scan for references before renaming.

---

## Adding personal / private spaces (from solo → multi-owner)

v1 of this template ships as solo user (one `Owner-Space/`). To add a second owner:

1. Create a new `{name}-space/` folder with a `_README.md`
2. Add a "Personal Spaces" section to `vault/AGENTS.md` with access rules
3. Update `vault-operator/operator-prompt.md` under "What you CANNOT do" to list both spaces
4. Update the `.obsidianignore` if you want either space excluded from sync

This is a manual upgrade for now. A proper multi-owner preset is on [the roadmap](ROADMAP.md).

---

## Changing the default `Daily/` location

If you prefer daily notes in a different folder:

1. Move `vault/00_Inbox/Daily/` to new location
2. Obsidian → Settings → Daily notes → New file location → update path
3. Update `vault/_Templates/daily-note.md` if it references paths

---

## Removing the demo content later

If you kept `_EXAMPLE-*` files during setup and now want them gone:

```bash
rm -rf vault/02_Work/_EXAMPLE-AcmeCorp
rm vault/03_Projects/_EXAMPLE-*.md
rm vault/07_Ideas/_EXAMPLE-*.md
```

Then log the change in `vault-operator/changes/`.

---

## Updating skills

Obsidian skills (obsidian-markdown, obsidian-bases, json-canvas, obsidian-cli, defuddle) install per-machine:

```bash
npx skills add https://github.com/kepano/obsidian-skills.git --yes
```

Re-run periodically to get updates.

The `vault-operator-audit` skill is bundled in this repo at `vault-operator/skills/vault-operator-audit/` and updates when you `git pull`.

---

## Importing another vault later

You can re-use `/_intake/` anytime:

1. Recreate `/_intake/` folder
2. Drop new files in
3. Tell the operator: *"There are new files in /_intake/, triage them into the existing scheme"*

Unlike the initial setup, this uses your existing folder structure — the operator just routes the new files.
