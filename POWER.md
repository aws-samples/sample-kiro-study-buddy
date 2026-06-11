---
name: "aws-study-buddy"
displayName: "Kiro Study Buddy"
description: "Turn Kiro into a personal study companion for AWS certification exams. Includes 5 study modes: always-on study context, Socratic scenario practice, service comparisons, a timed exam simulator, and question breakdown."
keywords: ["aws", "certification", "cloud practitioner", "developer", "sysops", "devops", "specialty", "exam", "study", "well-architected", "architecture"]
author: "Marcus Santos - Sr. AWS ProServe Tech Lead, Lucas Leme - Sr. AWS ProServe Tech Lead"
---

# Kiro Study Buddy

Turn Kiro into your personal study companion for AWS certification exams. This power provides five complementary study modes grounded in official AWS documentation via a bundled MCP server.

## What This Power Does

This power provides 5 study modes that leverage Kiro's built-in AWS Documentation MCP server to deliver accurate, citation-backed study sessions grounded in official AWS sources.

| Mode | Activation | Description |
|------|-----------|-------------|
| Study Companion | Always active | Every Kiro response is tailored for your chosen AWS exam: simple language, exam domain mapping, official citations |
| Scenario Practice | `#scenario-practice` | Socratic method — Kiro presents customer scenarios and guides you with questions |
| Service Comparator | `#service-comparator` | Structured side-by-side service comparisons with exam angle and decision flowcharts |
| Exam Simulator | `#exam-simulator` | Timed exam-style questions, scoring, justification feedback, pass/fail projection |
| Question Breakdown | `#question-breakdown` | Step-by-step method for deconstructing exam questions — keyword analysis, elimination, and selection |

## Prerequisites

- **Kiro IDE** installed
- **`uv` package manager** installed (required to run the bundled AWS Documentation MCP server). Install from: https://docs.astral.sh/uv/getting-started/installation/
- No AWS credentials required — the documentation MCP server only reads public AWS docs

# Onboarding

Follow these steps to set up and verify the Kiro Study Buddy power in Kiro.

## Step 1: Verify AWS Documentation MCP

This power bundles the `awslabs.aws-documentation-mcp-server` MCP server, which is installed automatically when you add the power. It requires `uv` (Python package manager) to be installed on your system.

To verify it's working, ask Kiro:

```text
Search the AWS documentation for Amazon S3 storage classes
```

If Kiro returns results from official AWS docs, you're good to go.

## Step 2: Select Your AWS Certification Exam

Before any study interaction, Kiro MUST establish an Exam Context for the session. This is mandatory and must follow the exact procedure below.

### 2a. Fetch the Current Exam List Dynamically

**ALWAYS fetch the current exam list dynamically. Do NOT rely on a hardcoded list.**

1. Use the AWS Documentation MCP server to read the official exam guides index page at `https://docs.aws.amazon.com/aws-certification/latest/examguides/aws-certification-exam-guides.html`.
2. Extract every certification listed on that page: the full exam name, exam code, and certification level (Foundational, Associate, Professional, Specialty).
3. If the MCP server lookup fails, fall back to searching the AWS Documentation MCP server for "AWS certification exam guides" and extract the exam list from the results.
4. If both fail, fall back to a web search for the official AWS certification exam guides page and extract the list from there.

### 2b. Present the List

**Formatting is critical for user experience.** The list MUST always follow this exact format — no exceptions, regardless of how the data was retrieved:

```markdown
Which AWS certification exam are you studying for? Pick a number or enter the exam code:

**Foundational**

1. [Full Exam Name] ([EXAM-CODE])
2. [Full Exam Name] ([EXAM-CODE])

**Associate**

3. [Full Exam Name] ([EXAM-CODE])
4. [Full Exam Name] ([EXAM-CODE])
...

**Professional**

N. [Full Exam Name] ([EXAM-CODE])
...

**Specialty**

N. [Full Exam Name] ([EXAM-CODE])
...
```

**Formatting rules:**
- Group exams by certification level: **Foundational**, **Associate**, **Professional**, **Specialty** — in that order.
- Level headers MUST be bold (e.g., `**Foundational**`).
- Use a single continuous numbered list across all levels (1, 2, 3... not restarting at each level).
- Each exam line MUST follow the format: `N. Full Exam Name (EXAM-CODE)` — number, period, space, full official name, space, exam code in parentheses.
- Add a blank line between the level header and the first exam in that level.
- Add a blank line between the last exam of one level and the next level header.
- If an exam is marked as retiring or has a last-day-to-test date, append `(retiring [date])` after the exam code.
- Do NOT add extra columns, tables, bullet points, or any other formatting. Use only the numbered list format shown above.
- Do NOT omit any exams from the fetched list.

Accept either the number (e.g., "3") or the exam code (e.g., "SAA-C03") as valid input.

### 2c. Validate and Look Up Exam Metadata

1. Search the AWS Documentation MCP server for the exact exam code provided.
2. Extract: content domains and weights, question count, time limit, and passing score from the official exam guide.
3. If the MCP server does not return sufficient metadata, fall back to a web search for the official exam guide.
4. Display the confirmation using the **exact template defined in `study.md` Step 5**. Do NOT paraphrase or improvise — follow the template verbatim every time.

Once the exam context is established, all study modes will tailor their content to your chosen exam for the rest of the session.

> **Note:** Only AWS certifications are supported. Azure, GCP, and other cloud provider certifications are out of scope.

## Step 3: Start Studying

The Study Companion mode is always active. Start asking questions:

```text
What is Amazon S3 and when would I use it?
```

For targeted practice, activate one of the manual modes:

```text
#scenario-practice Give me a scenario for my exam's first domain
```

```text
#service-comparator Compare Amazon RDS Multi-AZ vs Read Replicas
```

```text
#exam-simulator Give me a set of 5 exam-like questions
```

# When to Load Steering Files

- General study questions, concept explanations, service overviews → Study Companion (always active via `study.md`)
- Practicing architectural thinking with guided scenarios → `scenario-practice.md`
- Comparing AWS services for exam preparation → `service-comparator.md`
- Timed exam simulation with scoring → `exam-simulator.md`
- Practicing the step-by-step question breakdown method → `question-breakdown.md`
