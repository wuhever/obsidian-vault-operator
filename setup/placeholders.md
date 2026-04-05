# Placeholders — Canonical List

Every `{{TOKEN}}` used in the template. The setup wizard replaces all of these during Phase 4.

---

## Tokens

| Token | What it means | Example value | Where it appears |
|---|---|---|---|
| `{{VAULT_NAME}}` | Short slug for the vault | `sarah-phd-vault` | `vault/README.md`, `vault/AGENTS.md`, `vault-operator/operator-prompt.md` |
| `{{OWNER_NAME}}` | Display name of the vault owner | `Sarah` | `vault-operator/operator-prompt.md` (Key People), `vault/{owner}-space/_README.md` |
| `{{OWNER_SLUG}}` | Lowercase/hyphenated version of owner name | `sarah` | Folder name `{owner}-space/` |
| `{{VAULT_PURPOSE}}` | One-sentence description of what the vault is for | `PhD research on marine biology` | `vault/AGENTS.md`, `vault/README.md` |
| `{{ORG_OR_TOPIC}}` | Short phrase for "Relevance to ___" | `your research` | `vault/_Templates/research-note.md` |
| `{{VAULT_PATH}}` | Absolute path to the `vault/` directory | `C:\Users\sarah\Documents\sarah-phd-vault\vault` | `vault-operator/operator-prompt.md`, `vault-operator/CLAUDE.md` |
| `{{VAULT_OPERATOR_PATH}}` | Absolute path to the `vault-operator/` directory | `C:\Users\sarah\Documents\sarah-phd-vault\vault-operator` | `vault-operator/operator-prompt.md`, `vault-operator/CLAUDE.md` |

---

## Derivation rules

When the wizard collects answers, derive these automatically:

- `{{OWNER_SLUG}}` = `{{OWNER_NAME}}` lowercased, spaces → hyphens, strip special chars
  - "Sarah Smith" → `sarah-smith`
  - "Dr. Ali Al-Hameiri" → `ali-al-hameiri`

- `{{ORG_OR_TOPIC}}` = inferred from `{{VAULT_PURPOSE}}`
  - "PhD research on X" → `your research`
  - "AI engineering notes" → `your work`
  - "Personal knowledge base" → `your interests`
  - Default: `your work`

- `{{VAULT_PATH}}` and `{{VAULT_OPERATOR_PATH}}` = user-provided repo path + `/vault` or `/vault-operator`

---

## Verification

After Phase 4 of the wizard, run:

```bash
grep -rn "{{" vault/ vault-operator/ setup/ README.md
```

Should return zero matches (except references inside this file and `setup/SETUP-PROMPT.md`, which are documentation, not template content).

If any `{{TOKEN}}` remains in a user-facing file, the wizard failed partway — either re-run the replacement for that specific token, or restart the wizard.

---

## Future tokens (v0.2+)

When multi-owner support lands, these will be added:
- `{{OWNER_COUNT}}` — number of personal spaces to create
- `{{OWNER_2_NAME}}`, `{{OWNER_2_SLUG}}`, etc. — for each additional owner
