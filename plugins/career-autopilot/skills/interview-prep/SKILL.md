---
name: interview-prep
description: >
  Use when the user says "prep me for the <company> interview", "interview prep", "persiapan interview",
  "what will they ask", "siapkan jawaban interview", or when inbox-sync finds an interview invite
  and the user accepts the offer to prepare.
---

# Interview brief

Adapt to the segment (`${CLAUDE_PLUGIN_ROOT}/segments/<segment>.md`): fresh graduates get practice for online tests, group interviews and "tell me about a project"; returners get a short, confident answer about the break; side-income users get a short call script (availability, pay, how they work).

Inputs: the Applications row (or a link/description the user gives), `Profile`, `Stories`, and the invite email if any (who, which round, format).

## Research (web, 3–6 searches)

- Company: what it sells, size and presence in the job's country, recent news from the last 6 months.
- Team/product the role sits in, if public.
- Interviewers named in the invite: role and team only, from their public professional profiles or company pages. Nothing personal.
- Typical process for this company and role family, from public sources. Label it as reported, not certain.

## Brief (Drive `Career Autopilot/interviews/<company>-<role>-<date>.md`)

1. **Round**: who, format, length, what this round usually tests.
2. **Pitch**: a 60-second "tell me about yourself" for this role, from Profile only.
3. **Why this company / role**: 3 specific points tied to research.
4. **Likely questions** (10–15) split into technical, scenario/system design, behavioural, customer (for customer-facing roles). For each: the best-matching Story id and a 2–3 line answer outline.
5. **Gaps to address**: from fit-check gaps, with an honest framing for each ("not used X in production; used Y which solves the same problem; here's how I'd ramp").
6. **Questions to ask them**: 5, specific to the role and the employment model (for agency/vendor roles: client, duration, conversion criteria and timeline, who manages performance).
7. **Logistics**: time in the user's timezone, link/location, what to have open.

Then offer a mock: ask one question at a time, wait for the user's answer, give short feedback (structure, specificity, missing result numbers), next question.
Add any new story the user tells during the mock to `Stories` with `Source: user` after confirming the wording with them.
