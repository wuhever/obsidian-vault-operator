# _intake/ — Drop your existing files here

This folder is the **one-time bulk import zone** for the `/setup` wizard.

## How to use it

1. **Before** running `/setup`, drop any existing files or folders you want organized into this directory.
2. **Run `/setup`** — the agent will analyze what's here, propose a folder scheme, and route every file into the right place in `vault/`.
3. **After setup**, this folder is renamed to `/_intake-backup/` (gitignored). Delete it yourself when you're confident nothing was lost.

## What to drop here

- Markdown notes (`.md`)
- PDFs (papers, reports, contracts)
- Images (screenshots, diagrams)
- Word docs, Google Docs exports
- Folders of anything — the agent will look at your structure too

## What NOT to drop here

- Secrets, API keys, `.env` files (they'll get synced everywhere — never put these in a vault)
- Files you already have in `vault/` (the wizard only processes this folder)
- Anything you want to keep private from AI agents

## After setup

Once setup runs, use **`vault/00_Inbox/`** for ongoing drops. That folder stays forever and gets triaged on an ongoing basis by the operator. `_intake/` is just for the initial import.

See the repo README for the full picture.
