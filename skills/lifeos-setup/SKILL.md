---
name: lifeos-setup
description: Set up or change a LifeOS dashboard in Notion step by step with quick choices - areas, views, WIP, periods, tutorial. Use for "set up LifeOS" or adding/removing areas.
---

# LifeOS setup

Turns a duplicated LifeOS template into the user's own dashboard, then writes a
tutorial page and a LifeOS Guide page that the other LifeOS skills read.
Re-running it changes an existing setup (add/remove/rename areas, change views) and
never duplicates anything.

The full system spec (databases, views, dashboard layout, Notion API limits) is in
`spec/lifeos.yaml` in the LifeOS repo. Read it when you need exact property names,
view configs or limits. The tutorial text is in `references/tutorial.md`.

## How to talk during setup

- One step at a time. Each step = at most 2 short sentences of explanation + a quick
  choice (`ask_user_input` buttons when available, otherwise a numbered list).
- Put the explanation inside the question text as well: some clients hide text
  that sits right before the buttons.
- No walls of text. Say what the step does and what the user will see in Notion.
- Use the user's language for the conversation; Notion content stays English
  unless the user asks otherwise.
- Never change anything in Notion before step 7 ("Build").

## Prerequisites

- Notion tools are available (Notion connector or the official Notion plugin,
  which brings the Notion MCP server). If none are available, stop and show the
  short steps: Claude app → Settings → Connectors → Notion (and the Notion plugin
  if offered); Claude Code → install `notion-workspace-plugin` from
  `makenotion/claude-code-notion-plugin` and restart. Do not continue without it.
  LifeOS never adds its own Notion server.
- The user has duplicated the public LifeOS template. Buttons ("+ Idea",
  "Processed") and the Parking default only come from the template — the API
  cannot create them.

## Flow

### 0. Detect mode
Search Notion for a page titled "LifeOS Guide".
- Found → **change mode**: read it (database IDs, areas, WIP) and ask what to change
  (Add area / Remove area / Rename area / Change an area's view / Rerun full setup).
  Jump to the matching step, then to 7.
- Not found → **new setup**, continue with 1.

### 1. Start
"LifeOS is one Notion dashboard for goals, streams and ideas. Setup takes about
5 minutes; nothing changes until you confirm the plan."
Choices: Start / What's inside? (answer in 3 bullets, then ask again).

### 2. Find the template copy
"Open the LifeOS template and press Duplicate. I'll find the copy in your workspace."
Choices: Done / I can't find Duplicate.
Then search Notion for databases "Goals & Streams" and "Inbox" under a page "LifeOS".
- Exactly one match → confirm it in one line.
- Several → ask which one (show page path + last edited).
- None → explain once more and wait.
Store: dashboard page id, Goals & Streams data source id, Inbox data source id.

### 3. Areas
"An area is a big part of life. Every goal and stream belongs to one area; each area
gets its own tab on the dashboard."
Multi-select, all pre-selected: Work, Self-development, Sport, Health, Finance,
Family, Soul, Travel. Extra choice: Add my own (then ask for names, max 12 areas
total, keep 1–25 characters each).

### 4. View per area
"Each area gets a board by status by default: Parking → Planned → In progress → Done."
Choices: Boards for all (default) / Choose per area.
If per area, for each area: Board (default) / Timeline (good for trips, seasons) /
Table (good for long lists).

### 5. Rhythm
"How many streams can be In progress at once? Fewer = more finishing."
Choices: 3 / 4 (default) / 5.
Weekly focus stays at max 3 — mention it, do not ask.

### 6. Periods
"Goals can carry a period like 'Q1 2027'."
Choices: Current year + next 2 quarters + next year (default) / My own.
Compute from today's date.

### 7. Plan → Build
Show the plan as a short list (areas, view per area, WIP, periods, pages to create).
Choices: Build / Change something.
On Build, do these in order and verify each by reading it back:

1. **Area options** on both databases: `ALTER COLUMN "Area" SET SELECT(...)` with the
   chosen areas (keep existing option colors; new ones get unused colors).
   Before removing an option, count records using it; if any, ask first.
2. **Periods**: `ALTER COLUMN "Period" SET SELECT(...)` on Goals & Streams.
3. **Area tabs** on the dashboard:
   - For each new area: create the view with `create_view` (parent = dashboard page,
     `show_data_source_title` false) using the spec's `area_view` variant, then move
     the new linked block into a new `<tab>` before `</tabs>` with one
     `update_content` (include every existing `<database>` tag unchanged).
   - For each removed area: say exactly which tab will go, get a yes, then remove
     that tab with `update_content` (`allow_deleting_content: true`). Only the linked
     view goes; records stay.
   - Rename = rename the option, the tab title and the view name.
4. **Tutorial page** "📖 How LifeOS works" under the dashboard, from
   `references/tutorial.md` with the placeholders filled. Link it at the top of the
   left column. In change mode, update it instead of creating a new one.
5. **LifeOS Guide** page (child of the dashboard, can be collapsed in a toggle):
   database ids, area list, WIP limit, weekly focus max, setup date, skill version.
   Other LifeOS skills read this first.

### 8. Verify
Fetch the dashboard and both data sources. Check: every chosen area has an option and
a tab; no tab for a removed area; tutorial and Guide exist. Fix and re-check once;
report anything still off in plain words.

### 9. Finish
Two lines + links (dashboard, tutorial). Then three first actions:
press "+ Idea"; pick an area and press "Processed"; mark up to 3 streams as Weekly focus.
Offer the daily skills (capture, inbox, focus, status, update) if they are not installed,
and the Notion-skills option (upload them to the user's Notion, see repo README).

## Limits to mention only when relevant

- Notion Free allows 1 chart per workspace; the Areas wheel needs it.
- Buttons cannot check conditions: pressing "Processed" with an empty Area creates a
  stream without an area (visible on Overview, not on an area tab).
- The API cannot create buttons, delete views or reorder view tabs; those stay manual.
