# AI Safety and Security Plan

This plan documents the security and safety controls that should be included as Realtor AI Agent moves from concept to implementation.

## Data Handling

The assistant may collect personal information such as names, contact details, location preferences, budget, buying timeline, and property requirements.

Recommended controls:

- Collect only the fields needed for lead qualification.
- Store leads in Firestore with restrictive access rules.
- Avoid logging full contact details in plaintext application logs.
- Add a retention policy for stale leads.
- Document what data is sent to the LLM provider.

## Prompt Injection Controls

The chat interface should treat user input as untrusted.

Recommended controls:

- Keep system and developer instructions server-side.
- Use structured output validation for lead extraction.
- Reject requests to reveal prompts, internal routing logic, or stored lead data.
- Log prompt injection attempts as security events.
- Add tests for common prompt injection patterns.

## Real Estate Compliance Boundaries

The assistant should avoid:

- Legal advice
- Financial advice
- Guaranteed approval or pricing claims
- Fair-housing-sensitive language
- Unsupported claims about neighborhoods or protected classes

Recommended response behavior:

- Provide general process guidance.
- Ask clarifying questions.
- Route sensitive questions to a licensed professional.
- Keep summaries factual and based on user-provided details.

## Human Handoff

High-value or sensitive interactions should be routed to a human.

Handoff triggers:

- User asks for legal or financial advice.
- User provides urgent timeline or complex requirements.
- User asks about regulated or sensitive topics.
- Lead score crosses a qualification threshold.

## Testing Checklist

- Lead classification works for buyer, seller, renter, and investor scenarios.
- Required fields are extracted into structured JSON.
- Missing fields trigger follow-up questions.
- Prompt injection attempts are refused or neutralized.
- Firestore records do not include unnecessary sensitive data.
- Handoff flow works without exposing internal prompts or system details.
