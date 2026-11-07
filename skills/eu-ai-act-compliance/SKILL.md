---
name: eu-ai-act-compliance
description: Specialist for the EU AI Act (Regulation (EU) 2024/1689). Use whenever a project builds, uses, sells or deploys AI in or for the EU: apps that call an AI model (Claude, GPT, etc.), chatbots, AI-generated images/video/voice/text, deepfakes, scoring or ranking people, biometrics, emotion recognition, AI in hiring, education, credit, insurance or health. Classifies the risk level, names the owner's role (provider/deployer), lists the obligations and deadlines that apply, and writes a compliance file for the project. Not legal advice.
---

# EU AI Act compliance specialist

Reply in the user's language. You produce a practical assessment, not legal advice: always end by telling the owner to confirm with a lawyer before launch.

## Before you start

- Dates and secondary rules are still moving (the Commission's "Digital Omnibus" proposal of late 2025 proposed delaying some high-risk deadlines; guidelines and codes of practice keep being published). **Check the current official timeline before stating any date as fact**, using:
  - Official text: https://eur-lex.europa.eu/eli/reg/2024/1689/oj
  - Commission AI Act page: https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai
  - AI Act Service Desk / AI Office guidance.
  - Spain: AESIA (Agencia Española de Supervisión de la Inteligencia Artificial), https://aesia.digital.gob.es
- Read the project's audit folder (`docs/audit/`, see `project-audit-log`) if it exists, so the assessment uses real facts about the system.

## Step 1: Is it an "AI system" and is the AI Act in scope?

- AI system (Art. 3(1)): machine-based, some autonomy, infers from input how to generate outputs (predictions, content, recommendations, decisions). Apps that call an LLM API count.
- Territorial scope (Art. 2): placed on the EU market, used in the EU, or its output is used in the EU, even if the company is outside the EU.
- Out of scope: purely personal non-professional use; scientific R&D before market; military/defence; some open-source (not if prohibited, high-risk or Art. 50).

## Step 2: Name the owner's role (Art. 3)

- **Provider**: develops the AI system (or has it developed) and puts it on the market or into service under their own name. Building an app on top of an AI API and publishing it usually makes the owner a provider of that AI system.
- **Deployer**: uses an AI system under their own authority in a professional activity.
- Importer, distributor, authorised representative: other chain roles.
- A deployer becomes a provider if they put their name on a high-risk system, substantially modify it, or change its purpose so it becomes high-risk (Art. 25).
- **GPAI model provider** (Art. 53): only if they train/release a general-purpose model. Using Claude or GPT through an API does not make the owner a GPAI provider; the model maker carries those duties.

## Step 3: Classify the risk

1. **Prohibited (Art. 5)**: stop and tell the owner it cannot ship. Includes: harmful subliminal/manipulative techniques; exploiting vulnerabilities (age, disability, social or economic situation); social scoring; predicting crime only from profiling/personality; untargeted scraping of facial images to build face databases; emotion recognition at work or in education (except medical/safety); biometric categorisation to infer race, political views, union membership, religion, sex life or orientation; real-time remote biometric identification in public spaces for law enforcement (narrow exceptions).
2. **High-risk (Art. 6)**:
   - Safety component of a product under EU harmonisation law in Annex I (toys, machinery, medical devices, vehicles, lifts, radio equipment...) that needs third-party conformity assessment. Relevant for robotics/hardware projects.
   - Annex III areas: biometrics; critical infrastructure; education and training (admission, grading, proctoring); employment (CV screening, promotion, firing, task allocation, monitoring); essential services (public benefits, creditworthiness, life/health insurance pricing, emergency dispatch); law enforcement; migration and border; justice and democratic processes.
   - Art. 6(3) exception: an Annex III system is not high-risk if it only does a narrow procedural task, improves a finished human activity, detects patterns without replacing human assessment, or is preparatory. Never applies if it profiles people. If you use it, document why (Art. 6(4)) and register it.
3. **Transparency duties (Art. 50)**, apply on top of any level:
   - Chatbots and any AI that talks with people: tell users they are dealing with AI unless obvious.
   - Generated or edited audio, image, video, text: mark outputs as AI-generated in a machine-readable way (provider duty).
   - Deepfakes: deployer must disclose they are artificially generated or manipulated (lighter rule for clearly artistic, satirical or fictional work).
   - AI-generated text published to inform the public on matters of public interest: disclose, unless human-reviewed under editorial responsibility.
   - Emotion recognition or biometric categorisation: inform the people exposed.
4. **Minimal risk**: no specific duties beyond AI literacy; voluntary codes encouraged.

## Step 4: Obligations that apply

**Everyone (Art. 4, AI literacy)**: providers and deployers make sure people who operate the AI have enough AI literacy. Keep a short record of how (training, guide).

**High-risk providers**: risk management system (Art. 9); data and data governance (Art. 10); technical documentation per Annex IV (Art. 11); automatic logs (Art. 12); instructions for deployers (Art. 13); human oversight design (Art. 14); accuracy, robustness, cybersecurity (Art. 15); quality management system (Art. 17); keep documentation 10 years (Art. 18); conformity assessment (Art. 43); EU declaration of conformity (Art. 47); CE marking (Art. 48); registration in the EU database (Art. 49); post-market monitoring (Art. 72); serious-incident reporting (Art. 73).

**High-risk deployers (Art. 26)**: use per instructions; assign competent human oversight; check input data is relevant; monitor and report risks/incidents; keep logs at least 6 months; inform workers and affected people; fundamental-rights impact assessment (Art. 27) when a public body or providing public services, or for credit scoring and life/health insurance pricing. Do the GDPR DPIA too (see `gdpr-compliance`).

**Penalties (Art. 99)**: prohibited practices up to €35M or 7% of worldwide turnover; most other obligations up to €15M or 3%; wrong or misleading information to authorities up to €7.5M or 1%. For SMEs and start-ups, the lower of the two amounts.

## Step 5: Timeline (verify before quoting, see "Before you start")

As originally adopted: in force 1 Aug 2024; prohibitions and AI literacy from 2 Feb 2025; GPAI model duties and penalties from 2 Aug 2025; most rules, including Annex III high-risk and Art. 50 transparency, from 2 Aug 2026; Annex I product high-risk from 2 Aug 2027.

## Step 6: Write the compliance file

Create or update `docs/compliance/AI-ACT.md` in the project:

```
# EU AI Act assessment: <project>
Date: <YYYY-MM-DD>   Assessed by: Claude (<model>) for <owner>   Status: draft, pending legal review
## System description      (purpose, users, AI models/APIs used, inputs, outputs, where used)
## Role                    (provider / deployer / ..., with reason)
## Risk classification     (prohibited / high-risk (which Annex point) / Art. 50 / minimal, with reason)
## Obligations that apply  (checklist: [ ] item, article, owner of the task, evidence link)
## Transparency notices    (exact text shown to users, where it appears)
## Human oversight         (who can stop or override the AI, how)
## Open questions for the lawyer
## Sources checked         (links + date checked)
```

Then:
- Add the user-facing AI notice to the product (e.g. "Este asistente usa inteligencia artificial"), label AI-generated media, and mention AI use in the privacy policy.
- Log the assessment in the project's audit journal (`project-audit-log`).
- Give the owner a short summary: risk level, top 3 actions, what needs a lawyer.
