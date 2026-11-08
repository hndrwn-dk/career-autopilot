---
name: career-autopilot-setup
description: "Career Autopilot plugin setup. This skill IS the setup: run it directly, never look for a repository, project folder or install step, and never fetch code from GitHub for it. Use when the user says \"set up career autopilot\", \"start career autopilot\", \"check my setup\", \"health check\", \"cek setup\", \"pasang career autopilot\", \"mulai cari kerja\", \"add a profile for my wife\", pastes a block starting with CAREER-AUTOPILOT-SETTINGS, or before the first job search. Sends the click-through onboarding page first, verifies connectors, creates the data store, sets the user's situation, field, work arrangement and countries, and schedules runs."
---

# Setup and health check

Data store: `${CLAUDE_PLUGIN_ROOT}/references/store.md`. In this skill "Filters" and "Profile" mean the store documents.

## Quick start: onboarding gate (always first, before anything else)

The user should be able to start in under two minutes by clicking, not typing. Do these steps in order:

1. **Load the Artifact tools** (store.md, section 1). Do this before deciding anything.
2. **Find the profile's dashboard** (store.md, section 2). If found, read `onboarding/answers` and `meta/summary`.
   - `onboarding/answers` missing, or `meta/summary` has no `onboarded: true` → onboarding is not done.
     Send the dashboard link with this one sentence (in English if the user writes in English):
     "Buka halaman ini, klik pilihan di tab Mulai, tekan Simpan, lalu Salin, dan tempel di sini."
     Then **stop**. No setup questions in chat, no job search, no multiple-choice question cards.
   - Onboarding done (`onboarded: true`) → the user is returning: continue with what they asked (a health check runs Full setup).
3. **No dashboard** → create it (career-autopilot-dashboard, Create), send the link with the same sentence, and **stop**.
4. **Chat fallback** only when the Artifact database tools are truly unavailable after a tool search. Say so in one line
   ("Halaman dashboard tidak bisa dibuat di sini, jadi saya tanya lewat chat."), then ask the three questions below.

**When the user comes back** with the pasted text ("Lanjutkan setup Career Autopilot dari dashboard" plus "Jawaban saya: …"),
or just "sudah" / "done": apply the answers (career-autopilot-dashboard, Onboarding answers), then continue at
"After onboarding" below.

**Chat fallback questions** (only in case 4). Ask three things in one friendly message:
1. What work they are looking for (any words: "admin", "jaga toko", "kerja dari rumah", "SRE").
2. Where: city or area, or remote.
3. Whether they have a CV (upload it) or want Claude to make one.
Infer `segment`, `preset` (an example or `none`) and `work_mode` from the answers and set `mode: off`.

**After onboarding.** Share the five simple scam rules from `${CLAUDE_PLUGIN_ROOT}/references/scam-signals.md`,
handle the CV (`cv: build` → career-autopilot-cv-builder; `cv: have` → ask for the file), create the schedule for the
chosen mode (step 9), and run career-autopilot-find-jobs once. Everything else (hours, schedule, voice sample) is asked
later, only when it changes a result ("Lowongan ini dibayar per jam; berapa minimal per jam yang Anda mau?").
Use Full setup only when the user asks for full setup or a health check, or pastes a settings block.

## Full setup

Speak plainly. Many users are not technical: explain a connector as "akses ke Gmail Anda supaya saya bisa membaca balasan
lamaran", not by tool name. Ask in small groups of questions, never one long form.
Run every step, never stop at the first failure, and finish with one table: Check | Status (OK / Missing / Error) | What to do.

## 0. Profiles (one account, several people)

Each profile has its own dashboard and store: `Career Autopilot` (default) or `Career Autopilot · <profile>`
(e.g. `· Siti`, `· Raka`). Setting up for someone else ("add a profile for my wife") → ask the profile name, create
that profile's dashboard, and send its link with the onboarding sentence. Drive files go under `Career Autopilot/<profile>/`.
The person whose data it is should agree to it being collected; when setting up for someone else, say so once.

## 1. Connectors

Load each tool (ToolSearch if deferred) and make one harmless read.

| Connector | Test | Needed for |
|---|---|---|
| Artifact tools with database | find the dashboard (store.md) | dashboard and all saved data (required for saving) |
| Gmail | search threads `newer_than:1d`, 1 result | recruiter mail, status sync, drafts |
| Google Drive | search files named "Career Autopilot" | CV file, shortlists, interview briefs, exports (optional) |
| Browser (built-in browser or Claude in Chrome) | list tabs | prefilling forms, sites without an API |
| Scheduling (scheduled-task tool) | tool present | `active` / `watch` runs |
| Google Calendar | list calendars | interview slots (optional) |

- Absent → Missing; say in plain words what it would let Claude do and how to add it. Offer a connector suggestion if that tool exists.
- Present but errors → Error; quote the error in one line.
- Gmail missing → no status sync or drafts in Gmail; drafts appear in the chat instead. Drive missing → CV and briefs stay in the chat.

## 2. Store

Make sure the profile's store has `settings/filters` and `settings/profile` (create empty documents if missing).
A legacy `Career Autopilot Tracker` sheet → import it once (store.md, section 6).

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
  Show it in plain words, apply edits, create the Drive file `Career Autopilot/presets/<name>.md` (shared by all profiles; to change it later, create a new file and point Filters to it) and set
  Filters `preset: custom:<name>`.
- `none` → career-autopilot-fit-check scores against each posting's own requirements.

Several presets: union `target_roles` and `keywords`, lowest `min_match`, weights of the first. Write only empty keys.

## 5. Work arrangement

Ask, if empty: remote, hybrid, onsite or any (`work_mode`); for onsite/hybrid, home area and `max_commute_minutes`;
`hours_per_week` and `schedule` if not full-time; `pay_unit` (hour/day/project/month) and `pay_floor`.
Salary floor per target country: for every country in `countries` (and `remote` if allowed) that has no
`salary_floor_<code>` yet, ask in one message for the minimum in that country's currency, showing the official default
next to each (from `${CLAUDE_PLUGIN_ROOT}/skills/career-autopilot-fit-check/references/filters.md`, Default salary floors; for Singapore the
MOM EP or S Pass qualifying salary when a work pass is needed, otherwise the Local Qualifying Salary). Save one
`salary_floor_<code>` line per country with the user's figure, or the default if they accept it.
When a country is added later ("cari juga di Jepang"), ask for its floor the same way before searching there.
Remote: ask which countries' employers they can legally work for (`remote_scope`) and their timezone overlap (`remote_timezones`).

## 6. Countries

If Filters has no `countries`, ask (any countries). For each, look it up in
`${CLAUDE_PLUGIN_ROOT}/skills/career-autopilot-find-jobs/references/sources.md`. Not listed → find its 2–3 main portals (official first)
with a web search, show them, save to Filters `country_portals`. Ask per country whether a work permit is needed (`needs_sponsorship`).

## 7. Settings block

A block from `CAREER-AUTOPILOT-SETTINGS` to `END-SETTINGS`: write every `key: value` line into Filters (overwriting).
`profile: <name>` selects or creates that profile first. Lines starting `profile.` go to Profile without the prefix, only
for keys career-autopilot-profile-builder allows. A `CV-TEXT` … `END-CV` section counts as the CV. A template users can copy:
`${CLAUDE_PLUGIN_ROOT}/settings-template.txt`.

## 8. Profile and writing voice

Profile empty → CV available: "upload your CV and say: build my profile". No CV: offer career-autopilot-cv-builder.
Ask once whether the user wants to paste 1–2 emails or messages they wrote, so drafts sound like them (`writing_sample`).

## 9. Schedule by mode (Filters `mode`, default `off`)

Find the scheduling tools. List existing tasks; update one named `Career Autopilot` (default profile) or
`Career Autopilot - <profile>` instead of adding another.

| mode | schedule | prompt |
|---|---|---|
| active | daily at `run_time` (default 09:40) | `Run the Career Autopilot run (career-autopilot-run skill) in active mode for profile "<profile or default>".` |
| watch | weekly on `run_day` (default Sunday) at `run_time` | same prompt with `watch mode` |
| off | delete nothing; tell the user an existing task can be paused | — |

Use `CRON_TZ=<Filters timezone>`. Only `active` mode needs the user's computer (browser forms).
Turn on push notifications; email only if the user asked. Write `autopilot_task` to Filters and say when it runs and whether runs ask for approval.

## 10. Dashboard

Add a row "Dashboard" with its link to the summary table (create it first if it does not exist).

## 11. Summary

The table, then one line: "Siap" / "Ready" when everything needed for the chosen mode passes, otherwise the single most important fix.
Do not change account settings yourself.
