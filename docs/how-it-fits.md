# How the two entry points fit together

ExamForge has one brain and two bodies.

## The shared brain: prediction intelligence

The same rules govern both the chat skill and the CLI kit:
- **Signal-weighting hierarchy** (past papers → model answers → slide repetition → verbal emphasis → insider info → textbook).
- **Explicit-marker extraction** ("purple" facts): what the professor literally said is on the exam, quoted, Arabic translated.
- **Confidence tagging** (HIGH/MEDIUM/LOW) so predictions never bluff.
- **Faithfulness**: bound to the student's materials; the professor's terminology preserved; no substituting generic web questions when real materials exist.

In the skill this lives in `skill/examforge/references/prediction-and-analysis.md`.
In the kit it lives in `claude-code-kit/.../shared/references/exam_prediction.md` (installed to `.learning/references/`).
The two are deliberately kept in sync — edit both when you change the method.

## Two bodies

**Chat skill** — zero setup, single session. Ingests materials pasted or uploaded in a chat, produces an HTML/docx guide + prediction, optionally an Anki CSV. No memory between chats, so it cannot schedule reviews itself.

**CLI kit** — installed into a project, persistent `.learning/` state. `/ingest-materials` stores the sources and runs the extraction pass; `/predict-exam` builds the guide and **seeds the review scheduler** with the predicted questions; `/review` drills them on a spaced schedule; `/generate-exam` prints a mock.

## The seam

If a student starts in chat and wants ongoing review, the skill emits `learn-faster-handoff.md` (exam-weighted topics + tagged Q/A + purple statements). Dropping that into a kit-initialized project lets `/predict-exam` (or manual import) seed the scheduler without re-ingesting. This is the one-way bridge from the stateless skill to the stateful kit.

## Why not a single tool

True spaced repetition needs state persisted across days. claude.ai chat skills have none; Claude Code projects do. So the retention half *must* live in the CLI kit. Forcing everything into the chat skill would break the spaced repetition; forcing everything into the CLI would lose the zero-setup path. Keeping both, with a shared brain and a clean handoff, is the honest design.
