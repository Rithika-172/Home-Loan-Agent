# Home Credit LAP Qualification Voice Agent

Prompt-engineering submission for the AI Intern (Prompt Engineer) assignment: an AI voice agent that tells existing Home Credit customers about a pre-approved Loan Against Property offer (up to Rs. 75 lakh), collects 7 eligibility data points, and hands qualified leads to a senior loan expert.

## Contents

| File | Purpose |
|------|---------|
| `system_prompt.md` | The complete system prompt (paste this into the voice platform) |
| `test_scenarios.md` | 22 test scripts with expected results |
| `submission/` | Call recordings, transcripts, and the results table |

## Approach

1. Turned the assignment into explicit business rules (property type, ownership, documents, loan amount, occupation and income mode, market value, tenure) with exact pass/fail outcomes.
2. Designed a silent state per call. On every customer turn the agent follows one loop: extract all facts, apply corrections, check transfer, check disqualification, check over-limit amount, update state, ask only the earliest unanswered item.
3. Separate branches for busy customers (callback), wrong person, existing loan or EMI reduction (transfer specialist), and loan above 75 lakh (offer the maximum).
4. A strict handoff gate: no qualification message until all 7 items are answered and every rule passed.
5. Guardrails against invented interest rates, fees, or a minimum property value. Product questions are answered only from `additional_context_from_rag`.
6. Voice-specific rules: short turns, one question at a time, amounts spoken in words, no lists.
7. Variables supported: company_name, customer_name, agent_name, agent_gender, current_date, current_day, current_time, additional_context_from_rag, language_to_speak, conversation_history, customer_utterance.

## Design decisions

- No separate "existing loan?" question is asked. The transfer branch triggers when the customer mentions it, as the assignment states, which keeps the checklist at exactly 7 questions.
- Market value has no minimum threshold, because the assignment gives none.
- Over-limit loan amounts are not rejected. The agent explains the limit and asks whether to proceed with 75 lakh.

## Test results

Fill this in after your calls.

| ID | Scenario | Result (Pass/Fail) | Recording | Transcript | Notes |
|----|----------|--------------------|-----------|------------|-------|
| T01 | Happy path | | | | |
| T02 | Agricultural | | | | |
| T03 | Cash income | | | | |
| T04 | No originals | | | | |
| T07 | Loan above 75L, accept | | | | |
| T10 | Existing loan | | | | |
| T12 | Out-of-order answers | | | | |
| T13 | Busy customer | | | | |

## Prompt iterations

Note here what you changed after failed tests (for example "T12: agent re-asked ownership, so I added the extract-first rule").

## Platform

Built and tested on: (Retell AI / Bolna), voice: (name), LLM: (name).
