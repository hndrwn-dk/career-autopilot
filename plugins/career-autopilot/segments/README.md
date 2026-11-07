# Segments

A segment describes the user's situation, not their field. It changes how the profile is built, how jobs are
scored, where to search and how applications are written. Set it in Filters `segment` (one value).
Presets (field) and segments (situation) combine: e.g. `segment: fresh-graduate` + `preset: finance-accounting`.

| Segment | For |
|---|---|
| experienced | working professionals with a track record (default) |
| fresh-graduate | students in their final year, new graduates, first job or internship |
| career-returner | people returning after a break: caregiving, raising children, health, relocation, study |
| side-income | part-time, freelance, gig or work-from-home alongside other commitments |
| career-switcher | moving into a new field, using transferable skills |

Each file has the same sections: Profile, Scoring, Sources, Filters defaults, Writing, Checks.
Setup copies "Filters defaults" into empty Filters keys. fit-check uses "Scoring" unless Filters `weights` is set.
