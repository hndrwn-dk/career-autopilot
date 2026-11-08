---
name: dashboard
description: "Use when the user says \"open my dashboard\", \"buka dashboard\", \"show my job search\", \"lihat progres lamaran\", \"update my dashboard\", \"dashboard saya\", or at the end of setup. Creates the user's private Career Autopilot dashboard page once, and keeps it in sync with the tracker. Other skills call this skill's \"Sync\" section."
---

# Dashboard

A private web page for the user (one per profile) showing their pipeline, next actions, platform safety and scams
skipped. It is a claude.ai artifact made from `assets/dashboard.html`; its data lives in the artifact's database and
Claude writes it. The tracker sheet stays the source of truth; the dashboard mirrors it.

Needs the Artifact tool with database access (on claude.ai: publish, declare capabilities, and the db write/read
actions, e.g. `db_write` / `db_get` or the Artifact tool's `write_db` / `read_db`). If these tools are not available
(for example in Claude Code), say once that the dashboard is not available here and point the user to the tracker sheet.

## Create (once per profile)

1. Filters has `dashboard_url` → it exists: open it with the Artifact tool and go to Sync. If it no longer loads, recreate.
2. Copy `${CLAUDE_PLUGIN_ROOT}/skills/dashboard/assets/dashboard.html` to the working folder unchanged. Publish it as a new
   artifact: title `Career Autopilot` (default profile) or `Career Autopilot · <profile>`, icon `chart`.
3. Declare its capabilities as exactly:
   `{"db":{"rules":[{"path":"","read":"view","write":"owner"}]},"user":{}}`
   (only the owner, through Claude, writes; the page itself never writes).
4. Save the returned URL to Filters `dashboard_url`, then run Sync with every row of the tracker.
5. Tell the user in one line: the dashboard is private to them; they can open it any time or say "buka dashboard".

## Data written (never anything else)

| Path | Fields |
|---|---|
| `jobs/<id>` | `company`, `role`, `city`, `country`, `work_mode` (remote/hybrid/onsite), `pay` (as posted, short), `model` (employment model), `status`, `match` (0–100), `channel`, `link` (https posting URL), `next_action`, `flags` (up to 3 short strings), `reason` (skip/scam reason, short), `source`, `updated` (ISO time with offset) |
| `meta/summary` | `profile`, `mode`, `segment`, `language` (`id`/`en`), `tracker_url`, `last_run`, `next_run`, `scams_skipped_total`, `skipped_total`, `platforms` (`{"<name>":{"used":n,"cap":n,"paused_until":"ISO or empty"}}`, today only) |
| `meta/run` | `state` (`running`/`idle`), `activity` (one short line), `updated` |

`<id>`: `<company>-<role>` lowercased, every character outside `a-z0-9` replaced by `-`, collapsed, at most 120 characters. Keep the id for the life of the job.

`status` values: `worth_a_look`, `queued`, `ready`, `submitted`, `in_review`, `assessment`, `interview`, `offer`, `rejected`, `withdrawn`, `closed`, `skipped`, `scam`.
Map tracker statuses: Ready to submit → `ready`; Needs manual apply → `queued` with next_action; Submitted, In Review, Assessment, Interview, Offer, Rejected, Withdrawn, Closed → same words in snake_case.

Privacy: never write phone numbers, emails, addresses, salary floors, current salary, CV contents, recruiter names or
anything from Profile beyond `profile`, `segment` and `language`. `pay` is only what the posting itself states.

## Sync (called by other skills)

- Write `meta/run` `running` with the step ("Mencari lowongan · MyCareersFuture") at the start of find-jobs, apply-assist batches and autopilot-run; `idle` with a one-line result at the end.
- After find-jobs: every shortlisted posting as `worth_a_look` (with match, flags, next_action "Cek dan putuskan apply"); excluded postings as `skipped`, scams as `scam`, each with `reason`. Only the most recent 100 skipped/scam rows; delete older ones.
- After apply-assist / autopilot-run prefill: `ready` with next_action naming the tab and what is left; after the user confirms: `submitted`.
- After inbox-sync: the new status and next_action for each matched row.
- `meta/summary`: update counts, `last_run`, `next_run` (from the scheduled task), and today's platform usage from Filters `platform_usage_*` / `platform_pause_*`.
- Keep at most 500 `jobs` documents: delete `rejected`/`closed`/`withdrawn` rows older than 60 days first.
- Batch writes (one call for many documents where the tool allows). For a document that exists, pass its current version if the tool asks for one.
- A dashboard write failure never stops the main task: note it once and continue.
