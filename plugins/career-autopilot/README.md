# Career Autopilot

A Claude plugin for job hunting. You choose the profession and the target countries; the plugin adapts.

- **Any profession.** Role presets set target titles, keywords, skill groups and scoring weights. The plugin ships with example presets for tech roles, and `setup` can draft a custom preset for any field (finance, healthcare, education, design, operations…) from your CV and the roles you name.
- **Any country.** Built-in sources and work-permit notes for Singapore, APAC, EMEA and US/Canada. For any other country, Claude finds the main job portals on first use and saves them to your settings.

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
2. Pick a preset: one of the bundled examples (`sre-platform`, `tam-presales`, `storage-infra`), **`custom`** (Claude drafts one for your field and saves it in your Drive), or `none`. Everything stays editable.
3. Tell Claude your target countries (e.g. `Singapore, Australia, Germany, Canada`).
4. Upload your CV and say **"build my profile"**.
5. Optional: paste a settings block (format below) to set everything in one go.

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
preset: custom:marketing-manager
mode: watch
countries: Singapore, Australia, United Kingdom
remote_ok: yes
...
END-SETTINGS
```

Every key is documented in `skills/fit-check/references/filters.md`.

## What always stays with you

Passwords and logins, consent and terms checkboxes, diversity questions, date of birth, home address, ID numbers, the final Submit, and sending email.

## LinkedIn

LinkedIn's terms prohibit automation. It is off by default; when enabled the plugin works slowly in your own signed-in browser with a daily cap, and your account carries the risk. Public company ATS boards and official country job portals are the default sources.
