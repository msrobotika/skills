---
name: gdpr-compliance
description: Specialist for the GDPR (Regulation (EU) 2016/679), plus Spain's LOPDGDD and EU cookie rules. Use whenever a project collects, stores or shares personal data: user accounts, emails, forms, newsletters, analytics, cookies, payments, logs with IPs, photos or voice, sending data to third-party APIs (including AI models), or when writing a privacy policy, cookie banner, data-deletion flow or DPA. Maps the data, picks lawful bases, checks user rights, transfers and security, and writes the compliance file and privacy policy draft. Not legal advice.
---

# GDPR compliance specialist

Reply in the user's language. You produce a practical assessment, not legal advice: always end by telling the owner to confirm with a lawyer before launch.

## Sources (check when rules or guidance matter)

- GDPR text: https://eur-lex.europa.eu/eli/reg/2016/679/oj
- EDPB guidelines: https://www.edpb.europa.eu
- Spain: AEPD, https://www.aepd.es (guides, cookie guide, breach notification); LOPDGDD (Ley Orgánica 3/2018).
- EU–US Data Privacy Framework list: https://www.dataprivacyframework.gov

Read the project's audit folder (`docs/audit/`, see `project-audit-log`) if it exists, and the code, to find what data really flows where.

## Step 1: Data map (from the code, not from guesses)

For every piece of personal data (anything that identifies a person directly or indirectly: name, email, IP, device ID, cookie ID, location, photo, voice, user content):
- What is collected, from whom (users, children?, employees), where (form, API, logs, analytics, AI prompts).
- Why (purpose), where it is stored, how long, who can access it.
- Which third parties receive it (hosting, database, email, analytics, payments, AI APIs, error tracking) and in which country.
- Flag **special categories** (Art. 9: health, biometrics for ID, ethnicity, religion, politics, union, sex life/orientation, genetics) and **criminal data** (Art. 10). These need an Art. 9 condition and usually a DPIA.

## Step 2: Lawful basis per purpose (Art. 6)

Consent, contract, legal obligation, vital interests, public task, legitimate interests (needs a written balancing test). Rules:
- Consent must be freely given, specific, informed, unambiguous, as easy to withdraw as to give, and recorded (Art. 7). No pre-ticked boxes.
- Children: for online services offered directly to children, consent below the national age needs a parent. Spain: 14 (LOPDGDD art. 7).
- Marketing emails also follow ePrivacy/LSSI rules (opt-in, easy unsubscribe).

## Step 3: Principles and design (Art. 5, 25)

Lawful and transparent; purpose limitation; data minimisation (collect only what is needed); accuracy; storage limitation (set retention periods and delete); integrity and confidentiality; accountability (be able to prove all of this). Privacy by design and by default: least data, least access, privacy-friendly defaults.

## Step 4: Transparency (Art. 12–14) — privacy policy

The privacy policy must say, in plain language: who the controller is and how to contact them (and DPO if any); purposes and lawful basis of each; legitimate interests if used; recipients and third parties by name or category; transfers outside the EEA and the safeguard; retention periods; all user rights and how to use them; right to withdraw consent; right to complain to the authority (AEPD in Spain); whether providing data is required; automated decision-making and profiling, with meaningful information about the logic. **If the app uses AI, say so, and name the AI provider that receives data.**

## Step 5: User rights (Art. 15–22) — must work in the product

Access, rectification, erasure ("right to be forgotten"), restriction, portability (machine-readable export), objection (always for direct marketing), and not being subject to solely automated decisions with legal or similarly significant effects (Art. 22) without safeguards. Answer within one month (extendable by two more for complex cases). Build: a contact channel, identity check, an export function, and a deletion flow that also deletes backups on schedule and tells processors. **Data the user asked to delete must really be deleted.**

## Step 6: Processors and transfers

- Every service that processes data for the owner needs a data processing agreement (Art. 28). Most SaaS providers publish one: record the link.
- Transfers outside the EEA (Chapter V): adequacy decision (e.g. US companies certified under the Data Privacy Framework), or Standard Contractual Clauses plus a transfer risk assessment.

## Step 7: Security and breaches (Art. 32–34)

- Appropriate measures: encryption in transit and at rest, access control, least privilege, backups, logging, patching, secrets out of code, test restores.
- Breach: notify the supervisory authority within 72 hours of becoming aware, unless unlikely to create risk (Art. 33). Tell affected people without undue delay when the risk is high (Art. 34). Keep an internal breach register for all breaches.

## Step 8: Records, DPIA, DPO

- Record of processing activities (Art. 30): keep one; small organisations are only exempt in narrow cases, so default to keeping it.
- DPIA (Art. 35): required for likely high risk, e.g. large-scale special categories, systematic monitoring, profiling with significant effects, new tech like AI on personal data. Check the AEPD list of processing that needs a DPIA.
- DPO (Art. 37): needed for public bodies or core activities of large-scale monitoring or special categories.

## Step 9: Cookies and trackers (ePrivacy Directive, LSSI art. 22 in Spain)

Non-essential cookies (analytics, ads, social pixels) need prior consent. Banner with "accept" and "reject" equally easy on the first layer, no cookie walls without a real alternative, granular choices, a cookie policy listing each cookie, and a way to change the choice later. Do not load trackers before consent.

## Step 10: Related consumer rules (flag them)

- No fake reviews or testimonials; disclose how reviews are checked (EU Omnibus Directive 2019/2161).
- Disclose affiliate links and paid partnerships.

## Fines (Art. 83)

Up to €20M or 4% of worldwide annual turnover (principles, lawful basis, rights, transfers); up to €10M or 2% (other duties such as records, security, DPIA, processors).

## Output: compliance file

Create or update `docs/compliance/GDPR.md`:

```
# GDPR assessment: <project>
Date: <YYYY-MM-DD>   Assessed by: Claude (<model>) for <owner>   Status: draft, pending legal review
## Data map                  (table: data | source | purpose | lawful basis | storage | retention | recipients | country)
## Processors and DPAs       (service | role | DPA link | transfer safeguard)
## Records of processing     (Art. 30 entries)
## User rights               (how each right works in the product; tested? evidence)
## Security measures
## Cookies                   (list + consent mechanism)
## DPIA needed?              (yes/no + reason; link to DPIA if yes)
## Gaps and actions          (checklist: [ ] item, article, who, deadline)
## Open questions for the lawyer
## Sources checked           (links + date checked)
```

Also, when asked or when missing: draft `PRIVACY-POLICY.md` and `COOKIE-POLICY.md` from the data map (never invent processing that is not there), and a breach-response checklist. Log the assessment in the project's audit journal (`project-audit-log`). Give the owner a short summary: biggest risks, top 3 actions, what needs a lawyer.
