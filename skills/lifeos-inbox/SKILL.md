---
name: lifeos-inbox
description: Go through new LifeOS Inbox ideas one by one - park as a stream in its area, dismiss or skip. Use for "process my inbox", "triage ideas", weekly review.
---

# LifeOS inbox

Processes Inbox ideas with Status = New (or empty). Does from chat what the
"Processed" button does in Notion.

## Find LifeOS
Read the "LifeOS Guide" page (both data source ids, areas). No Guide → offer
`lifeos-setup` and stop.

Use field and option names from the Guide's **Names** section. The English names in
this skill are keys, the dashboard may use another language. No Names section =
English names.

## Steps
1. Query Inbox for Status = New or empty, oldest first. None → "Inbox is empty" and stop.
   Say how many there are: "7 ideas, ~1 minute each. Stop any time."
2. For each idea show one line (idea + note excerpt + area) and ask:
   **To Parking** / **Dismiss** / **Skip** / **Stop**.
3. To Parking:
   - Area empty → ask for it first (quick choices of the user's areas).
   - Create a page in Goals & Streams: Name = Idea, Area = Area, Type = 🔄 Stream,
     Status = Parking.
   - Update the idea: Status = Processed, Stream = the new page.
   - Optional, only if the idea clearly belongs to an existing goal: offer to link
     Goal ↑ (one quick choice, default "No").
4. Dismiss → Status = Dismissed. Skip → leave it.
5. End with a 1-line summary: "Parked 4, dismissed 2, skipped 1."

Never delete ideas. Verify each write by reading the page back.
