# Interview prep — interactive probability study guide & mock exam

An interactive, self-contained study environment for data-science interview
probability: an ICAP-structured study guide (fundamentals + advanced) with
explorers, simulators, self-checks and an optional LLM tutor, plus a
40-question timed mock exam.

Live site: deployed via Cloudflare Pages. Built with plain HTML/JS (MathJax for
equations); the optional tutor uses a DeepSeek API key that you provide and
that never leaves your own browser's localStorage.

## Folder layout
- `probability-study-guide.html` — interactive study guide (Part I fundamentals + Part II advanced,
  ICAP ladder, explorers/simulators, self-checks, DeepSeek tutor, Mistake Log/snapshot export).
- `probability-mock-exam.html` — 40-question timed mock exam with copyable results report.
- `index.html` — landing page.
- `evaluations/`, `practice/`, `results/` — personal study data; kept local only
  (gitignored, never in the public repo or on the live site).

## Serving locally (needed for the DeepSeek tutor)
```
python -m http.server 8000 --directory .
```
then open http://localhost:8000/probability-study-guide.html

## DeepSeek tutor
- Both pages embed a DeepSeek chat widget ("🎓 Ask tutor" button, bottom-right) used by both pages.
  Click ⚙ Key and paste your DeepSeek API key (from platform.deepseek.com); it is stored only in
  the browser's localStorage and sent only to api.deepseek.com. Models: deepseek-chat / deepseek-reasoner.
- Study guide: tutor sees the section you are reading (explain simply / quiz me / interview follow-ups).
- Exam: before submit the tutor only clarifies wording; after submit it can interpret the report and
  explain wrong questions.
- If the browser blocks the API call when the page is opened as a local file (CORS), run
  `python -m http.server` in this folder and open http://localhost:8000/.
- The study guide also has a self-check question after every topic (answers hidden until "Check").

## Mistake Log (错题本, "mistake notebook") export
In the study guide sidebar: **📕 Mistake Log (.html)** downloads `mistake-log-<date>.html` — built like the
page snapshot (same styling, rendered math, grouped under topic headings) but with the guide's own
teaching text removed, so only what was generated while studying remains. A plain Markdown version
(`Mistake Log as .md` / `Copy .md`) is also available. Both contain, per topic: AI-generated questions, your
answers, the AI grading/explanations, model answers, your own explanation and interview question,
and your "takeaway" note — plus every self-check you got wrong (question, your pick, correct
answer, explanation). All of this is stored in the browser's localStorage, so export it
periodically; clearing browser data would erase it.

## Page snapshot & progress transfer (study guide sidebar)
- **📸 Snapshot page (.html)** — saves `study-guide-snapshot-<date>.html`: a read-only copy of the
  entire study guide with everything baked in place at that moment — generated questions, your
  answers, AI grading, model answers, takeaways, self-check selections and feedback, explorer
  graphs as images. No scripts, no API key. Open it in any browser later as a dated record.
- **Export .json / Import .json** — dump or restore all progress (localStorage) so you can move
  between browsers/machines or keep a backup.
