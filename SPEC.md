# Todo App — Project Specification

## Overview
A single-file todo list web application built with plain HTML, CSS, and JavaScript.
No build tools, no frameworks, no backend. All data persists in the browser via localStorage.
Hosted as a static site on Netlify, source on GitHub.

---

## Repository & Hosting
- **GitHub:** https://github.com/Ben78777/test
- **Hosting:** Netlify (auto-deploys from `main` branch)
- **Config:** `netlify.toml` sets publish directory to `.`

---

## Tech Stack
- HTML5 / CSS3 / Vanilla JavaScript (ES6+)
- No npm, no build step, no dependencies
- Single file: `index.html`
- Data storage: `localStorage` (keys: `todos`, `customTags`)

---

## Visual Design
- **Theme:** Dark mode only
- **Font:** System font stack (`-apple-system`, `BlinkMacSystemFont`, `Segoe UI`)
- **Max width:** 580px, centred

### Colour Palette
| Token            | Hex       | Usage                          |
|------------------|-----------|--------------------------------|
| Background       | `#0f1117` | Page background                |
| Surface          | `#1a1d27` | Cards, form panel              |
| Surface hover    | `#22263a` | Button/card hover states       |
| Border           | `#2e3347` | Card borders, input borders    |
| Accent (indigo)  | `#6366f1` | Buttons, active states, focus  |
| Text primary     | `#e2e8f0` | Body text, headings            |
| Text muted       | `#64748b` | Placeholders, secondary info   |
| High priority    | `#ef4444` | Red — priority dot, left border|
| Medium priority  | `#f59e0b` | Amber — priority dot, border   |
| Low priority     | `#22c55e` | Green — priority dot, border   |
| Overdue badge    | `#f87171` on `#3b0f0f` | Overdue due date  |
| Today badge      | `#fbbf24` on `#3b2a0a` | Due today         |

---

## Data Model

### Todo object
```json
{
  "id": 1711700000000,
  "text": "Task description",
  "done": false,
  "priority": "high",
  "dueDate": "2026-03-29T14:00",
  "tags": ["Work", "Personal"]
}
```
- `id`: Unix timestamp (from `Date.now()`)
- `priority`: `"high"` | `"medium"` | `"low"` | `null`
- `dueDate`: `datetime-local` string or `null`
- `tags`: array of tag name strings

### Custom tags
Stored separately in `localStorage` key `customTags` as a plain array of strings.

### Preset tags (hardcoded, always available)
`Work`, `Personal`, `Shopping`, `Health`

---

## Features

### Add a task
- Text input + Enter key or Add button
- Optional: due date + time (`datetime-local` picker)
- Optional: priority level (dropdown: None / High / Medium / Low)
- Optional: tags (popover chip picker — preset + custom)
- New tasks are prepended to the top of the list

### Task card
- Checkbox to toggle done/undone
- Coloured dot on the left that shows priority; clicking cycles: None → High → Medium → Low → None
- Left border colour reflects priority (or overdue state)
- Task text; click ✏️ to edit inline (Enter to save, Escape to cancel)
- Due date badge (if set): `Overdue` (red) / `Today HH:MM` (amber) / `Tomorrow HH:MM` / `Mar 29 HH:MM`
- Tag chips displayed below text
- ✏️ Edit and 🗑️ Delete buttons appear on hover

### Overdue / due-today highlighting
- Overdue (due date in the past, task not done): red left border + red "Overdue" badge
- Due today (not yet past, not done): amber left border + amber "Today HH:MM" badge

### Filters
- **Status:** All | Active | Done
- **Priority:** High | Medium | Low (toggleable; click again to clear)
- **Tag:** Auto-generated chip row showing all tags used across current todos; click to filter

### Tag management
- Click `+ Tags` in the add form to open the tag popover
- Preset tags always shown; toggle any to add to the new task
- Custom tag creation: type a name in the "New tag..." input and press Enter or `+`
- Custom tags can be deleted from the popover (only if no tasks currently use them)

### Sorting
Tasks are sorted by priority within each view: High → Medium → Low → None.

### Footer
- Shows count of active (incomplete) items
- "Clear completed" button removes all done tasks

### Persistence
- All todos and custom tags survive page refresh via `localStorage`
- No server, no account required

---

## File Structure
```
/
├── index.html       # Entire application (HTML + CSS + JS)
├── netlify.toml     # Netlify publish config
└── SPEC.md          # This file
```

---

## Known Constraints
- No user accounts — data is local to the browser/device
- No real-time sync or sharing between devices
- No offline service worker (but works offline since it's fully static)
- No drag-to-reorder (not currently in scope)

---

## Future Ideas (not yet implemented)
- Light/dark mode toggle
- Drag-to-reorder tasks
- Subtasks / checklists within a task
- Notes field per task
- Export todos as JSON or CSV
- Recurring tasks
