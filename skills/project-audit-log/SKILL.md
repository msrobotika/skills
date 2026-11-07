---
name: project-audit-log
description: Always-on audit trail for every project built with Claude Code. Use at the start of any project work (new or existing, code or not), and keep using it after every meaningful step: creating files, design or tech decisions, adding dependencies or third-party services, handling personal data, using AI models, tests, releases. Keeps an append-only, dated, step-by-step record in docs/audit/ (journal, decisions, data and AI inventories, dependencies, evidence) so the owner can answer an audit (GDPR, EU AI Act, security, client or tax) months later. Also use when the user asks "what did we do", "document this", or "prepare for an audit".
---

# Project audit log

Reply in the user's language. Your job is to leave a record that a stranger (an auditor, a lawyer, the owner a year from now) can follow without asking anyone. Write facts, not marketing.

## When it runs

- **Start of work on a project**: if `docs/audit/` does not exist, create it (see structure). If it exists, read `README.md` and the last entries of `JOURNAL.md` first.
- **After every meaningful step**: add a journal entry. Batch tiny edits into one entry per step; never skip a step that changed behaviour, data, dependencies, security or AI use.
- **End of a session**: add a closing entry: what was done, what is pending, what was not verified.
- Not a git repo? Still keep the log; suggest `git init` so the history is verifiable.

## Structure (create once, per project)

```
docs/audit/
  README.md          what the project is, owner, start date, how to read this folder
  JOURNAL.md         append-only step-by-step log (main record)
  DECISIONS.md       decision records (why we chose X over Y)
  DATA-INVENTORY.md  personal data handled: what, why, where, who receives it, retention
  AI-USE.md          AI models/services used, for what, by whom (Claude Code itself included), AI Act class
  DEPENDENCIES.md    libraries, APIs and services with version, license, purpose, date added
  SECURITY.md        secrets handling, access, known risks, incidents (no secret values ever)
  RELEASES.md        each release/deploy: date, version/commit, what changed, checks run
  evidence/          test outputs, screenshots, exported reports (redacted)
docs/compliance/     filled by the gdpr-compliance and eu-ai-act-compliance skills
```

## Journal entry format (JOURNAL.md)

Newest at the bottom. Never edit or delete past entries; to fix one, add a new entry that says "Correction to <entry id>".

```
### <YYYY-MM-DD HH:MM TZ> · #<n> · <short title>
- Who: owner request / Claude (<model>) / owner by hand
- Asked: <the owner's request in one line>
- Done: <what changed, in plain words>
- Files: <paths created/changed/deleted>
- Commands/tools: <key commands run, installs, external services touched>
- Why: <reason, or link to DECISIONS.md #n>
- Data/AI impact: <none | what personal data or AI use changed → updated DATA-INVENTORY / AI-USE>
- Checked: <tests run and result, or "not verified">
- Commit: <hash, if any>
```

## Decision record format (DECISIONS.md)

```
## D<n> · <YYYY-MM-DD> · <decision>
Context: <problem>
Options: <A, B, C>
Chosen: <X>, because <reasons>
Consequences: <trade-offs, follow-ups>
```

## Rules

- **Truthful**: write what really happened, including failures, skipped steps and things not tested. Never backfill invented entries; if earlier steps were not logged, add one entry "Reconstructed from git history on <date>" and mark it as reconstructed.
- **No secrets or personal data in the log**: no passwords, keys, tokens, real customer data. Name the secret ("Stripe test key in .env") but not the value. Redact screenshots.
- **Timestamps**: real local date and time with timezone (get them from the system, do not guess).
- **Link, don't copy**: refer to commits, files and compliance docs instead of duplicating them.
- **Keep inventories current**: any new dependency, third-party service, data field or AI use updates the matching file in the same step.
- **AI transparency**: record that Claude Code (and any other AI, e.g. Codex) wrote or changed code, with the model name. Some audits and clients ask for this.
- Commit the audit files together with the change they describe when the project uses git.

## Hand-offs to other specialists

- New or changed personal data → run or update `gdpr-compliance`.
- New or changed AI feature → run or update `eu-ai-act-compliance`.
- Before a release → add a RELEASES.md entry with the checks run, and point to the latest compliance files.

## "Prepare for an audit" request

Produce `docs/audit/AUDIT-PACK.md`: project summary; timeline of key entries; decision list; current data inventory, AI use and dependencies; compliance status with open gaps; evidence index; known limitations. State the date range covered and anything missing. Offer to export it as PDF or a doc.
