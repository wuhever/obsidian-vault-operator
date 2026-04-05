# obsidian-vault-operator

> An open-source template for pairing an Obsidian vault with an AI operator workspace. Clone, drop your existing files into `/_intake/`, run `/setup`, and get a personalized, agent-ready knowledge system.

Built for solo users — students, researchers, engineers, builders — who want a structured Obsidian vault plus an AI "operator" that keeps it organized over time.

---

## What this is

Two directories that work together:

- **`vault/`** — the Obsidian vault. Numbered folders (`00_Inbox`, `01_Identity`, `02_Work`, ...), templates, frontmatter conventions, and agent rules. Open this in Obsidian.
- **`vault-operator/`** — an admin workspace that sits **outside** the vault. It holds your operator prompt, session logs, change logs, and a reusable audit skill. Open this in Claude Code / Cursor / Copilot CLI / Antigravity when you want an agent to audit, triage, or reorganize your vault.

The operator never guesses — it reads the prompt, checks the logs, proposes changes, waits for your approval, executes, and logs what it did. Every session is traceable.

---

## Quickstart (3 steps)

### 1. Clone and add your files

```bash
git clone https://github.com/wuhever/obsidian-vault-operator.git my-vault
cd my-vault
```

**If you have existing files** (markdown notes, PDFs, research, course materials, anything): drop them into `/_intake/`. The agent will analyze them during setup and design a folder scheme around what you've got.

**If you're starting fresh**, skip this — `/_intake/` can stay empty.

### 2. Run the setup wizard

Open this folder in your AI coding IDE (Claude Code, Cursor, Copilot CLI, Antigravity — any of them works). Tell the agent:

```
Run the setup wizard in setup/SETUP-PROMPT.md
```

The agent will:
1. Ask you 5 quick questions (your name, what this vault is for, its path on disk)
2. If `/_intake/` has files, propose a folder scheme adapted to your content
3. Replace placeholders across all files with your values
4. Move your intake files into the right folders with frontmatter added
5. Back up `/_intake/` to `/_intake-backup/` (delete it yourself when confident)
6. Log everything to `vault-operator/context/` and `vault-operator/changes/`

### 3. Open in Obsidian

Open the `vault/` folder as an Obsidian vault. Read `vault/README.md`. You're ready to go.

---

## Syncing across devices (optional)

This template assumes you'll use **[Obsidian Sync](https://obsidian.md/sync)** to keep your vault synchronized across laptop, desktop, phone. See [docs/OBSIDIAN-SYNC.md](docs/OBSIDIAN-SYNC.md) for the setup steps.

You can also use Git for syncing the vault across machines — but if you have PDFs, images, or `.base`/`.canvas` files, Obsidian Sync handles them much better.

---

## What's inside

```
obsidian-vault-operator/
├── _intake/             Drop your existing files here before /setup
├── vault/               The Obsidian vault (open this in Obsidian)
├── vault-operator/      Admin workspace (open this in your AI IDE)
├── setup/               The setup wizard prompt and config
├── docs/                Guides: setup, sync, customization, IDE compat, roadmap
├── LICENSE              MIT
└── README.md            You are here
```

See [docs/SETUP.md](docs/SETUP.md) for a detailed walkthrough of the wizard, [docs/CUSTOMIZATION.md](docs/CUSTOMIZATION.md) for post-setup tweaks, and [docs/ROADMAP.md](docs/ROADMAP.md) for what's coming next (multi-owner setups, shell-script fallback, preset library).

---

## Who this is for

- **Students** with scattered course notes, research PDFs, and paper drafts
- **Researchers / PhD candidates** with a growing library of papers, experiments, and chapters
- **Engineers & builders** with project notes, SOPs, and ideas spread across folders
- **Solo operators** who want a knowledge base that an AI agent can reason about and keep clean

Not yet supported (on the roadmap): two-person teams, families with shared+personal spaces, AI-only vaults. For now: solo user, v1.

---

## IDE compatibility

The `/setup` wizard is just a markdown prompt. It runs identically in:

- [Claude Code](https://claude.com/claude-code)
- [Cursor](https://cursor.com/)
- [GitHub Copilot CLI](https://docs.github.com/copilot/github-copilot-in-the-cli)
- [Google Antigravity](https://antigravity.google/)
- Any other agent IDE that reads markdown instructions

See [docs/IDE-COMPAT.md](docs/IDE-COMPAT.md) for minor per-IDE notes.

---

## Contributing

Scheme presets, routing rules, and bug reports welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, remix it.

---

Built by [@wuhever](https://github.com/wuhever) from a working two-person business-vault system, generalized for solo use.
