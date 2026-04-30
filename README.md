# ai-error-resolution-agent
Ai Agent to fix integration errors 

**Type:** AI-Powered In-Product Feature | B2B SaaS | Compliance Tech  
**Company:** Sprinto  
**Status:** Shipped

---

## Overview

Our integration module is the most critical part of the product — it connects customer systems (HRMS, MDM, cloud providers) to Sprinto's compliance engine. It is also where the highest volume of errors occurred.

After analyzing error patterns, we identified that a significant portion were **user-side errors** — things like expired tokens, insufficient permissions, misconfigured scopes — not engineering bugs. These had error codes but displayed vague, unhelpful messages to users, causing them to raise support tickets unnecessarily.

We built an **AI Fix-It Agent** that detects user-side errors in real time, interprets the error context, and surfaces the top 3 actionable fix suggestions directly inside the product — enabling customers to self-serve and resolve issues without contacting support.

---

## Problem

- Integration module had the highest error rate across the product
- Errors were broadly categorized but not surfaced meaningfully to users
- Users saw vague error messages with no clear next step
- Default behavior: raise a support ticket → CS team → Engineering → resolution
- This created high support load, slow resolution times, and poor customer experience

---

## Solution

An in-product AI agent that:
1. Detects when a user-side integration error occurs
2. Classifies the error type using predefined error codes and context
3. Calls Claude Sonnet 3.5 with a structured prompt containing error metadata, product context, and resolution patterns
4. Returns the top 3 most likely fixes in plain language
5. Displays them inline on the error page with step-by-step instructions the user can follow immediately

---

## Impact

| Metric | Result |
|---|---|
| AI fix suggestion accuracy | 90% |
| Support ticket reduction | 30% |
| Mean time to resolution | Significantly reduced |
| Customer satisfaction | Improved (post-launch CSAT increase) |

---

## Repo Structure

| File | Description |
|---|---|
| `problem-statement.md` | Error pattern analysis, user-side vs system-side classification |
| `prd.md` | Full Product Requirements Document |
| `solution-architecture.md` | High-level AI agent design and technical approach |
| `metrics-and-impact.md` | Success metrics, post-launch results, future iterations |

---

## Key Links

- Company: [Sprinto](https://sprinto.com)
