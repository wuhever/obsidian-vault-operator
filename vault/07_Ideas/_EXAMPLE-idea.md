---
type: idea
idea-name: Weekly Review Automation
status: draft
priority: medium
created: 2026-01-15
---

# Idea — Weekly Review Automation

*This is a demo idea — fictional. Delete this file when you're comfortable with the template, or keep it as a working example.*

## What

Every Friday, have an AI agent scan the week's new notes, summarize key decisions, flag open action items, and generate a weekly review note in `{{OWNER_SLUG}}-space/Goals/`.

## Why This Matters

- Weekly reviews are high-leverage but tedious
- Agent already has full vault context
- Output becomes input to next week's planning

## How It Could Work

1. Operator runs every Friday afternoon
2. Reads all files modified in the past 7 days
3. Summarizes + extracts action items
4. Writes `weekly-review-YYYY-MM-DD.md` with links to source notes
5. Logs the run in `vault-operator/changes/`

## Effort Estimate

**Complexity:** Low / Medium / High → Low
**Time to prototype:** 1-2 hours

## Next Steps

- [ ] Define the output template
- [ ] Write the review SOP in `06_Operations/`
- [ ] Test on one week's data
- [ ] Schedule it (cron or manual trigger)
