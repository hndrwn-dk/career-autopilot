# Career Autopilot

A Claude plugin that helps anyone look for work: an experienced professional, a fresh graduate, a parent going back
to work after years at home, someone who wants a few hours of side income, or a person changing fields. You set the
situation, the field, the countries and whether the work is remote or onsite; the plugin adapts.

It finds jobs, checks how well they fit, skips scams, prefills application forms in your own browser (you press Submit),
writes emails that sound like you (you press Send), follows replies in Gmail, makes a CV if you do not have one, and
prepares you for interviews.

Nothing about you is in the plugin. Your data stays in your own private dashboard on claude.ai (and, if you want, exports in your own Google Drive), so anyone can install it.

## What makes it different

| | |
|---|---|
| For everyone | Five situations (segments) change scoring, sources and tone: `experienced`, `fresh-graduate`, `career-returner`, `side-income`, `career-switcher`. A fresh graduate is scored on education and projects, not years; a returner's career break is not penalised; side income is scored on schedule, pay per hour and safety. |
| Any field | Example presets for finance, nursing, marketing, supply chain and tech, plus custom presets Claude drafts for any other field. |
| Any country, any work mode | Remote, hybrid or onsite, with commute limit, hours per week, schedule and pay per hour, day, project or month. Built-in sources for Singapore, APAC, EMEA and US/Canada; other countries' portals are found on first use. |
| Account safety | A reminder mode for LinkedIn, JobStreet, Indeed, Upwork and similar platforms: you confirm the risk once, Claude stays under daily caps, warns at 80%, and pauses at the first warning sign. |
| Scam guard | "Agents" who ask you to pay first, like or comment first, join a paid class or install an app are skipped automatically, along with task scams, money-mule and reshipping jobs, pay-to-join schemes, fake government recruitment, and overseas offers that match trafficking patterns. Paste any offer you received and ask "ini penipuan bukan?". |
| No hassle | Click-through onboarding: Claude sends a private page where you answer by clicking (no typing), then press Save and Copy and paste the copied text into the chat. Nothing else is asked until it changes a result. Works in chat only if you do not connect Gmail or Drive. |
| Sounds like you | Every email, reply and cover letter follows a writing guide that removes AI-sounding patterns, and can match a sample of your own writing. |
| No CV needed | `career-autopilot-cv-builder` interviews you in plain language and makes a CV, including an honest line for a career break if you want one. |
| Watch mode | Already employed? A weekly digest of only the strongest matches, nothing filled in. |
| Honest flags | Contract-via-agency, vendor placement, undefined "conversion to permanent", hidden client, licence conversion needed, title that does not match the duties. |
| Family use | Several profiles on one account (`Career Autopilot · <name>`), each with its own dashboard, data and schedule. |
| Dashboard | A private page per profile with three tabs: Start (click-through onboarding), Dashboard (pipeline, next actions, platform usage, scams skipped, kept in sync after every run) and Quick commands (buttons that copy a command to paste into Claude). |
| Interview prep | A brief per interview plus a mock interview, adapted to the situation (online tests for graduates, a short break explanation for returners, a call script for side jobs). |

## Install

Claude desktop app: **Customize → Plugins → Add marketplace** → `hndrwn-dk/career-autopilot` → install **Career Autopilot**.
Or upload `career-autopilot.plugin` on the same page.

Claude Code:

```
/plugin install career-autopilot --marketplace hndrwn-dk/career-autopilot
```

## Update

Installed from the marketplace: **Customize → Plugins → Career autopilot → ⋯ → Check for updates → Update**. No need to remove and reinstall. Check that the version number changed.
Installed from a `.plugin` file: upload the new file on the same page.

Skills are all named `career-autopilot-…` (for example `/career-autopilot-setup`), so they never clash with other plugins.

## Enable the browser (for filling in forms)

Searching, fit checks, scam checks and email drafts work without a browser. Prefilling application forms needs one of these:

- **Built-in browser** in the Claude desktop app: nothing to install; allow each job site when asked. It is rolling out gradually.
- **Claude in Chrome**: install it from the Chrome Web Store ("Add to Chrome"), sign in with the same Claude account and pin it. Then in the Claude desktop app open **Settings → Connectors → Claude in Chrome → Configure** and turn it on. Desktop Google Chrome only.

Keep the browser (and, for scheduled `active` runs, the Claude desktop app) open while Claude works, and sign in to job sites yourself.

## First run

Quick start: say **"mulai cari kerja"** (or pick **career-autopilot-setup** from the `/` menu). Claude sends only a link to your private dashboard: click your answers in the Start tab, press **Simpan**, then **Salin**, and paste the copied text into the chat. Claude then shows matching jobs and asks for anything else only when it matters. If the dashboard cannot be created in your Claude app, Claude asks the same questions in chat.

Full setup:

1. Say **"mulai cari kerja"** or **"set up career autopilot"**, or pick **career-autopilot-setup** from the `/` menu. Claude sends your dashboard link first; after onboarding it checks Gmail, Google Drive and the browser.
2. Answer a few plain questions: your situation, the kind of work, remote or onsite, hours, pay, countries.
3. Upload your CV and say **"build my profile"**, or say **"buatkan CV"** if you do not have one.
4. Optional: paste 1–2 emails you wrote so drafts sound like you.
5. Optional: fill `plugins/career-autopilot/settings-template.txt` and paste it to set everything at once.

## Workflow

Chat is where you ask; the dashboard is where you look. Every button on the dashboard copies a command to paste into the chat.

1. Once: install the plugin and connect Gmail (and Google Drive if you like).
2. New chat: type **mulai cari kerja**. Claude replies with your dashboard link.
3. Dashboard, Start tab: click your answers, press **Simpan**, then **Salin**.
4. Chat: paste the copied text and attach your CV (or ask Claude to make one). Claude finds matching jobs.
5. Dashboard: new jobs, statuses and next actions appear by themselves.
6. Dashboard: press **Apply** on a job card, paste in the chat. Claude fills in the form in your browser; you check it and press Submit.
   Interview invite? Press **Interview prep** on the card and paste.

Steps 5 and 6 repeat as new jobs come in.

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
| "check my application emails" | statuses updated in your dashboard, next actions, scams listed separately |
| "buatkan CV" | CV made by interview, saved to your Drive if connected |
| "prep me for the <company> interview" | interview brief and mock interview |
| "add a profile for my wife" | a separate dashboard and settings for another person |
| "buka dashboard" / "open my dashboard" | your private dashboard: pipeline, next actions, platform safety, scams skipped |

## Where your data lives

Everything Career Autopilot remembers about you (profile, settings, jobs, stories, onboarding answers) is stored in the
database of your private dashboard page on claude.ai. Every skill reads and writes it there with Claude's Artifact
tools, which every claude.ai user has, so saving works without any extra connector.

- Profile, settings, stories and onboarding answers are readable only by you, even if you share the dashboard link.
- Google Drive is optional. It holds files: your CV, shortlists, interview briefs and exports. The Drive connector can
  create or replace whole files but cannot add rows to a Google Sheet, so Career Autopilot never keeps its data in a Sheet.
- "export my tracker" / "ekspor data saya" creates a new CSV file in Drive (`Career Autopilot/<profile>/tracker-<date>.csv`).
- If something cannot be saved, Claude says so once in the reply instead of pretending it worked.
- An older `Career Autopilot Tracker` sheet from a previous version is imported once and then left alone.

## New-user smoke test

Run this after every change to setup or onboarding:

1. Use a fresh account, or a new profile: say **"add a profile for Test"**.
2. In a new chat, type **"mulai cari kerja"**.
   Expected: only the dashboard link and one sentence ("Buka halaman ini, klik pilihan di tab Mulai, tekan Simpan, lalu Salin, dan tempel di sini."). No questions in chat, no job search.
3. Open the link, answer the 9 questions in the Start tab, press **Simpan**, then **Salin**.
4. Paste the copied text into the chat.
   Expected: Filters filled from your answers (Claude lists them), the dashboard's Start tab no longer opens by default, and a first shortlist appears in the chat and in the Dashboard tab.
5. Type **"cari lowongan"** in a profile whose onboarding is not finished.
   Expected: the dashboard link again, not a search.

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
