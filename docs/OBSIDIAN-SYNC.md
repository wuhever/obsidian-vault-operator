# Obsidian Sync — Setup Across Devices

Optional but recommended. Obsidian Sync keeps your vault synced across laptop, desktop, phone, tablet.

---

## Why Obsidian Sync (vs. Git / Dropbox / iCloud)

- **Handles `.base` and `.canvas` files correctly** (most alternatives don't)
- **Version history** — up to 12 months of snapshots per file on Plus plan
- **End-to-end encrypted** — optional passphrase
- **Works on mobile** natively (iOS, Android)
- **Doesn't sync agent infrastructure** (skills, `.agents/`, `.claude/`) because `.obsidianignore` excludes them

Alternatives like Git work fine for text-only vaults but break on PDFs, images, and Obsidian's database/canvas files. Dropbox and iCloud can corrupt plugin state.

---

## Cost

As of 2026: **Obsidian Sync Plus is $5/month** or $4/month billed annually. Standard plan is cheaper but has size limits that matter for PDF-heavy vaults.

Check [obsidian.md/sync](https://obsidian.md/sync) for current pricing.

---

## Setup steps

### On your first device

1. Open your vault in Obsidian
2. Settings → Core plugins → enable **Sync**
3. Settings → Sync → **Sign up / Log in** (Obsidian account)
4. **Choose a remote vault** → Create new
5. Name it (e.g., `my-vault-remote`)
6. **Pick region** closest to you (US, EU, Asia)
7. **Set encryption password** — write it down, Obsidian can't recover it
8. **Connect** → initial upload starts (can take a few minutes for large vaults)

### On your second+ device

1. Open Obsidian on the new device
2. **Create new vault** → give it any local name
3. Settings → Core plugins → enable **Sync**
4. Settings → Sync → Log in with same Obsidian account
5. **Choose remote vault** → select the one you created
6. Enter your encryption password
7. **Connect** → initial download starts

---

## What syncs and what doesn't

### Syncs (via Obsidian Sync)
- All `.md` files
- `.base` and `.canvas` files
- PDFs, images, attachments in the vault
- `_Templates/` folder
- `.obsidian/` settings (optional — Sync toggles this per type)

### Does NOT sync (excluded by `.obsidianignore`)
- `.agents/`, `.claude/`, `skills/` — machine-specific, each user installs skills locally
- `_intake-backup/` — gitignored
- OS files (`.DS_Store`, `Thumbs.db`)
- `.env` files

---

## Conflict handling

- **Markdown files:** Obsidian Sync auto-merges using diff-match-patch. Occasionally produces duplicate text — review after merges.
- **`.base` / `.canvas` files:** Last-write-wins. **Do not edit from two devices simultaneously.**
- **Settings (`.obsidian/*.json`):** Merged key-by-key. May need an Obsidian restart after first sync on a new device.

If you see a file named `*sync-conflict*` or `*Conflicted copy*`, compare both versions, keep the correct one, delete the conflict copy.

---

## Version history & recovery

Plus plan keeps **12 months** of file versions.

- **Restore a file:** right-click in Obsidian → Open version history → pick version → Restore
- **Restore a deleted file:** Settings → Sync → Deleted files → find file → Restore

Sync is **not a backup** — deletions propagate. If a file is deleted and version history expires, it's gone. For real backups, also use git or a separate backup service.

---

## The `vault-operator/` side

The `vault-operator/` directory is **separate from the vault** — it lives outside the Obsidian vault and **is not synced by Obsidian Sync.**

Options for syncing it across devices:
1. **Git** — commit it to a private repo (recommended)
2. **Manual copy** — just copy the folder across devices
3. **Don't sync it** — use one main device for operator work

Most people only run the operator from one machine, so not syncing it is fine.

---

## Mobile

Obsidian mobile (iOS/Android) reads the synced vault just like desktop. You can read, edit, and create notes on the go.

The setup wizard and operator skills are desktop-only — mobile is for reading and light editing.

---

## Troubleshooting

- **"Connection failed"** — check your Obsidian account, firewall, or try a different region
- **Slow initial sync** — large vaults (GBs of PDFs) can take 10-30 min first time
- **Missing files on mobile** — mobile has download-on-demand; tap a file to pull it
