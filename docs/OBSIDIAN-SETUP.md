# Obsidian — App Setup

After the `/setup` wizard runs, you need to install Obsidian itself and configure it to work properly with your new vault. This guide walks through everything.

**Time needed:** ~10 minutes.
**Cost:** $0 (Obsidian is free for personal use).

---

## Step 1 — Install Obsidian

Download from [obsidian.md/download](https://obsidian.md/download). Installers are available for:

- **Windows** — `.exe` installer
- **macOS** — `.dmg`
- **Linux** — AppImage, Snap, or Flatpak
- **iOS / Android** — App Store / Play Store (mobile apps, for later)

Run the installer. No account needed to use Obsidian locally (only needed later if you add Obsidian Sync).

---

## Step 2 — Open your vault

1. Open Obsidian
2. On the first launch, you'll see a vault picker dialog
3. Click **"Open folder as vault"**
4. Navigate to your vault directory (e.g., `C:\Users\sarah\Documents\sarah-school\my-school\`)
5. Click **Open** / **Select Folder**

Obsidian now treats that folder as your vault. The file explorer on the left shows `00_Inbox/`, `_Templates/`, `09_Reference/`, your numbered topical folders, etc.

> [!tip]
> If Obsidian asks "Do you trust the author of this vault?", click **Trust author and enable plugins**. The template doesn't include any plugins by default — this prompt appears because the folder is pre-structured.

---

## Step 3 — Enable core plugins

Obsidian ships with "core plugins" that are disabled by default. You need a few of these on.

**Go to:** Settings (gear icon, bottom-left) → **Core plugins**

Enable these:

| Plugin | Why you need it |
|---|---|
| **Daily notes** | Auto-creates a dated note in `00_Inbox/Daily/` every day |
| **Templates** | Lets you insert `_Templates/` content with one command |
| **Backlinks** | Shows which notes link TO the current note |
| **Outgoing links** | Shows which notes the current note links TO |
| **Graph view** | Visual map of how your notes connect |
| **Bases** | Reads `.base` files (database views over your notes) |
| **Canvas** | Reads `.canvas` files (visual diagrams, mind maps) |
| **File recovery** | Auto-saves snapshots, lets you recover deleted content |
| **Search** | Full-text search across all notes |
| **Tags view** | Browse notes by frontmatter tags |
| **Command palette** | Ctrl/Cmd+P to run any command |

Leave the rest off unless you specifically need them.

---

## Step 4 — Configure Daily Notes

Once **Daily notes** is enabled in core plugins:

**Go to:** Settings → Daily notes

Set these values:

| Setting | Value |
|---|---|
| Date format | `YYYY-MM-DD` |
| New file location | `00_Inbox/Daily` |
| Template file location | `_Templates/daily-note` |
| Open daily note on startup | ✅ (optional, recommended) |

Now, when you press **Ctrl/Cmd + P** → type "daily" → enter, Obsidian creates today's note in `00_Inbox/Daily/2026-04-05.md` using your template.

---

## Step 5 — Configure Templates

**Go to:** Settings → Templates

Set:

| Setting | Value |
|---|---|
| Template folder location | `_Templates` |
| Date format | `YYYY-MM-DD` |
| Time format | `HH:mm` |

Now you can insert any template via **Ctrl/Cmd + P** → "Insert template" → pick one.

**Example workflow:**
1. Create a new note in `07_Ideas/` (or wherever your ideas folder is)
2. `Ctrl/Cmd + P` → "Insert template" → select `idea-note`
3. Obsidian drops the full template structure into your note with today's date

---

## Step 6 — Recommended settings tweaks

**Go to:** Settings → Files and links

| Setting | Recommended value | Why |
|---|---|---|
| Default location for new notes | `00_Inbox` | Any unlabeled new note lands in the inbox |
| New link format | `Shortest path when possible` | Cleaner wikilinks: `[[note-name]]` instead of full paths |
| Use Wikilinks | ✅ On | Matches the template's convention |
| Detect all file extensions | ✅ On | Shows PDFs, images, etc. in the file explorer |
| Confirm file deletion | ✅ On | Safety net |

**Go to:** Settings → Editor

| Setting | Recommended value |
|---|---|
| Readable line length | ✅ On (better for reading) |
| Show inline title | ✅ On |
| Strict line breaks | Off |

**Go to:** Settings → Appearance

- Pick a theme you like. The default is fine.
- Base color scheme: System / Light / Dark (your preference)

---

## Step 7 — Learn the essential keyboard shortcuts

| Shortcut | What it does |
|---|---|
| `Ctrl/Cmd + N` | New note |
| `Ctrl/Cmd + O` | Open/create note by name |
| `Ctrl/Cmd + P` | Command palette (run any command) |
| `Ctrl/Cmd + E` | Toggle edit / preview mode |
| `Ctrl/Cmd + Click` | Follow a wikilink |
| `Ctrl/Cmd + F` | Search within current note |
| `Ctrl/Cmd + Shift + F` | Search across all notes |
| `Ctrl/Cmd + B` | Toggle left sidebar |
| `Ctrl/Cmd + L` | Toggle right sidebar |
| `[[` | Start a wikilink — Obsidian autocompletes from existing notes |
| `#` | Start a tag (inside frontmatter, not inline) |

---

## Step 8 — Verify `.obsidianignore` is working

Your vault should ignore `.claude/`, `.agents/`, `skills/` folders — these hold agent infrastructure and shouldn't appear in Obsidian.

**Check:** in Obsidian's file explorer, you should NOT see any of these folders. If you do, verify `vault/.obsidianignore` exists and contains those entries.

---

## Step 9 — Try it out

Create your first note to verify everything works:

1. Press `Ctrl/Cmd + N` — a new note opens
2. Add some frontmatter at the top:
   ```yaml
   ---
   type: note
   status: active
   created: 2026-04-05
   ---
   ```
3. Write something. Add a wikilink: `[[00_Inbox/_README]]` — should autocomplete.
4. `Ctrl/Cmd + E` to preview. The wikilink should render as a clickable link.
5. Open the graph view (`Ctrl/Cmd + P` → "graph") — you should see your note connected to others.

---

## Optional — Community plugins

Obsidian has a huge community plugin ecosystem. These are worth considering **after** you're comfortable with the basics:

| Plugin | What it does |
|---|---|
| **Dataview** | Query your vault like a database (advanced) |
| **Calendar** | Visual calendar that navigates daily notes |
| **Templater** | More powerful templates than core (JavaScript, variables) |
| **Advanced Tables** | Better markdown table editing |
| **Natural Language Dates** | Type `@today` or `@next friday` → inserts actual date |
| **Excalidraw** | Draw diagrams inside Obsidian |

**To install:** Settings → Community plugins → **Turn on community plugins** → Browse → search and install.

Don't install these on day one. Use the vault for a week, notice what friction you have, then add plugins to solve specific problems.

---

## Optional — Sync across devices

If you want your vault on phone + laptop + desktop, see [OBSIDIAN-SYNC.md](OBSIDIAN-SYNC.md).

**TL;DR:** Obsidian Sync is $5/month, handles PDFs + images + `.base`/`.canvas` files correctly, has 12 months of version history, and doesn't corrupt plugin state (unlike Dropbox/iCloud).

---

## Troubleshooting

**"I don't see my folders in Obsidian."**
Check that you opened the correct folder. If you opened the repo root (`sarah-school/`) instead of the vault subfolder (`sarah-school/my-school/`), close and reopen with the vault subfolder.

**"Templates aren't showing up."**
Settings → Templates → verify template folder is set to `_Templates` (no trailing slash).

**"Daily note creates in the wrong place."**
Settings → Daily notes → verify "New file location" is `00_Inbox/Daily`.

**"Wikilinks don't autocomplete."**
Press `[[` in edit mode (not preview). Obsidian indexes files on open — wait 5 seconds after opening the vault if the index is still building.

**"Bases / Canvas files won't open."**
Enable the **Bases** and **Canvas** core plugins in Settings → Core plugins.

---

## Next steps

- Read [SETUP.md](SETUP.md) if you haven't run the wizard yet
- Read [OBSIDIAN-SYNC.md](OBSIDIAN-SYNC.md) to sync across devices
- Read [CUSTOMIZATION.md](CUSTOMIZATION.md) for post-setup tweaks
- Start using your vault — the best way to learn Obsidian is to write in it
