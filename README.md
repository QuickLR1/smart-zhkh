# Smart Housing Services

## Project title

Development of an Intelligent Information System for Processing and Routing Citizen Requests in Housing and Communal Services.

## Author and supervisor

- Student: Isain Bexultan
- Group: SE2402
- GitHub account: QuickLR1
- Supervisor: Shynar Akhmetzhanova
- Project type: Individual diploma project

The student is responsible for research, requirements analysis, architecture,
implementation, testing, documentation, and project management.

The supervisor provides academic guidance and reviews key deliverables
at agreed checkpoints.

## Overview

Smart Housing Services is a planned web application for submitting,
classifying, and routing citizen requests related to housing and communal
services.

The proposed system will analyse the text of a request, suggest a category,
and recommend a responsible service using a configured service directory.
A dispatcher will review the recommendation and correct it when necessary.

## Problem statement

Manual classification and assignment of citizen requests may lead to
inconsistent routing and additional processing effort.

The project will investigate whether text classification combined with
explicit routing rules can support dispatchers in this process.

These are initial problem assumptions. User discussions and a review of
existing systems are planned to validate them and refine the requirements.

## Target users

- Residents who submit requests and track their status.
- Dispatchers who review categories and assign responsible services.
- Service staff who process assigned requests and update their status.

## Aim

To develop and evaluate a prototype that classifies citizen requests
and recommends responsible services while allowing dispatcher review
and correction.

## Objectives

1. Investigate user needs and existing request-handling processes.
2. Review relevant scientific literature and existing systems.
3. Define functional and non-functional requirements.
4. Compare suitable technologies and classification approaches.
5. Design the architecture, data model, and user interface.
6. Implement request submission, classification, routing, and status tracking.
7. Evaluate the prototype against a simple keyword-based baseline.
8. Document the results, limitations, and future improvements.

## Planned scope

The initial prototype is intended to support:

- Text-based request submission with an address.
- Storage and retrieval of requests.
- Suggested request categories.
- Service recommendations based on category and configured routing rules.
- Dispatcher review and manual correction.
- Assignment to service staff.
- Request status updates.
- Resident access to their own requests.
- Role-based access for residents, dispatchers, and service staff.

Provisional categories include water supply, heating, electricity,
waste collection, and building maintenance. The final categories and
supported input languages will be defined during requirements analysis.

## Out of scope

The initial prototype will not include:

- Production integration with municipal information systems.
- Automatic dispatch to real emergency services.
- Payments or utility billing.
- City-wide production deployment.
- Training a large language model from scratch.

Demonstrations will use a sample service directory and non-sensitive
test data.

## Example scenario

1. A resident submits a request about a heating problem.
2. The system stores the request and assigns an identifier.
3. The classifier suggests the Heating category.
4. Routing rules recommend a service from the configured directory.
5. A dispatcher confirms or corrects the recommendation.
6. Service staff update the request status.
7. The resident checks the status of the request.

## Expected outcomes

- A documented analysis of the problem and user needs.
- A literature review and comparisons of existing systems and technologies.
- Requirements with priorities and acceptance criteria.
- Architectural diagrams with editable source files.
- A user interface prototype.
- A working application prototype at a later development stage.
- An evaluation of classification and routing performance.
- A traceable development history linked to YouTrack tasks.

No measured performance improvements are claimed at this stage.

## Proposed technologies

The following stack is provisional and requires a documented comparison
with alternatives before the final selection.

| Area | Initial candidate | Intended purpose |
|---|---|---|
| Backend | Python and FastAPI | Request processing and application API |
| Database | PostgreSQL | Structured storage of users, requests, and services |
| Frontend | React | Interfaces for residents, dispatchers, and service staff |
| Text classification | TF-IDF and logistic regression with scikit-learn | Initial supervised classification approach |
| Baseline | Keyword-based rules | Simple comparison method |
| Version control | Git and GitHub | Change history and pull requests |
| Task management | YouTrack | Tasks, priorities, deadlines, and progress |

## Evaluation plan

The planned evaluation will include:

- Functional tests against requirement acceptance criteria.
- Access-control tests for user roles.
- Classification evaluation using a separate labelled test set.
- Macro-F1 and per-category precision and recall.
- Comparison with a keyword-based classification baseline.
- Routing correctness against predefined expected service assignments.
- Response-time measurements under documented test conditions.

Dataset size, category distribution, performance targets, and measurement
conditions will be defined in the evaluation plan.

## Current status

The project is at the initial planning and documentation stage.

Established:
- GitHub repository.
- YouTrack project.
- Task SHS-1 for preparation of this README.

In progress:
- Initial project description and scope definition.

Planned:
- User discussions and validation of problem assumptions.
- Literature review and system comparison.
- Technology comparison.
- Requirements and architecture.
- Interface prototype.
- Verification and evaluation plan.
- Implementation and testing.
- Supervisor review of key deliverables.

A runnable application is not yet available.

## Documentation plan

The following locations are planned. They will be added as the
corresponding tasks are completed.

| Location | Planned contents |
|---|---|
| docs/ | Proposal, research, comparisons, requirements, evaluation plan, and review records |
| diagrams/ | Editable diagram sources and readable exports |
| prototype/ | Interface mockups and prototype instructions |
| src/ | Application source code |
| tests/ | Automated tests and supporting test materials |

Documentation links will be added when the files exist.

## Setup, execution, and testing

There is currently no runnable application.

Dependency installation, configuration, execution, and testing instructions
will be added when the first executable version is available.

Passwords, API keys, and personal data must not be committed.
Configuration examples will use placeholder values.

## Development workflow

1. Create a YouTrack task with an owner, expected outcome, priority,
   deadline, and acceptance criteria.
2. Create a task branch containing the task ID.
3. Commit coherent changes with descriptive messages referencing the task.
4. Open a pull request describing the change and how it was checked.
5. Review the change and address any comments before merging.
6. Add the pull request or commit link to the YouTrack task.
7. Close the task only after its acceptance criteria are met.

Significant changes will be reviewed with the supervisor at agreed checkpoints.
Self-checks do not replace supervisor feedback.

Submission versions will be identified with the required Git tags:
pre-defense-1, pre-defense-2, and final-pre-defense.

## Project links

- [GitHub repository](https://github.com/QuickLR1/smart-zhkh)
- [YouTrack project](https://smarthzkh.youtrack.cloud/projects/SHS)
- [README task SHS-1](https://smarthzkh.youtrack.cloud/projects/SHS/issues/SHS-1/Prepare-the-initial-project-README)
