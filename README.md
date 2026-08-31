# Interview prep — interactive probability study guide & mock exam

An interactive, self-contained study environment for data-science interview
probability: an ICAP-structured study guide (fundamentals + advanced) with
explorers, simulators, self-checks and an optional LLM tutor, plus a
40-question timed mock exam.

Live site: deployed via Cloudflare Pages. Built with plain HTML/JS. MathJax is
bundled locally (`vendor/mathjax/`), so equations render with no internet
connection. The optional AI tutor is bring-your-own-key (several providers
supported) and the key never leaves your own browser's localStorage.

Security note: each page sets a Content-Security-Policy that blocks all
third-party scripts and restricts network calls to the five supported AI
providers. Still, the tutor key sits in localStorage — use a low-value,
spending-capped API key, and remove it (⚙ Setup) on shared machines.

## Folder layout
- `vendor/mathjax/` — bundled MathJax build + fonts (keeps the site fully offline-capable).
- `probability-study-guide.html` — interactive study guide (Part I fundamentals + Part II advanced,
  ICAP ladder, explorers/simulators, self-checks, AI tutor, Mistake Log/snapshot export).
- `probability-mock-exam.html` — 40-question timed mock exam with copyable results report.
- `index.html` — landing page.
- `evaluations/`, `practice/`, `results/` — personal study data; kept local only
  (gitignored, never in the public repo or on the live site).

## Serving locally (needed for the AI tutor)
```
python -m http.server 8000 --directory .
```
then open http://localhost:8000/probability-study-guide.html

## AI study tutor
- Both pages embed an AI chat widget ("🎓 Ask tutor" button, bottom-right).
  Click ⚙ Setup, choose a provider — DeepSeek, OpenAI, Anthropic (Claude), Google Gemini, or
  OpenRouter — and paste that provider's API key. Keys are stored only in the browser's
  localStorage (one per provider) and sent only to the provider you chose. Each provider offers
  suggested models, and you can type any model ID it supports.
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
