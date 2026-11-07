# Career Autopilot

A Claude plugin for job hunting, built for tech professionals (SRE, platform, cloud, storage, TAM, solutions architects and similar) with first-class support for Singapore and APAC.

It reads your CV, keeps a tracker in Google Sheets, finds roles that match, scores the fit, prefills application forms in your own browser (you press Submit), drafts recruiter emails (you press Send), syncs replies from Gmail, and builds an interview brief for every invite.

Nothing about you is baked into the plugin. Your profile lives in your own tracker sheet, so anyone can install it and use their own CV.

## Install

Claude desktop app: **Customize → Plugins → Add marketplace** → `hndrwn-dk/career-autopilot` → install **Career Autopilot**.
Or upload `career-autopilot.plugin` on the same page.

Claude Code:

```
/plugin install career-autopilot --marketplace hndrwn-dk/career-autopilot
```

## First run

1. Say **"set up career autopilot"**. Claude checks Gmail, Google Drive/Sheets and the browser, then creates the `Career Autopilot Tracker` sheet.
2. Pick a preset (or none): `sre-platform`, `tam-presales`, `storage-infra`. Presets fill sensible target roles, keywords and scoring weights; you can edit everything afterwards.
3. Upload your CV and say **"build my profile"**.
4. Optional: paste a settings block (format below) to set everything in one go.

## Modes

| Mode | For | What it does |
|---|---|---|
| `active` | actively looking | daily run: inbox sync, new jobs, forms prefilled up to Submit |
| `watch` | employed, open to the right offer | weekly run: only very strong matches, no forms filled, a short digest email |
| `off` | not looking | nothing scheduled; commands still work on demand |

## Daily use

| Say | What happens |
|---|---|
| "find jobs" / "cari lowongan" | ranked shortlist with match % and reasons |
| "check this job: <link>" | fit check with gaps, blockers and employment-model flags |
| "apply to 1 and 3" | forms prefilled in the browser; you tick consents and submit |
| "draft an email for this job" | Gmail draft; sent only when you say so |
| "check my application emails" | tracker statuses updated, next actions listed |
| "prep me for the <company> interview" | interview brief: company, role, likely questions, your STAR stories |

## Settings block

```
CAREER-AUTOPILOT-SETTINGS v1
preset: sre-platform
mode: watch
countries: Singapore
remote_ok: yes
...
END-SETTINGS
```

Every key is documented in `plugins/career-autopilot/skills/fit-check/references/filters.md`.

## What always stays with you

Passwords and logins, consent and terms checkboxes, diversity questions, date of birth, home address, ID numbers, the final Submit, and sending email.

## LinkedIn

LinkedIn's terms prohibit automation. It is off by default; when enabled the plugin works slowly in your own signed-in browser with a daily cap, and your account carries the risk. Public company ATS boards and MyCareersFuture are the default sources.
