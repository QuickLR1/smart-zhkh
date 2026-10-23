# Preliminary User Validation

## Method

Three participants completed a Russian-language online questionnaire.
The supplied response export contains entries dated 24 October 2026.

All three selected consent to the use of anonymised responses in
the academic report. The student confirmed that the responses were
provided by real participants.

Participants are identified below as P1, P2, and P3.
The English summaries are paraphrases of their Russian responses,
not verbatim quotations.

The recruitment procedure and participant demographics were not
recorded in the supplied export. This is a small exploratory sample,
not a representative survey of residents.

## Response summary

| Participant | Reported experience | Difficulty | Suggested improvement |
|---|---|---|---|
| P1 | Contacted telephone support about an unexpectedly large bill | Difficulty identifying the right contact, a long wait, and uncertainty about whether the issue was being handled | Digitise the process |
| P2 | Visited a main office about a proposed alteration involving a staircase landing or attic space; the exact circumstances require clarification | Had to return several days later and learned the outcome during a visit | Provide an intuitive system |
| P3 | Visited an office about maintenance of the surrounding residential area | Travel to a distant office, repeated reminders, and concerns about response times; requested a written answer | Enable digital submission and status tracking |

P3 left the question about the greatest inconvenience and the final
optional comment blank. These missing answers were not filled in
or treated as additional evidence.

## Findings

### Remote submission

P2 and P3 described office visits, including a repeat visit in P2's case.
All three expressed interest in a digital or more intuitive process.

This supports investigating remote submission as a user need.
It does not establish that no digital channel already exists.

### Visibility of progress

P1 explicitly reported not knowing whether the issue was being handled.
P2 reported learning the outcome during an office visit.
P3 requested a written response and suggested status tracking.

These accounts support providing visible request statuses and
clear communication of processing outcomes.

### Identifying the responsible organisation

P1 and P3 selected that they experienced difficulties identifying
where to direct their request. P2 selected that this was easy.

The mixed responses suggest that routing assistance may be useful,
but the questionnaire does not establish the causes of the difficulty
or prove that automated text classification is necessary.

## Relationship to requirements

| Finding | Relevant requirement | Interpretation |
|---|---|---|
| Interest in digital submission and avoiding office visits | FR-02: request submission | Supports investigating a remote submission workflow |
| Uncertainty about progress and outcomes | FR-03: view own requests and statuses; FR-08: status updates | Supports making processing progress visible |
| Difficulty identifying where to direct a request in two responses | FR-05: service recommendation; FR-06: dispatcher confirmation | Provides preliminary motivation for routing assistance, subject to staff validation |
| Repeat contacts and the need to understand what happened | FR-09: change history | Motivates a traceable record as a design response; participants did not explicitly request an audit log |

These links describe how findings inform design.
They do not mean that the implementation has passed acceptance tests.

## Scope implications

P1's billing case is outside the prototype's core scope, which excludes
utility billing and payment processing. It informs general communication
needs but does not justify adding billing functionality.

P2's case may involve property alteration or approval rather than a
routine maintenance request. Clarification is required before assigning
it to a supported category.

P3's surrounding-area maintenance case is relevant to communal services,
but responsibility and category depend on the specific problem.

The sample therefore supports general workflow needs more strongly
than the exact proposed classification categories.

## Limitations

- The sample contains only three responses.
- The responses describe resident experiences, not dispatcher workflows.
- The supplied file records questionnaires, not follow-up discussions.
- The accounts were not independently checked against service records.
- No processing-time measurements were collected.
- No prototype usability sessions are documented by these responses.
- No trained classifier or routing algorithm was evaluated.
- The findings cannot be generalised to all residents or organisations.

## Follow-up discussions

Short follow-up discussions are planned to clarify:

- P1: what progress information would have been useful after the call.
- P2: the exact nature of the issue and why a second visit was necessary.
- P3: which organisation handled the request and what status information
  would have reduced the need for reminders.

Actual discussion dates and answers will be recorded after the
conversations take place.

A separate discussion with a dispatcher or service representative
is desirable to validate categories, routing rules, and responsibility.

## Source

Anonymised summaries are based on the supplied questionnaire export:
"Новая форма (Ответы).xlsx", containing three response records.

The original export should be retained as supporting material.
