# Filter keys (Filters tab)

| Key | Example | Meaning |
|---|---|---|
| preset | sre-platform, tam-presales | role presets in use |
| mode | active / watch / off | how autopilot behaves |
| target_roles | Site Reliability Engineer, Platform Engineer | titles to search |
| keywords | kubernetes, openshift, object storage | search terms |
| target_companies | Red Hat, Google, NetApp | companies to check directly |
| exclude_companies | Acme | never apply |
| countries | Singapore, Australia, Germany, Canada | any countries; `remote` too |
| country_portals | Portugal: net-empregos.pt, … | portals found for countries not in sources.md |
| remote_ok | yes | include remote roles open to the user's country |
| needs_sponsorship | singapore: yes | per country |
| languages_spoken | English, Indonesian | any other required language is a blocker |
| salary_floor_<region> | salary_floor_sg: SGD 12,000/month | exclude below |
| seniority | senior, staff, lead | allowed levels |
| exclude_keywords | intern, junior | title words to skip |
| employment_types | permanent, contract (direct) | allowed models |
| min_contract_months | 12 | shorter contracts get flagged |
| min_match | 75 | apply threshold in active mode |
| watch_min_match | 88 | threshold in watch mode |
| weights | must_have:45, years:15, stack:20, certs:10, domain:5, scope:5 | scoring |
| max_applications_per_day | 10 | pacing in active mode |
| company_boards | greenhouse:acme, lever:foo | saved ATS boards |
| use_linkedin | no | include LinkedIn in unattended runs |
| linkedin_daily_cap | 40 | LinkedIn descriptions per day |
| run_time | 09:40 | local time of scheduled runs |
| run_day | Sunday | watch-mode weekday |
| timezone | Asia/Singapore | IANA zone |
| language | id / en | language for summaries and drafts to the user |
| availability | weekdays after 18:00 SGT | used when proposing interview slots |
| last_inbox_sync | 2026-11-01 | set by inbox-sync |

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
