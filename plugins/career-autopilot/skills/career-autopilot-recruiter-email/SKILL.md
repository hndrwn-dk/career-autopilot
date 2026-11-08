---
name: career-autopilot-recruiter-email
description: "Use when a posting says to apply by email, or the user says \"email the recruiter\", \"draft an application email\", \"reply to this recruiter\", \"buatkan email lamaran\", \"balas email rekruter\", \"follow up on my application\", or when career-autopilot-inbox-sync finds a recruiter message that needs a reply."
---

# Recruiter email: draft, then send on approval

Guardrails: `${CLAUDE_PLUGIN_ROOT}/skills/career-autopilot-apply-assist/references/guardrails.md`.
Writing: `${CLAUDE_PLUGIN_ROOT}/references/writing-style.md` for every draft (application, reply, follow-up, thank-you note). Scam check `${CLAUDE_PLUGIN_ROOT}/references/scam-signals.md` on every incoming message before drafting: an always-skip signal → no draft, tell the user why.

## Application by email

1. Recipient: from the posting or the user only.
2. Subject: what the posting asks for; else `Application: <Role> – <full_name>` (+ reference number if any).
3. Body, under 180 words, in the posting's language: the role and where it was seen · 3–4 lines of the strongest matching facts from Profile and Stories · work authorization in one line if relevant · notice period · sign-off with name, regional phone, LinkedIn.
4. Attach the chosen CV from Drive `Career Autopilot/CV`. If attaching is not possible, say so; share a Drive link only if the user agrees.
5. Create a Gmail draft and show recipient, subject and body.
6. Send only on the user's word. Then log to `Applications` (Channel `Email`, recipient in Notes).

## Replies

- Same thread. Propose interview times only from Filters `availability` or what the user says now; check Google Calendar for clashes if connected.
- Agency recruiter asking for the client name, rate or package: draft a reply that asks for the client, role scope, employment model, duration and conversion terms before sharing expectations. Include the user's expectation only if the user tells you to.
- Follow-up: only when asked, at least 7 days after applying, one short message.

## Style

Follow writing-style.md. Language: the recruiter's. After the user edits a draft, offer once to save their wording as `writing_sample`.

## Other messages it can draft

- Thank-you note after an interview (same day, under 100 words, one specific point from the conversation the user tells you).
- Polite withdrawal or declining an offer, only when the user decides to.
- Freelance proposals and replies to clients on marketplaces (text for the user to paste).
