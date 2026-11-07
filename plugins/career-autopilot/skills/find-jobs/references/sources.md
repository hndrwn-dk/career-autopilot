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

### Singapore
- **MyCareersFuture** (government portal; every EP-eligible posting must be advertised here first under the Fair Consideration Framework, so it is the widest source).
  Search API used by the site: `https://api.mycareersfuture.gov.sg/v2/jobs?search=<keywords>&limit=20&page=0&sortBy=new_posting_date`.
  Unofficial: confirm the response shape on first use. Fallback: `https://www.mycareersfuture.gov.sg/search?search=<keywords>` in the browser.
  Postings show a salary range (SGD/month): use it for the salary filter.
- **NodeFlair** (tech roles, often with salary), **eFinancialCareers** (banks and financial institutions), **JobStreet**, **Glints**: browser search; read only, no login unless the user signs in.

### Indonesia
- Glints, JobStreet ID, Kalibrr, LinkedIn. Browser search.

### Malaysia / wider APAC
- JobStreet MY, LinkedIn, company boards via ATS APIs. Remote-APAC roles: ATS discovery with `"APAC" remote`.

Add other countries here as users need them.

## Gmail queries for recruiter outreach

- `newer_than:14d (opportunity OR position OR role OR opening OR "your profile") -category:promotions -category:social`
- `newer_than:14d from:(linkedin.com) subject:(job OR jobs)` for job alerts
- Agencies often omit the client name: record the agency, mark Model `via agency`, and list it as "client unknown".
