# Project Plan and Risk Register

## 1. Purpose and planning status

This document defines responsibilities, milestones, dependencies,
and initial risks for Smart Housing Services.

The preparation-stage submission date is 24 October 2026.
Later milestone dates are provisional and must be agreed with
the supervisor and aligned with the university schedule.

This plan does not claim that all listed deliverables are completed.
Actual task status and supporting links are maintained in YouTrack.

## 2. Responsibilities

### Student

Isain Bexultan, SE2402, is responsible for:

- Research and source verification.
- Discussions with potential users.
- Requirements and architecture.
- Prototype and application development.
- Dataset preparation and evaluation.
- Testing and defect correction.
- Git history and YouTrack task maintenance.
- Report and presentation preparation.

### Supervisor

Shynar Akhmetzhanova provides academic guidance and reviews key
deliverables at agreed checkpoints.

Feedback will be recorded after an actual review.
Listing a review milestone does not mean that approval has occurred.

## 3. Preparation-stage deliverables

| Deliverable | Repository location or evidence | Completion condition |
|---|---|---|
| Project overview | README.md | Required project information and current links are present |
| Proposal and scope | docs/project-proposal.md | Problem, aim, objectives, users, and scope are described |
| Initial requirements | docs/requirements.md | Requirements have priorities and acceptance criteria |
| Architecture diagrams | diagrams/ | Three diagrams have editable sources and readable exports |
| UX prototype | prototype/ | Main demonstration workflow is checked and limitations are documented |
| Verification plan | docs/verification-plan.md | Tests, metrics, conditions, and baseline are defined |
| Existing-system comparison | docs/existing-systems.md | Three systems are compared against eight criteria with evidence |
| Technology comparison | docs/technology-comparison.md | Three decisions include alternatives and justification |
| Literature review | docs/literature-review.md | Twelve sources are discussed, including eight scientific works with types identified |
| Project plan and risks | docs/project-plan-and-risks.md | Responsibilities, dependencies, milestones, and risks are documented |
| Relevance evidence | Planned: docs/user-validation.md | Actual discussions or client agreement are documented and assumptions remain identifiable |
| Supervisor feedback | Planned: docs/supervisor-feedback.md | Actual comments and decisions on addressing them are recorded |
| Submission materials | Main report PDF and YouTrack evidence PDF | Required sections and readable task screenshots are included |

File locations identify intended evidence. Their existence, content,
and task status must be checked before submission.

## 4. Milestones

| Milestone | Expected result | Dependency | Target |
|---|---|---|---|
| M1: Preparation submission | Analysis, initial design, prototype materials, plans, and submission PDFs | Preparation-stage documents and evidence | 24 October 2026 |
| M2: Requirements and data feasibility review | Agreed scope, category definitions, language scope, and a feasible data strategy | User discussions, supervisor feedback, and source review | Date to be agreed |
| M3: Core application workflow | Authentication, persistent requests, assignments, statuses, and history | M2 and database design | Date to be agreed |
| M4: Classification and routing integration | Keyword baseline, supervised candidate where feasible, and routing rules | M2 dataset feasibility and M3 workflow | Date to be agreed |
| M5: Evaluation and correction | Recorded functional tests, model comparison, and documented limitations | M3 and M4 | Date to be agreed |
| M6: Final documentation and demonstration | Updated report, presentation, reproducible setup, and tagged submission | M5 and supervisor review | University deadline to be confirmed |

Later dates will be added when agreed. No timetable is attributed
to the supervisor without confirmation.

## 5. Dependencies

- User findings may change requirements, categories, and priorities.
- Requirements guide architecture, interface scenarios, and tests.
- Category definitions must precede consistent dataset labelling.
- Data availability must be checked before committing to supervised training.
- The request workflow can be developed independently of model training.
- Classification output feeds routing, but routing also requires
  a service directory and coverage rules.
- Integrated evaluation requires executable components and recorded versions.
- Final reports must reflect observed results and actual task status.

## 6. Task and version-control workflow

Each meaningful work item is represented by a YouTrack task containing:

- Responsible student.
- Expected outcome.
- Priority and deadline.
- Acceptance criteria.
- Links to relevant changes or deliverables.

Changes are prepared in task branches and submitted through pull requests.
Branch names and commit or pull-request descriptions include the task ID.

Before merging, the change is checked against its acceptance criteria.
A completed task must link to the actual result.

Significant deliverables are reviewed with the supervisor at agreed
checkpoints. Student self-checks do not replace supervisor feedback.

Any departure from the intended workflow is recorded accurately.
Historical activity must not be fabricated or backdated.

## 7. Initial risk register

Likelihood and impact are qualitative planning estimates.

| ID | Risk | Likelihood | Impact | Mitigation or response | Owner |
|---|---|---|---|---|---|
| RSK-01 | Suitable labelled requests cannot be obtained | High | High | Investigate data access early; document provenance; use clearly labelled synthetic examples for demonstrations; do not claim real-world model validation |
| RSK-02 | Category labels are ambiguous or inconsistent | Medium | High | Define annotation rules and examples; review disagreements; provide manual handling for unclear requests |
| RSK-03 | Russian and Kazakh requirements exceed available data | Medium | High | Validate language scope and evaluate each supported language separately |
| RSK-04 | Request data contains personal information | Medium | High | Use only permitted data; minimise and anonymise records before experiments; keep confidential data out of the repository |
| RSK-05 | The classifier does not outperform keyword rules | Medium | Medium | Compare on the same held-out set; analyse errors; report the result without concealing baseline performance |
| RSK-06 | Routing rules select the wrong service | Medium | High | Test routing independently; handle zero and multiple matches; require dispatcher confirmation |
| RSK-07 | The scope becomes too large for one student | High | High | Prioritise the submission-to-resolution workflow; defer optional integrations and enhancements |
| RSK-08 | Access-control defects expose other users' records | Medium | High | Enforce checks on the server and test direct API access with different users and roles |
| RSK-09 | Supervisor review is delayed | Medium | High | Request a review early, identify specific decisions, and record pending feedback honestly |
| RSK-10 | Submission links or exported files are inaccessible | Medium | High | Check repository and YouTrack access, open both PDFs, and verify the submitted version |
| RSK-11 | The UX demo is mistaken for an implemented AI system | Medium | Medium | Label rule-based behaviour, temporary storage, simulated roles, and missing backend functionality explicitly |
| RSK-12 | The preparation deadline is reached before evidence is complete | High | High | Prioritise required deliverables, report remaining gaps, and discuss unresolved items with the supervisor |

## 8. Review checkpoints

Proposed checkpoints for agreement with the supervisor:

1. Problem, scope, relevance evidence, and initial requirements.
2. Architecture, prototype, and data feasibility.
3. Core implementation and access-control design.
4. Evaluation design and interpretation of results.
5. Final report and defence materials.

Each review record should include the date, reviewed version,
actual comments, planned response, and links to resulting changes.

## 9. Submission checklist

- Confirm the permitted repository platform: the original requirements
  allow GitHub or GitLab, while the submission message requests GitLab accounts.
- Ensure the supervisor and committee have the required access.
- Check that README links point to existing materials.
- Check that diagram sources and exports are included.
- Open the prototype and verify its documented demonstration scenario.
- Confirm that task states reflect actual progress.
- Prepare one PDF containing the required YouTrack board and task screenshots.
- Prepare a separate main PDF report containing all required sections.
- Record missing evidence and known limitations.
- Create the appropriate submission tag after checking the submitted version.
- Supply the repository link, tag, completed-work summary, and outstanding tasks.

The required stage tags are pre-defense-1, pre-defense-2, and
final-pre-defense. The tag corresponding to this submission must
be confirmed before creation. Existing submission tags must not be moved.

## 10. Project links

- Repository: https://github.com/QuickLR1/smart-zhkh
- YouTrack: https://smarthzkh.youtrack.cloud/projects/SHS
