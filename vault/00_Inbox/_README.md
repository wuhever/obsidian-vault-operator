---
type: system
status: active
created: 2026-01-01
---

# Inbox

This is the vault's **catch-all folder**. Drop anything here that doesn't have a home yet.

## How It Works

1. **You or your AI agent** saves a file here when you're unsure which folder it belongs in
2. **The Vault Operator** periodically scans this folder (excluding `Daily/`)
3. The Operator reads each file, determines the correct destination based on its content and frontmatter, then moves it to the right folder
4. Moves are logged in `vault-operator/changes/`

## What Goes Here

- Quick captures and rough notes
- Files from external sources that need sorting
- Anything you want to save now and organize later

## What Does NOT Go Here

- Daily notes — those go in `Daily/` (auto-created by Obsidian's Daily Notes plugin)
- Files you already know the destination for — put them directly in the right folder

## Subfolders

- **`Daily/`** — Daily notes, created automatically using the `_Templates/daily-note` template. These stay here permanently and are excluded from triage.
