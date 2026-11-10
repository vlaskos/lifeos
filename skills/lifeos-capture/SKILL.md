---
name: lifeos-capture
description: Save an idea to the LifeOS Inbox in Notion fast. Use when the user says "save an idea", "remember to...", "idea:", or shares a thought to park for later.
---

# LifeOS capture

Puts one or more ideas into the LifeOS **Inbox** with Status = New.

## Find LifeOS
Search Notion for the page "LifeOS Guide" and read it (Inbox data source id, areas).
No Guide → say LifeOS isn't set up yet and offer `lifeos-setup`. Stop.

## Steps
1. Take the idea text from the message. Several ideas → one Inbox page each.
2. Area:
   - If the user named an area or it's obvious, use it.
   - Otherwise suggest the most likely area as the first quick choice, plus 2–3
     others and "No area yet". One question for all ideas when there are several.
3. Create the Inbox page(s): Idea = text, Area = choice (or empty), Status = New.
   Put extra detail the user gave into Note.
4. Confirm in one line with a link, e.g. "Saved to Inbox → Travel."
   If the area is empty, add: "Pick an area before processing it."

Do not create streams here; turning ideas into streams is `lifeos-inbox`.
