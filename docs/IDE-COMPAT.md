# IDE Compatibility

The `/setup` wizard is a plain markdown prompt (`setup/SETUP-PROMPT.md`). It works in any AI IDE that can read files and take multi-step actions. Here are notes per IDE.

---

## Claude Code

**Verified.** This template was built for and tested primarily with Claude Code.

- Invoke: `claude` from the repo root
- Trigger the wizard: `"Run the setup wizard in setup/SETUP-PROMPT.md"` or `/setup` if you've added it as a custom slash command
- Claude Code auto-reads `CLAUDE.md` files — the vault's `CLAUDE.md` will load automatically when you work inside `vault/`

---

## Cursor

**Should work.** Uses Claude/GPT under the hood, reads markdown prompts fine.

- Invoke: Open repo folder → open chat panel
- Trigger: `"Read setup/SETUP-PROMPT.md and run the setup wizard"`
- Cursor respects `.cursorrules` — if you want per-project rules, copy them from `CLAUDE.md` manually

---

## GitHub Copilot CLI

**Should work.** 

- Invoke: `gh copilot` from repo root
- Trigger: `"Follow the instructions in setup/SETUP-PROMPT.md"`
- Copilot CLI has different tool names than Claude — the wizard prompt doesn't assume specific tool names, so this should work

---

## Google Antigravity

**Should work.** Antigravity is agent-based and reads markdown instructions the same way.

- Invoke: Open project → start new agent session
- Trigger: `"Read and execute setup/SETUP-PROMPT.md"`

---

## Gemini CLI / Codex / Others

**Likely works** but untested. The wizard uses only these capabilities:
- Reading files
- Writing files
- Moving/renaming files
- Asking the user questions

Any agent with those capabilities should complete the wizard. Report back in an issue if you test it.

---

## What if my agent doesn't have a built-in "ask user" mechanism?

The wizard will fall back to printing questions in chat and waiting for your text reply. That works in any agent — it just feels less polished than native question UIs.

---

## Differences you might notice

| IDE | Question UI | Auto-reads CLAUDE.md | Skill support |
|---|---|---|---|
| Claude Code | Native (structured) | Yes | Yes (Skill tool) |
| Cursor | Chat messages | No (use .cursorrules) | No |
| Copilot CLI | Chat messages | No | No |
| Antigravity | Chat messages | Varies | Varies |

None of these differences affect the setup outcome — placeholders get replaced and files get routed either way.

---

## Running the vault-operator-audit skill

After setup, you'll want to run audits. The skill lives at `vault-operator/skills/vault-operator-audit/SKILL.md`.

- **Claude Code:** invoke via the `Skill` tool or tell Claude *"run the vault-operator-audit skill"*
- **Other IDEs:** open `SKILL.md` and tell the agent *"follow this skill's phases to audit my vault"*
