# Problem Statement — AI Error Resolution Agent

## Context

Sprinto helps companies automate compliance (SOC 2, ISO 27001, GDPR etc.) by integrating with their existing tools — HRMS, MDM, cloud providers, identity platforms. The **integration module** is the most critical and most used part of the product.

It is also where the highest concentration of errors occurred.

---

## Error Pattern Analysis

After monitoring product telemetry and reviewing support ticket data, a clear pattern emerged:

**Not all errors were equal.**

We segregated errors into two categories:

### System-Side Errors
- Infrastructure failures, API timeouts, Sprinto-side bugs
- Required engineering intervention
- Could not be self-served by users

### User-Side Errors
- Expired OAuth tokens
- Insufficient permissions or missing scopes
- Misconfigured API keys
- Incorrect account selections
- Missing required fields or wrong data format

**User-side errors made up a significant share of total integration errors.**

---

## The Real Problem

Despite having error codes, the product displayed **vague, generic error messages** to users:

> "Integration failed. Please try again or contact support."

Users had no context, no next step, and no way to self-diagnose. The default path was:

```
User hits error → Raises support ticket → CS team investigates
→ Escalates to Engineering → Resolution communicated back to user
```

This created:
- **High support load** on CS and Engineering teams
- **Slow resolution times** — often 24-48 hours for issues users could fix in minutes
- **Poor customer experience** — users felt blocked on critical compliance workflows
- **Wasted engineering time** on issues that were not bugs

---

## User Insight

Through support ticket analysis and customer interviews, the core insight was:

> Users don't need us to fix the error for them. They need to know **what the error means** and **what to do next** — in plain language, right where the error happens.

---

## Opportunity

Build a self-serve resolution layer directly inside the product — an AI agent that interprets user-side errors and gives users actionable fix steps without needing to contact support.
