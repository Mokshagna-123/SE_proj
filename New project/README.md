# FinSpec AI — Project Requirements and SDLC Assistant

## Problem statement

Software teams working on digital personal-loan origination need a clear way to turn a stakeholder description into reviewable software requirements and a suitable delivery lifecycle. FinSpec AI accepts one project description, extracts traceable requirement candidates from that text, flags quality and possible compliance themes, recommends an SDLC approach from the same text, and creates an IEEE-style SRS Word document.

The project domain is financial software requirements engineering. It does not evaluate borrowers, make credit decisions, or provide legal advice.

## Run

Requires Python 3.10+. No package installation or API key is needed.

```powershell
python server.py
```

In Git Bash, if `python` is not on your PATH, run `/c/Users/Moksh/AppData/Local/Programs/Python/Python314/python.exe server.py` from the project folder. The server uses port **8766** by default to avoid an older instance. Open <http://127.0.0.1:8766>. Enter a project description and choose **Generate requirements & SDLC**. Review and edit requirement candidates, add reviewer notes, approve items, or request changes. Optional `.txt`, `.md`, and `.csv` files can supply supporting evidence excerpts. Download the SRS Word document or a JSON project pack. Briefs and review decisions are saved locally and can be reopened under **Saved project briefs**.

## Reference workflow implemented

1. **Requirements Agent:** reads the submitted description only, preserves source excerpts, assigns a category, priority, confidence, and draft status. It targets at least six candidates; when the description does not provide enough direct statements, added items are clearly marked as low-confidence assumptions requiring human review.
2. **Quality and compliance review:** checks wording, likely duplicates, and missing clarification areas. Description-named compliance themes are reminders only. It creates a draft risk register, clarification queue, and requirement-to-description traceability.
3. **Governance & SDLC Agent:** ranks Agile, DevSecOps, Spiral, V-Model, Waterfall, and Agile + V-Model hybrid using lifecycle cues from the description. The result includes the selected approach, explanation, and relative ranking. A loopback-only local LLM may semantically compare the alternatives; deterministic cue scoring is the no-model fallback.
4. **Evidence and review:** optional text documents are matched to the project description and shown as source-labelled evidence excerpts. Requirement extraction and SDLC remain based only on the project description. Review decisions and agent steps are saved in an audit trail.
5. **SRS Generation Agent:** creates a Word `.docx` using IEEE 830-style sections. It includes the original brief, requirement statements with trace excerpts, quality/risk/evidence/review records, SDLC advice, and monospaced use-case, sequence, and state diagrams. The JSON project pack carries the structured outputs and simple coverage counters.

## Source boundary

The project description is the sole source for requirement extraction and SDLC selection. Optional uploaded text is evidence-only and does not influence either output. No project-characteristic sliders are used. An optional OpenAI-compatible model may be configured through `FINSPEC_LLM_URL` only when hosted on loopback (`localhost` / `127.0.0.1`); it receives only the submitted description, its requirement suggestions are accepted only when they include an exact source excerpt, and its SDLC ranking must cover all six alternatives. If no local endpoint is configured or it fails, deterministic extraction and lifecycle cue scoring are used. No cloud LLM endpoint is accepted. Evidence matching uses simple lexical term overlap; it is not a semantic vector database. Coverage counters are descriptive and do not establish measured improvement over a real baseline. Compliance flags and risks are reminders for human review, not a compliance determination. Assumption candidates are not facts and must be confirmed or rejected by the project team.

## Files

- `server.py` — requirements extraction, quality checks, SDLC selection, and Word SRS generation.
- `public/` — the single-brief interface and generated results view.
- `docs/SRS.md` — project specification for this prototype.
