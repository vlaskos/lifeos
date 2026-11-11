---
name: lifeos-update
description: Change LifeOS goals and streams in Notion by talking - close, move, rename, set next step, link to a goal, add a goal. Use for "close stream X", "move X to planned".
---

# LifeOS update

Natural-language edits to Goals & Streams.

## Find LifeOS
Read the "LifeOS Guide" page (data source ids, areas). No Guide → offer
`lifeos-setup` and stop.

Use field and option names from the Guide's **Names** section. The English names in
this skill are keys, the dashboard may use another language. No Names section =
English names.

## Steps
1. Find the record(s) by name (fuzzy). Several matches → quick choice with area and
   status shown. None → say so and offer to create it.
2. Map the request to fields:
   - close/finish → Status = Done (and untick Weekly focus)
   - start/move to → Status (In progress / Planned / Parking)
   - next step → Next step ("one verb, 30 minutes or less"; offer to shorten if long)
   - belongs to goal X → Goal ↑
   - deadline/when → Deadline / When
   - new goal/stream → create with Type, Area (ask if unknown), Status = Parking
3. Guards:
   - Moving to In progress beyond the WIP limit → say so and ask which one to pause.
   - Weekly focus beyond 3 → ask which one to drop.
   - Never delete records; offer Status = Done or Parking instead.
4. If the change is exactly what was asked, apply it without an extra question.
   If it is a guess, confirm first with one quick choice.
5. Read back and confirm in one line with a link.
