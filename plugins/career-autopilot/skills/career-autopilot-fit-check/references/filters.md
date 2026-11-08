# Filter keys (Filters tab)

| Key | Example | Meaning |
|---|---|---|
| profile | Siti | which person this store belongs to (career-autopilot-setup step 0) |
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
| citizenship | Indonesia | decides work rights per country; asked only when the user looks abroad |
| relocation | none / alone / family | whether the user would move for the job |
| family | spouse, children | who moves along: spouse, children, parents. Never the number, names or ages of children (profile-builder privacy rule) |
| relocation_support | required / preferred / none | relocation package: flights, shipping, temporary housing, visa costs for the family |
| living_cost_<code> | living_cost_sg: SGD 9,000–12,400/month + school SGD 3,100/child | monthly living cost for the household in that country (Cost of living below); saved when the user moves alone or with family |
| rotation_pattern | 14/14, 28/28 | days on / days off for rotation work (offshore, mining, remote sites) |
| rotation_region | Asia Pacific, Middle East | where the user accepts to fly in for rotations; crew-change point travel |
| languages_spoken | English, Indonesian | any other required language is a blocker |
| salary_floor_<region> | salary_floor_sg: SGD 5,600/month | exclude below; see "Default salary floors" when the user has none |
| | salary_floor_id: IDR 15,000,000/month · salary_floor_au: AUD 9,000/month · salary_floor_eu: EUR 4,500/month · salary_floor_remote: USD 3,000/month | one line per target country, in that country's currency. Key = lowercase ISO country code (sg, id, my, au, gb, us, ca, de…), a region (eu, gcc) or `remote`. The most specific key wins: country, then region, then remote. A country with no key gets the official default after the user agrees. |
| seniority | senior, staff, lead | allowed levels |
| exclude_keywords | intern, junior | title words to skip |
| employment_types | permanent, contract (direct), part-time, freelance / project, casual / gig, internship, graduate programme, returnship, rotation | allowed models |
| min_contract_months | 12 | shorter contracts get flagged |
| min_match | 75 | apply threshold in active mode |
| ready_send_min_match | 80 | from this score a prefilled form can go on the "Siap dikirim" list, sent only after the user's go-ahead in chat |
| watch_min_match | 88 | threshold in watch mode |
| weights | must_have:45, years:15, stack:20, certs:10, domain:5, scope:5 | scoring |
| max_applications_per_day | 10 | pacing in active mode |
| company_boards | greenhouse:acme, lever:foo | saved ATS boards |
| use_platforms | linkedin, jobstreet | account platforms allowed in unattended runs (default none) |
| platform_caps | linkedin: opened=30, prefilled=3 | overrides of the daily caps in career-autopilot-find-jobs/references/platforms.md |
| platform_ack_<platform> | 2026-11-08 | date the user accepted the account-risk reminder |
| platform_pause_<platform> | 2026-11-10 | paused until this date after a warning sign |
| platform_usage_<platform> | 2026-11-08 opened=12 searches=3 prefilled=1 | today's counters |
| run_time | 09:40 | local time of scheduled runs |
| run_day | Sunday | watch-mode weekday |
| timezone | Asia/Singapore | IANA zone |
| language | id / en | language for summaries and drafts to the user |
| availability | weekdays after 18:00 SGT | used when proposing interview slots |
| dashboard_url | https://claude.ai/artifact/… | the user's private dashboard (career-autopilot-dashboard skill) |
| last_inbox_sync | 2026-11-01 | set by career-autopilot-inbox-sync |

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

## Internships and graduate programmes

The minimum wage floor does not apply to an internship: interns usually get an allowance (Indonesia: uang saku under the
pemagangan rules), not a wage. Do not exclude an internship on pay; ask the user once for a minimum allowance or "tidak
masalah", and flag unpaid internships (segment fresh-graduate, Checks).

## Figures shown on the dashboard's Start tab

The Start tab (`career-autopilot-dashboard/assets/dashboard.html`, `FLOORS` and `SHORT`) shows these defaults before the user saves.
Keep both places in step; check them once per month.

| Country | Default | Source |
|---|---|---|
| Indonesia | UMP/UMK of the work location, e.g. DKI Jakarta IDR 5,729,876/month (2026); part time ÷ 126 per hour | Kemnaker / provincial decree; PP 36/2021 Pasal 16 |
| Singapore | EP SGD 5,600/month; with family SGD 6,000 fixed (Dependant's Pass); locals SGD 1,800 (LQS) | MOM |
| Malaysia | EP category III RM 5,000/month from 1 June 2026 (II RM 10,000, I RM 20,000); all categories may bring dependants | MOHA / MDEC |
| Australia | AUD 79,423/year, Skills in Demand 482 Core Skills, from 1 July 2026; family on the same visa | Home Affairs |
| Netherlands | EUR 5,942/month excl. holiday pay (highly skilled migrant 30+, also EU Blue Card), under 30 EUR 4,357 (2026) | IND |
| Germany | EU Blue Card EUR 50,700/year; shortage occupations, IT and recent graduates EUR 45,934.20 (2026) | Make it in Germany |

## Other countries

Use the official national minimum wage or the work-permit salary threshold for that country (e.g. Malaysia national minimum wage, Indonesia provincial UMP/UMK, Australia national minimum wage and skilled-visa income thresholds, UK National Living Wage and Skilled Worker thresholds, EU Blue Card thresholds per country, US state minimum wage). Look up the current figure on the government site, show it with its source and date, and save it as the default floor only after the user agrees.

# Family relocation (when `relocation: family`)

Moving with a spouse and children needs a work route that allows dependants, and usually a higher salary than the work
permit alone. Treat the family minimum as part of the floor for that country, and check the current rule once per month.

| Country | Family rule | Source |
|---|---|---|
| Singapore | Dependant's Pass for a legally married spouse and unmarried children under 21: the EP or S Pass holder must earn a fixed monthly salary of at least SGD 6,000 (own salary, not household income; fixed allowances count, bonuses and overtime do not). Parents on a Long-Term Visit Pass: SGD 12,000. Meeting it allows an application, not approval. | MOM Dependant's Pass eligibility |
| Other countries | Look up the dependant or family visa rule for the work route (e.g. Malaysia EP category, Australia employer-sponsored visa, UK Skilled Worker dependants, Gulf family residence visa salary minimum, Japan dependent visa) on the government site, show it with source and date, and save it only after the user agrees. | government site |

Also weigh, and show in the report, whether the offer covers: visas for the family, flights, shipping, temporary housing,
school fees or international-school allowance, health insurance for dependants. A posting that says "local candidates only",
"no relocation" or "no visa sponsorship" is a hard exclude when `relocation` is alone or family and the user needs a permit.

For Indonesian citizens going abroad: work through the employer directly (jalur mandiri) or a P3MI agency listed as active in
SISKOP2MI (siskop2mi.bp2mi.go.id, Kementerian P2MI). Official placement charges no registration or recruitment fee to the candidate.
Register the job in SISKOP2MI before leaving, so the worker is protected.

# Cost of living (when `relocation` is alone or family)

The Start tab shows these monthly estimates next to the salary floors (`COL` in dashboard.html; keep both in step, check monthly).
Household = one adult (alone) or 2 adults + 2 children (family; the real number of children is never stored). Before tax.

| Country (city) | Alone | Family | School note |
|---|---|---|---|
| Singapore | SGD 3,500–4,900 | SGD 9,000–12,400 | international school ≈ SGD 3,100 per child a month (local places for foreign children are scarce) |
| Australia (Sydney) | AUD 4,300–5,500 | AUD 11,000–13,700 | public schools may charge temporary visa holders in some states |
| Netherlands (Amsterdam) | EUR 3,000–3,500 | EUR 6,000–7,800 | public school free; international ≈ EUR 1,500 per child a month |
| Malaysia (Kuala Lumpur) | RM 5,500–8,500 | RM 10,000–15,000 | international school adds ≈ RM 8,000–16,000 a month for 2 children |

Sources: Numbeo via Expatica (1 June 2026: single and family-of-four costs excluding rent, 1- and 3-bedroom rents), 2026 relocation
guides for school fees. Other countries and cities: look up the same items for the posting's city when a job comes up.

In career-autopilot-fit-check, per posting abroad:
1. Living cost for the posting's city and household (rent for 1 or 3 bedrooms, living costs, school when children come and local school is not open to them).
2. Take-home pay from the posted salary with the country's official tax calculator or rates (e.g. IRAS, ATO, Belastingdienst; note special
   regimes such as the Dutch 30% ruling only when the posting or user mentions them).
3. Report one line "Biaya hidup: gaji bersih ± X, kebutuhan ± Y → sisa ± Z / kurang ± Z". Shortfall → flag "Gaji tidak cukup untuk biaya hidup
   <keluarga|sendiri>". Never exclude on this alone; the user decides. No posted pay → say the gross pay needed instead.

# Rotation and offshore work (when `employment_types` has rotation)

- Pattern: compare the posting's rotation (14/14, 21/21, 28/28, 4/4 weeks) with `rotation_pattern`; a different pattern is a flag, not an exclude, unless the user says it is fixed.
- Pay: day rate or monthly; rotation roles often pay only for days on. Compare like with like; say which one the posting uses.
- Travel: who pays the flight to the crew-change point (heliport, port, mine site) and whether travel days are paid.
- Safety training and medicals often required before mobilisation: e.g. BOSIET/FOET with CA-EBS, HUET, an offshore medical (OEUK or national equivalent), H2S, GWO for offshore wind, STCW for vessels. Missing ones are a flag "pelatihan keselamatan perlu"; exclude only when the posting says they must be valid now and the job starts within weeks.
- "Single status" or "bachelor status" means the family cannot come: exclude when `relocation: family`.
- Employer: operator, drilling contractor, service company or manpower/crewing agency. Agency → check its licence (Indonesia: P3MI in SISKOP2MI for jobs abroad; crewing agencies for ships hold a Kemenhub SIUPPAK licence).

# Remote for employers abroad (when `remote_scope` is wider than the user's country)

- Classify how the user would be paid: employee through an Employer of Record (Deel, Remote.com, Oyster and similar), or independent contractor.
- Contractor → flag "kontraktor: pajak dan jaminan sosial Anda urus sendiri" and note that pay should be in a normal bank transfer or a known payment service, never crypto (scam-signals).
- Check the posting's location rule ("anywhere", "APAC only", "must reside in the US") against `remote_scope`, and working hours against `remote_timezones`.

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
Medicine, nursing, law, teaching, engineering, accounting and similar often need local registration or a conversion exam. Flag it in career-autopilot-fit-check.
