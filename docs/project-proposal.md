# Project Proposal and Scope

## Project information

**Title:** Development of an Intelligent Information System for Processing
and Routing Citizen Requests in Housing and Communal Services.

**Student:** Isain Bexultan  
**Group:** SE2402  
**Supervisor:** Shynar Akhmetzhanova  
**Project type:** Individual diploma project  
**Working name:** Smart Housing Services

## Problem statement

Citizen requests concerning housing and communal services describe
different problems, such as heating failures, water supply interruptions,
waste collection issues, and building maintenance needs.

Processing a request requires understanding its content, identifying
the relevant category, and selecting a responsible service.

The project investigates the assumption that manual classification
and assignment can create additional work for dispatchers and lead
to inconsistent routing.

At this stage, these difficulties are working assumptions rather
than verified findings from a particular organisation. Discussions
with potential users and analysis of existing systems will be used
to validate and refine the problem statement.

## Aim

To develop and evaluate a web-based prototype that classifies
citizen requests and recommends responsible services while allowing
dispatchers to review and correct the recommendations.

## Objectives

1. Investigate the needs of residents, dispatchers, and service staff.
2. Review scientific literature on text classification and request routing.
3. Compare existing systems and alternative technical approaches.
4. Define functional and non-functional requirements with acceptance criteria.
5. Design the system architecture, data model, and user interface.
6. Implement request submission, classification, routing recommendations,
   and status tracking.
7. Evaluate the prototype against a keyword-based baseline.
8. Document the findings, limitations, and opportunities for further work.

## Target users

### Residents

Residents submit requests describing a problem and its location.
They can view their own requests and follow status updates.

### Dispatchers

Dispatchers review incoming requests, check suggested categories,
and confirm or correct service assignments.

### Service staff

Service staff view assigned requests and update their processing status.

## Proposed solution

The proposed system combines text classification with explicit
service-routing rules.

A resident submits a request through a web interface. The backend
stores the request and passes its text to a classification component.

The classifier suggests a category. A separate routing component
uses the category and a configured service directory to recommend
a responsible service. Location may be used where the directory
defines service coverage.

A dispatcher checks the recommendation before confirming the
assignment. Requests that cannot be classified or matched to a
service require manual review.

The prototype supports decision-making. It does not guarantee
that the initial recommendation is correct.

## Intelligent component

The intelligent component will analyse the text of a request
and predict its category.

An initial candidate is a supervised text-classification pipeline
using TF-IDF features and logistic regression. This choice is
provisional and will be compared with reasonable alternatives.

A keyword-based classifier will serve as a baseline.

The classification model will require labelled examples.
Dataset availability, category balance, supported input languages,
and data preparation procedures remain to be established.

Training and evaluation data will be separated to avoid evaluating
the model on the same examples used for training.

## Scope

The planned prototype includes:

- Text-based request submission with a location.
- Storage of requests and their processing history.
- Automatic category suggestions.
- Service recommendations from a demonstration service directory.
- Dispatcher confirmation and correction.
- Assignment of requests to service staff.
- Status updates and resident status tracking.
- Role-based access to relevant functions and records.

Provisional categories are:

- Water supply.
- Heating.
- Electricity.
- Waste collection.
- Building maintenance.
- Other / Needs review.

The final category definitions and supported input languages
will be specified during requirements analysis.

## Exclusions

The initial prototype excludes:

- Production integration with municipal information systems.
- Real emergency-service dispatch.
- Utility payments and billing.
- City-wide production deployment.
- Training a large language model from scratch.
- Automatic execution of maintenance work.

The prototype will use a demonstration service directory.
Test data will be synthetic or appropriately anonymised.
Synthetic data will be identified as such and will not be treated
as evidence of real-world performance.

## Main user scenario

1. A resident enters a request description and address.
2. The system saves the request and provides an identifier.
3. The classifier suggests a category.
4. Routing rules recommend a responsible service where a match exists.
5. A dispatcher reviews and confirms or corrects the recommendation.
6. Service staff receive the assignment and update its status.
7. The resident checks the latest status.

## Expected outcomes

The project is expected to produce:

- A validated problem statement and documented requirements.
- A critical literature review.
- Comparisons of existing systems and technology alternatives.
- Architectural diagrams and a user interface prototype.
- A working application prototype at a later stage.
- A classification and routing evaluation.
- Development history linked to project-management tasks.
- A final report describing results and limitations.

These are intended deliverables, not claims of completed work.

## Evaluation approach

Functional behaviour will be checked against requirement
acceptance criteria.

Classification quality will be evaluated on a separate labelled
test set using macro-F1 and per-category precision and recall.
Results will be compared with the keyword-based baseline.

Routing will be checked against expected assignments in the
configured service directory. Classification errors and routing-rule
errors will be examined separately.

Additional checks will cover role-based access and response times
under documented test conditions.

Dataset size, performance targets, and measurement conditions
will be specified before the final evaluation.

## Engineering complexity

The project requires the integration of a user interface,
application API, database, text-classification component,
and service-routing logic.

Key engineering challenges include defining consistent categories,
obtaining suitable labelled data, handling uncertain predictions,
maintaining access restrictions, and keeping request status
and assignment history consistent.

## Initial risks and responses

| Risk | Planned response |
|---|---|
| Limited access to labelled requests | Investigate available data and clearly document dataset limitations |
| Ambiguous or multi-topic requests | Define annotation rules and provide dispatcher review |
| Uneven category distribution | Inspect class balance and report per-category metrics |
| Incorrect service recommendations | Validate routing rules and require dispatcher confirmation |
| Excessive project scope | Prioritise the main submission-to-assignment workflow |
| Limited access to potential users | Arrange discussions early and distinguish assumptions from findings |

## Current stage

The project is in the initial analysis and planning stage.
The GitHub repository and YouTrack project have been created.

User validation, literature analysis, detailed requirements,
architecture, implementation, and evaluation remain to be completed.
Supervisor feedback will be recorded after an actual review.

## Project links

- [GitHub repository](https://github.com/QuickLR1/smart-zhkh)
- [YouTrack project](https://smarthzkh.youtrack.cloud/projects/SHS)
