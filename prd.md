# PRD — AI Error Resolution Agent
**Product:** Sprinto Integration Module  
**Feature:** In-Product AI Fix-It Agent  
**Author:** Yuvraj Gulati  
**Status:** Shipped

---

## 1. Objective

Enable customers to self-resolve user-side integration errors directly inside the product by surfacing AI-generated, context-aware fix suggestions at the point of failure — eliminating the need to raise a support ticket for resolvable errors.

---

## 2. Goals

| Goal | Metric |
|---|---|
| Reduce support ticket volume from integration errors | 25-30% reduction |
| Improve fix suggestion accuracy | 90%+ |
| Reduce mean time to resolution for user-side errors | Target: under 10 minutes self-served |
| Improve customer satisfaction on integration flows | CSAT improvement post-launch |

---

## 3. Non-Goals

- This feature does not attempt to fix system-side or engineering errors
- It does not auto-remediate errors on the user's behalf (no automated token refresh etc.)
- It does not replace CS or engineering escalation for complex issues

---

## 4. Users

**Primary:** Sprinto customers managing integrations — typically IT admins, DevOps engineers, or compliance managers connecting their tools to Sprinto.

**Secondary:** Sprinto CS team — reduced ticket load, faster triage for escalated issues.

---

## 5. User Stories

**As an IT admin**, when my integration fails, I want to understand what went wrong and how to fix it immediately — without waiting for support — so I can unblock my compliance workflows.

**As a compliance manager**, when I see an integration error, I want clear next steps in plain language so I don't need technical expertise to resolve it.

**As a CS agent**, I want fewer tickets for user-resolvable errors so I can focus on complex customer issues that actually need human intervention.

---

## 6. Feature Description

### Error Classification Layer
- On any integration error event, the system checks the error code against a classification map
- Errors are tagged as `user-side` or `system-side`
- Only `user-side` errors trigger the AI agent

### AI Fix-It Agent
- Triggered automatically when a `user-side` error is detected
- Passes structured context to Claude Sonnet 3.5:
  - Error code and raw message
  - Integration type (e.g., AWS, Okta, Google Workspace)
  - User action that triggered the error
  - Known resolution patterns from historical data
- Model returns top 3 suggested fixes ranked by likelihood
- Fixes are displayed in plain language with step-by-step instructions

### Error Page UI
- Error page is updated to show:
  - What went wrong (human-readable summary)
  - Top 3 fix suggestions with expandable steps
  - "Still stuck? Contact support" fallback CTA
  - Feedback prompt: "Did this fix your issue?" (Yes / No)

---

## 7. Acceptance Criteria

- [ ] User-side errors are correctly classified and trigger the AI agent
- [ ] System-side errors do not trigger the agent and show standard error UI
- [ ] AI suggestions are displayed within 3 seconds of error detection
- [ ] Each suggestion includes a title and step-by-step resolution instructions
- [ ] "Did this fix your issue?" feedback is captured and stored
- [ ] Support CTA is always visible as a fallback
- [ ] Feature is behind a flag for staged rollout

---

## 8. Out of Scope for V1

- Auto-remediation (agent fixing the error without user action)
- Multi-language support
- Suggestions for system-side errors
- Integration with ticketing system for auto-escalation

---

## 9. Success Metrics (Post-Launch)

| Metric | Target | Result |
|---|---|---|
| Ticket reduction from integration errors | 25% | 30% achieved |
| AI suggestion accuracy (user-confirmed) | 85% | 90% achieved |
| Self-serve resolution rate | 60% of user-side errors | Tracked via feedback |
| CSAT on integration flows | Improvement vs baseline | Positive improvement |
