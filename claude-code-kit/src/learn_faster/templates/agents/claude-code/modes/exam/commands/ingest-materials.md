---
description: Ingest the student's own course materials (slides, transcripts, past papers) for source-grounded exam prediction
---

## Context

- Existing learning state: !`ls .learning/ 2>/dev/null`
- Reference: read `.learning/references/exam_prediction.md` before proceeding.

## Your Task

Load the student's real course materials into the learning state so later prediction and review are grounded in *their* professor's content — not generic online examples.

### Step 1 — Ask what they have

Ask the student which materials they can provide (accept file paths or pasted text): lecture slides, professor audio/voice-note transcripts (English or Arabic), past exam papers, official model answers, lab/practical manuals, textbook chapters, class notes. Explicitly request the two strongest prediction sources: **past exam papers** and **model answers**. Also ask for the course name, exam type (midterm/final, written/practical/OSPE), total marks + distribution, and whether the exam includes image/spot identification.

### Step 2 — Store materials

Create `.learning/<topic-slug>/materials/` and save or reference each source there. Record an inventory in `.learning/<topic-slug>/materials/inventory.json` (source type, filename, language).

### Step 3 — Explicit-marker extraction pass (do this first, before anything else)

Following `exam_prediction.md`, scan transcripts/notes for statements where the professor *explicitly* flagged exam material. For Arabic, use the cue table; capture verbatim quote + English translation + the topic it points to + source location. Save to `.learning/<topic-slug>/materials/exam_statements.md` (the "purple" facts). On large transcripts (100+ pages) run this as a lightweight first pass, then chunk-read.

### Step 4 — Build the signal map

Log every topic with its evidence weight (past-paper hit, slide-repetition count, verbal emphasis, model-answer depth) to `.learning/<topic-slug>/materials/signal_map.json`. This feeds `/predict-exam`.

### Step 5 — Confirm

Summarize: sources ingested, count of explicit professor exam statements found, and the top-weighted topics. Tell the student to run `/predict-exam` next.

**Do not** fabricate materials or pull generic exam questions from the web at this stage. Only ingest and analyze what the student provides.
