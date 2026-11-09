# ExamForge

> [!IMPORTANT]
> **This project has moved to [SamDozer/exam-study-guide-predictor](https://github.com/SamDozer/exam-study-guide-predictor) and is no longer maintained.**
>
> Everything useful here was merged into that repository: the exam-solving layer, the Learn FASTER kit (now `learn-faster-kit/`, "Enhanced Learn FASTER"), and the spaced-repetition hand-off. The prediction method there is newer and stronger. It adds slide-formatting detection, scope and per-doctor analysis, past papers read from photos, Egyptian exam question styles, and optional Anki import.
>
> Install the skill from [`dist/exam-study-guide-predictor.skill`](https://github.com/SamDozer/exam-study-guide-predictor/blob/main/dist/exam-study-guide-predictor.skill) instead of `dist/examforge.skill`. This repository is archived and kept for reference only.

**Predict the paper → forge the study guide → drill it to retention.**

ExamForge turns your *own* course material — lecture slides, professor transcripts (English or Arabic), past exam papers, model answers, lab manuals, notes — into a source-grounded study guide, an evidence-ranked prediction of what the exam will actually ask, and a spaced-repetition drill built from that prediction.

Built for **biology-family courses** (biotechnology, biology, biochemistry, bioinformatics, chemistry, microbiology, molecular biology) but adapts to the material you give it.

## Two entry points, one prediction core

ExamForge exists because two things a student needs live in two different runtimes:

| | Runtime | Gives you | Persistence |
|---|---|---|---|
| **ExamForge skill** | claude.ai chat | One-shot: study guide + exam prediction (HTML/docx) | None (single session) |
| **Enhanced Learn FASTER** | Claude Code / Codex CLI | Ongoing coached spaced repetition, progress tracking, printable mock exams | Yes (`.learning/` state across days) |

They share one intelligence: the same signal-weighting, "purple" explicit-marker extraction, Arabic-cue parsing, and faithfulness rules. Use the skill for a fast guide with zero setup; graduate to the CLI kit when you want the predicted paper drilled on a spaced schedule until exam day.

## What makes it different from stock Learn FASTER

Stock Learn FASTER generates practice from concepts you've already learned in the tool and even *searches online for exam examples*. ExamForge inverts that: it **ingests your professor's actual materials**, extracts what the professor explicitly said is on the exam, predicts the real paper with confidence tags, and seeds the spaced-repetition scheduler with **those** questions — not generic ones.

Key features:
- **Purple vs red** — what the professor literally said is on the exam (fact, quoted, Arabic translated) is kept distinct from what ExamForge predicts is likely (inference, confidence-tagged).
- **Evidence-weighted prediction** — past papers strongest, then model answers, slide repetition, verbal emphasis, your insider tips; textbook last.
- **Reads Arabic transcripts** — catches spoken cues like *"ده مهم للامتحان"* and folds them into English output.
- **Marks-driven** — asks total marks + distribution and prioritizes accordingly.
- **Conditional sections** — calculations, visual/spot-ID tables, and protocol breakdowns activate only when the material contains them.
- **Source-faithful** — bound to your materials; outside knowledge only for central-but-poorly-explained points, always flagged.

## Install & use

### A. The chat skill (fastest)
Download `dist/examforge.skill` and use **Save skill** in the Claude app / claude.ai (availability depends on plan/org), or drop `skill/examforge/` into a Claude Code skills directory. Then just say *"predict my microbiology final from these slides"* and attach files.

### B. The Claude Code kit (ongoing spaced repetition)
Needs [`uv`](https://docs.astral.sh/uv/). Install the **bundled, enhanced** kit from this repo (not Hugo's original — the ExamForge commands only exist here):
```bash
uv tool install learn-faster --from ./claude-code-kit
learn-faster                 # choose Exam-Oriented mode
```
Then, in a project directory:
```
/ingest-materials     # load your slides, transcripts, past papers, model answers
/predict-exam         # source-grounded prediction + guide; seeds the review scheduler
/review               # spaced-repetition drills on the predicted paper
/generate-exam        # printable mock exam (PDF) from your material
```

The chat skill can also emit a `learn-faster-handoff.md` to seed the kit if you started in chat.

## Repository layout

```
skill/examforge/            # claude.ai chat skill (SKILL.md + references)
dist/examforge.skill        # packaged, installable skill
claude-code-kit/            # Learn FASTER (MIT © Hugo Lau), extended with ExamForge exam commands
docs/how-it-fits.md         # how the two entry points share one prediction core
NOTICE.md                   # component attribution & license details
```

## Credit & license

MIT. ExamForge's prediction intelligence is generalized from exam-prep prompts by **Hossam Mahmoud**. The spaced-repetition engine is **Learn FASTER**, MIT © 2025 **Hugo Lau** — bundled and extended under `claude-code-kit/`. See [NOTICE.md](NOTICE.md) for exact attribution and the list of modifications.
