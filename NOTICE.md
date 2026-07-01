# Components & attribution

ExamForge bundles and extends two independently-licensed parts:

1. **ExamForge skill** (`skill/`, `dist/`) — the claude.ai chat skill for source-grounded
   study-guide generation and exam prediction. Derived and generalized from exam-prep
   prompts by Hossam Mahmoud. MIT.

2. **Learn FASTER** (`claude-code-kit/`) — a Claude Code / Codex spaced-repetition learning
   kit, MIT © 2025 Hugo Lau. Upstream: https://github.com/cheukyin175/learn-faster-kit
   (the `hluaguo/learn-faster-kit` remote is a byte-identical synced mirror, verified
   against the same final commit). Its original `LICENSE` is retained in that directory.

   ExamForge **modifications** to Learn FASTER, all within its exam mode:
   - added `commands/ingest-materials.md` and `commands/predict-exam.md`
   - added `shared/references/exam_prediction.md`
   - extended `modes/exam/system_prompts/learn-faster.md` and the exam-generator flow to
     prefer the student's own materials over generic/online examples.
