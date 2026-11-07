---
name: autopilot-run
description: >
  Use when a scheduled Career Autopilot run starts, or the user says "run career autopilot",
  "run autopilot now", "jalankan autopilot", "jalankan sekarang". One unattended pass in the
  mode set in Filters (active or watch), ending with a short summary.
---

# Scheduled run

Runs unattended. Never ask questions mid-run: make the safe choice, note it, continue.
Guardrails `${CLAUDE_PLUGIN_ROOT}/skills/apply-assist/references/guardrails.md` apply in full.
Turning on `active` mode approves searching and prefilling forms. It never approves Submit, sending email, or any guardrail item.

## 0. Load

Read Profile, Filters, Applications, Skip from `Career Autopilot Tracker`.
- `mode` is `off` → stop: "Autopilot is off."
- Profile empty → stop: "Profile is empty. Upload your CV and say: build my profile."
- The prompt names a mode that differs from Filters → use Filters and mention it.

## 1. Replies

Run inbox-sync. Flip `Ready to submit` rows to `Submitted` when a confirmation email matches.

## 2. New roles

Run find-jobs without its final question. LinkedIn only if `use_linkedin: yes`.
- `active`: queue postings with no hard-filter hit and score ≥ `min_match`, best first, up to `max_applications_per_day` minus forms already prefilled today. Leftover queued jobs go first.
- `watch`: keep only score ≥ `watch_min_match` and an allowed employment model. Do not queue anything. Max 5.

## 3. Prefill (active only)

List browser tabs. No browser reachable → leave jobs queued, say so in the summary.
For each queued job follow apply-assist steps 2–7, except: the mode is the approval; attach the CV if the tools allow, else note it; leave the tab open; never press Submit.
Append to Applications with Status `Ready to submit`, Applied On empty, Next Action naming the tab and what is left.
A form that cannot be filled: Status `Needs manual apply` with the reason.

## 4. Summary (the notification / email)

In Filters `language`. Leave out empty sections. No tool names.

```
Career Autopilot · <date> · <mode>

Ready to submit (<n>) – open the browser, check each tab, tick consents, Submit
- <Company> · <Role> · <City> · <match>% · <what is left>

Worth a look (<n>)                      ← watch mode
- <Company> · <Role> · <City> · <match>% · <model> · <one-line why> · <link>

Replies
- Interview / assessment: <Company> · <Role> · <next step / deadline>
- Offer: <Company> · <Role>
- Rejected: <Company> · <Role>

Skipped: <n> (<top reasons>) · Waiting for reply: <n>
Tracker: <sheet link>
```

Mention `Ready to submit` rows older than 3 days without a confirmation email.
