# Kiro Study Buddy - Changelog

All notable changes to the Kiro Study Buddy power are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.2] — 2026-06-09

### Fixed

- **Exam context confirmation consistency** — replaced the loose "briefly confirm what was found" instruction in `steering/study.md` Step 5 with a rigid, mandatory template. The confirmation output now renders identically every time: intro line, "Exam Context Established" detail table, "Content Domains" table, heaviest domain callout, and study mode triggers. Updated `POWER.md` Step 2c to reference the `study.md` template as the single source of truth.
- **Session summary tabular format** — replaced the free-form session summary in `steering/exam-simulator.md` with a fully table-based layout (overview metrics, per-question breakdown, domain performance, pass/fail projection). Prevents line-break collapse and ensures consistent rendering.
- **Exam simulator session setup consistency** — replaced the loose session setup instructions in `steering/exam-simulator.md` with a rigid template: H2 header, detail table (Exam, Time budget, Question mix), bullet-point rules with fixed wording, and standalone "Start" prompt.

## [1.1.1] — 2026-06-08

### Fixed

- **Exam simulator answer formatting** — added explicit `CRITICAL FORMATTING RULES` block to `steering/exam-simulator.md` enforcing one answer option per line. The existing code-fence templates showed the correct layout but lacked a behavioral instruction, causing Kiro to intermittently collapse all options onto a single line. Mirrors the fix already applied in `question-breakdown.md` (v1.1.0).

## [1.1.0] — 2026-06-05

### Added

- **Question Breakdown study mode** — new study mode activated via `#question-breakdown` that teaches a structured four-step method for deconstructing AWS certification exam questions:
  - **Step 1: Keyword Identification** — identify main keywords, objective, and constraints in the question scenario
  - **Step 2: Elimination Round** — eliminate obviously wrong answers with justification
  - **Step 3: Final Answer Selection** — differentiate between remaining plausible options
  - **Step 4: Reflection & Reinforcement** — summarize the concept tested, distractor pattern, and confidence self-assessment with targeted study recommendations
- **Question source flexibility** — students can have Study Buddy generate a question or paste their own from a third-party exam platform
- **Session continuation** — practice multiple questions in sequence with a session summary showing domain strengths and areas to review
- **All question types supported** — works with multiple choice (1/4), select-two (2/5), and select-three (3/6)

### Fixed

- **Markdown formatting** — replaced unsupported HTML `<u>` underline tags with italic formatting for the objective phrase in rewritten question displays
- **Answer option line breaks** — added explicit formatting rules ensuring each answer option appears on its own line in all rewritten question displays

## [1.0.9] — 2026-05-28

### Changed

- **Authors** — updated the `author` field in POWER.md from "AWS Study Tools Team" to the individual authors: Marcus Santos and Lucas Leme (Sr. AWS ProServe Tech Leads).

## [1.0.8] — 2026-05-28

### Changed

- **Product name** — renamed from "AWS Certification Study Buddy" to "Kiro Study Buddy" across README, POWER.md, and CHANGELOG to avoid confusion with official AWS products.

## [1.0.7] — 2026-05-27

### Added

- **ZIP download option** — added an alternative installation method (download ZIP from GitLab) for users without Git installed. Marked Git as optional in the prerequisites table.
- **Disclaimer section** — added a standalone disclaimer clarifying this tool is not an official AWS Certification product, contains no questions from official question banks, and that practice results do not predict actual exam outcomes.

### Changed

- **Accessibility** — replaced "click" with device-agnostic language throughout the README.

## [1.0.6] — 2026-05-27

### Fixed

- **BBR scan findings** — resolved findings flagged by the BBR scan across documentation and steering files.

## [1.0.5] — 2026-05-08

### Fixed

- **Exam list onboarding** — embedded the dynamic exam list fetch and formatting instructions directly into POWER.md to guarantee they are always in context on power activation. Previously these instructions lived only in `study.md` which was not reliably auto-loaded, causing the formatted exam selection list to sometimes not appear during onboarding.

## [1.0.4] — 2026-05-07

### Changed

- **Clone URL** — updated installation instructions with the correct repository URL (`git@git.example.com:example-org/kiro-study-buddy.git`).
- **uv install instructions** — added Homebrew (`brew install uv`) as the first option for macOS users in the troubleshooting section.

### Added

- **Responsible AI section** — added a disclaimer covering AI hallucination risk, supplementary nature of the tool, score approximation limitations, and human-judgment-is-final principle.

## [1.0.3] — 2026-05-06

### Added

- **Model recommendations** — added a "Recommended models" section to the README with guidance on when to use Claude Opus vs Claude Sonnet for each study mode, instructions for selecting the model in Kiro, and a disclaimer that only these two models have been tested.

## [1.0.2] — 2026-05-06

### Changed

- **MCP auto-approve** — added `read_documentation`, `read_sections`, `search_documentation`, and `recommend` to the auto-approve list for the AWS documentation MCP server. These are read-only tools that no longer require manual confirmation.

## [1.0.1] — 2026-05-06

### Changed

- **Installation instructions** — replaced GitHub-based installation (Option 1) with a single flow: clone from GitLab and install as a local power. Reflects the current distribution method.

## [1.0.0] — 2026-04-28

Initial public release of the Kiro Study Buddy power for Kiro.

### Core Features

- **Four study modes** — always-on study companion, Socratic scenario practice, service comparator, and timed exam simulator.
- **Any AWS certification** — dynamic exam selection at session start with automatic metadata lookup (domains, weights, question count, time limit, passing score) from official AWS documentation.
- **Official sources only** — all content grounded in AWS documentation via the bundled `awslabs.aws-documentation-mcp-server`. No guessing, no hallucinations.

### Exam Simulator

- **Timed simulation** — per-question time budgets calculated dynamically from the exam's official time limit and question count.
- **Three question formats:**
  - Multiple choice (1 of 4 options) for all exam levels.
  - Multiple response — select two (2 of 5 options) for all exam levels.
  - Multiple response — select three (3 of 6 options) for Professional and Specialty exams only.
- **Ready / Next protocol** — timer starts when a question is presented, pauses when the user types "Ready" to answer, and does not restart until the user types "Next" after reviewing feedback.
- **Detailed feedback** — correct, partially correct, and incorrect evaluations with explanations, official documentation references, and exam domain mapping.
- **Session summary** — score, total time used, per-question breakdown, domain performance, and pass/fail projection against the exam's actual passing score.
- **Exam transcript** — visual transcript modeled after real AWS certification results, displayed after every completed session:
  - Scaled score on a 100–1000 range.
  - Pass/fail status with a congratulatory or encouragement message.
  - Domain performance table with "Needs Improvement" / "Meets Competencies" indicators per domain.
- **Transcript file export** — optional save of the exam transcript as a markdown file to `ExamResults/<EXAM_CODE>/` with a timestamped filename (`YYYYMMDD-HHMM-EXAM_CODE.md`) for progress tracking over time.

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

### Documentation

- Comprehensive README with installation, usage, troubleshooting, and contribution guidelines.
- POWER.md with onboarding steps and steering file routing.
