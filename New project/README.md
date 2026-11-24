# FinSpec AI — Financial Requirements & SDLC Decision Support

## Problem statement

Financial-sector software projects gather requirements from stakeholders, documents, controls, and legacy interfaces. Manual analysis can miss requirements, leave ambiguity and conflict unresolved, weaken traceability, or delay security/compliance validation. FinSpec AI turns a stakeholder brief and project context into structured requirement candidates, source-linked evidence, quality findings, and a ranked, justified SDLC recommendation with a project-specific workflow.

The demonstrator uses **Indian digital personal-loan origination**. This is requirements engineering and SDLC decision support: it does not score borrowers, approve loans, or make legal determinations.

## Run

Requires Python 3.10+. No package installation or cloud API key is needed.

```powershell
python server.py
```

Open http://127.0.0.1:8765. Edit the seeded project brief and delivery-factor sliders, import supporting TXT/MD notes or CSV content, then select **Analyze & recommend**. Review the requirements, quality findings, evidence, ranked SDLC models, workflow, and generated outputs. Approve the baseline or request changes with a comment.

## Architecture

The orchestrator runs sequentially:

1. **Requirements Analysis Agent:** extracts functional/nonfunctional requirement candidates; classifies, checks ambiguity/conflict/duplicates, raises clarification questions, and retrieves source evidence.
2. **Decision & SDLC Agent:** uses visible project characteristics and deterministic MCDA/rules to rank Agile, DevSecOps, Spiral, V-Model, Waterfall, and an Agile–V-Model hybrid.
3. **Documentation stage:** generates a run-specific SRS, user stories, use cases, acceptance criteria, compliance mapping, risk register, traceability matrix, open issues, assumptions, and project-specific SDLC workflow.

Optional local-model requirement suggestions are supported via `FINSPEC_LLM_URL` and optionally `FINSPEC_LLM_MODEL` (OpenAI-compatible local endpoint). Suggestions remain low-confidence and require human validation. The deterministic analysis and SDLC engine work without a model.

## Generated outputs

Every run provides the ten common reports: Input Analysis, Risk Assessment, Anomaly/Issue, Evidence, Decision Evaluation, Recommendation, Action Plan, Human Review, Audit Trail, and Performance. It also generates an SRS, User Stories, Use Cases, Acceptance Criteria, Compliance Control Matrix, Threat and Risk Register, Requirements Traceability Matrix, Open Issues, SDLC Workflow, and Assumptions/Dependencies. Download each artifact individually or export the full JSON bundle.

## Evidence and privacy

The local knowledge base includes source-attributed RBI and MeitY summaries with official URLs, jurisdiction/version metadata, and topical tags. It is seed evidence only. Compliance or legal stakeholders must verify current text, applicability, and effective dates before relying on a mapping. Retrieval currently uses lexical token overlap.

Common direct identifiers are masked before project text is persisted. This is not guaranteed anonymization. Use synthetic or approved de-identified project data; do not enter live applicant data. Review roles are simulated workflow labels; the prototype has no authenticated accounts, enforceable RBAC, or production security controls.

## Evaluation

The performance report compares structured requirement candidates with a naive sentence-extraction baseline and reports completeness, traceability, category coverage, and evidence-link proxies. The seeded case is synthetic; metrics are not external validation. The project SRS is [docs/SRS.md](docs/SRS.md).
