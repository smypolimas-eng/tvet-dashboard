# MY TVET Dashboard — Plan

## Overview

Build a single-file (`index.html`) dashboard page titled **MY TVET Dashboard**.
The page is built with plain HTML, CSS, and vanilla JavaScript — no frameworks,
no build tools, no external dependencies beyond a Google Font import.

The dashboard displays:
- Three summary cards: **Students Registered**, **Tasks Remaining**, **Workshop Status**
- One **Preparation Checklist** (5 items pre-ticked, 3 open) with interactive tick-off
- A **Students Table** listing registered students with sample names and status
- A **Facilitators Table** listing facilitators with their assigned sessions
- All data is hard-coded sample data embedded in a JavaScript `DATA` object

Visual style: bold, **electric blue** (`#0057FF`) and **orange** (`#FF6B00`) as the
two primary accent colors; strong Poppins typography; dark header bar.

---

## Color Palette

| Role | Value |
|---|---|
| Primary accent | `#0057FF` (electric blue) |
| Secondary accent | `#FF6B00` (orange) |
| Card 1 background | `#0057FF` |
| Card 2 background | `#FF6B00` |
| Card 3 background | `#0039B3` (deep blue variant) |
| Page background | `#F0F4FF` (light blue-tinted grey) |
| Header background | `#001A66` (near-black blue) |

---

## Sub-Tasks

---

### Sub-Task 1 — Page Shell & Typography

**Intent**
Create the base HTML document with the correct `<head>` metadata, Google Fonts
import, and a top-level layout container. This is the skeleton every other
sub-task builds on.

**Expected Outcomes**
- `index.html` exists with valid HTML5 boilerplate
- Page title reads "MY TVET Dashboard"
- A dark header bar shows the dashboard title in bold white Poppins type
- Poppins (weights 600 and 800) is loaded and applied globally
- A CSS grid layout area (`<main>`) exists ready to receive cards and tables

**Todo List**
1. Create `index.html` with HTML5 doctype, `<head>`, `<body>`
2. Add `<title>MY TVET Dashboard</title>` and viewport meta tag
3. Import Poppins from Google Fonts (weights 400, 600, 800)
4. Write base CSS reset and font defaults inside a `<style>` block
5. Add a `<header>` with a bold title and a subtitle (e.g. "Workshop Management")
6. Add a `<main>` wrapper that will hold all sections

**Relevant Context**
- Header background: `#001A66`, text: white
- Page background: `#F0F4FF`

**Status:** `[ ] pending`

---

### Sub-Task 2 — Students Registered Card

**Intent**
Build the first summary card showing student registration stats using sample data.

**Expected Outcomes**
- Electric blue card (`#0057FF`) with white text
- Displays: label "Students Registered 🎓", large headline number, two sub-stats
  (Confirmed, Waitlisted)
- Rounded corners, generous padding, bold number

**Sample Data**
```
Students Registered: 48
  Confirmed: 40
  Waitlisted: 8
```

**Todo List**
1. Add `<section class="card card--blue">` inside a `.cards-grid` wrapper in `<main>`
2. Include emoji icon, label, large `<span class="card__number">`, and two sub-stats
3. Define shared `.card` CSS and `.card--blue` color override
4. Populate values from `DATA.students` via `renderCards()` function

**Status:** `[ ] pending`

---

### Sub-Task 3 — Tasks Remaining Card

**Intent**
Build the second summary card showing how many preparation tasks are still open,
with a live progress bar that updates when the checklist is used.

**Expected Outcomes**
- Orange card (`#FF6B00`) with white text
- Displays: label "Tasks Remaining ✅", large remaining count, progress bar
- Progress bar fill color: white (semi-transparent) against orange background
- Recalculates live when checklist items are toggled

**Sample Data**
```
Tasks Remaining: 3  (computed)
Total Tasks: 8
Tasks Done: 5
```

**Todo List**
1. Add `<section class="card card--orange">` inside `.cards-grid`
2. Include label, large number `<span>`, and `<div class="progress-track"><div class="progress-fill"></div></div>`
3. Add CSS for `.progress-track` and `.progress-fill`
4. `renderCards()` sets `progress-fill` width from `(done/total * 100)%`

**Status:** `[ ] pending`

---

### Sub-Task 4 — Workshop Status Card

**Intent**
Build the third summary card showing overall workshop readiness and a day countdown.

**Expected Outcomes**
- Deep blue card (`#0039B3`) with white text
- Displays: label "Workshop Status 🏫", a status badge, and "X days to go"
- Badge is green pill for "On Track", red pill for "At Risk"

**Sample Data**
```
Status: On Track
Workshop Date: 7 days from today
```

**Todo List**
1. Add `<section class="card card--deepblue">` inside `.cards-grid`
2. Include label, `<span class="badge badge--ontrack">On Track</span>`, countdown line
3. Add CSS for `.badge` pill shape, `.badge--ontrack` (green), `.badge--atrisk` (red)
4. Render badge class conditionally from `DATA.workshop.status`

**Status:** `[ ] pending`

---

### Sub-Task 5 — Preparation Checklist

**Intent**
Build an interactive checklist with 5 pre-ticked items and 3 open items.
Ticking/unticking updates the Tasks Remaining card in real time.

**Expected Outcomes**
- Section titled "📋 Preparation Checklist" below the cards
- 8 items rendered from `DATA.tasks.items`; 5 start checked
- Checked rows show strikethrough and muted text
- Any toggle immediately recalculates and re-renders the Tasks Remaining card

**Sample Data**
```
items: [
  { label: "Send confirmation emails",   done: true  },
  { label: "Reserve lab room",           done: true  },
  { label: "Print handouts",             done: true  },
  { label: "Install workshop software",  done: true  },
  { label: "Prepare attendance sheet",   done: true  },
  { label: "Brief all facilitators",     done: false },
  { label: "Test all demo exercises",    done: false },
  { label: "Set up feedback form",       done: false }
]
```

**Todo List**
1. Add `<section class="checklist">` below `.cards-grid`
2. Render a `<label>` with `<input type="checkbox">` for each item; set `checked`
   from `done` flag
3. Add CSS for `.checklist__item` and `.checklist__item--done` (strikethrough + muted)
4. On `change` event: toggle `done` in `DATA.tasks.items`, call `renderCards()`

**Status:** `[ ] pending`

---

### Sub-Task 6 — Students Table

**Intent**
Add a full-width table below the checklist listing registered students with
their name, registration number, confirmation status, and assigned group.

**Expected Outcomes**
- Section titled "👩‍🎓 Registered Students"
- Table with columns: #, Name, Reg No., Status, Group
- Status cell is color-coded: green chip for Confirmed, amber for Waitlisted
- 10 sample rows rendered from `DATA.students.list`

**Sample Data (10 students)**
```
{ name: "Amara Dlamini",   reg: "T2024-001", status: "Confirmed",  group: "A" },
{ name: "Bongani Khumalo", reg: "T2024-002", status: "Confirmed",  group: "A" },
{ name: "Celeste Mokoena", reg: "T2024-003", status: "Confirmed",  group: "B" },
{ name: "Derick Nkosi",    reg: "T2024-004", status: "Waitlisted", group: "-" },
{ name: "Emeka Okafor",    reg: "T2024-005", status: "Confirmed",  group: "B" },
{ name: "Fatima Patel",    reg: "T2024-006", status: "Confirmed",  group: "C" },
{ name: "Gift Sibande",    reg: "T2024-007", status: "Confirmed",  group: "C" },
{ name: "Hlengiwe Zulu",   reg: "T2024-008", status: "Waitlisted", group: "-" },
{ name: "Ivan Ferreira",   reg: "T2024-009", status: "Confirmed",  group: "A" },
{ name: "Joy Mahlangu",    reg: "T2024-010", status: "Confirmed",  group: "B" }
```

**Todo List**
1. Add `<section class="table-section">` after the checklist
2. Render a `<table>` with `<thead>` and `<tbody>` from `DATA.students.list`
3. Apply `.chip--confirmed` (green) and `.chip--waitlisted` (amber) CSS to status cells
4. Style table with alternating row colors, electric blue header row

**Status:** `[ ] pending`

---

### Sub-Task 7 — Facilitators Table

**Intent**
Add a second table listing facilitators, their role, and the session they lead.

**Expected Outcomes**
- Section titled "🧑‍🏫 Facilitators"
- Table with columns: #, Name, Role, Session, Status
- Status shows "Ready" or "Pending" with matching color chips
- 5 sample rows rendered from `DATA.facilitators`

**Sample Data (5 facilitators)**
```
{ name: "Mr. T. Ndlovu",   role: "Lead Instructor", session: "Opening & Demo",       status: "Ready"   },
{ name: "Ms. P. Sithole",  role: "Facilitator",     session: "Group A Lab Work",     status: "Ready"   },
{ name: "Mr. K. Moagi",    role: "Facilitator",     session: "Group B Lab Work",     status: "Pending" },
{ name: "Ms. R. Adams",    role: "Facilitator",     session: "Group C Lab Work",     status: "Ready"   },
{ name: "Mr. S. Langa",    role: "IT Support",      session: "All Sessions Support", status: "Ready"   }
```

**Todo List**
1. Add `<section class="table-section">` after the students table
2. Render a `<table>` with `<thead>` and `<tbody>` from `DATA.facilitators`
3. Reuse `.chip--ready` (green) and `.chip--pending` (amber) CSS classes
4. Style consistently with the students table (same header color, alternating rows)

**Status:** `[ ] pending`

---

## Data Shape Reference

```
DATA
├── students
│   ├── total: 48
│   ├── confirmed: 40
│   ├── waitlisted: 8
│   └── list: [ { name, reg, status, group }, ... ]   (10 rows)
├── tasks
│   └── items: [ { label, done }, ... ]               (8 items, 5 done)
├── workshop
│   ├── status: "On Track"
│   └── daysRemaining: 7
└── facilitators: [ { name, role, session, status }, ... ]  (5 rows)
```

---

## Page Layout (top → bottom)

```
┌─────────────────────────────────────────┐
│  HEADER — MY TVET Dashboard             │
├──────────┬──────────┬────────────────── ┤
│  Card 1  │  Card 2  │     Card 3        │
│ Students │  Tasks   │  Workshop Status  │
│ (blue)   │ (orange) │  (deep blue)      │
├─────────────────────────────────────────┤
│  📋 Preparation Checklist               │
├─────────────────────────────────────────┤
│  👩‍🎓 Registered Students (table)         │
├─────────────────────────────────────────┤
│  🧑‍🏫 Facilitators (table)                │
└─────────────────────────────────────────┘
```

---

## File Structure

```
index.html   ← single file: HTML + <style> + <script>
```
