# Solution Architecture — AI Error Resolution Agent

> High-level technical overview. This document captures the product and engineering collaboration that shaped the AI agent design.

---

## Architecture Overview

```
Integration Error Occurs
        |
        v
Error Classification Service
  [user-side?] ──No──> Standard Error UI (system-side handling)
        |
       Yes
        |
        v
AI Agent Trigger
        |
        v
Context Builder
  - Error code + raw message
  - Integration type (AWS, Okta, GWS, etc.)
  - Triggering user action
  - Historical resolution patterns
        |
        v
Claude Sonnet 3.5 API Call
  [Structured prompt with context]
        |
        v
Response Parser
  - Extracts top 3 fix suggestions
  - Ranks by likelihood
  - Formats as plain-language steps
        |
        v
Error Page UI
  - Human-readable error summary
  - Top 3 fix suggestions (expandable)
  - Feedback capture (resolved / not resolved)
  - Support CTA fallback
```

---

## Key Components

### 1. Error Classification Service
- Maintains a mapping of error codes to error type (`user-side` / `system-side`)
- Built and maintained collaboratively between Product and Engineering
- Updated as new error patterns are identified post-launch
- Ensures the AI agent is only triggered where it can add value

### 2. Context Builder
Before calling the AI model, structured context is assembled:

```json
{
  "error_code": "AUTH_TOKEN_EXPIRED",
  "error_message": "OAuth token has expired for integration XYZ",
  "integration_type": "Google Workspace",
  "user_action": "Triggered compliance check",
  "resolution_patterns": [
    "Re-authenticate via OAuth flow",
    "Check token expiry settings in Google Admin Console",
    "Verify Sprinto has required scopes"
  ]
}
```

### 3. AI Model — Claude Sonnet 3.5
- Model: `claude-sonnet-3-5` (Anthropic)
- Chosen for strong instruction-following, structured output quality, and low latency
- Prompt is engineered collaboratively by PM and Engineering to:
  - Stay within product context and not hallucinate external tools
  - Return exactly 3 suggestions in ranked order
  - Use plain, non-technical language appropriate for the user persona
  - Include step-by-step resolution instructions per suggestion

### 4. Response Parser
- Parses model output into structured suggestion objects
- Each suggestion contains: `title`, `steps[]`, `confidence_rank`
- Falls back to generic guidance if model output is malformed

### 5. Error Page UI
- Updated error page component with AI suggestions panel
- Expandable suggestion cards with step-by-step instructions
- Feedback capture: "Did this fix your issue?" → stored for model improvement
- Always-visible support CTA to prevent user dead-ends

---

## Prompt Design Principles

Developed collaboratively between Product and Engineering:

1. **Grounded in context** — prompt includes error code, integration type, and known patterns to prevent generic responses
2. **Constrained output** — model is instructed to return exactly 3 suggestions, ranked, in a specific format
3. **Plain language** — prompt specifies the audience (non-technical compliance managers and IT admins)
4. **No hallucination guardrails** — model is explicitly told not to suggest tools or steps outside of the integration's known configuration surface
5. **Feedback loop** — user feedback (resolved/not resolved) fed back into prompt iteration cycles

---

## Engineering Collaboration Notes

- PM and Engineering co-designed the error classification taxonomy
- Prompt engineering was a joint effort — PM owned the user language requirements, Engineering owned the context payload structure
- Feature shipped behind a feature flag for controlled rollout
- Pilot cohort selected based on integration type and error frequency
- Post-pilot: accuracy measured via user feedback before GA release
