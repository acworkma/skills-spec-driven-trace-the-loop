# Trace worksheet: inbound document triage

Follow one behavior from intent to evidence. Keep the headings and the labels in the first column: Mona reads them
to check your work.

## Trace 1

| Link | What you found |
| --- | --- |
| Intent | Brief prompt: "Classify each document with a confidence score; auto-route confident ones, send the rest to people." |
| Requirement | 003-FR-004: auto-route only non-Other documents at or above their type's threshold; the rest go to human review with a reason |
| Scenario | 003-US1-AS1: claim forms at 0.96 and 0.72 against a 0.90 threshold |
| Feature | features/document-triage.feature, "Confidence determines who routes a claim form" (0.96, 0.90 and 0.72) |
| Code | src/document-triage.js, triageDocument: confidence < threshold sends the document to human-review |
| Evidence | npm run test:bdd -- --tags @003-US1-AS1: 3 scenarios (3 passed) |
| Not proven by the evidence | That a document sent to human review carries a reason, and that Operations can change a type's threshold (003-FR-005) |


## Trace 2

| Link | What you found |
| --- | --- |
| Intent | |
| Requirement | |
| Scenario | |
| Feature | |
| Code | |
| Evidence | |
| Not proven by the evidence | |

## Gaps

- **Scenario with no automated evidence:**
- **Why it matters:**
- **Unconfirmed capability:**
- **Who could confirm it:**
