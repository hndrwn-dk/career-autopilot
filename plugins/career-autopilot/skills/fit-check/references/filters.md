# Filter keys (Filters tab)

| Key | Example | Meaning |
|---|---|---|
| preset | sre-platform, tam-presales | role presets in use |
| mode | active / watch / off | how autopilot behaves |
| target_roles | Site Reliability Engineer, Platform Engineer | titles to search |
| keywords | kubernetes, openshift, object storage | search terms |
| target_companies | Red Hat, Google, NetApp | companies to check directly |
| exclude_companies | Acme | never apply |
| countries | Singapore, Malaysia | where to search |
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

# Work-pass notes (check current thresholds with a web search when it matters)

- Singapore: Employment Pass needs a new application by each new employer; the employer applies. Assessed on a qualifying salary that rises with age (higher in financial services) plus COMPASS points. Jobs must usually be advertised on MyCareersFuture first. S Pass for mid-skilled roles has quotas.
- Malaysia: Employment Pass via the employer (ESD); categories by salary.
- Indonesia: citizens need nothing; foreigners need a KITAS/RPTKA through the employer.
- Australia: employer-sponsored Skills in Demand visa; check the occupation list.
- Remote roles: check whether the company hires in the user's country directly or via an employer of record.
