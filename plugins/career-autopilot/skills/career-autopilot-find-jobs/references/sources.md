# Job sources

Space requests at least 1 second apart. If a fetch tool refuses a host, try the same URL from a tab in the
user's browser with `fetch()`; if that fails too, note the source as unavailable and move on. Never work around a site that blocks access.

## Public ATS job board APIs (no login)

| ATS | List endpoint | Notes |
|---|---|---|
| Greenhouse | `https://boards-api.greenhouse.io/v1/boards/{board}/jobs?content=true` | location in `location.name` |
| Lever | `https://api.lever.co/v0/postings/{company}?mode=json` | EU boards: `api.eu.lever.co` |
| Ashby | `https://api.ashbyhq.com/posting-api/job-board/{org}?includeCompensation=true` | pay when published |
| SmartRecruiters | `https://api.smartrecruiters.com/v1/companies/{company}/postings?limit=100` | detail `.../postings/{id}` |
| Workable | `https://apply.workable.com/api/v1/widget/accounts/{subdomain}` | |
| Recruitee | `https://{company}.recruitee.com/api/offers/` | |
| Workday | no public API; open `*.myworkdayjobs.com` in the browser and use its search | |

Board name = first path segment after the host (`job-boards.greenhouse.io/acme` → `acme`).
Discovery queries: `site:job-boards.greenhouse.io "site reliability" Singapore`, `site:jobs.lever.co kubernetes Singapore`, `site:jobs.ashbyhq.com "solutions architect" APAC`.

## Country portals

Built-in starting points by region. Any country not listed: find its official portal and 1–2 leading private boards with a
web search, then save them to Filters `country_portals`. Read-only browsing; log in only when the user signs in.
Portals change: if one no longer works, search for its replacement and update `country_portals`.

### Singapore (primary)
- **MyCareersFuture**: government portal; most roles open to work-pass holders must be advertised here first (Fair Consideration Framework), so it is the widest source. Search API used by the site: `https://api.mycareersfuture.gov.sg/v2/jobs?search=<keywords>&limit=20&page=0&sortBy=new_posting_date` (unofficial: confirm the response shape on first use; fallback `https://www.mycareersfuture.gov.sg/search?search=<keywords>` in the browser). Salary ranges are SGD/month.
- JobStreet SG, LinkedIn, eFinancialCareers (finance), NodeFlair (tech), Glints.

### APAC
| Country | Starting points |
|---|---|
| Malaysia | MYFutureJobs (official), JobStreet MY |
| Indonesia | Karirhub Kemnaker (official), JobStreet ID, Glints, Kalibrr, Dealls; jobs abroad for Indonesian citizens: SISKOP2MI (official, Kementerian P2MI) |
| Australia | Workforce Australia (official), SEEK |
| New Zealand | SEEK NZ, Trade Me Jobs |
| Japan | Hello Work (official), Daijob and CareerCross (English-friendly) |
| Hong Kong | Labour Department iES (official), JobsDB HK, CTgoodjobs |
| India | National Career Service (official), Naukri |
| Philippines, Thailand, Vietnam | JobStreet / JobsDB, local official portal via web search |

### EMEA
| Country / area | Starting points |
|---|---|
| EU / EEA (all) | EURES (EU-wide official portal) |
| Germany | Jobbörse der Bundesagentur für Arbeit (official), StepStone |
| Netherlands | werk.nl (official), Indeed NL |
| Ireland | Jobs Ireland (official), IrishJobs |
| United Kingdom | Find a job on GOV.UK (official), Reed, Totaljobs |
| Nordics | national employment-service portals (e.g. Arbetsförmedlingen, NAV), via web search |
| UAE / Saudi / Qatar | Bayt, GulfTalent, national portals via web search |

### US / Canada
| Country | Starting points |
|---|---|
| United States | USAJOBS (federal government roles only), Indeed, LinkedIn, Dice (tech); most private employers: company ATS boards above |
| Canada | Job Bank (official; shows whether an employer has an LMIA), Indeed CA, LinkedIn |

## Remote and freelance

Remote job boards (check each posting's location restriction; for `remote_scope: worldwide` keep only "anywhere" or the user's region, and note when the role is contractor-only):
- Remotive (public API `https://remotive.com/api/remote-jobs?search=<keywords>`; unofficial for automation, confirm the shape on first use), We Work Remotely, Remote OK, Working Nomads, Himalayas: browser or WebFetch, read only.
- ATS discovery with `"remote" "<region or country>"` (see above).

Freelance and project marketplaces (the user signs up and applies personally; Claude finds listings the user can see and drafts proposals):
- Global: Upwork, Fiverr, Freelancer, Contra; Toptal and similar vetted networks for senior freelancers.
- Indonesia: Sribulancer, Projects.co.id, Fastwork. Southeast Asia: Fastwork (TH, ID, VN), FastJobs (SG, MY, PH) for part-time and hourly jobs.

Part-time, flexible and returner roles:
- Country portals' part-time / flexible filters.
- Web search: `returnship <country>`, `part time work from home <city> site:<official portal>`, `school hours jobs <city>`.

Graduate and entry level:
- Company graduate programmes (search `graduate programme <company or industry> <country> <year>`), country portals' entry-level filters, university career portals the user names.

Prefer official portals and company sites for side-income searches; marketplace and social-media listings get the scam check every time.

## Moving abroad (Filters `relocation` alone or family)

- Search terms: `"visa sponsorship"`, `"relocation package"`, `"relocation support"`, `"open to international candidates"` with the role and country; on ATS boards check the location and "work authorisation" questions.
- Official portals that show sponsor-ready roles: Canada Job Bank (LMIA), UK GOV.UK Find a job plus the Home Office register of licensed sponsors, Netherlands IND recognised sponsors, Singapore MyCareersFuture (roles open to work-pass holders).
- Skip postings that say "citizens/PR only", "no sponsorship", "local candidates only".

## Offshore and rotation work (Filters `employment_types` has rotation, or `work` has energy)

- Energy and offshore boards: Rigzone, Oil and Gas Job Search, Energy Jobline; offshore wind roles on the same boards and on developers' careers pages.
- Company careers pages and ATS boards of operators, drilling contractors and service companies in the user's region (search `"rotation" "14/14" <role> careers`, `"28/28" offshore <role> <region>`).
- Mining and remote-site roles: country portals with `FIFO` / `rotation` / `roster` (Australia SEEK: `FIFO`; Indonesia: `rotasi`, `roster 2:2`).
- Ships and offshore vessels: company fleets and licensed crewing agencies only (Indonesia: Kemenhub SIUPPAK licence; abroad via SISKOP2MI).
- Always run the scam check: fake rig and ship offers are common.

## Gmail queries for recruiter outreach

- `newer_than:14d (opportunity OR position OR role OR opening OR "your profile") -category:promotions -category:social`
- `newer_than:14d from:(linkedin.com) subject:(job OR jobs)` for job alerts
- Agencies often omit the client name: record the agency, mark Model `via agency`, and list it as "client unknown".
