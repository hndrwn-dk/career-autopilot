# Filter keys (Filters tab)

| Key | Example | Meaning |
|---|---|---|
| profile | Siti | which person this tracker belongs to (career-setup step 0) |
| segment | experienced / fresh-graduate / career-returner / side-income / career-switcher | the user's situation |
| preset | finance-accounting, custom:barista | role presets in use |
| mode | active / watch / off | how autopilot behaves |
| target_roles | Site Reliability Engineer, Platform Engineer | titles to search |
| keywords | kubernetes, openshift, object storage | search terms |
| target_companies | Red Hat, Google, NetApp | companies to check directly |
| exclude_companies | Acme | never apply |
| countries | Singapore, Australia, Germany, Canada | any countries; `remote` too |
| country_portals | Portugal: net-empregos.pt, … | portals found for countries not in sources.md |
| work_mode | remote / hybrid / onsite / any (comma list allowed) | allowed work arrangements |
| remote_scope | Indonesia, Singapore, worldwide | countries whose employers the user may legally work for remotely |
| remote_timezones | UTC+7 to UTC+9 | acceptable working-hours overlap |
| max_commute_minutes | 45 | for hybrid/onsite, from `home_area` |
| home_area | Bekasi Barat | area name only, never a full address |
| hours_per_week | 20 | for part-time and side income |
| schedule | weekdays 09:00-14:00 | when the user can work |
| pay_unit | hour / day / project / month | unit for `pay_floor` |
| pay_floor | IDR 50,000 | minimum pay in `pay_unit` |
| needs_sponsorship | singapore: yes | per country |
| languages_spoken | English, Indonesian | any other required language is a blocker |
| salary_floor_<region> | salary_floor_sg: SGD 5,600/month | exclude below; see "Default salary floors" when the user has none |
| | salary_floor_id: IDR 15,000,000/month · salary_floor_au: AUD 9,000/month · salary_floor_eu: EUR 4,500/month · salary_floor_remote: USD 3,000/month | one line per target country, in that country's currency. Key = lowercase ISO country code (sg, id, my, au, gb, us, ca, de…), a region (eu, gcc) or `remote`. The most specific key wins: country, then region, then remote. A country with no key gets the official default after the user agrees. |
| seniority | senior, staff, lead | allowed levels |
| exclude_keywords | intern, junior | title words to skip |
| employment_types | permanent, contract (direct), part-time, freelance / project, casual / gig, internship, graduate programme, returnship | allowed models |
| min_contract_months | 12 | shorter contracts get flagged |
| min_match | 75 | apply threshold in active mode |
| watch_min_match | 88 | threshold in watch mode |
| weights | must_have:45, years:15, stack:20, certs:10, domain:5, scope:5 | scoring |
| max_applications_per_day | 10 | pacing in active mode |
| company_boards | greenhouse:acme, lever:foo | saved ATS boards |
| use_platforms | linkedin, jobstreet | account platforms allowed in unattended runs (default none) |
| platform_caps | linkedin: opened=30, prefilled=3 | overrides of the daily caps in find-jobs/references/platforms.md |
| platform_ack_<platform> | 2026-11-08 | date the user accepted the account-risk reminder |
| platform_pause_<platform> | 2026-11-10 | paused until this date after a warning sign |
| platform_usage_<platform> | 2026-11-08 opened=12 searches=3 prefilled=1 | today's counters |
| run_time | 09:40 | local time of scheduled runs |
| run_day | Sunday | watch-mode weekday |
| timezone | Asia/Singapore | IANA zone |
| language | id / en | language for summaries and drafts to the user |
| availability | weekdays after 18:00 SGT | used when proposing interview slots |
| dashboard_url | https://claude.ai/artifact/… | the user's private dashboard (career-dashboard skill) |
| last_inbox_sync | 2026-11-01 | set by inbox-sync |

# Default salary floors (when the user gives none)

Use the official reference for the country, tell the user which one, and let them change it. Thresholds change: before relying on a figure, check the official page once per month and update this table.

## Singapore (Ministry of Manpower, mom.gov.sg)

Singapore has no national minimum wage. Reference points:

| Situation | Default `salary_floor_sg` | Source and notes |
|---|---|---|
| Needs an Employment Pass (PMET roles) | EP qualifying salary: SGD 5,600/month (financial services SGD 6,200), higher with age | MOM EP eligibility, in force since 1 Jan 2025. From 1 Jan 2027 for new applications: SGD 6,000 (financial services SGD 6,600). Age-adjusted figure: MOM Self-Assessment Tool (SAT). |
| Needs an S Pass (mid-skilled roles) | S Pass qualifying salary: SGD 3,300/month (financial services SGD 3,800), higher with age | MOM S Pass eligibility, in force since 1 Sep 2025. From 1 Jan 2027 for new applications: SGD 3,600 (financial services SGD 4,000). |
| Singapore citizen or PR, full time | Local Qualifying Salary: SGD 1,800/month | MOM LQS from 1 Jul 2026. Not a legal minimum wage for every job, but the level a full-time local must earn to count toward an employer's quota. Sectors under the Progressive Wage Model (cleaning, security, landscape, retail, food services and others) have their own higher wage ladders: check the MOM PWM page for the job's sector. |
| Part-time locals | No fixed floor; use `pay_floor` per hour | The LQS has a pro-rated part-time rule; ask the user for an hourly floor. |

For a work-pass holder the EP or S Pass figure is a hard floor: an employer cannot get the pass approved below it. Always state that meeting it does not guarantee approval (EP also needs COMPASS points).

## Other countries

Use the official national minimum wage or the work-permit salary threshold for that country (e.g. Malaysia national minimum wage, Indonesia provincial UMP/UMK, Australia national minimum wage and skilled-visa income thresholds, UK National Living Wage and Skilled Worker thresholds, EU Blue Card thresholds per country, US state minimum wage). Look up the current figure on the government site, show it with its source and date, and save it as the default floor only after the user agrees.

# Work-permit notes (orientation only; check the current rule with a web search whenever a threshold decides the outcome)

## Singapore and APAC
- Singapore: Employment Pass is applied for by each new employer; assessed on a qualifying salary that rises with age (higher in financial services) plus COMPASS points. S Pass for mid-skilled roles has quotas.
- Malaysia: Employment Pass through the employer; categories by salary.
- Indonesia: foreigners need a work permit (RPTKA/KITAS) through the employer.
- Australia: employer-sponsored Skills in Demand visa; skilled independent visas via points.
- Japan: work visa sponsored by the employer, category by job type; highly-skilled professional points route.
- Hong Kong: General Employment Policy via the employer; talent schemes exist.

## EMEA
- EU: EU Blue Card through the employer when the salary meets the country's threshold; national skilled-worker permits otherwise.
- Germany: EU Blue Card or skilled-worker visa; recognition of foreign qualifications may be needed for regulated jobs.
- Netherlands: highly skilled migrant permit; the employer must be an IND recognised sponsor.
- United Kingdom: Skilled Worker visa; the employer must hold a sponsor licence, and salary and occupation thresholds apply.
- Ireland: Critical Skills or General Employment Permit.
- Gulf states: employer-sponsored work visa; some roles are reserved for nationals.

## US / Canada
- United States: most employer routes need sponsorship (H-1B is lottery-based and capped; L-1 for intra-company transfers; TN for Canadian and Mexican citizens; O-1 for extraordinary ability). Treat "no sponsorship" as a hard filter when the user needs it.
- Canada: employer route usually needs an LMIA (Job Bank shows LMIA-approved postings); permanent route via Express Entry; intra-company transfers and some trade-agreement categories are LMIA-exempt.

## Regulated professions (any country)
Medicine, nursing, law, teaching, engineering, accounting and similar often need local registration or a conversion exam. Flag it in fit-check.
