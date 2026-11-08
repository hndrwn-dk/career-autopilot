# Role presets

A preset tells Career Autopilot what a good match looks like for one kind of role: target titles, search keywords,
skill groups, credential equivalents, scoring weights and field-specific checks. Presets are optional; without one,
career-autopilot-fit-check scores each posting against its own requirements.

## Layout

```
presets/
  README.md          this file
  _template.md       empty template for a new preset
  examples/          ready-to-use examples, one file per field
```

Examples in `examples/`:

| Name | Field |
|---|---|
| finance-accounting | accounting, controlling, FP&A, audit |
| healthcare-nursing | registered nurses and nurse leaders |
| marketing-digital | digital, performance, content and brand marketing |
| operations-supply-chain | supply chain, logistics, procurement, operations |
| sre-platform | SRE, platform, DevOps, cloud infrastructure |
| storage-infra | storage, backup and data infrastructure |
| tam-presales | technical account managers, solutions architects, pre-sales |

## Where presets live

| Kind | Location | Filters value |
|---|---|---|
| Example | `presets/examples/<name>.md` in this plugin | `preset: finance-accounting` |
| Custom (per user) | the user's Drive, `Career Autopilot/presets/<name>.md` | `preset: custom:<name>` |

Several presets: comma list, e.g. `preset: custom:product-marketing, marketing-digital`.
Custom presets stay in each user's Drive and never enter this repo. To start from an example, ask
"copy the marketing-digital preset and adjust it for me": setup saves the copy as a custom preset.

## Writing one

Copy `_template.md`. Notes:
- `stack` in weights means skills, tools and methods for any field: software for engineers, procedures for clinicians, channels and platforms for marketers.
- `certs` covers certifications, licences and registrations.
- Keep "Things to check" to points that change whether someone should apply.

## Contributing an example

Add a file to `examples/` and a row to the table above. Keep it field-generic: no personal data, no company names.
