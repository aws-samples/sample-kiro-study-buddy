# Kiro Study Buddy - Changelog

All notable changes to the Kiro Study Buddy power are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] — 2026-06-11

Initial public release of the Kiro Study Buddy power for Kiro.

### Features

- **Five study modes** — always-on study companion, Socratic scenario practice, service comparator, timed exam simulator, and question breakdown method.
- **Any AWS certification** — dynamic exam selection at session start with automatic metadata lookup (domains, weights, question count, time limit, passing score) from official AWS documentation.
- **Official sources only** — all content grounded in AWS documentation via the bundled `awslabs.aws-documentation-mcp-server`. No guessing, no hallucinations.

### Exam Simulator

- Timed simulation with per-question time budgets calculated dynamically from the exam's official time limit and question count.
- Three question formats: multiple choice (1 of 4), select two (2 of 5), and select three (3 of 6) for Professional and Specialty exams.
- Ready / Next protocol for precise time tracking per question.
- Detailed feedback with correct, partially correct, and incorrect evaluations, official documentation references, and exam domain mapping.
- Session summary with score, time breakdown, domain performance, and pass/fail projection.
- Exam transcript with scaled score (100–1000), pass/fail status, and domain competency assessment.
- Transcript file export to `ExamResults/<EXAM_CODE>/` for progress tracking.
- Rigid session setup, question presentation, and summary templates for consistent rendering.
- Explicit formatting rules enforcing one answer option per line.

### Question Breakdown

- Four-step method: Keyword Identification → Elimination Round → Final Answer Selection → Reflection & Reinforcement.
- Question source flexibility — generate a question or paste from a third-party platform.
- All question types supported: multiple choice (1/4), select-two (2/5), select-three (3/6).
- Session continuation with domain strengths and areas to review.
- No-guessing policy with documentation grounding and citation requirements.

### Scenario Practice

- Socratic method — guided questions instead of direct answers.
- Per-question grading (A–F) with a final scenario grade.
- Domain-targeted practice using the active exam's content domains.
- Three difficulty levels: beginner, intermediate, advanced.

### Service Comparator

- Structured side-by-side comparisons: summary, key differences table, exam angle, real-world analogy, and decision flowchart.
- Dynamically determines high-value comparisons based on the active exam's domains.

### Study Companion

- Always-on mode — every response uses simple language, maps to exam domains, cites official documentation, and filters for exam relevance.
- Active learning prompts after each explanation.
- Rigid exam context confirmation template for consistent output.

### Documentation

- Comprehensive README with installation, usage, troubleshooting, model recommendations, responsible AI, disclaimer, and contribution guidelines.
- POWER.md with onboarding steps and steering file routing.
- MCP auto-approve for read-only documentation tools.
