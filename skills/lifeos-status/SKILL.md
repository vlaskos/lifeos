---
name: lifeos-status
description: Short LifeOS status from Notion - weekly focus, deadlines, stagnating streams, Inbox count, WIP. Use for "what's my status", "what's next", "where am I", daily check-in.
---

# LifeOS status

Read-only summary. Changes nothing.

## Find LifeOS
Read the "LifeOS Guide" page (data source ids, WIP limit). No Guide → offer
`lifeos-setup` and stop.

Use field and option names from the Guide's **Names** section. The English names in
this skill are keys, the dashboard may use another language. No Names section =
English names.

## Report (keep it under ~10 lines)
- **Focus this week** — streams with Weekly focus, each with its Next step
  (flag ones with no next step).
- **Deadlines ≤ 30 days** — name + date, nearest first.
- **WIP** — "In progress 3/4".
- **Stagnation** — up to 3 In progress streams with the oldest Updated time,
  with how long ago.
- **Inbox** — number of New ideas.

Then one suggestion that fits what you see, as quick choices, e.g.:
"Process inbox (6)" / "Plan the week" / "Done for now" — route to `lifeos-inbox`
or `lifeos-focus`.
