# Career Autopilot

A Claude plugin that helps anyone look for work: an experienced professional, a fresh graduate, a parent going back
to work after years at home, someone who wants a few hours of side income, or a person changing fields. You set the
situation, the field, the countries and whether the work is remote or onsite; the plugin adapts.

It finds jobs, checks how well they fit, skips scams, prefills application forms in your own browser (you press Submit),
writes emails that sound like you (you press Send), follows replies in Gmail, makes a CV if you do not have one, and
prepares you for interviews.

Nothing about you is in the plugin. Your data stays in your own Google Sheet and Drive, so anyone can install it.

## What makes it different

| | |
|---|---|
| For everyone | Five situations (segments) change scoring, sources and tone: `experienced`, `fresh-graduate`, `career-returner`, `side-income`, `career-switcher`. A fresh graduate is scored on education and projects, not years; a returner's career break is not penalised; side income is scored on schedule, pay per hour and safety. |
| Any field | Example presets for finance, nursing, marketing, supply chain and tech, plus custom presets Claude drafts for any other field. |
| Any country, any work mode | Remote, hybrid or onsite, with commute limit, hours per week, schedule and pay per hour, day, project or month. Built-in sources for Singapore, APAC, EMEA and US/Canada; other countries' portals are found on first use. |
| Account safety | A reminder mode for LinkedIn, JobStreet, Indeed, Upwork and similar platforms: you confirm the risk once, Claude stays under daily caps, warns at 80%, and pauses at the first warning sign. |
| Scam guard | "Agents" who ask you to pay first, like or comment first, join a paid class or install an app are skipped automatically, along with task scams, money-mule and reshipping jobs, pay-to-join schemes, fake government recruitment, and overseas offers that match trafficking patterns. Paste any offer you received and ask "ini penipuan bukan?". |
| No hassle | Three questions to start; nothing else is asked until it changes a result. Works in chat only if you do not connect Gmail or Drive. |
| Sounds like you | Every email, reply and cover letter follows a writing guide that removes AI-sounding patterns, and can match a sample of your own writing. |
| No CV needed | `career-autopilot-cv-builder` interviews you in plain language and makes a CV, including an honest line for a career break if you want one. |
| Watch mode | Already employed? A weekly digest of only the strongest matches, nothing filled in. |
| Honest flags | Contract-via-agency, vendor placement, undefined "conversion to permanent", hidden client, licence conversion needed, title that does not match the duties. |
| Family use | Several profiles on one account (`Career Autopilot Tracker - <name>`), each with its own tracker, CV and schedule. |
| Dashboard | A private page per profile with the pipeline, next actions, platform usage and scams skipped, kept in sync by Claude after every run. |
| Interview prep | A brief per interview plus a mock interview, adapted to the situation (online tests for graduates, a short break explanation for returners, a call script for side jobs). |

## Install

Claude desktop app: **Customize → Plugins → Add marketplace** → `hndrwn-dk/career-autopilot` → install **Career Autopilot**.
Or upload `career-autopilot.plugin` on the same page.

Claude Code:

```
/plugin install career-autopilot --marketplace hndrwn-dk/career-autopilot
```

## Enable the browser (for filling in forms)

Searching, fit checks, scam checks and email drafts work without a browser. Prefilling application forms needs one of these:

- **Built-in browser** in the Claude desktop app: nothing to install; allow each job site when asked. It is rolling out gradually.
- **Claude in Chrome**: install it from the Chrome Web Store ("Add to Chrome"), sign in with the same Claude account and pin it. Then in the Claude desktop app open **Settings → Connectors → Claude in Chrome → Configure** and turn it on. Desktop Google Chrome only.

Keep the browser (and, for scheduled `active` runs, the Claude desktop app) open while Claude works, and sign in to job sites yourself.

## First run

Quick start: say **"mulai cari kerja"** (or pick **career-autopilot-setup** from the `/` menu) and answer three questions (what work, where or remote, CV or no CV). Claude shows matching jobs right away and asks for anything else only when it matters.

Full setup:

1. Say **"mulai cari kerja"** or **"set up career autopilot"**, or pick **career-autopilot-setup** from the `/` menu. Claude checks Gmail, Google Drive and the browser and creates your tracker.
2. Answer a few plain questions: your situation, the kind of work, remote or onsite, hours, pay, countries.
3. Upload your CV and say **"build my profile"**, or say **"buatkan CV"** if you do not have one.
4. Optional: paste 1–2 emails you wrote so drafts sound like you.
5. Optional: fill `plugins/career-autopilot/settings-template.txt` and paste it to set everything at once.

## Modes

| Mode | For | What it does |
|---|---|---|
| `active` | actively looking | daily run: inbox sync, new jobs, forms prefilled up to Submit |
| `watch` | employed, open to the right offer | weekly run: only very strong matches, no forms filled, a short digest |
| `off` | not looking | nothing scheduled; commands still work on demand |

## Daily use

| Say | What happens |
|---|---|
| "find jobs" / "cari lowongan" / "cari kerja sampingan dari rumah" | ranked shortlist with match %, work mode, pay and reasons |
| "check this job: <link>" | fit check with gaps, blockers, scam check and flags |
| "ini penipuan bukan?" + a pasted WhatsApp/email offer | scam check with the reason, in plain words |
| "apply to 1 and 3" | forms prefilled in the browser; you tick consents and submit |
| "draft an email for this job" / "balas email HRD ini" | Gmail draft in your voice; sent only when you say so |
| "check my application emails" | tracker statuses updated, next actions, scams listed separately |
| "buatkan CV" | CV made by interview, saved to your Drive |
| "prep me for the <company> interview" | interview brief and mock interview |
| "add a profile for my wife" | a separate tracker and settings for another person |
| "buka dashboard" / "open my dashboard" | your private dashboard: pipeline, next actions, platform safety, scams skipped |

## Settings

Every key is documented in `plugins/career-autopilot/skills/career-autopilot-fit-check/references/filters.md`.
Segments: `plugins/career-autopilot/segments/`. Presets: `plugins/career-autopilot/presets/`.

## What always stays with you

Passwords and logins, consent and terms checkboxes, diversity questions, date of birth, home address, ID numbers, payments, the final Submit, and sending email.

## Account safety on LinkedIn and similar platforms

LinkedIn, JobStreet/JobsDB, SEEK, Indeed, Glassdoor, Glints, Kalibrr, Naukri, XING, Upwork, Fiverr and similar platforms mostly prohibit automation and can restrict accounts. Career Autopilot always runs them in account-safety mode:

- a reminder before first use of each platform, which you confirm (repeated every 30 days)
- read-only browsing in your own signed-in browser, one page at a time with pauses
- low daily caps per platform (12 job descriptions, 5 search pages, 3 quick-apply prefills), with a heads-up at 80%
- an immediate 48-hour pause on that platform at any CAPTCHA, "unusual activity" message or limit warning
- no automated messages, connection requests, likes, comments or marketplace proposals: Claude drafts, you send
- unattended runs use only the platforms you list in `use_platforms`, at half the caps

Sources without an account (company career sites, official portals, remote boards) are always tried first.

## License

MIT © Tursina Labs. See `LICENSE`.
