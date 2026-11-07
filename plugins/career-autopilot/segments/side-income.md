# Segment: side-income

For part-time work, freelance and project work, tutoring, online selling support, admin or customer service from home,
and other work alongside another job, study or caring for a family.

## Profile
- A short profile is enough: skills the user can offer (e.g. bookkeeping, baking, sewing, translation, tutoring maths, social media, data entry, customer service), languages, tools they can use, availability.
- `hours_per_week`, `schedule` (e.g. "weekdays 9:00–14:00"), `work_mode`, `max_commute_minutes`, `pay_unit` and `pay_floor`.
- Portfolio links or photos of work where relevant (Drive links the user provides).
- No CV needed: cv-builder can make a one-page profile.

## Scoring
`must_have:35, schedule_fit:25, pay:15, stack:15, safety:10`.
- schedule_fit: hours, days and location match the user's availability.
- pay: meets `pay_floor` in `pay_unit` (hour, day, project, month).
- safety: 10 when there are no scam flags, 0 when any flag fires.

## Sources
- Country portals with part-time and work-from-home filters.
- Freelance marketplaces (see find-jobs sources, section Freelance and remote). The user signs up and applies on those platforms personally; Claude drafts proposals.
- Local community job groups the user names: Claude reads only what the user pastes.

## Filters defaults
| Key | Value |
|---|---|
| work_mode | remote, hybrid, onsite |
| employment_types | part-time, freelance, project, casual |
| pay_unit | hour |
| min_match | 65 |

## Writing
Short and warm. Say what the user can do, when they are available, and one proof (a past job, a photo, a reference). Freelance proposals: answer the client's question in the first line, give a price or ask the one question needed to price it.

## Checks
- Apply scam-signals to every posting and message, strictly.
- Platform fees and payment protection: prefer platforms that hold payment in escrow.
- Hours that conflict with the user's main job contract or school schedule: flag.
