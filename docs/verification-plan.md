# Verification and Evaluation Plan

## Purpose and status

This plan defines how Smart Housing Services will be checked against
its requirements and how its classification component will be evaluated.

The checks below are planned. This document does not claim that the
backend, database, authentication, or trained model already exists.

The current browser prototype demonstrates user interactions only.
It cannot establish compliance with security or persistence requirements.

## Evaluation questions

1. Can users complete the request submission and processing workflow?
2. Are records accessible only to authorised users?
3. Are requests preserved when classification fails?
4. Does the trained classifier outperform a simple keyword baseline?
5. Do routing rules select the expected service?
6. Are the proposed response-time targets met under documented conditions?

## Functional verification

| Test ID | Requirements | Procedure | Expected result |
|---|---|---|---|
| T-01 | FR-01 | Sign in with valid and invalid demonstration credentials. | Valid credentials open the correct role interface; invalid credentials are rejected. |
| T-02 | FR-02 | Submit a request with a description and address. | One request is stored with an ID, owner, timestamp, and Submitted status. |
| T-03 | FR-02 | Submit a blank or whitespace-only description or address. | Submission is rejected with a clear validation message. |
| T-04 | FR-03, NFR-01 | As Resident A, attempt to open Resident B's request through both the interface and API. | Access is denied and no protected request content is returned. |
| T-05 | FR-04 | Process supported, ambiguous, and out-of-scope request examples. | The system returns a supported category or flags the request for manual review. |
| T-06 | FR-05 | Test routing cases with one, zero, and multiple matching services. | One match produces a recommendation; zero or multiple matches require manual review. |
| T-07 | FR-06 | Correct a suggested category and service, then confirm the assignment. | The final values are saved and the request becomes Assigned. |
| T-08 | FR-06, FR-07 | Inspect service queues before and after dispatcher confirmation. | The request appears in the selected service queue only after confirmation. |
| T-09 | FR-07, NFR-01 | Attempt to access another service's request through the API. | Access is denied. |
| T-10 | FR-08 | Move a request from Assigned to In progress and then Resolved, providing a resolution note. | Permitted changes are saved and visible to the resident. |
| T-11 | FR-08 | Attempt invalid status transitions and resolution without a note. | Invalid changes are rejected and the existing status is preserved. |
| T-12 | FR-09 | Change a category, assignment, and status. | History records the actor, timestamp, and previous and new values. |
| T-13 | FR-10 | Apply status and category filters separately and together. | Only matching requests are displayed. |

## Reliability and security checks

| Test ID | Requirements | Procedure | Expected result |
|---|---|---|---|
| T-14 | NFR-02 | Save a request and restart the application. | The request, assignment, and history remain available. |
| T-15 | NFR-03 | Make the classification component unavailable and submit a valid request. | The request is saved for manual review without automatic assignment. |
| T-16 | NFR-04 | Inspect password storage and authentication behaviour. | Passwords use salted password hashes rather than plaintext; valid login still works. |
| T-17 | NFR-01 | Attempt protected actions with the wrong role. | The server rejects unauthorised operations without modifying records. |
| T-18 | NFR-06 | Follow setup instructions from a fresh checkout. | The application starts using documented dependencies and configuration. |

## Interface checks

For NFR-05, inspect the request form and status view at viewport widths
of 360 and 1366 pixels.

Check that:
- Controls do not overlap.
- Text remains readable.
- There is no horizontal page scrolling.
- Validation messages explain how to correct invalid input.

Walk through these scenarios:
1. Resident submission and status tracking.
2. Dispatcher confirmation of a correct recommendation.
3. Dispatcher correction of an incorrect recommendation.
4. Manual handling of an uncertain request.
5. Service staff processing and resolution.

Record the browser, viewport, observed issues, and screenshots.

## Classification dataset

The evaluation requires labelled request texts.

Before training:
1. Document the source and permitted use of the data.
2. Remove or anonymise personal information.
3. Define the category labels and annotation rules.
4. Record the number of examples per category.
5. Identify duplicates and near-duplicate requests.
6. Separate synthetic examples from real examples.

A provisional split is 70% training, 15% validation, and 15% testing.
The final split must account for dataset size and category balance.

Duplicate or near-duplicate examples must remain in the same partition.
Where several records describe the same incident, group them together.

The test set must not be used for model selection or threshold tuning.
If there is too little data for a credible evaluation, report that
limitation rather than presenting unstable results as conclusive.

## Baseline and candidate model

Baseline:
A keyword-based classifier with documented category rules and a
manual-review fallback.

Initial candidate:
TF-IDF text features with logistic regression.

The candidate remains provisional pending the technology comparison.
Both approaches must be evaluated on the same held-out test set.

Keyword rules must be defined without inspecting test-set outcomes.
Any confidence threshold must be selected using validation data.

## Classification metrics

Report:
- Macro-F1, giving equal weight to each category.
- Precision, recall, and F1 for each category.
- Confusion matrix.
- Number of test examples per category.
- Manual-review rate.
- Classification coverage: the proportion receiving a category prediction.
- Error examples and their likely causes.

Report performance across all test examples. Predictions referred for
manual review must not be silently removed to improve the main score.
Any metrics calculated only on automatically classified examples must
be labelled separately and accompanied by coverage.

A minimum quality target will be set after the dataset feasibility
review and before final model evaluation.

If the model does not outperform the baseline, report the result
and investigate the errors.

## Routing evaluation

Test routing independently from classification using predefined
categories, addresses, service coverage, and expected assignments.

Include:
- Exactly one matching service.
- No matching service.
- Multiple matching services.
- An unsupported category.
- A dispatcher correction.

Report the proportion of routing test cases with the expected outcome.
The expected outcome may be manual review rather than an assignment.

Also test the complete classification-to-routing workflow separately,
so model errors can be distinguished from routing-rule errors.

## Performance evaluation

For NFR-07, the provisional target is a 95th-percentile response time
of at most 2 seconds for request-list retrieval with:
- 10 concurrent users.
- 1,000 stored requests.

Proposed procedure:
1. Populate the database with demonstration records.
2. Warm up the application for one minute.
3. Run the documented workload for five minutes.
4. Repeat the measurement three times.
5. Record response times, error rate, and actual request count.

Record:
- Processor and memory.
- Operating system.
- Browser or load-test tool.
- Application and dependency versions.
- Database configuration.
- Whether client and server are on the same machine.
- Dataset size and workload script.

Report each run and investigate failures.
These conditions and targets are proposed, not measured results.

## Test records

Each executed test will record:
- Test ID and linked requirement.
- Date and tester.
- Git commit or submission tag.
- Environment and input data.
- Expected and actual results.
- Pass, fail, or blocked status.
- Evidence and related defect task, if applicable.

Unexecuted tests will be marked Not run.
Tests requiring unavailable components will be marked Blocked.

## Completion criteria

Verification of the implemented prototype will require:
- Passing mandatory functional tests.
- Passing access-control and data-preservation tests.
- Documenting remaining defects and limitations.
- Comparing the classifier with the baseline on held-out data.
- Reporting actual measurements without substituting targets for results.

For the current preparation stage, the deliverable is this plan.
Full application verification will take place after implementation.
