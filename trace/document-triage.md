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
| Intent | Brief prompt: "Time prior-authorization requests and appeals; flag expedited ones; alert at half the window." |
| Requirement | 003-FR-016: notify the on-call queue when expedited documents arrive outside business hours; 003-FR-014: start the deadline clock at receipt |
| Scenario | 003-US4-AS3: expedited appeal received at 11:40 p.m. on a Saturday; its clock starts at 11:40 p.m. and the on-call queue is notified |
| Feature | features/document-triage.feature, "An expedited weekend appeal keeps its original clock" |
| Code | src/document-triage.js, triageDocument: timed document types return receivedAt as clockStartsAt |
| Evidence | npm run test:bdd -- --tags @003-US4-AS3: 1 scenario (1 passed), 3 steps (3 passed) |
| Not proven by the evidence | That the on-call queue is notified: the spec THEN line requires it, but the test checks only that the deadline clock starts at the original receipt time |

## Gaps

- **Scenario with no automated evidence:** 003-FR-011-review
- **Why it matters:** Without a check, a wrong-member attachment could leave automatic attachment active and prevent the required Privacy Office incident review.
- **Unconfirmed capability:** The system can pause automatic attachment and open a Privacy Office incident review.
- **Who could confirm it:** Engineering lead, Privacy Office
