---
name: setup
description: >
  Use when the user says "set up career autopilot", "start career autopilot", "check my setup",
  "health check", "cek setup", "pasang career autopilot", "mulai cari kerja", "add a profile for my wife",
  pastes a block starting with CAREER-AUTOPILOT-SETTINGS, or before the first job search. Verifies
  connectors, creates the tracker, sets the user's situation, field, work arrangement and countries,
  and schedules runs.
---

# Setup and health check

## Quick start (default for new users)

The user should be able to start in under two minutes. Ask only three things, in one friendly message:
1. What work they are looking for (any words: "admin", "jaga toko", "kerja dari rumah", "SRE").
2. Where: city or area, or remote.
3. Whether they have a CV (upload it) or want Claude to make one.

Then create the tracker if Drive is connected (otherwise run in chat-only mode), infer `segment`, `preset` (an example
or `none`) and `work_mode` from the answers, set `mode: off`, share the five simple scam rules from
`${CLAUDE_PLUGIN_ROOT}/references/scam-signals.md`, and run find-jobs once. Everything else (pay, hours, countries,
schedule, voice sample, autopilot) is asked later, only when it changes a result ("Lowongan ini dibayar per jam;
berapa minimal per jam yang Anda mau?"). Use the full steps below only when the user asks for full setup, a health
check, or pastes a settings block.

## Full setup

Speak plainly. Many users are not technical: explain a connector as "akses ke Gmail Anda supaya saya bisa membaca balasan
lamaran", not by tool name. Ask in small groups of questions, never one long form.
Run every step, never stop at the first failure, and finish with one table: Check | Status (OK / Missing / Error) | What to do.

## 0. Profiles (one account, several people)

The tracker is a sheet named `Career Autopilot Tracker` (default profile) or `Career Autopilot Tracker - <profile>`
(e.g. `- Siti`, `- Raka`). List sheets with these names.
- None → create the default one, unless the user is setting up for someone else ("for my wife") → ask the profile name.
- One → use it.
- Several → use the one the user or the scheduled prompt names; otherwise ask which.
Every other skill works on the active profile's tracker; Drive files go under `Career Autopilot/<profile>/` for named profiles.
The person whose data it is should agree to it being collected; when setting up for someone else, say so once.

## 1. Connectors

Load each tool (ToolSearch if deferred) and make one harmless read.

| Connector | Test | Needed for |
|---|---|---|
| Gmail | search threads `newer_than:1d`, 1 result | recruiter mail, status sync, drafts |
| Google Drive | search files named "Career Autopilot" | tracker, CV, presets, shortlists, interview briefs |
| Browser (built-in browser or Claude in Chrome) | list tabs | prefilling forms, sites without an API |
| Scheduling (scheduled-task tool) | tool present | `active` / `watch` runs |
| Google Calendar | list calendars | interview slots (optional) |

- Absent → Missing; say in plain words what it would let Claude do and how to add it. Offer a connector suggestion if that tool exists.
- Present but errors → Error; quote the error in one line.
- Gmail or Drive missing → the plugin still works in chat-only mode: shortlists and drafts in the conversation, no tracker. Say so.

## 2. Tracker sheet

Create the active profile's sheet if missing; otherwise add any missing tab or header.

| Tab | Columns |
|---|---|
| Applications | No, Company, Role, Location, Work Mode, Status, Channel, Employment Model, Applied On, Link, Job ID, Match %, Last Update, Next Action, Notes |
| Profile | Key, Value |
| Filters | Key, Value |
| Skip | Company, Role, Link, Reason, Date |
| Stories | Id, Title, Situation, Task, Action, Result, Skills, Source |

## 3. Situation (segment)

If Filters has no `segment`, ask one plain question, e.g. "Mana yang paling sesuai dengan Anda sekarang?":
sudah bekerja/berpengalaman · baru lulus atau masih kuliah · ingin kembali bekerja setelah jeda · cari kerja sampingan, paruh waktu atau freelance · pindah ke bidang baru.
Map to `experienced`, `fresh-graduate`, `career-returner`, `side-income`, `career-switcher`.
Read `${CLAUDE_PLUGIN_ROOT}/segments/<segment>.md` and write its "Filters defaults" into empty Filters keys.

## 4. Field (preset)

Format and locations: `${CLAUDE_PLUGIN_ROOT}/presets/README.md`.

If Filters has no `preset`, ask what kind of work the user wants (any field, any level). Then:
- An example in `${CLAUDE_PLUGIN_ROOT}/presets/examples/` fits → offer it as is, or as a custom copy the user can adjust.
- Otherwise, or if the user asks for `custom` → draft one from `${CLAUDE_PLUGIN_ROOT}/presets/_template.md`, from the
  work the user names, their CV (if any) and 2–3 web searches on how such postings are worded in their target countries.
  Show it in plain words, apply edits, save to Drive `Career Autopilot/presets/<name>.md` (shared by all profiles) and set
  Filters `preset: custom:<name>`.
- `none` → fit-check scores against each posting's own requirements.

Several presets: union `target_roles` and `keywords`, lowest `min_match`, weights of the first. Write only empty keys.

## 5. Work arrangement

Ask, if empty: remote, hybrid, onsite or any (`work_mode`); for onsite/hybrid, home area and `max_commute_minutes`;
`hours_per_week` and `schedule` if not full-time; `pay_unit` (hour/day/project/month) and `pay_floor`.
No salary floor from the user → propose the official default for each country from
`${CLAUDE_PLUGIN_ROOT}/skills/fit-check/references/filters.md` (Default salary floors; for Singapore the MOM EP or S Pass
qualifying salary when a work pass is needed, otherwise the Local Qualifying Salary), with its source, and save it once the user agrees.
Remote: ask which countries' employers they can legally work for (`remote_scope`) and their timezone overlap (`remote_timezones`).

## 6. Countries

If Filters has no `countries`, ask (any countries). For each, look it up in
`${CLAUDE_PLUGIN_ROOT}/skills/find-jobs/references/sources.md`. Not listed → find its 2–3 main portals (official first)
with a web search, show them, save to Filters `country_portals`. Ask per country whether a work permit is needed (`needs_sponsorship`).

## 7. Settings block

A block from `CAREER-AUTOPILOT-SETTINGS` to `END-SETTINGS`: write every `key: value` line into Filters (overwriting).
`profile: <name>` selects or creates that profile first. Lines starting `profile.` go to Profile without the prefix, only
for keys profile-builder allows. A `CV-TEXT` … `END-CV` section counts as the CV. A template users can copy:
`${CLAUDE_PLUGIN_ROOT}/settings-template.txt`.

## 8. Profile and writing voice

Profile empty → CV available: "upload your CV and say: build my profile". No CV: offer cv-builder.
Ask once whether the user wants to paste 1–2 emails or messages they wrote, so drafts sound like them (`writing_sample`).

## 9. Schedule by mode (Filters `mode`, default `off`)

Find the scheduling tools. List existing tasks; update one named `Career Autopilot` (default profile) or
`Career Autopilot - <profile>` instead of adding another.

| mode | schedule | prompt |
|---|---|---|
| active | daily at `run_time` (default 09:40) | `Run the Career Autopilot run (autopilot-run skill) in active mode for profile "<profile or default>".` |
| watch | weekly on `run_day` (default Sunday) at `run_time` | same prompt with `watch mode` |
| off | delete nothing; tell the user an existing task can be paused | — |

Use `CRON_TZ=<Filters timezone>`. Only `active` mode needs the user's computer (browser forms).
Turn on push notifications; email only if the user asked. Write `autopilot_task` to Filters and say when it runs and whether runs ask for approval.

## 10. Summary

The table, then one line: "Siap" / "Ready" when everything needed for the chosen mode passes, otherwise the single most important fix.
Do not change account settings yourself.
