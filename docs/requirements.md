# Initial System Requirements

## Purpose and status

This document describes the planned behaviour of Smart Housing Services
and how it will be verified.

These are initial requirements based on the project proposal.
They are pending validation with potential users and the supervisor.
The acceptance criteria describe planned checks, not completed tests.

## Users

- Resident: submits requests and views their status.
- Dispatcher: reviews requests and confirms service assignments.
- Service staff: processes requests assigned to their service.

## Priorities

- Must: necessary for the core prototype.
- Should: desirable after the core functionality is available.

## Functional requirements

| ID | Priority | Requirement | Acceptance criterion |
|---|---|---|---|
| FR-01 | Must | Users can sign in with a predefined role. | Valid credentials open the appropriate interface. Invalid credentials are rejected. |
| FR-02 | Must | Residents can submit a request containing a description and address. | A valid submission is saved with a unique ID, owner, creation time, and Submitted status. Empty descriptions or addresses are rejected. |
| FR-03 | Must | Residents can view their own requests. | A resident can see the description and current status of their requests but cannot access another resident's requests. |
| FR-04 | Must | The system suggests a category for each request. | Processing produces a category from the supported list or flags the request for manual review. Classification quality is evaluated separately on labelled data. |
| FR-05 | Must | The system recommends a responsible service using configured rules. | A request with one matching service receives that recommendation. Requests with no match or multiple matches are flagged for manual review. |
| FR-06 | Must | Dispatchers can confirm or correct recommendations. | The selected category and service are saved. A request is assigned only after dispatcher confirmation. |
| FR-07 | Must | Service staff can view requests assigned to their service. | Assigned requests appear in the relevant service queue. Staff cannot access another service's queue. |
| FR-08 | Must | Service staff can update request status. | Assigned requests can move to In progress and then Resolved. The resident sees the saved status. |
| FR-09 | Must | The system records changes to categories, assignments, and statuses. | Each change has a timestamp, actor, and previous and new values. |
| FR-10 | Should | Dispatchers can filter requests by status and category. | The displayed list contains only requests matching the selected filters. |

## Initial categories

- Water supply.
- Heating.
- Electricity.
- Waste collection.
- Building maintenance.
- Other / Needs review.

The category definitions and supported input languages will be finalised
after user discussions and a review of available data.

## Request processing rules

1. A new request receives Submitted status.
2. Classification and routing produce recommendations.
3. A dispatcher reviews the request and confirms a service.
4. The request receives Assigned status.
5. Staff of the assigned service can change it to In progress.
6. Staff can mark it Resolved after adding a resolution note.

Requests needing manual review remain Submitted until the dispatcher
assigns them. A review flag is separate from the processing status.

Residents cannot change assignments or processing statuses.
Transitions outside the defined sequence must be rejected in the
initial prototype.

## Non-functional requirements

| ID | Priority | Requirement | Acceptance criterion |
|---|---|---|---|
| NFR-01 | Must | Access restrictions are enforced by the server. | Unauthorised requests to view or modify protected records are rejected, including attempts made directly through the API. |
| NFR-02 | Must | Saved data survives application restarts. | Requests, assignments, and history remain available after restarting the application and reconnecting to the database. |
| NFR-03 | Must | Classification failure does not cause request loss. | If classification is unavailable, the request is saved and flagged for dispatcher review without automatic assignment. |
| NFR-04 | Must | Passwords are not stored in plaintext. | Inspection confirms that password records contain salted password hashes rather than original passwords. |
| NFR-05 | Must | The main interface supports desktop and mobile screens. | At viewport widths of 360 and 1366 pixels, the request form and status view have no overlapping controls or horizontal page scrolling. |
| NFR-06 | Must | Setup and execution are documented. | A fresh checkout can be started by following the documented installation and configuration steps. |
| NFR-07 | Should | Request list retrieval remains responsive under the defined test load. | The proposed target is a 95th-percentile response time of at most 2 seconds with 10 concurrent users and 1,000 stored requests. The test hardware and procedure are documented. |

The performance target is provisional and requires review.
It is not a measured result.

## Classification evaluation

The classification component will be compared with a keyword-based
baseline using the same held-out labelled test set.

The evaluation will report:

- Dataset origin and size.
- Number of examples in each category.
- Training, validation, and test split procedure.
- Macro-F1.
- Precision and recall for each category.
- Confusion matrix.
- Examples of incorrect predictions.
- Proportion of requests referred for manual review.

Test examples must not be used for training or model selection.
Synthetic data, if used, must be clearly identified.

Routing rules will also be tested independently using predefined
categories, addresses, and expected services.

A model-quality target will be defined after the dataset review
and before final evaluation. No achieved accuracy is claimed at
this stage.

## Open decisions

The following decisions require further investigation:

- Supported input languages.
- Final category definitions.
- Availability of labelled request data.
- Service coverage and address-matching rules.
- Handling of requests containing several different problems.
- Performance targets and test conditions.

## Traceability

Requirement IDs will be referenced in implementation tasks and tests.
Changes to this document will be recorded in Git and linked to YouTrack.
