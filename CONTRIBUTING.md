# Contributing

Thanks for your interest in improving `obsidian-vault-operator`. This is a small project maintained for friends, family, and anyone who finds it useful — contributions are welcome but kept simple.

## What's most useful to contribute

### 1. New scheme presets

The setup wizard uses presets in `setup/scheme-presets.md` to create folder structures based on the user's vault type (student, researcher, business, hobbyist-builder, personal, custom). If you've used this template for a different kind of vault — legal, teaching, writing, music production, startup ops, fitness tracking, homeschooling — submit a preset.

A preset is just a markdown block with:
- Name + one-line description
- Target user
- Signals in `/_intake/` that would trigger it
- Folder scheme (5-8 folders using the 00-09 numbering pattern)
- Rationale for any distinctive folders

See existing presets in `setup/scheme-presets.md` as examples.

### 2. Routing rules

`setup/intake-routing-rules.md` contains heuristics for where the agent should send files based on extension, filename patterns, and frontmatter. If you find files being misrouted, open an issue or PR with the pattern and the correct destination.

### 3. IDE compatibility notes

If you run the wizard in an IDE not yet documented in `docs/IDE-COMPAT.md`, add notes about what worked and what didn't.

### 4. Bug reports

If `/setup` breaks, mis-routes files, or leaves placeholders unreplaced, open an issue with:
- Which IDE/agent you were using
- What you put in `/_intake/`
- What the agent did vs. what you expected

## What's out of scope

- Adding new frontmatter types (the 14 canonical types cover nearly everything — if you think you need a new one, use `type: note` with a `subtype` property)
- Changing the 00-09 numbering pattern or the universal folders (Inbox, Reference, Templates, Owner-Space are intentionally fixed — topical folders inside that numbering are fully customizable via presets)
- Shell/Node rewrites of the wizard (the markdown-prompt approach is the whole point — it works in any agent IDE)

## Pull request checklist

- [ ] Run the full `/setup` wizard on a fresh clone after your changes
- [ ] Confirm no placeholders are left unreplaced (`grep -r "{{" .`)
- [ ] Update `docs/` if your change affects user-facing behavior
- [ ] Keep changes scoped — one PR per concern

## License

By contributing, you agree your changes will be released under the [MIT License](LICENSE).
