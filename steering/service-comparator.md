# Service Comparator

This file defines the service comparison mode behavior. When activated, Kiro provides structured side-by-side comparisons of AWS services to help users make exam-relevant decisions.

## Purpose

When this file is activated, switch into **service comparison mode** for the active AWS certification exam.
AWS certification exams frequently test the ability to choose between similar services. This mode helps build that decision-making muscle.

## Prerequisites

Before starting a comparison, verify that an Exam Context has been established (see `study.md`). If no Exam Context exists, ask which AWS certification exam is being studied and establish it before proceeding.

## How to Compare Services

When asked about two or more AWS services (or "when would I use X vs Y?"), structure the response as follows:

### 1. One-Sentence Summary of Each Service
Plain language, no jargon. What does it do in the simplest terms?

### 2. Key Differences Table
Present a comparison table with columns:
| Aspect | Service A | Service B |
|--------|-----------|-----------|
| Primary use case | ... | ... |
| Scaling model | ... | ... |
| Pricing model | ... | ... |
| Availability/Durability | ... | ... |
| When to choose this one | ... | ... |

### 3. The Exam Angle
- Which of the active exam's content domains does this comparison relate to?
- What keywords in a question would signal you should pick Service A vs Service B?
- Common exam traps or distractors related to these services

### 4. Real-World Analogy
A non-technical analogy that makes the difference stick.

### 5. Quick Decision Flowchart
A simple "If X, then use A. If Y, then use B." decision guide.

## Determining High-Value Comparisons

Do NOT use a hardcoded list of comparisons. Instead, dynamically determine which service comparisons are most relevant based on:

1. The active exam's content domains and topic areas from the Exam Context
2. The AWS services that are in scope for the active exam
3. Services that commonly appear together in exam questions for the active certification

If asked for a random comparison or "give me a comparison to study", pick a high-value comparison relevant to the active exam's domains. Use the AWS Documentation MCP server to verify which services are in scope for the exam.

## Rules

- Always use the AWS Documentation MCP server to verify current service details
- Cite the official documentation URL for each service
- Flag if a service or feature is out of scope for the active exam
- Reference the active exam's domain names when mapping comparisons to exam content
