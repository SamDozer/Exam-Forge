---
description: Produce a source-grounded exam prediction + study guide from ingested materials, and seed the spaced-repetition scheduler
---

## Context

- Learning state: !`ls .learning/ 2>/dev/null`
- Reference: read `.learning/references/exam_prediction.md` before proceeding.

## Your Task

Turn the ingested materials into (1) a study guide + (2) an evidence-ranked prediction of the actual exam, then seed the review scheduler so daily drills use the predicted paper.

### Step 1 — Load ingested state

Read from `.learning/<topic-slug>/materials/`: `inventory.json`, `exam_statements.md` (purple facts), and `signal_map.json`. If these don't exist, tell the student to run `/ingest-materials` first and stop.

### Step 2 — Predict, using the signal hierarchy

Following `exam_prediction.md`:
- Rank topics by evidence (past papers strongest → model answers → slide repetition → verbal emphasis → insider info → textbook).
- Reverse-engineer the professor's question style and paper structure from past papers + model answers.
- Generate predicted questions with model answers, each tagged 🔴HIGH / 🟡MEDIUM / 🟢LOW with a one-line signal justification, mirroring the professor's phrasing and answering to the mark depth.
- Keep **purple** (professor said it) visually and logically distinct from **red** (predicted).

### Step 3 — Build the guide

Ask the student: deep no-missing-detail guide, ultra-condensed rapid sheet, both, or strict-extract (professor's flagged points only). Ask output format (HTML default, or Markdown). Build only the sections the material justifies — activate calculations, visual/data-ID, and protocol sections only when the content is present; keep the image machinery available for image-heavy courses. Save to `.learning/<topic-slug>/exam_guide.html` (or `.md`).

### Step 4 — Seed the review scheduler (the merge payoff)

Convert HIGH/MEDIUM predicted questions and the purple must-know facts into review items and register them with the existing scheduler, e.g.:
```
python3 .learning/scripts/review_scheduler.py --add --topic "<topic-slug>" --from-guide
```
If the script has no such flag, write the items into the topic's `review_schedule.json` in the same shape the scheduler already reads (mirror an existing entry), prioritizing by confidence tag and exam marks. This makes the spaced-repetition drills the *actual predicted paper*, not generic questions.

### Step 5 — Report

Summarize the top HIGH-confidence predictions, note which extra source (usually more past papers) would most improve accuracy, and tell the student that `/review` will now drill these on a spaced schedule and `/generate-exam` will build a printable mock from them.

**Faithfulness:** stay bound to the student's materials; flag any outside-source clarification; never substitute generic web questions when real materials exist.
