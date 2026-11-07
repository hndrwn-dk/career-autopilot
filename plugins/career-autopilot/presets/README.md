# Role presets

A preset tells Career Autopilot what a good match looks like for one kind of role. The bundled files
(`sre-platform`, `tam-presales`, `storage-infra`) are examples for tech roles. Any profession works the same way.

## Where presets live

| Kind | Location | Filters value |
|---|---|---|
| Bundled | this folder | `preset: sre-platform` |
| Custom (per user) | the user's Drive, `Career Autopilot/presets/<name>.md` | `preset: custom:<name>` |

Several presets: comma list, e.g. `preset: custom:product-marketing, tam-presales`.
Custom presets stay in the user's own Drive, so they never end up in this repo.

## Template

```markdown
# Preset: <name>

<one line: who this is for>

| Key | Value |
|---|---|
| target_roles | <titles, comma list> |
| keywords | <search terms, comma list> |
| seniority | <allowed levels> |
| exclude_keywords | <title words to skip> |
| min_match | 75 |
| weights | must_have:45, years:15, stack:20, certs:10, domain:5, scope:5 |

## Skill groups (overlap counts once per group)

- <Group>: <tool, method or skill>, <…>

## Credential equivalents (a credential counts as proof of the skill)

<licence / certification> → <skill>

## Things to check in these postings

- <field-specific red flags or checks, e.g. licence required in that country, shift work, travel, quota>
```

`stack` in weights means "skills, tools and methods" for any field: software for engineers, instruments and procedures for clinicians, channels and platforms for marketers.
`certs` covers certifications, licences and registrations (e.g. CPA, nursing registration, PMP).

## Examples of custom presets

- `custom:registered-nurse` — skill groups: ICU, ED, med-surg; credential check: nursing registration in the target country (flag if a conversion exam is needed).
- `custom:finance-controller` — skill groups: IFRS/GAAP, consolidation, ERP (SAP, Oracle, NetSuite); credentials: CPA, ACCA, CA.
- `custom:product-designer` — skill groups: research, interaction, visual, design systems; portfolio link required.
