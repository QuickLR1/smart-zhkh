# Technology Comparison and Initial Decisions

## Purpose and status

This document compares alternatives for three key decisions:
the backend framework, database, and request-classification approach.

The comparison considers the requirements of an individual diploma
project: role-based workflows, persistent structured data, integration
with text classification, and reproducible evaluation.

Product capabilities are supported by official documentation.
Suitability assessments are project-specific engineering judgments.

No application benchmarks or classifier accuracy measurements have
been completed. Choices remain subject to implementation feasibility,
available data, and supervisor feedback.

## 1. Backend framework

### Requirements

The backend must validate submissions, enforce access restrictions,
manage request states, store history, and invoke classification.

Relevant requirements: FR-01, FR-02, FR-06, FR-08, FR-09, and NFR-01.

### Alternatives

| Criterion | FastAPI | Django |
|---|---|---|
| Main approach | API-oriented Python framework. [T1] | Python web framework with integrated application facilities. [T2] |
| Input handling | Type-based validation using Pydantic. [T1] | Forms support validation and conversion of submitted data. [T2] |
| API documentation | Automatic OpenAPI-based interactive documentation. [T1] | The reviewed core overview does not establish an equivalent automatic API documentation workflow; additional tooling would need selection. |
| User management | Provides security tools; application-specific account and permission handling must be assembled. [T1] | Includes accounts, groups, permissions, and sessions. [T2] |
| Database integration | Database library and migration tooling require separate selection. | Includes an object-relational mapper. [T2] |
| Fit for this project | Suitable for a focused API connected to a separate interface and Python classifier. | Suitable when integrated authentication and administration are the main development priorities. |
| Main trade-off | More responsibility for assembling authentication, persistence, and administration. | More framework conventions to adopt when the immediate goal is a small API. |

### Initial decision

Use FastAPI as the initial backend candidate.

Its documented request validation and API documentation fit the planned
API-based architecture. Python also allows the classifier and backend
to share a language.

This is not a claim that FastAPI is faster or more secure than Django
in this application. Authentication and object-level access checks
still require explicit implementation and tests.

Reconsider Django if assembling user management and administration
becomes a substantial obstacle for the individual project.

## 2. Database

### Requirements

The system must preserve relationships between users, requests,
services, assignments, and history.

Relevant requirements: FR-02, FR-06, FR-09, and NFR-02.

### Alternatives

| Criterion | PostgreSQL | SQLite |
|---|---|---|
| Deployment approach | Database server requiring configuration and a connection from the application. | Embedded database suitable for local application storage. [T4] |
| Structured relationships | Supports primary keys, foreign keys, uniqueness, and check constraints. [T3] | A relational alternative suitable for a small local prototype; required integrity settings must be verified during implementation. |
| Setup effort | Requires a running database service and credentials. | Does not require a separate database server. [T4] |
| Concurrent writes | Candidate for a shared server-based application; actual performance must be tested. | Supports one writer at a time per database file; short transactions can take turns. [T4] |
| Local demonstration | Additional setup is required. | Attractive for a simple local demonstration. [T4] |
| Fit for the intended application | Suitable for the planned shared backend and related records. | Suitable if deployment remains small and local. |
| Main trade-off | More operational setup for an individual student. | Write-concurrency and deployment constraints must be considered before expanding the system. |

### Initial decision

Use PostgreSQL for the implemented application.

The planned application has shared persistent records and explicit
relationships. Database constraints can help prevent invalid references,
such as assigning a request to a nonexistent service.

SQLite remains a reasonable fallback for a limited local deployment.
It is not rejected as incapable of supporting web applications.

Switching databases would require repeating persistence and integrity
checks. Passing tests against SQLite alone would not prove correct
PostgreSQL behaviour.

The current HTML UX prototype uses neither database. Its temporary
in-memory state is a demonstration limitation.

## 3. Request classification

### Requirements

The system must suggest request categories, support dispatcher
correction, and refer uncertain cases for review.

Relevant requirements: FR-04, FR-06, and NFR-03.

### Alternatives

| Criterion | Keyword rules | TF-IDF with logistic regression |
|---|---|---|
| Mechanism | Match manually defined words or patterns to categories. | Convert text into numerical features and train a supervised classifier. [T5, T6] |
| Training data | Does not require statistical training; rules still need representative examples for design and testing. | Requires labelled training examples and separate evaluation data. |
| Inspectability | A matched rule can be inspected directly. | Feature weights can support inspection, but predictions require more analysis than a single rule match. |
| Wording variation | Unlisted expressions and ambiguous matches may be missed. | Can learn associations present in training examples; generalisation must be measured. |
| Uncertainty handling | No match or conflicting matches can trigger manual review. | A validation-selected threshold can trigger review; probability estimates must not be treated as guaranteed correctness. |
| Implementation effort | Suitable for a simple baseline and UX demonstration. | Requires data preparation, training, validation, and model versioning. |
| Main limitation | Manual rule maintenance and limited language coverage. | Dependence on the quantity, quality, and representativeness of labelled data. |
| Evaluation | Test on the same held-out examples as the candidate model. | Compare macro-F1, per-category metrics, and review coverage against the baseline. |

The keyword approach describes a project-designed baseline, not a
specific commercial product.

The scikit-learn documentation describes text feature extraction and
classification workflows. LogisticRegression supports sparse input,
which is relevant to text feature matrices. [T5, T6]

### Initial decision

Implement keyword rules as the baseline.

Evaluate TF-IDF with logistic regression as the first supervised
candidate, subject to obtaining a suitable labelled dataset.

The trained approach is not assumed to outperform the baseline.
Both methods will use the same held-out test set, as described in
the verification plan.

If the available data is insufficient, report that limitation and
retain the rule-based demonstration. Do not describe the current
UX prototype as a trained AI system.

## Summary of decisions

| Area | Initial choice | Main justification | Reconsider when |
|---|---|---|---|
| Backend | FastAPI | API-oriented workflow and explicit request validation | Integrated account administration becomes the dominant implementation need |
| Database | PostgreSQL | Shared persistent records with explicit relationships | Deployment is reduced to a small local-only demonstration |
| Classification | TF-IDF with logistic regression, compared with keyword rules | A supervised candidate that can be evaluated within the Python workflow | Labelled data is insufficient or measured performance does not justify the approach |

## Additional implementation notes

React remains a provisional frontend candidate in the project README.
It has not been selected through the three comparisons above.

The existing UX prototype uses plain HTML, CSS, and JavaScript.
It does not demonstrate that the planned backend or frontend stack
has already been implemented.

Exact dependency versions will be selected and pinned during
implementation. Setup instructions and performance results will
refer to those versions.

## Sources

Official documentation reviewed on 23 October 2026.

[T1] FastAPI. Features.
https://fastapi.tiangolo.com/features/

[T2] Django. Getting started with Django.
https://www.djangoproject.com/start/

[T3] PostgreSQL. Constraints.
https://www.postgresql.org/docs/current/ddl-constraints.html

[T4] SQLite. Appropriate Uses for SQLite.
https://sqlite.org/whentouse.html

[T5] scikit-learn. Working with text documents.
https://scikit-learn.org/stable/auto_examples/text/index.html

[T6] scikit-learn. LogisticRegression.
https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html
