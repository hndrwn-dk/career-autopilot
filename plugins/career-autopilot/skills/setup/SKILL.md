---
name: setup
description: >
  Use when the user says "set up career autopilot", "start career autopilot", "check my setup",
  "health check", "cek setup", "pasang career autopilot", pastes a block starting with
  CAREER-AUTOPILOT-SETTINGS, or before the first job search. Verifies connectors, creates the
  tracker sheet, applies a role preset and settings, and schedules the run for the chosen mode.
---

# Setup and health check

Run every step, never stop at the first failure, and finish with one table:
Check | Status (OK / Missing / Error) | What to do.

## 1. Connectors

Load each tool (ToolSearch if deferred) and make one harmless read.

| Connector | Test | Needed for |
|---|---|---|
| Gmail | search threads `newer_than:1d`, 1 result | recruiter mail, status sync, drafts |
| Google Drive | search files named "Career Autopilot" | CV storage, shortlists, interview briefs |
| Google Sheets / Drive file create | read or create the tracker (step 2) | tracker |
| Browser (built-in browser or Claude in Chrome, whichever the session has) | list tabs | prefilling forms, LinkedIn, sites without an API |
| Scheduling (scheduled-task tool) | tool present | `active` / `watch` runs |
| Google Calendar | list calendars | interview slots (optional) |

- Absent → Missing; name the connector to add. If a connector-suggestion tool exists, offer it.
- Present but errors → Error; quote the error in one line.

## 2. Tracker sheet

Look for a spreadsheet named exactly `Career Autopilot Tracker`. Create it if missing; otherwise add any missing tab or header.

| Tab | Columns |
|---|---|
| Applications | No, Company, Role, Location, Status, Channel, Employment Model, Applied On, Link, Job ID, Match %, Last Update, Next Action, Notes |
| Profile | Key, Value |
| Filters | Key, Value |
| Skip | Company, Role, Link, Reason, Date |
| Stories | Id, Title, Situation, Task, Action, Result, Skills, Source |

## 3. Preset

If Filters has no `preset`, ask once which fits: `sre-platform`, `tam-presales`, `storage-infra`, several (comma list), or `none`.
Read the files from `${CLAUDE_PLUGIN_ROOT}/presets/`. For several presets, union `target_roles` and `keywords`,
take the lowest `min_match`, and use the weights of the first one. Write only keys that are empty in Filters.

## 4. Settings block

A block from `CAREER-AUTOPILOT-SETTINGS` to `END-SETTINGS`: write every `key: value` line into Filters (overwriting).
Lines starting `profile.` go to Profile without the prefix, but only for keys allowed in
`${CLAUDE_PLUGIN_ROOT}/skills/profile-builder/SKILL.md` (never ID numbers, bank details, passwords, date of birth).
A `CV-TEXT` … `END-CV` section counts as the CV: run profile-builder on it.

## 5. Profile

Profile empty → next step for the user: "upload your CV and say: build my profile".
Filters missing `countries`, `salary_floor_*`, `needs_sponsorship` or `languages_spoken` → ask for them in one message.

## 6. Schedule by mode (Filters `mode`, default `off`)

Find the scheduling tools. List existing tasks; update one named `Career Autopilot` instead of adding a second.

| mode | schedule | prompt |
|---|---|---|
| active | daily at `run_time` (default 09:40) | `Run the Career Autopilot run (autopilot-run skill) in active mode for the "Career Autopilot Tracker" sheet.` |
| watch | weekly on `run_day` (default Sunday) at `run_time` | same prompt with `watch mode` |
| off | delete nothing; tell the user an existing task can be paused | — |

Use `CRON_TZ=<Filters timezone>`. The task needs the user's computer only in `active` mode (browser forms); `watch` can run in the cloud.
Turn on push notifications; email only if the user asked for the summary by email.
Write `autopilot_task` to Filters and say in one line when it runs and whether runs ask for approval.

## 7. Summary

The table, then one line: "Ready" when everything needed for the chosen mode passes, otherwise the single most important fix.
Do not change account settings yourself.
