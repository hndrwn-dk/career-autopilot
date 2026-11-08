---
name: career-autopilot-fit-check
description: "Use when the user asks \"is this job a fit\", \"check this job\", \"how well do I match\", \"cek kecocokan\", \"cocok gak\", pastes a job link, description or a chat message with a job offer, asks \"apakah ini penipuan?\", \"ini scam bukan?\", \"is this offer legit\", or when career-autopilot-find-jobs or career-autopilot-run needs to score a posting against the profile and filters."
---

# Check fit

Load `Profile` and `Filters`. Keys: `references/filters.md`. If Filters has `preset`, read each one for skill groups,
credential equivalents and field-specific checks: example names from `${CLAUDE_PLUGIN_ROOT}/presets/examples/<name>.md`,
`custom:<name>` from the user's Drive `Career Autopilot/presets/<name>.md`. A preset file that cannot be read: continue
without it and say so. No preset: derive skill groups from the posting itself.

## 0. Scam check

Apply `${CLAUDE_PLUGIN_ROOT}/references/scam-signals.md` before anything else. An exclude signal ends the check: log to `Skip`, tell the user plainly.

## 1. Hard filters (any hit → exclude with the reason)

Read the full description:
- Required language the user does not speak. "Nice to have" is not a blocker; mention it.
- Work rights the user cannot meet ("citizens/PR only", "no sponsorship", "must hold a valid work pass", "security clearance required") when Profile says they need sponsorship there.
- Posted pay below the user's floor for the posting's country: `salary_floor_<country code>`, else the region key (e.g. `eu`), else `salary_floor_remote` for remote roles, else `pay_floor` in `pay_unit`. Compare in the posting's currency; convert only with a rate looked up that day and say so. No floor at all for that country → do not exclude on pay; ask the user for one (career-autopilot-setup step 5). Convert units only when the posting gives hours or days; otherwise compare like with like and flag when unsure.
- Work arrangement outside `work_mode`: e.g. onsite-only when the user wants remote; hybrid/onsite beyond `max_commute_minutes` from the user's area (estimate with a quick map or transit lookup when the address is given).
- Remote roles restricted to countries or timezones outside `remote_scope` / `remote_timezones` ("US residents only", "must overlap 9–5 EST").
- Hours or schedule that cannot fit `hours_per_week` / `schedule` (e.g. weekend shifts when the user said weekdays only).
- A professional licence or registration the posting requires in that country (e.g. nursing, medical, legal, engineering, teaching, accounting) that Profile does not hold → exclude when it is a must-hold now; flag "licence conversion needed" when it can be obtained after hire.
- Seniority outside `seniority`, or title words in `exclude_keywords`.
- Employment model not allowed by `employment_types` (see 2).
- Company in `exclude_companies`, already in `Applications` or `Skip`, posting closed.
- Posting forbids AI assistance in applications → do not prefill; tell the user to apply personally.

## 2. Employment model

Classify: `permanent` · `contract (direct)` · `contract via agency` · `vendor placement` (on a client's site through a vendor) · `part-time` · `freelance / project` · `casual / gig` · `internship` · `graduate programme` · `returnship`.
Work mode: `remote` · `hybrid` · `onsite`; note the remote scope when stated.
Flag, do not exclude, unless `employment_types` rules it out:
- Promised "conversion to permanent" with no timeframe or criteria → flag "conversion not defined".
- Agency posting with the client hidden → flag "client unknown".
- Contract shorter than `min_contract_months`.

## 3. Match score (0–100)

Weights from Filters `weights`, else the segment file's Scoring (`${CLAUDE_PLUGIN_ROOT}/segments/<segment>.md`), else the preset's, else `must_have:45, years:15, stack:20, certs:10, domain:5, scope:5`.
Segment-only components (education, projects, flexibility, schedule_fit, pay, safety, transferable) are defined in the segment file.
- must_have: share of required items proven by Profile. Any "required/must/essential" item that is missing caps the total at 70.
- years: Profile years vs. requested years for the main skill.
- stack: skills, tools and methods; overlap per skill group from the preset (a group counts once), else per named item.
- certs: certifications, licences and registrations held, or covered by an equivalent from the preset.
- domain: industry or sector overlap.
- scope: seniority, team size, customer-facing vs. internal match the profile.

Only facts in Profile count. A credential proves the skill exists, not years of use.

## 4. Report

Score · work mode and pay in one line · 2–3 strongest matches · every gap stated plainly ("asks for 3+ yrs Go; profile shows none") · flags · work-pass note (section 5).
Recommend applying when the score ≥ `min_match` (in `watch` mode: ≥ `watch_min_match`, default 88) and there is no hard-filter hit.

## 5. Work-pass note

When the posting is in a country where Profile says the user needs sponsorship, add the rule from `references/filters.md`.
When the outcome depends on a threshold (salary minimum, points), say so and check the current rule with one web search instead of quoting a number from memory.
