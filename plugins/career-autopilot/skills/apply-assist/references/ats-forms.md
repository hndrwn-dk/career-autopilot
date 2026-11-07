# Form patterns by ATS / portal

General: prefer the page's form-input tool for text fields; use clicks for custom radios, comboboxes and flag pickers. Take a screenshot before and after each page of a multi-step form.

## Greenhouse / Lever / Workable / Recruitee
Plain inputs. Location is often an autocomplete: type the city, pick from the list. Custom questions at the end: answer only from Profile.

## Ashby
Upload the CV first and wait for parsing to autofill name/email, then correct anything it got wrong.

## SmartRecruiters
Often ends with an equal-opportunity survey: leave it.

## Workday (*.myworkdayjobs.com)
Needs an account: the user signs in. Multi-page; "My Experience" can import from the CV, then check each role's dates. Skills field: type, Enter, tick the option. Save errors are server-side: ask the user to sign in again.

## Oracle Recruiting / SuccessFactors / Taleo
Start with email + terms (the user ticks). Sessions expire fast; refill if bounced to the job page. Phone country code is a combobox: type the country, pick it.

## iCIMS
Form sits in a same-origin iframe; fill through it. File upload inside the iframe usually needs the user to click.

## MyCareersFuture (Singapore)
Applying needs Singpass sign-in by the user. After sign-in the form is short: CV pick plus screening questions. Treat screening questions as Yes/No rule 4 in guardrails.

## LinkedIn Easy Apply
Check phone country code. Replace any remembered cover letter. Last page often has a follow-company checkbox: untick only if the user asks.

## Email applications
Hand over to recruiter-email.
