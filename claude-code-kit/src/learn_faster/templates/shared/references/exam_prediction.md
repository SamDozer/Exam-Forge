# ExamForge — Source-Grounded Exam Prediction (reference)

This reference extends Learn FASTER's exam mode with **source-grounded prediction**: instead of generating practice from generic online examples, it builds the study material from the student's *own* course files and predicts the real paper. Used by `/ingest-materials` and `/predict-exam`.

Scope: biology-family courses (biotech, biology, biochemistry, bioinformatics, chemistry, microbiology, molecular biology) but adapts to the material given.

## Signal-weighting hierarchy (what predicts the exam)

Rank every candidate topic by evidence, strongest first:

1. **Past exam papers (strongest).** Recurring items across papers are near-guarantees. Track exact phrasing, predict the rephrase.
2. **Official model answers.** Reveal expected depth and wording for full marks.
3. **Repetition across slides.** A concept restated on many slides or given its own objectives/summary slide is emphasized.
4. **Professor verbal emphasis (transcripts/notes).** Explicit spoken exam cues — see cue tables below.
5. **Student insider info** ("the Dr said…"). High-value verbal emphasis; always ask for it.
6. **Textbook prominence (weakest).** Only if it aligns with a higher signal.

Convergent signals (past paper + verbal emphasis + slide repetition) = top priority.

## Confidence tags

- 🔴 **HIGH** — in past paper(s), or explicitly flagged by professor, or multiple strong signals. "Expect this."
- 🟡 **MEDIUM** — repeated across slides or single verbal emphasis, unconfirmed by past papers. "Likely."
- 🟢 **LOW** — plausible from syllabus/marks, weak signal. "Cover if time allows."

Never inflate confidence — the student budgets scarce revision time on these tags.

## Explicit-marker extraction pass (run first, produces the "purple" facts)

Scan transcripts/notes for statements where the professor *explicitly* flagged exam material. Capture verbatim quote (original + English translation if Arabic), the topic it points to, and source location. These are **facts**, kept separate from predictions.

**Purple = professor literally said it's on the exam (fact). Red = HIGH-confidence prediction or trap (inference/warning).** A topic can be both.

Large transcripts (100+ pages): run this scan first as a lightweight pass, log hits, then chunk-read the rest.

### Arabic exam-cue phrases (dialectal variants; output stays English)

| Arabic cue | Meaning | Weight |
|---|---|---|
| ده مهم للامتحان / دي مهمة في الامتحان | important for the exam | HIGH |
| هييجي في الامتحان / ده جاي / متوقع ييجي | this is coming in the exam | HIGH |
| ركزوا على / خدوا بالكم من | focus on / pay attention to | HIGH/MED |
| لازم تعرفوا | you must know this | HIGH |
| متوقع سؤال / في سؤال على ده | expect a question on this | HIGH |
| احفظوا / دي محفوظة | memorize this | must-memorize |
| ده أساسي / دي نقطة أساسية | fundamental / key point | MED/HIGH |
| اللي فات ده مش مهم / سيبوا ده | skip this / not important | de-prioritize |

English cues: "important for the exam," "will be on the test," "you must know this," "expect a question," "key concept for the exam," "focus your study on," "the most critical part for the exam is," "guaranteed," "exam alert."

## Faithfulness rule

Build from the student's sources; preserve the professor's exact terminology (don't "correct" it into textbook language — the exam grades their terms). Outside knowledge only when a concept is central and repeated but explained too poorly to study from; flag every such addition as outside-source. Do not "search online for exam examples" when the student has provided real materials — their materials override generic web examples.

## Reverse-engineering question style

From past papers + model answers, extract: favored stems ("Compare…", "Explain the mechanism…", "Given the data, calculate…", "Identify the specimen and justify…"), depth expected (2 lines vs 10), recurring paper structure (predict the slots, then fill with this year's likely content), and MCQ distractor style. Predicted questions mirror this and answer to the mark depth.

## Seeding the review scheduler

After prediction, convert the HIGH/MEDIUM predicted questions and the purple must-know facts into review items for `.learning/<topic>/` so `review_scheduler.py` schedules them. Weight initial priority by confidence tag and exam marks. This is what makes ExamForge different from stock Learn FASTER: the spaced-repetition drills are the *actual predicted paper*, not generic questions.
