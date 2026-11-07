# LinkedIn rules

LinkedIn's User Agreement prohibits automated access; accounts can be restricted. Say this once per session before the first LinkedIn step.

- Only in the user's own signed-in browser. Never type a password.
- Sequential only: one request at a time, at least 3 seconds apart. No parallel fetches.
- Cap: Filters `linkedin_daily_cap` (default 40) job descriptions per day across all runs.
- Search page: `https://www.linkedin.com/jobs/search/?keywords=<kw>&geoId=<geo>&f_TPR=r604800` (past week; `r86400` = 24h).
- Read descriptions from the open job pane or page text. Do not call undocumented endpoints in a loop.
- Any error, CAPTCHA or "unusual activity" page: stop LinkedIn for the session and tell the user.

geoIds: Singapore 102454443 · Indonesia 102478259 · Malaysia 106808692 · Australia 101452733 · Japan 101355337 · UAE 104305776.
Check a geoId by opening the search URL once and confirming the location label.
