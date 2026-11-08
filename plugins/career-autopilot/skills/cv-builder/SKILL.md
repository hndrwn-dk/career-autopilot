---
name: cv-builder
description: "Use when the user has no CV or an outdated one and says \"buatkan CV\", \"saya belum punya CV\", \"make me a resume\", \"update my CV\", \"CV untuk fresh graduate\", \"CV untuk kembali bekerja\", or when profile-builder finds no CV. Builds a CV and the Profile through a short interview."
---

# Build a CV by interview

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

## 3. Save

- Make the CV as a document the user can edit and download (a Docs artifact where available, or a .docx when the user asks for Word). Also save a PDF copy to Drive `Career Autopilot/CV/` when a PDF export is available.
- Run profile-builder on the confirmed text so Profile and Stories are filled, and set `cv_default`.
- Offer a second version when the user targets two kinds of work (e.g. `cv_admin` and `cv_tutor`).
