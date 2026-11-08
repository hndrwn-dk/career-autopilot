---
name: profile-builder
description: "Use when the user uploads or shares a CV/resume and says \"build my profile\", \"read my CV\", \"update my profile\", \"baca CV saya\", \"buat profil dari CV\", \"add a story\", or when another Career Autopilot skill needs profile data that is missing."
---

# Build the profile from a CV

The Profile tab is the only source for anything written into a form, email or interview answer.
Write only what the CV says or the user states. Never infer years, tools, degrees, salaries, visa status or certifications.

## Keys

Source: CV = from the CV · ask = ask the user · calc = computed from CV dates.

| Key | Source | Note |
|---|---|---|
| full_name, email | CV | |
| phone_default, phone_<region> | ask | e.g. phone_sg |
| location_current | CV/ask | city, country |
| nationality | ask | only used for work-authorization answers |
| work_auth_<country> | ask | e.g. work_auth_singapore: "Employment Pass holder, needs new EP for a new employer" — exact words from the user |
| needs_sponsorship_outside | ask | yes/no |
| linkedin_url, github_url, portfolio_urls | CV/ask | open each once to confirm it resolves |
| headline | CV | one line |
| years_total | calc | |
| years_<skill> | calc | show the arithmetic per skill so the user can correct it |
| skills | CV | comma list |
| certifications | CV | one per line: name, issuer, year if given |
| roles | CV | one line per role: title, company, city, start–end, employment model (permanent / contract via agency / vendor placement) |
| achievements_<n> | CV | one quantified achievement per key |
| education | CV | school, qualification, field, years; note equivalents only if the user states them |
| languages | CV/ask | with level |
| notice_period | ask | |
| salary_floor_<region> | ask | e.g. salary_floor_sg: SGD 5,600/month. If the user has no figure, propose the official default from `fit-check/references/filters.md` (Default salary floors), say which rule it is, and let them raise it |
| current_salary | ask, optional | only if the user wants forms to show it |
| preferred_employment | ask | permanent / contract / either |
| willing_to_relocate | ask | |
| cv_default, cv_<label> | auto/ask | file name in Drive plus a one-line "use for" note |
| facts_confirmed | ask | extra facts the user confirmed |
| career_break | ask, optional | dates and the user's own one-line description; nothing beyond what they say |
| availability_note | ask | e.g. "weekdays 9-2, can start next month" |
| writing_sample | ask, optional | 1–2 messages the user wrote, for voice matching |
| tone | ask, optional | e.g. formal, friendly, Bahasa Indonesia baku |
| portfolio_links | ask, optional | Drive or web links to work samples |

Never store: ID or passport numbers, bank or card details, passwords, date of birth, gender, marital status, number or ages of children, religion, health. A full home address never goes in; `home_area` (district or city) is enough.

## Steps

0. No CV, or the user says it is old → offer cv-builder instead; it fills the Profile at the end.
1. Read the CV. Extract the keys above. Read the segment file (`${CLAUDE_PLUGIN_ROOT}/segments/<segment>.md`, section Profile) for what matters most for this user.
2. Show a compact table plus the arithmetic lines, and list every empty `ask` key. Ask for them in one message.
3. After the user confirms, write to `Profile` (overwrite only changed keys).
4. Save the CV in Drive folder `Career Autopilot/CV` if missing; set `cv_default`.
5. Turn each strong achievement into a STAR row in `Stories` (Situation, Task, Action, Result, Skills) using only CV facts; mark `Source: CV`. Ask the user to fill any missing Result numbers rather than inventing them.
6. Suggest target roles and keywords that the CV supports, in whatever field the CV is in. If no preset is set, offer an example preset that fits or a custom preset (setup step 3).

## Several CVs

Store each as `cv_<label>` with when to use it (e.g. `cv_tam: customer-facing roles`). apply-assist picks by role.
