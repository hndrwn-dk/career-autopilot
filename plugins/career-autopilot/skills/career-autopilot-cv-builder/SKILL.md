---
name: career-autopilot-cv-builder
description: "Use when the user has no CV or an outdated one and says \"buatkan CV\", \"saya belum punya CV\", \"make me a resume\", \"update my CV\", \"CV untuk fresh graduate\", \"CV untuk kembali bekerja\", or when career-autopilot-profile-builder finds no CV. Builds a CV and the Profile through a short interview."
---

# Build a CV by interview

Data store: `${CLAUDE_PLUGIN_ROOT}/references/store.md` (Profile, Filters, Applications, Skip and Stories are documents there; a failed write is reported once).

For anyone: first-time job seekers, returners, people looking for side income, career switchers, experienced
people whose CV is out of date. Writing rules: `${CLAUDE_PLUGIN_ROOT}/references/writing-style.md`.
Segment guidance: `${CLAUDE_PLUGIN_ROOT}/segments/<segment>.md`.

## 1. Interview (plain language, in the user's language)

Ask in small groups of 2–3 questions, never a long form. Adapt to the segment and skip what does not apply.

1. Name, city, phone, email; LinkedIn or portfolio if any.
2. What kind of work they want, and when and how (hours, remote/onsite, how far they can travel).
3. Work history, most recent first: where, what they did, when. Include part-time, family business, freelance, volunteering.
4. For each: one thing they are proud of. Ask for a number when there is one ("berapa pelanggan per hari?").
5. Education and courses, certificates, licences.
6. Skills and tools; languages and level.
7. A break in work history: ask only "Do you want the CV to mention it, and how would you like to describe it?" Use their words.

Never ask for or store: ID numbers, date of birth, marital status, religion, health, photo (unless the user's target country expects a photo and the user wants one).

## 2. Draft

- One page for under ~10 years of experience, at most two pages otherwise.
- Order by segment: fresh-graduate → Education, Projects/Internships, Experience, Skills. side-income → Summary of what they offer, Availability, Experience, Skills. Others → Summary, Experience, Education, Skills.
- Bullets: one action and one result each, from the user's answers only.
- Summary: 2 lines, specific, no buzzwords.

Show the draft as text, apply the user's corrections, then confirm.

## Country formats

Build the version for the country the user applies to (ask when Filters `countries` has several); keep one `cv_<country>` per format.

| Country | Format |
|---|---|
| Indonesia | 1–2 pages; a professional photo is common but optional; no religion or marital status unless the user insists; Indonesian or English as the posting |
| Singapore, Malaysia | 2 pages fine; no photo needed; state work pass status in one line if relevant (e.g. "Requires Employment Pass") |
| Australia, New Zealand, UK, Ireland, US, Canada | no photo, no date of birth or marital status; ATS-friendly (single column, standard headings, no tables or text in images); Australia often uses 2–3 pages |
| Germany, Austria, Switzerland | tabular Lebenslauf, reverse chronological, photo optional; dates as MM/YYYY; often with a cover letter |
| Netherlands, Nordics | concise, 1–2 pages, no photo needed |
| Japan | rirekisho (standard form, photo, handwritten or typed) plus shokumu keirekisho (work history); ask the employer which they want |
| Gulf states | photo and nationality are commonly included; state visa status and notice period |

Everywhere: same facts, only the layout changes. Never invent personal details a format usually asks for; leave them for the user.

## 3. Save

- Make the CV as a document the user can edit and download (a Docs artifact where available, or a .docx when the user asks for Word). Also save a PDF copy to Drive `Career Autopilot/CV/` when a PDF export is available.
- Run career-autopilot-profile-builder on the confirmed text so Profile and Stories are filled, and set `cv_default`.
- Offer a second version when the user targets two kinds of work (e.g. `cv_admin` and `cv_tutor`).
