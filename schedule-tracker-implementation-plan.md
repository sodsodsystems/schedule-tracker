# ICpEP.SE Schedule Tracker — Implementation Plan

**Stack:** Google Sheets (database) → Google Apps Script (API layer) → GitHub Pages (static frontend)

---

## 1. Google Sheets — Data Layer

**Status:** Not yet built

### Sheet: `Officers`
| Column | Type | Notes |
|---|---|---|
| officer_id | text | short slug, e.g. `riza` |
| name | text | display name |
| codename | text | ties into KumEng: Refactor branding |
| committee | text | Executive Board / Communications / Technical / Logistics |
| color | text | hex, assigned per officer for grid blocks |
| email | text | used for Apps Script access check |

### Sheet: `ClassBlocks`
| Column | Type | Notes |
|---|---|---|
| officer_id | text | matches `Officers` |
| day | text | Mon–Sat |
| start_time | text | 24h format, e.g. `08:00` |
| end_time | text | 24h format |
| subject | text | e.g. `CPE 401` |
| term | text | e.g. `2026-2027-1st` — supports semester reset |

### Sheet: `Overrides` (optional, phase 2)
| Column | Type | Notes |
|---|---|---|
| officer_id | text | |
| date | date | specific date, not recurring |
| status | text | unavailable / traveling / on-duty |
| note | text | free text |

**Implementation steps:**
1. Create the spreadsheet, add the three tabs with headers above.
2. Build a Google Form for `ClassBlocks` entry (one submission per class) that appends rows — keeps officers out of the raw sheet.
3. Data-validate `day` and `committee` columns with dropdowns to avoid typos breaking the frontend grid.

---

## 2. Google Apps Script — API Layer

**Status:** Not yet built

**Purpose:** Serves the sheet data as JSON, and gates access by officer email.

### Endpoints (as URL parameters on one Web App)
- `?action=schedules` → returns all `ClassBlocks` joined with `Officers` (color, committee)
- `?action=officers` → returns officer list for the filter chips
- `?action=overrides` → returns current-term overrides

### Access control
Use `Session.getActiveUser().getEmail()` inside the script, checked against the `Officers.email` column (or your org's email domain). If the visitor isn't recognized, return a 403-style JSON error instead of data.

**Implementation steps:**
1. In the Sheet: `Extensions → Apps Script`.
2. Write a `doGet(e)` function that reads `e.parameter.action`, pulls the relevant range via `SpreadsheetApp`, and returns `ContentService.createTextOutput(JSON.stringify(data)).setMimeType(ContentService.MimeType.JSON)`.
3. Add the email-check gate at the top of `doGet` before any data is read.
4. Deploy as **Web App**: Execute as "Me", Access "Anyone within [org domain]" — this is what makes the email check meaningful (Apps Script will know who's visiting).
5. Copy the deployed Web App URL for use in the frontend `fetch()` calls.
6. Re-deploy (new version) any time the script changes — Apps Script doesn't auto-update live URLs on edit.

---

## 3. Frontend — Missing Features on Top of the Mockup

**Status:** Static mockup exists with hardcoded sample data; below are the gaps to close.

### 3.1 Live data fetch
Replace the hardcoded `.class-block` divs with a `fetch()` to the Apps Script URL on page load, then render blocks dynamically.
- Build a small render function: given `{officer_id, day, start_time, end_time, subject, color}[]`, compute grid position (day → column, time → row offset/height) and inject blocks.
- Cache the response in memory for the session to avoid re-fetching on every filter click.

### 3.2 Committee filter (chips)
Currently static/decorative in the mockup.
- On chip click: filter the in-memory schedule array by `committee`, re-render the grid.
- Keep "All Officers" as the reset state.

### 3.3 Overlap finder
The banner in the mockup is hardcoded text.
- Algorithm: for the currently filtered officer set, compute the complement of all `ClassBlocks` per day (i.e., free time = full day minus each officer's blocks), then intersect free-time ranges across all officers in the set.
- Render the result as the banner text, updating whenever the filter or data changes.
- Edge case: if the filtered group is empty or has no common slot, show a clear empty state ("No common free time this week for this group.") rather than a blank banner.

### 3.4 Access gate on the frontend
Static GitHub Pages sites can't check identity themselves, so the real gate lives in Apps Script (Section 2). Frontend still needs a graceful flow:
- On load, attempt the fetch; if Apps Script returns the 403-style error, show a "Sign in with your @[org] Google account" message with a link that opens the Apps Script URL directly (Google will prompt sign-in there), then a "Reload" button once done.
- This isn't seamless SSO, but it's the realistic ceiling for a static-only frontend.

### 3.5 Semester reset flow
- Add a `term` filter (dropdown or auto-detect current term by date) so old terms' `ClassBlocks` don't clutter the live view.
- Officers input new-term data via the Form; old rows stay in the sheet as history rather than being deleted.

### 3.6 Mobile responsiveness
- Grid currently assumes desktop width (7 columns + time rail). For mobile: collapse to a single selected day at a time with day-tabs above the grid, or a per-officer list view instead of the full grid.
- Test the officer color-blocks at smaller font sizes — `.class-block` text may need to truncate (`text-overflow: ellipsis`) on narrow columns.

### 3.7 Per-officer detail view (nice-to-have)
- Clicking a name in the legend filters the grid to just that officer, showing their full week.
- Useful for "when is [officer] free" lookups without needing the overlap logic.

---

## 4. Hosting — GitHub Pages

**Status:** Not yet deployed

**Implementation steps:**
1. Push the frontend (`index.html`, plus any separate CSS/JS files) to a GitHub repo.
2. Repo Settings → Pages → set source branch (usually `main`) and root folder.
3. Site will be live at `https://<username>.github.io/<repo-name>/`.
4. Hardcode the Apps Script Web App URL as a constant in the frontend JS (it's not a secret key, just an endpoint — the real protection is the email check server-side).
5. Since the repo can stay public (no sensitive data committed, only client code), no GitHub Pro plan is needed.

---

## 5. Suggested Build Order

1. Sheets schema + Form (Section 1)
2. Apps Script `doGet` with the two/three endpoints, no auth yet — verify JSON output manually
3. Wire frontend to live fetch (3.1), confirm real data renders in the existing grid design
4. Add committee filter (3.2) and overlap finder (3.3)
5. Add Apps Script email gate (Section 2, access control) + frontend sign-in fallback (3.4)
6. Mobile pass (3.6) and term/reset handling (3.5)
7. Deploy to GitHub Pages (Section 4)
8. Optional: per-officer detail view (3.7)
