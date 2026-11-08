# Where Career Autopilot keeps data (the store)

Every profile's data lives in the database of that profile's **dashboard** page (a private claude.ai artifact).
It is the single source of truth. Every skill reads and writes it with the Artifact database tools, which every
claude.ai user has. Google Drive is only used for files (CV, shortlists, interview briefs, presets, exports), never
for row-by-row updates: the Drive connector can create or replace a whole file but cannot append rows to a sheet.

## 1. Load the tools first

Before deciding anything about the user's data, load the Artifact tools if they are deferred (one ToolSearch call):
the artifact list tool, publish tools, capability declaration, and the database tools (`db_get`, `db_list`,
`db_query`, `db_write`; on some clients the Artifact tool's `read_db` / `write_db` actions). Only after a search
finds none of them is the store unavailable (see 7).

## 2. Find the profile's store

List the user's artifacts whose title is `Career Autopilot` (default profile) or `Career Autopilot · <profile>`
(the artifact list tool, query "Career Autopilot"). A legacy title `Career Autopilot · Demo` is a demo, never a store.
- Found → that artifact's slug is the store. Its link is the dashboard link.
- Not found → there is no store yet; career-autopilot-setup creates it (career-autopilot-dashboard, Create).
- Several profiles → use the one the user or the scheduled prompt names; otherwise ask which.

## 3. Names used in the skills → documents

| Name in skills | Document(s) | Notes |
|---|---|---|
| Profile | `settings/profile` | one document, `{key: value}` (keys in career-autopilot-profile-builder) |
| Filters | `settings/filters` | one document, `{key: value}` (keys in career-autopilot-fit-check/references/filters.md) |
| Applications | `jobs/<id>` with status `queued`, `ready`, `submitted`, `in_review`, `assessment`, `interview`, `offer`, `rejected`, `withdrawn`, `closed` | fields below |
| Shortlist | `jobs/<id>` with status `worth_a_look` | |
| Skip | `jobs/<id>` with status `skipped` or `scam` | `reason`, `date` |
| Stories | `stories/<id>` | `title`, `situation`, `task`, `action`, `result`, `skills`, `source` |
| Onboarding | `onboarding/answers` | written by the dashboard page |
| Dashboard state | `meta/summary`, `meta/run`, `meta/ready` | see career-autopilot-dashboard; `meta/ready` = the numbered "Siap dikirim" list from the last run |

`jobs/<id>` fields: `company`, `role`, `city`, `country`, `work_mode`, `pay`, `model`, `status`, `match`, `channel`,
`link`, `job_id`, `applied_on`, `next_action`, `flags`, `reason`, `notes`, `source`, `date`, `updated`, `ready_to_send`.
`<id>` = `<company>-<role>` lowercased, every character outside `a-z0-9` replaced by `-`, collapsed, at most 120 characters.
"Append a row to Applications/Skip" means: write that `jobs/<id>` document. "Already in Applications or Skip" means:
a `jobs` document with that id or link exists.

## 4. Writing

- Read before you write: `db_get` (or a query) gives each document's version; pass it as `ifVersion` on every op on a
  document that exists. New documents need no version.
- Use `merge` to change a few fields (e.g. one Filters key); `set` only for a brand-new document.
- At most 50 ops per call, one call at a time, a short pause after a large batch.
- A refused write (version conflict): read again and retry once.
- Never write ID numbers, bank or card details, passwords, date of birth, or a full address anywhere in the store.

## 5. When a write cannot be done

Say it once, plainly, in the reply ("Catatan: status lowongan ini belum tersimpan di dashboard; saya coba lagi nanti."),
keep the result in the conversation, and continue. Never claim something was saved when it was not.

## 6. Export (optional)

"export my tracker" / "ekspor data saya": build a CSV of the `jobs` documents (and, if asked, Filters) and create a
NEW Drive file `Career Autopilot/<profile>/tracker-<YYYY-MM-DD>.csv`. Never try to edit an existing sheet in place.
Older exports stay as they are; say so.

Legacy: a `Career Autopilot Tracker` Google Sheet from an earlier version → read it once, import its rows into the store,
and tell the user the sheet is no longer updated.

## 7. No store available

If the Artifact database tools are truly unavailable after a tool search (for example in Claude Code), work in
chat-only mode: results stay in the conversation and nothing is remembered between conversations. Say this once.
