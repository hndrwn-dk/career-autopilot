# Job platforms with accounts: account-safety mode

Applies to every site where the user is signed in with a personal account: LinkedIn and similar job networks,
job portals with profiles, and freelance marketplaces. Most of them prohibit bots, scraping or automated actions in
their terms, and can warn, limit or ban an account. The user's account is what is at risk, so this mode is always on.

## Platforms covered

| Group | Platforms |
|---|---|
| Professional networks | LinkedIn, XING (DACH), Wellfound (startups) |
| Job portals with profiles | JobStreet / JobsDB, SEEK, Indeed, Glassdoor, Glints, Kalibrr, Naukri, StepStone, Monster, ZipRecruiter, Dice, Bayt, FastJobs |
| Freelance marketplaces | Upwork, Fiverr, Freelancer, Contra, Sribulancer, Projects.co.id, Fastwork |
| Official portals with login | MyCareersFuture (Singpass), national portals that need an account |

Any other site the user signs in to for job search counts too.

## Reminders (the "pengingat")

Show these in the user's language, briefly, never as a wall of text:
1. **First use of a platform in a session**: "<Platform> melarang otomasi di syarat penggunaannya. Saya akan bekerja pelan di browser Anda, membaca saja, dan berhenti kalau ada peringatan. Risikonya ada di akun Anda. Lanjut?" Wait for yes. Record `platform_ack_<platform>: <date>` in Filters; repeat the reminder after 30 days.
2. **At 80% of a daily cap**: "Hari ini sudah 32 dari 40 lowongan LinkedIn yang saya buka. Sisanya besok, supaya akun Anda aman."
3. **Cap reached**: stop that platform for the day and say so in the summary.
4. **Any warning sign** (CAPTCHA, "unusual activity", "you've reached the limit", forced logout, HTTP 429, a verification step): stop that platform at once, for 48 hours (`platform_pause_<platform>: <until>`), and tell the user what appeared. Never try to get around it.

## Rules for every account platform

- Only in the user's own browser, signed in by the user. Claude never types a password, never creates accounts, never solves CAPTCHAs.
- Read-only by default: search pages and job descriptions. No bulk scraping of profiles, no exporting contacts.
- One page at a time, never parallel tabs on the same platform. Wait 4–10 seconds between page loads, varied, and a longer pause every 10 pages.
- No calls to undocumented internal endpoints in loops; read what the page shows.
- Daily caps (conservative defaults chosen by this plugin, not limits published by the platforms; change in Filters `platform_caps`):

| Action | Default cap per platform per day |
|---|---|
| Job descriptions opened | 40 (LinkedIn), 60 (other portals) |
| Search result pages | 15 |
| Applications prefilled (Easy Apply / quick apply) | 5 |
| Messages, connection requests, proposals | 0 automated; Claude drafts, the user sends |

- Unattended runs (`autopilot-run`) use account platforms only when Filters `use_platforms` lists them, at half the caps above.
- Never: mass connection requests, auto-endorsements, auto-likes or comments, profile-view bots, bulk messaging, or sending marketplace proposals. Claude writes the text; the user posts it.
- Spread work out: prefer a short daily session over one long one.
- Prefer sources without an account first (company ATS boards, official portals' public search, remote boards). Account platforms fill the gaps.

## Counters

Keep `platform_usage_<platform>: <date> opened=<n> searches=<n> prefilled=<n>` in Filters, updated as work happens, reset each day.
Paused platforms (`platform_pause_*` in the future) are skipped silently in runs and named once in the summary.

## LinkedIn specifics

- Search page: `https://www.linkedin.com/jobs/search/?keywords=<kw>&geoId=<geo>&f_TPR=r604800` (past week; `r86400` = 24h).
- geoIds (confirm once by opening the search and reading the location label): Singapore 102454443 · Indonesia 102478259 · Malaysia 106808692 · Australia 101452733 · Japan 101355337 · UAE 104305776 · Germany 101282230 · Netherlands 102890719 · United Kingdom 101165590 · United States 103644278 · Canada 101174742. Other countries: read the geoId from the URL of a country search.
- Easy Apply counts toward the prefill cap; the user presses Submit.
