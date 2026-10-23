# Existing System Comparison

## Purpose

This comparison examines three systems relevant to citizen request
processing: iKOMEK109, FixMyStreet, and SeeClickFix 311 CRM.

The objective is to identify established approaches and inform the
design of Smart Housing Services. It is not to claim that existing
systems are ineffective or that the proposed prototype is superior.

## Method and evidence limits

The comparison uses official government, product, and developer sources
reviewed on 23 October 2026.

It is a documentary comparison, not a hands-on evaluation of administrator
interfaces or a performance benchmark.

"Not established" means that the reviewed sources do not provide enough
evidence. It does not mean that a capability is absent.

Service configurations may vary by deployment. Published descriptions
do not prove that every submission channel is currently operational.

## Selected systems

### iKOMEK109

iKOMEK109 is Astana's municipal contact centre for city services.
The official description explains that requests receive registration
numbers and are forwarded to responsible institutions or utility services.
It also describes several submission channels. [S1]

This is a relevant local reference for the proposed housing and communal
services workflow.

### FixMyStreet

FixMyStreet is an open-source platform for reporting local problems.
Its repository describes routing based on problem location and type,
with delivery by email or a web service such as Open311. [S3]

It is relevant as an inspectable reference for location-based routing
and integration with responsible authorities.

### SeeClickFix 311 CRM

SeeClickFix 311 CRM is a CivicPlus platform for resident requests and
government service workflows. Official materials describe multiple
submission channels and tools for tracking and managing requests. [S5, S6]

It is relevant as a reference for organised request processing and
communication between residents and government staff.

## Comparison matrix

| Criterion | iKOMEK109 | FixMyStreet | SeeClickFix 311 CRM |
|---|---|---|---|
| 1. Primary purpose | City-service enquiries and requests in Astana. [S1] | Reporting local problems to responsible authorities. [S3] | Resident service requests and government workflow management. [S5] |
| 2. Submission channels | Official description lists phone, website, Telegram, email, and mobile app; current availability of every channel was not tested. [S1] | Map-based website; official integration documentation also refers to an app. [S3, S4] | Web portal, mobile app, chatbot, and phone are described. [S5] |
| 3. Location and category handling | Broad city-service coverage; detailed category and address-processing logic is not established. [S1] | Uses problem location and type to identify the authority. [S3] | Reporting API retrieves available request types by location. [S7] |
| 4. Routing to responsible organisations | Registered requests are sent to responsible institutions or utility services; internal routing algorithm is not established. [S1] | Sends to the appropriate authority using location and type. [S3] | API request types can be associated with organisations; some community types have no organisation. [S7] |
| 5. Progress and status communication | Status tracking is described in an official 2023 overview; current interface details were not tested. [S2] | Reports support updates; Open311 integration can return status changes. [S3, S4] | Official materials describe progress tracking and updates. [S6] |
| 6. Integration evidence | Coordination with municipal and utility services is documented; a public developer API was not established. [S1] | Email and Open311 integration are documented. [S3, S4] | A reporting API and API-driven integrations are documented. [S5, S7] |
| 7. Source-code availability for study | A public source-code repository was not established by the reviewed sources. | Public source-code repository is available. [S3] | A public source-code repository was not established by the reviewed sources. |
| 8. Evidence for evaluated free-text classification | A reproducible classifier evaluation was not established by the reviewed sources. | Reviewed documentation explains location/type routing, but does not establish an evaluated free-text classifier. | Reviewed sources do not establish a reproducible evaluation of a classifier on the diploma's intended dataset and categories. |

## Implications for the proposed system

### Separate classification from routing

FixMyStreet demonstrates that identifying the responsible authority can
depend on both location and problem type. [S3]

Design implication:
The diploma should separate category prediction from service-routing
rules. A correct category alone does not guarantee a correct assignment.

### Make processing visible

The reviewed systems document progress communication or report updates.
[S2, S3, S6]

Design implication:
The prototype should expose a clear status sequence and retain a history
of assignments and status changes.

### Treat integration as a separate engineering task

FixMyStreet documents integration through Open311, while SeeClickFix
provides a reporting API. [S4, S7]

Design implication:
Real municipal integration would require agreed interfaces, data mapping,
access, and operational responsibilities. The diploma prototype therefore
uses a demonstration service directory.

### Retain human review

The comparison does not prove that an automated classifier can reliably
handle the project's categories and input data.

Design implication:
The proposed system will require dispatcher confirmation and provide
manual handling of uncertain classifications or unmatched services.
This is a project design decision, not a claim that other systems lack
human review.

## Project justification

Existing systems already support citizen reporting and service workflows.
The value of this diploma is therefore not the invention of request
submission or status tracking.

The engineering objective is to build a limited, inspectable prototype
that combines:

- Text-category recommendations.
- Explicit service-routing rules.
- Dispatcher confirmation and correction.
- A traceable request lifecycle.
- Reproducible comparison with a keyword-based baseline.

The prototype is intended for investigation and demonstration.
It is not presented as a replacement for iKOMEK109 or as a production
competitor to the reviewed platforms.

The practical need and final requirements still require validation
with potential users. A documentary comparison does not replace
the required user discussions.

## Limitations and further work

- Administrator workflows were not tested directly.
- No comparable measurements of accuracy, latency, or operating cost
  were obtained.
- No claim is made that any reviewed system lacks AI features.
- Current availability of all iKOMEK109 channels was not independently
  confirmed.
- The proposed prototype has not demonstrated better performance than
  any reviewed system.
- Public documentation may omit capabilities available in specific
  deployments or commercial configurations.

## Sources

All sources below were reviewed on 23 October 2026.

[S1] Akimat of Astana. About iKOMEK109.
Published 19 October 2022; page states an update on 3 June 2026.
https://www.gov.kz/org/astana/press/article/details/99399?lang=ru

[S2] Akimat of Astana. iKOMEK109 received 1.5 million requests
since the beginning of the year. Overview concerning 2023.
https://www.gov.kz/memleket/entities/astana/press/news/details/615020?lang=ru

[S3] mySociety. FixMyStreet source repository and project description.
https://github.com/mysociety/fixmystreet

[S4] mySociety. FixMyStreet Open311 integration.
https://www.fixmystreet.com/open311

[S5] CivicPlus. SeeClickFix 311 CRM product overview.
https://www.civicplus.com/seeclickfix-311-crm/

[S6] CivicPlus. SeeClickFix 311 CRM fact sheet overview.
https://www.civicplus.com/fact-sheets/crm/simplify-resident-request-management/

[S7] SeeClickFix. API v2: Reporting an Issue.
https://dev.seeclickfix.com/v2/issues/reporting/
