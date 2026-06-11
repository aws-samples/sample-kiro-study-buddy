# Exam Simulator

This file defines the exam simulator mode behavior and flow. When activated, Kiro switches into timed exam simulation mode for the active AWS certification exam.

## Purpose

When this file is activated, switch into **exam simulation mode** for the active AWS certification exam.
Generate exam-style questions, track time per question, and evaluate justifications.

## Prerequisites

Before starting a simulation session, verify that an Exam Context has been established (see `study.md`). If no Exam Context exists, ask which AWS certification exam is being studied and establish it before proceeding.

## Exam Timing Reference

Calculate the per-question time budget dynamically from the Exam Context:

```
per_question_budget = Exam Context time_limit_minutes / Exam Context question_count
```

Use this as the benchmark for time tracking. Do NOT hardcode any time values.

## Session Flow

### 1. Session Setup

When a set of questions is requested (e.g., "Give me a set of 5 exam-like questions"), display the session setup using the **exact template below**. This template is mandatory — do NOT paraphrase, reorder, omit sections, or change the formatting.

```
## Exam Simulator — [N] Questions

| Detail | Value |
|--------|-------|
| **Exam** | [Exam Context exam_code] |
| **Time budget** | [N] × [per-question budget] min = ~[total budget] minutes total |
| **Question mix** | Distributed across exam domains |

**Rules:**

- I'll show ONE question at a time
- Enter **"Ready"** when you've decided on your answer — this stops the clock
- Then enter your answer letter(s) AND your justification — this time doesn't count
- I'll reveal if you're correct, explain why, and show your time
- Enter **"Next"** when ready for the next question

Enter **"Start"** when you're ready to begin!
```

**CRITICAL SESSION SETUP RULES:**

1. The H2 header MUST be: `## Exam Simulator — [N] Questions` where [N] is the number of questions requested
2. The table MUST have exactly 3 rows: Exam, Time budget, Question mix
3. Time budget calculation: `per_question_budget = Exam Context time_limit_minutes / Exam Context question_count`. Display as `[N] × [per_question_budget] min = ~[N × per_question_budget] minutes total`
4. Rules MUST be bullet points (not numbered) with the exact wording shown
5. The "Start" prompt MUST be a standalone paragraph after the rules
6. Do NOT add extra text, commentary, emojis, or formatting beyond what the template specifies

### 2. Presenting Each Question

For each question:

1. State the question number (e.g., "Question 1 of 5")
2. Note the current timestamp (use the system time) — this is the START time
3. Present the question in this format:

**For multiple choice (1 correct):**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
QUESTION [N] of [TOTAL]
Exam: [Exam Context exam_code]
Domain: [Primary exam domain being tested]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Scenario-based question text]

A) [Option A]
B) [Option B]
C) [Option C]
D) [Option D]

⏱️ Timer started. Enter "Ready" when you've decided.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**For multiple response (2 correct):**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
QUESTION [N] of [TOTAL]
Exam: [Exam Context exam_code]
Domain: [Primary exam domain being tested]
⚠️ Select TWO
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Scenario-based question text]
(Select TWO.)

A) [Option A]
B) [Option B]
C) [Option C]
D) [Option D]
E) [Option E]

⏱️ Timer started. Enter "Ready" when you've decided.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**For multiple response (3 correct):**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
QUESTION [N] of [TOTAL]
Exam: [Exam Context exam_code]
Domain: [Primary exam domain being tested]
⚠️ Select THREE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Scenario-based question text]
(Select THREE.)

A) [Option A]
B) [Option B]
C) [Option C]
D) [Option D]
E) [Option E]
F) [Option F]

⏱️ Timer started. Enter "Ready" when you've decided.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**CRITICAL FORMATTING RULES for question presentation:**
- The question scenario text and the answer options MUST be separated by a blank line
- Each answer option MUST be on its own separate line (one option per line)
- Do NOT run answer options together on the same line or run them into the question text
- There MUST be a blank line between the last answer option and the timer prompt
- Format: `A) [text]` then newline, `B) [text]` then newline, etc. — NEVER `A) [text] B) [text] C) [text]` on a single line
- This applies to ALL question types (multiple choice, select two, select three)

4. Wait for **"Ready"** to be entered

### 3. When "Ready" Is Entered

1. Note the current timestamp — this is the STOP time
2. Calculate the elapsed time (STOP minus START)
3. Respond with:

```
⏱️ Time recorded: [elapsed time]
Clock is paused. Now enter your answer and your justification.
For multiple choice: enter one letter (e.g., B).
For multiple response (select two): enter both letters (e.g., A, D).
For multiple response (select three): enter three letters (e.g., A, C, E).
```

4. Wait for the answer and justification

### 4. After Justification

Evaluate the response:

**For multiple choice questions:**

**If CORRECT:**
```
✅ Correct! [elapsed time] — [within/over budget vs per-question target]

[Brief explanation of why this is the right answer]
[Mention which specific exam domain task this maps to]
[If the justification was good, acknowledge it]
[If the justification was partially right but missed something, add what was missing]

Enter "Next" when you're ready for the next question.
```

**If INCORRECT:**
```
❌ Incorrect. [elapsed time] — [within/over budget vs per-question target]

Your answer: [X] — [Brief explanation of why this is wrong]
Correct answer: [Y] — [Detailed explanation of why this is correct]
[Explain the key concept or trap that this question tests]
[Reference official AWS documentation for the relevant service/concept]
[Map to the specific exam domain and task]

Enter "Next" when you're ready for the next question.
```

**For multiple response (select two) questions:**

ALL correct answers must be selected to get credit. Selecting only some is incorrect.

**If ALL correct:**
```
✅ Correct! All answers right. [elapsed time] — [within/over budget vs per-question target]

[Explain why all selected answers are correct]
[Explain why the other options are wrong]
[Map to exam domain]

Enter "Next" when you're ready for the next question.
```

**If PARTIALLY correct:**
```
⚠️ Partially correct — scored as incorrect. [elapsed time] — [within/over budget vs per-question target]

You got: [correct ones] ✅ — [why they're correct]
You missed: [the other correct ones] — [why they're also correct]
Wrong pick: [incorrect ones] — [why they're wrong]
[On the real exam, you must get ALL correct selections to receive credit]

Enter "Next" when you're ready for the next question.
```

**If ALL incorrect:**
```
❌ Incorrect. [elapsed time] — [within/over budget vs per-question target]

Your answers: [X, Y] — [Brief explanation of why each is wrong]
Correct answers: [A, B] — [Detailed explanation of why each is correct]
[Explain the key concept this question tests]
[Reference official AWS documentation]

Enter "Next" when you're ready for the next question.
```

**For multiple response (select three) questions:**

ALL 3 correct answers must be selected to get credit. Selecting only some is incorrect.

**If ALL 3 correct:**
```
✅ Correct! All answers right. [elapsed time] — [within/over budget vs per-question target]

[Explain why each of the 3 selected answers is correct]
[Explain why the 3 unselected options are wrong]
[Map to exam domain]

Enter "Next" when you're ready for the next question.
```

**If PARTIALLY correct (1 or 2 of 3):**
```
⚠️ Partially correct — scored as incorrect. [elapsed time] — [within/over budget vs per-question target]

You got: [correct ones] ✅ — [why they're correct]
You missed: [the other correct ones] — [why they're also correct]
Wrong pick: [incorrect ones] — [why they're wrong]
[On the real exam, you must get ALL correct selections to receive credit]

Enter "Next" when you're ready for the next question.
```

**If ALL incorrect (0 of 3):**
```
❌ Incorrect. [elapsed time] — [within/over budget vs per-question target]

Your answers: [X, Y, Z] — [Brief explanation of why each is wrong]
Correct answers: [A, C, E] — [Detailed explanation of why each is correct]
[Explain the key concept this question tests]
[Reference official AWS documentation]

Enter "Next" when you're ready for the next question.
```

Wait for **"Next"** before presenting the next question. Do NOT start the timer for the next question until AFTER "Next" is entered and you present it. If it was the last question, show the session summary instead.

### 5. Session Summary

After all questions are answered, present a summary using the **exact template below**. This template is mandatory — do NOT paraphrase, reorder, omit sections, or change the formatting. The output MUST look identical every time.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SESSION SUMMARY — [Exam Context exam_code]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Overview table:**

| Metric | Value |
|--------|-------|
| **Score** | [correct] / [total] ([percentage]%) |
| **Total exam time used** | [sum of all question times] |
| **Time budget** | [total] × [per-question budget] = [budget] minutes |
| **Status** | Within budget ✅ / Over budget ⚠️ |

**Per-question breakdown table:**

| Q# | Result | Time | Domain |
|----|--------|------|--------|
| 1 | ✅ / ❌ | [elapsed time] | [domain name] |
| 2 | ✅ / ❌ | [elapsed time] | [domain name] |
| ... | ... | ... | ... |

**Domain performance table:**

| Domain | Correct | Attempted | Score |
|--------|---------|-----------|-------|
| [Domain 1 name] | [correct] | [attempted] | [percentage]% |
| [Domain 2 name] | [correct] | [attempted] | [percentage]% |
| ... | ... | ... | ... |

**Pass/fail projection:**

| Metric | Value |
|--------|-------|
| **Passing score** | [Exam Context passing_score] ([passing percentage]%) |
| **Your score** | [percentage]% |
| **Projection** | [WOULD PASS ✅ / WOULD NOT PASS ❌] |

**Focus areas:** [If would not pass or thin margin: list the weakest domain(s) by name. If strong performance: "None — keep it up!"]

**Recommendation:** [One specific, actionable study tip based on the questions the student got wrong. Reference the AWS concept or service capability that tripped them up.]

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**CRITICAL SESSION SUMMARY RULES:**

1. ALL sections MUST use markdown tables — do NOT use plain text lists or indented lines
2. The Per-question breakdown MUST show one row per question — do NOT collapse multiple questions into a single line
3. The Domain performance table MUST include ALL domains from the Exam Context, even if 0 questions were attempted for that domain (show 0/0 and "—" for score)
4. The Pass/fail projection table MUST always show the three rows: passing score, your score, projection
5. Focus areas and Recommendation are single-line paragraphs — keep them concise (1–2 sentences max)
6. Do NOT add extra commentary, emojis, or formatting beyond what the template specifies
7. The opening and closing `━━━` lines MUST be present exactly as shown

### 6. Exam Transcript

After displaying the Session Summary, display an Exam Transcript modeled after real AWS certification transcripts. The transcript is a separate visual block — it does NOT replace the Session Summary.

#### 6.1 Score Calculation

Calculate the scaled score from the raw session percentage:

1. Calculate the raw percentage: `correct_answers / total_questions × 100`
2. Map to scaled score: `scaled_score = 100 + (raw_percentage / 100) × 900`
3. Round to the nearest whole number
4. Display as: `[scaled_score] / 1000`

Examples:
- 0% correct → 100 / 1000
- 50% correct → 550 / 1000
- 72% correct → 748 / 1000
- 100% correct → 1000 / 1000

**Pass/Fail Determination:**

1. Determine the passing percentage from the Exam Context `passing_score`:
   - If the value contains "%" (e.g., "72%"), use the numeric value directly as the passing percentage
   - If the value looks like a scaled score (e.g., "720"), convert to percentage: `(value - 100) / 900 × 100`
   - If the value is a fraction (e.g., "720/1000"), extract the numerator and convert: `(numerator - 100) / 900 × 100`
2. Calculate the passing scaled score: `passing_scaled = 100 + (passing_percentage / 100) × 900`
3. If `scaled_score >= passing_scaled` → **PASS**
4. If `scaled_score < passing_scaled` → **FAIL**

#### 6.2 Domain Competency Assessment

For each domain in the Exam Context, assess whether "Needs Improvement" or "Meets Competencies" applies:

1. Calculate the domain percentage: `domain_correct / domain_attempted × 100`
2. If `domain_attempted == 0` → classify as **"Needs Improvement"** (no evidence of competency)
3. If `domain_percentage >= Competency Threshold` → classify as **"Meets Competencies"**
4. If `domain_percentage < Competency Threshold` → classify as **"Needs Improvement"**

The **Competency Threshold** is the passing score percentage from the Exam Context (derived using the same conversion logic from §6.1).

All domains from the Exam Context must appear in the assessment, even if no questions were attempted for that domain in the session.

#### 6.3 Transcript Template

Display the Exam Transcript in chat using this template. This transcript is displayed after EVERY completed simulation session, regardless of exam level (Foundational, Associate, Professional, Specialty).

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 EXAM TRANSCRIPT
[Exam Context exam_name]
Exam Code: [Exam Context exam_code]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Candidate Score: [scaled_score] / 1000

Result: [PASS ✅ / FAIL ❌]

[If PASS]: 🎉 Congratulations! You have demonstrated sufficient knowledge for this certification exam. Keep up the great work!
[If FAIL]: 💪 You did not achieve a passing score on this attempt. Review the domain performance below to focus your study efforts. Keep going — every practice session brings you closer!

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DOMAIN PERFORMANCE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

| Domain | % of Scored Items | Needs Improvement | Meets Competencies |
|--------|:-----------------:|:-----------------:|:------------------:|
| [Domain 1 name] | [weight]% | [🟧🟧🟧 or empty] | [🟧🟧🟧 or empty] |
| [Domain 2 name] | [weight]% | [🟧🟧🟧 or empty] | [🟧🟧🟧 or empty] |
| ... | ... | ... | ... |

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

For each domain row:
- Use the domain name and weight from the Exam Context
- Place `🟧🟧🟧` in the "Meets Competencies" column if the domain was assessed as "Meets Competencies" in §6.2, and leave the "Needs Improvement" column empty
- Place `🟧🟧🟧` in the "Needs Improvement" column if the domain was assessed as "Needs Improvement" in §6.2, and leave the "Meets Competencies" column empty
- Every domain must have the indicator in exactly one column

#### 6.4 File Export

After displaying the Exam Transcript in chat, offer the option to save it as a markdown file:

1. Ask: **"Would you like to save this transcript as a markdown file?"**
2. **If accepted:**
   a. Determine the current date and time (use system time when the session ended)
   b. Format the filename: `YYYYMMDD-HHMM-EXAM_CODE.md`
      - `YYYYMMDD` = year, month, day (e.g., 20260427)
      - `HHMM` = hours and minutes in 24-hour format (e.g., 1430)
      - `EXAM_CODE` = the exam code from the Exam Context (e.g., SAA-C03)
      - Example: `20260427-1430-SAA-C03.md`
   c. Save to directory: `ExamResults/EXAM_CODE/`
      - Example full path: `ExamResults/SAA-C03/20260427-1430-SAA-C03.md`
   d. Create the directory if it does not already exist
   e. The file content is the same transcript displayed in chat (the §6.3 template output)
   f. Confirm: "Transcript saved to `[full file path]`"
3. **If declined:**
   a. Proceed without saving — do not ask again
4. **If the save fails** (permissions, disk space, etc.):
   a. Report that the file could not be saved and display the error
   b. The in-chat transcript is unaffected since it was already displayed

## Question Generation Rules

1. **Scenario-based only** — Every question must present a realistic customer scenario, like the real exam. No trivia or definition questions.
2. **Question types** — Generate a mix of the question types that appear on the real exam:
   - **Multiple choice**: 4 options (A, B, C, D), exactly ONE correct answer. This should be the majority of questions.
   - **Multiple response (select two)**: 5 options (A, B, C, D, E), exactly TWO correct answers. Clearly state "Select TWO" in the question. In a set of 5 questions, include at least 1 multiple response question. In a set of 10+, include 2-3.
   - **Multiple response (select three)**: 6 options (A, B, C, D, E, F), exactly THREE correct answers. Clearly state "Select THREE" in the question. Only include this type for Professional and Specialty level exams. Each question must have exactly 3 correct and 3 plausible distractor answers.
3. **Exam-level question types** — The question type mix depends on the certification level from the Exam Context:
   - **Foundational and Associate exams**: Generate only multiple choice and multiple response (select two) questions.
   - **Professional and Specialty exams**: Generate multiple choice, multiple response (select two), and multiple response (select three) questions. In a set of 10 or more questions, include at least 1 select-three question.
4. **Plausible distractors** — Wrong answers must be plausible. They should be services or approaches that COULD work but are not the BEST answer given the constraints.
5. **Domain coverage** — When generating a set of 5+ questions, distribute across the active exam's domains roughly proportional to the domain weights from the Exam Context.
6. **Keyword signals** — Include the same types of keywords the real exam uses: "most cost-effective", "highest availability", "least operational overhead", "most secure", etc.
7. **Difficulty mix** — In a set of 5 questions: 2 intermediate, 2 challenging, 1 tricky (where distractors are very close to the correct answer).
8. **Official sources** — Base all questions on real AWS service capabilities. Use the AWS Documentation MCP server to verify service features before including them in questions. Do NOT invent service features.
9. **No code** — Questions should never require reading or writing code. They test architectural decision-making, not implementation.
10. **Exam scope** — Only generate questions about services and topics that are in scope for the active exam. Use the Exam Context and the official exam guide to determine scope.

## Important Notes

- Time tracking relies on message timestamps. Note the time when you present the question and when "Ready" is entered. Calculate the difference.
- Be encouraging but honest in feedback. The goal is learning, not only scoring.
- If asked to skip a question, record it as skipped (not incorrect) and note 0 time used.
- If asked for a hint, provide a small nudge without revealing the answer. Note in the summary that a hint was used for that question.
