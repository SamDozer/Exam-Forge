# Output Format & Section Catalog

Read before building the deliverable. Covers: which sections activate, color coding, and the HTML / .docx templates.

## Section catalog — activation rules

Build a section only if its trigger is met. Order sections by the mark distribution (highest-mark topics first within the guide), but keep the fixed scaffold below.

| Section | Activate when | Notes |
|---|---|---|
| 1. Table of Contents | Always | Clickable anchors in HTML. |
| 2. Exam Blueprint | Always | Exam type, total marks, per-section marks, question types, predicted paper structure. The prioritization map. |
| 3. Professor's Explicit Exam Statements | Transcripts/notes contain explicit markers | **Purple.** Verbatim quotes (Arabic + English translation) of everything the professor said is on the exam, each linked to its topic. This is the strict-extract deliverable on its own. |
| 4. High-Yield Concepts & Frameworks | Always | The must-know core, sorted by confidence + marks. Tag must-memorize vs must-understand. Include mnemonics/memory triggers. |
| 5. Core Mechanisms & Frameworks | Concept/process content present | WHY & HOW, not just WHAT — covers wet-lab mechanisms, analytical frameworks, and algorithmic/bioinformatics logic alike. Common-misunderstanding traps. Blue styling. |
| 6. Applied Methodologies / Workflows | Lab manual or protocol/code/pipeline present, OR practical/OSPE exam | Step → reason-for-step → critical-error point → result interpretation. Covers wet-lab protocols and computational/analysis pipelines. |
| 7. Visual / Data Interpretation | Image/graph/code-based exam, OR user uploaded visuals | Table: item • purpose/function • distinguishing features • expected result • "how it appears in the exam." Covers specimens, plates, gels, graphs, code blocks, maps, diagrams. Keep this machinery available even when dormant. |
| 8. Analytical / Calculations | Quantitative or formula content present (CFU/mL, dilutions, BOD, COD, enzyme activity/units, % solubilization, molarity, Beer–Lambert, yield, statistical tests, etc.) | Formula/framework + every variable defined + ≥2 solved step-by-step examples from the actual sources/past papers + common mistakes. |
| 9. Predicted Exam Questions + Model Answers | Always (unless strict-extract) | Core deliverable. Each tagged HIGH/MEDIUM/LOW with signal justification. Mirror the professor's phrasing; answer to the mark depth. |
| 9a. Question-Type Recognition | Always (unless strict-extract) | **IF I SEE THIS → IT MEANS THIS → I SHOULD DO THIS**, one row per question type present, using the professor's real past-exam wording. See `solving-layer.md` §1. |
| 9b. Solving Procedures & Worked Examples | Procedural/calculation/practical content present | Numbered *Given → Identify → Choose method → Execute → Interpret → Check* procedures, escalated worked examples, each tagged with its source (e.g. *Midterm Form A, Q3*). Blue. §2–4, §14. |
| 9c. Answer Templates & Mark-Earning Structure | Constructed-response questions expected | Exam-ready answer skeletons plus **MUST INCLUDE / GOOD TO INCLUDE / UNNECESSARY DETAIL** per question type. §5–6. |
| 9d. Distractor Bank | MCQ/true-false on the exam | **QUESTION → TEMPTING WRONG ANSWER → WHY IT LOOKS RIGHT → WHY IT IS WRONG → CORRECT RULE**, using real past-exam distractors. §8. |
| 9e. Sanity Checks & Stuck-Recovery | Procedural/calculation content present | **ANSWER → QUICK CHECK** table plus the per-type recovery protocol. §7, §9. |
| 9f. Reusable Question Patterns | Same structure recurs across sources | Lecture → worksheet → past exam → model answer mapping, with the invariant solving structure named. §10. |
| 10. Exam Traps & Common Mistakes | Always | Confused-pair contrasts, unit traps, misread mechanisms. |
| 10a. Source Errors & Contradictions | Audit found confirmed issues | **SOURCE SAYS → PROBLEM → EVIDENCE → WHAT TO FOLLOW FOR THE EXAM.** Omit only if genuinely nothing was found. §12. |
| 10b. Difficulty Self-Check | Always (unless strict-extract) | Per topic: Recognition / Basic / Application / Trap / Written — so the student sees where they're weak. §13. |
| 10c. Time Budget & Exam-Room Attack Plan | Student gave a time limit, or exam is imminent | **TIME AVAILABLE → TOPICS → EXACT TASK**, plus format-specific in-room strategy. §15–16. |
| 11. Rapid Revision Sheet | User chose "rapid" or "both" | Ultra-condensed one-pager: memory triggers, mnemonics, must-memorize list, formula strip, top predicted Qs. |
| 11a. Final-Minute Sheet | User chose "rapid" or "both", or exam imminent | The tightest layer: only formulas, decisive rules/distinctions, top traps, answer templates, recognition cues. Derived from the analysis above — introduces nothing new. |

If a triggered section has no real content in the sources, omit it rather than padding.

## Four revision layers

The guide is built as nested compressions, each derived from the analysis above — later layers introduce no new information:

1. **Full explanation** — for learning the topic (sections 4–8).
2. **Exam procedure** — for learning how to solve it (sections 9a–9f).
3. **High-density recall** — the one-page rapid sheet (11).
4. **Final-minute sheet** — formulas, rules, traps, templates, recognition cues only (11a).

## Color coding (consistent across HTML and docx)

- 🟣 **Purple** — the professor's *explicit* exam statements, quoted verbatim. Facts, not predictions. Highest priority.
- 🔴 **Red** — Exam Alerts, Traps, HIGH-confidence *predictions*, "we think this is coming."
- 🟢 **Green** — Key concepts / must-know facts.
- 🔵 **Blue** — Mechanisms & frameworks *and* required solving procedures / methods — the WHY, HOW, and HOW-TO-DO-IT.
- ⚫ **Gray (solid)** — supporting explanation or background from the course material.
- ⚪ **Grey/italic dashed** — Outside-source clarifications (must be visually distinct so the student knows it wasn't from the professor).

Four things must never be confused: a prediction must never visually resemble a confirmed professor statement, and outside-source clarification must never look like course material. Purple ≠ red; dashed-outside ≠ solid-gray background.

**Strict-extract deliverable:** if the user chose "strict extract," output *only* Section 3 (Professor's Explicit Exam Statements) plus a one-line blueprint — no predictions, no synthesis, ultra-condensed. This mirrors the "extract only what the professor explicitly flagged" objective.

## HTML template

Self-contained single file, internal CSS, collapsible sections, sticky clickable TOC. Skeleton:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>[COURSE] — Exam Master Guide</title>
<style>
  :root{
    --exam:#7c3aed; --exam-bg:#f3edfd;
    --alert:#c0392b; --alert-bg:#fdecea;
    --key:#1e8449;   --key-bg:#eafaf1;
    --mech:#1f6feb;  --mech-bg:#eaf2fd;
    --outside:#6b7280; --ink:#1a1a1a; --line:#e5e7eb; --bg:#ffffff;
  }
  *{box-sizing:border-box} 
  body{font-family:-apple-system,Segoe UI,Roboto,Arial,sans-serif;color:var(--ink);
       max-width:900px;margin:0 auto;padding:24px;line-height:1.55;background:var(--bg)}
  h1{border-bottom:3px solid var(--ink);padding-bottom:8px}
  h2{margin-top:36px;border-left:6px solid var(--ink);padding-left:10px}
  nav{position:sticky;top:0;background:var(--bg);border:1px solid var(--line);
      border-radius:10px;padding:14px 18px;margin:16px 0;box-shadow:0 1px 4px rgba(0,0,0,.05)}
  nav a{display:inline-block;margin:4px 10px 4px 0;text-decoration:none;color:var(--mech)}
  table{border-collapse:collapse;width:100%;margin:14px 0}
  th,td{border:1px solid var(--line);padding:8px 10px;text-align:left;vertical-align:top}
  th{background:#f5f6f8}
  .exam{background:var(--exam-bg);border-left:5px solid var(--exam);padding:10px 14px;border-radius:6px;margin:12px 0}
  .proc{background:var(--mech-bg);border-left:5px solid var(--mech);padding:10px 14px;border-radius:6px;margin:12px 0}
  .proc ol{margin:6px 0 0 18px}
  .bg{background:#f5f6f8;border-left:5px solid #9ca3af;padding:10px 14px;border-radius:6px;margin:12px 0;color:#374151}
  .src{font-size:.8em;color:var(--mech);font-weight:700;text-transform:uppercase;letter-spacing:.3px}
  .must{color:var(--alert);font-weight:700} .good{color:#d68910;font-weight:700} .skip{color:var(--outside)}
  .recog th:first-child{width:32%} .recog td:nth-child(2){font-style:italic}
  .exam blockquote{margin:6px 0;padding-left:10px;border-left:3px solid var(--exam);color:#4c1d95}
  .alert{background:var(--alert-bg);border-left:5px solid var(--alert);padding:10px 14px;border-radius:6px;margin:12px 0}
  .key{background:var(--key-bg);border-left:5px solid var(--key);padding:10px 14px;border-radius:6px;margin:12px 0}
  .mech{background:var(--mech-bg);border-left:5px solid var(--mech);padding:10px 14px;border-radius:6px;margin:12px 0}
  .outside{color:var(--outside);font-style:italic;border-left:3px dashed var(--outside);padding-left:10px;margin:10px 0}
  .tag{font-size:.75em;font-weight:700;padding:2px 8px;border-radius:20px;color:#fff}
  .high{background:var(--alert)} .med{background:#d68910} .low{background:var(--key)}
  details{border:1px solid var(--line);border-radius:8px;margin:10px 0;padding:6px 12px}
  summary{cursor:pointer;font-weight:600;padding:6px 0}
  .qa{border:1px solid var(--line);border-radius:8px;padding:12px;margin:12px 0}
  .marks{float:right;font-weight:700;color:var(--mech)}
  code,.formula{background:#f5f6f8;padding:2px 6px;border-radius:4px;font-family:Menlo,Consolas,monospace}
</style>
</head>
<body>
  <h1>[COURSE] — Exam Master Guide</h1>
  <p><em>[exam type] · Total: [marks] · [date if known]</em></p>

  <nav id="toc"><strong>Contents</strong><br>
    <!-- one <a href="#sec-N"> per active section -->
  </nav>

  <!-- SECTION PATTERN -->
  <h2 id="sec-2">2 · Exam Blueprint</h2>
  <!-- marks table + predicted paper structure -->

  <h2 id="sec-8">8 · Predicted Questions</h2>
  <div class="qa">
    <span class="marks">[X marks]</span>
    <span class="tag high">HIGH</span>
    <p><strong>Q:</strong> [predicted question in professor's style]</p>
    <p><em>Signal: appeared in 2023 & 2024 papers; verbally emphasized.</em></p>
    <details><summary>Model answer</summary>[answer to mark depth]</details>
  </div>

  <h2 id="sec-9a">9a · Question-Type Recognition</h2>
  <table class="recog"><tr><th>If I see this</th><th>It means this</th><th>I should do this</th></tr>
    <tr><td>[professor's actual stem wording]</td><td>[what's really being tested]</td><td>[method + sequence]</td></tr>
  </table>

  <div class="proc">
    <span class="src">Source: [Midterm Form A, Q3]</span>
    <p><strong>Procedure — [question type]</strong></p>
    <ol><li>Given: …</li><li>Identify: …</li><li>Choose method: …</li><li>Execute: …</li><li>Interpret: …</li><li>Check: …</li></ol>
    <p><span class="must">MUST INCLUDE</span> … · <span class="good">GOOD</span> … · <span class="skip">UNNECESSARY</span> …</p>
  </div>

  <div class="bg">⚫ Background (course material): …</div>

  <!-- Callout examples -->
  <div class="exam">🟣 Professor said (exam): <blockquote>"[verbatim quote]" — [English translation if Arabic]</blockquote>→ points to: [topic]</div>
  <div class="alert">⚠️ Exam alert: …</div>
  <div class="key">✅ Key: …</div>
  <div class="mech">🔵 Mechanism: …</div>
  <div class="outside">[Outside-source clarification: …]</div>
</body>
</html>
```

Fill every `[...]` placeholder. Remove sections that didn't activate and their TOC links. Keep the file fully self-contained (no external assets); embed uploaded images as base64 in `<img>` if the visual-ID section is active.

## Word (.docx) output

If the user picks docx, first read `/mnt/skills/public/docx/SKILL.md` and build with that skill. Map the same color coding to shaded paragraph/heading styles, keep the same section catalog and predicted-question tagging, and use a real Word table of contents. Save to `/mnt/user-data/outputs/`.

## Optional ongoing review (flashcards & spaced repetition)

Two escalating options beyond the static guide — offer, don't force:

**In-chat flashcards (one-off).** If opted in, produce an **Anki-ready CSV** (`flashcards.csv`): two columns, `Front,Back`, one predicted or key Q/A per row, properly quoted. Anki handles the actual scheduling. This is the ceiling of what a single chat session can do — there is no cross-session state here.

**Learn FASTER handoff (coached SRS in Claude Code).** True spaced repetition needs state persisted across days, which this chat skill cannot provide. For that, hand off to the companion **Learn FASTER** kit (Claude Code / Codex CLI). Produce a `learn-faster-handoff.md` containing:
- A topic/syllabus list drawn from the guide, ordered by exam weight (seeds its syllabus/`/learn` flow).
- The predicted + key Q/A pairs with confidence tags (seeds its practice/review items).
- The professor's explicit exam statements (so its exam-mode prioritizes them).

Then point the user to install and run it (this repo bundles the enhanced kit under `claude-code-kit/`; install from *your* fork so the ExamForge source-grounded commands are included):
```
# from the repo root, install the bundled, enhanced kit:
uv tool install learn-faster --from ./claude-code-kit
learn-faster            # choose Exam-Oriented mode
/ingest-materials       # load slides / transcripts / past papers
/predict-exam           # source-grounded prediction + guide, seeds the review scheduler
```
The two tools stay in their own runtimes; the handoff file is the clean seam between them. Don't claim the skill performs the spaced repetition — it prepares the material the kit schedules.

## Delivery

Save the file to `/mnt/user-data/outputs/` and present it with `present_files`. Keep any closing message short: name the sections built, the top few HIGH-confidence predictions, and what extra source (usually past papers) would most improve the prediction next time.
