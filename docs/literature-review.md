# Literature Review

## 1. Purpose and scope

This review examines research and technical sources relevant to
classifying citizen requests and recommending responsible services.

It addresses four questions:

1. Which text-classification approaches are suitable for the prototype?
2. How should limited and multilingual data affect model selection?
3. How should uncertain predictions and evaluation be handled?
4. What existing civic-reporting workflows inform the architecture?

The review includes eight scientific works and four official technical
or institutional sources. Six scientific works are from 2022–2025.
Two works from 2017 are retained for their relevance to selective
prediction and bias in citizen-reporting data.

This is a targeted initial review, not a systematic review or an
exhaustive account of all relevant research. It draws on the cited
publication records, abstracts, and accessible official descriptions.
It does not independently reproduce the reported experiments.

Preprints and technical research reports are identified separately
from journal and conference publications.

## 2. Text classification approaches

Li et al. [R1] organise text-classification research across traditional
and deep-learning approaches, including feature extraction, models,
datasets, and evaluation measures. This provides a framework for
comparing simple methods with more complex neural alternatives.

For this project, the practical starting point is a keyword baseline
and a supervised TF-IDF classifier. This is an engineering choice
based on the intended scope, not a conclusion that traditional
methods are universally better.

The scikit-learn text-processing examples [R9] provide implementation
references for sparse text representations and classification.
They support reproducible experimentation but do not establish
performance on housing-service requests.

Warner et al. [R6] introduce ModernBERT, an updated encoder architecture
evaluated on classification and retrieval tasks. The work demonstrates
that modern encoders are relevant alternatives to consider.

However, adopting such an encoder would require checking language
coverage, hardware needs, and task-specific performance. Its published
results do not establish suitability for Russian or Kazakh utility
requests. It is therefore a possible later experiment, not an initial
implementation requirement.

## 3. Limited labelled data and multilingual processing

Tunstall et al. [R2] propose SetFit, which adapts sentence transformers
using labelled text pairs and trains a classification head.
This is relevant if the project obtains a limited labelled dataset.

The method does not remove the need for representative examples,
consistent labels, and separate evaluation data. A small number of
examples that works on one benchmark is not a guaranteed sufficient
dataset for this project.

Wang et al. [R4] describe multilingual E5 embedding models, including
different model sizes. Their work motivates considering multilingual
representations if more than one input language is required.

Chen et al. [R5] describe M3-Embedding, supporting multilingual
retrieval and different representation strategies. Retrieval evidence
can motivate investigation of semantic representations, but it does
not directly demonstrate classification or correct service assignment.

Neither source proves performance on this project's categories.
Russian and Kazakh support would need separate validation using
appropriate examples. Language coverage must not be inferred solely
from a model being described as multilingual.

## 4. Evaluation and uncertain predictions

Muennighoff et al. [R3] introduce MTEB to evaluate embeddings across
multiple tasks and datasets. Their finding that no method dominates
all tasks supports task-specific evaluation rather than selecting
a model solely from a general leaderboard.

The project will therefore compare candidate methods on the same
held-out request dataset. It will report macro-F1, per-category
precision and recall, a confusion matrix, and representative errors.

Geifman and El-Yaniv [R7] investigate selective classification:
a predictor can decline to answer some inputs to trade coverage
for lower error on accepted predictions.

This motivates a manual-review path for uncertain requests.
However, their experiments concern image classification with neural
networks. Their numerical guarantees cannot be transferred directly
to the proposed text classifier.

The project will select any review threshold on validation data
and report both prediction quality and the proportion of requests
referred to a dispatcher. Rejected examples will not be silently
removed from the main evaluation.

## 5. Citizen-reporting data and operational workflows

Kontokosta, Hong, and Korsberg [R8] examine differences in the
propensity to report problems through New York City's 311 system,
including heating and hot-water issues.

The work highlights that reporting behaviour may vary with social,
demographic, and access-related factors. Request counts should
therefore not be treated as a complete measurement of actual need.

For this project, dataset provenance and representation limitations
must be documented. Findings from New York are relevant as a caution
but do not establish the same patterns in Astana.

The official iKOMEK109 description [R12] documents registration and
forwarding of requests to responsible institutions and utility services.
It grounds the project in a relevant local service workflow.

It does not establish an unresolved operational problem or quantify
manual-processing delays. Those claims require user discussions or
other direct evidence.

The FixMyStreet repository [R11] describes routing based on location
and problem type, with delivery through email or web services.
This supports separating category prediction from service selection.

FastAPI documentation [R10] describes validation and API documentation
facilities relevant to implementing a documented request-processing
interface. These facilities do not automatically implement secure
ownership checks or correct routing rules.

## 6. Structured source analysis

The limitations below describe limits of applying each source to this
project; they are not necessarily limitations claimed by its authors.

| ID | Source and type | Main contribution | Limitation for this project | Project implication |
|---|---|---|---|---|
| R1 | Li et al., 2022; journal survey | Organises traditional and deep text-classification methods and evaluation approaches | Broad survey, not a utility-request experiment | Compare method families and justify the initial baseline |
| R2 | Tunstall et al., 2022; research preprint | SetFit uses sentence-transformer adaptation for few-shot classification | Reported benchmark results do not establish the required local dataset size | Consider a later few-shot experiment if labelled data is limited |
| R3 | Muennighoff et al., 2023; EACL paper | Evaluates embeddings across multiple task types; no universal winner | General benchmarks differ from local requests | Evaluate models on the actual target categories |
| R4 | Wang et al., 2024; technical research report | Describes multilingual E5 representations and model-size alternatives | Multilingual training does not guarantee per-language domain performance | Test each intended input language separately |
| R5 | Chen et al., first submitted 2024, revised 2025; research preprint | M3-Embedding combines multilingual and multiple retrieval representations | Retrieval results are not request-classification or routing results | Treat embeddings as candidate features, not complete routing solutions |
| R6 | Warner et al., 2025; ACL paper | ModernBERT updates encoder architecture for classification and retrieval | Local language coverage and resource fit remain unverified | Consider neural encoders only after baseline and feasibility checks |
| R7 | Geifman and El-Yaniv, 2017; NeurIPS paper | Studies selective classification and risk–coverage trade-offs | Image-domain results do not transfer directly to this text task | Include manual review and report coverage alongside quality |
| R8 | Kontokosta et al., 2017; research preprint, presented at Data For Good Exchange | Investigates unequal reporting propensity in 311 data | Different city and institutional context | Document sampling limitations and avoid equating complaint volume with need |
| R9 | scikit-learn; official documentation | Provides text-processing and classification examples | Implementation guidance, not local empirical evidence | Build a reproducible feature and classification pipeline |
| R10 | FastAPI; official documentation | Describes request validation and interactive API documentation | Framework facilities do not establish application correctness | Document and test request contracts and authorisation separately |
| R11 | mySociety FixMyStreet; official repository | Documents civic reporting and location/type-based routing | Existing platform does not validate this prototype's model | Separate text classification from service-directory rules |
| R12 | Akimat of Astana; official iKOMEK109 description | Documents local registration and forwarding of requests | Does not prove current user difficulties or classifier performance | Use as contextual evidence and validate problems through discussions |

## 7. Synthesis and proposed design

The reviewed evidence supports a staged investigation.

First, define categories and annotation rules before selecting a
complex model. Document where examples come from and which users
or problem types may be missing.

Second, implement a keyword baseline and evaluate a TF-IDF classifier.
More advanced methods remain possible extensions if data, resources,
and measured results justify them.

Third, separate classification from routing. A text category is an
input to service selection, not proof that a particular organisation
is responsible for an address.

Fourth, require dispatcher confirmation and support manual handling
of uncertain or unmatched requests. Record the original recommendation
and the final decision for later analysis.

Finally, evaluate the complete workflow as well as its components.
A classifier can perform well while routing rules or access controls
remain incorrect.

These are proposed design decisions informed by the review.
They are not experimentally validated results of this diploma.

## 8. Remaining evidence gaps

- A suitable local labelled dataset has not yet been established.
- User discussions are still needed to validate the problem and workflow.
- No model has been trained or compared on project data.
- Supported input languages remain to be confirmed.
- Current prototype behaviour is rule-based and client-side only.
- The reviewed materials do not establish a novel algorithm or superiority
  over existing municipal systems.
- Additional recent domain-specific research should be incorporated
  as the dataset and final scope become clearer.

## 9. References

Sources reviewed on 24 October 2026.
Online technical documentation may change; implementation versions
will be recorded separately.

### Scientific works

[R1] Li, Q., Peng, H., Li, J., Xia, C., Yang, R., Sun, L.,
Yu, P. S., and He, L. (2022).
A Survey on Text Classification: From Traditional to Deep Learning.
ACM Transactions on Intelligent Systems and Technology, 13(2), Article 31.
https://doi.org/10.1145/3495162
Publication record:
https://eprints.whiterose.ac.uk/id/eprint/186633/

[R2] Tunstall, L., Reimers, N., Jo, U. E. S., Bates, L.,
Korat, D., Wasserblat, M., and Pereg, O. (2022).
Efficient Few-Shot Learning Without Prompts.
Research preprint, arXiv:2209.11055.
https://arxiv.org/abs/2209.11055

[R3] Muennighoff, N., Tazi, N., Magne, L., and Reimers, N. (2023).
MTEB: Massive Text Embedding Benchmark.
Proceedings of EACL, pp. 2014–2037.
https://aclanthology.org/2023.eacl-main.148/

[R4] Wang, L., Yang, N., Huang, X., Yang, L., Majumder, R.,
and Wei, F. (2024).
Multilingual E5 Text Embeddings: A Technical Report.
Technical research report, arXiv:2402.05672.
https://arxiv.org/abs/2402.05672

[R5] Chen, J., Xiao, S., Zhang, P., Luo, K., Lian, D.,
and Liu, Z. (2024; revised 2025).
M3-Embedding: Multi-Linguality, Multi-Functionality,
Multi-Granularity Text Embeddings Through Self-Knowledge Distillation.
Research preprint, arXiv:2402.03216, version 5.
https://arxiv.org/abs/2402.03216v5

[R6] Warner, B., et al. (2025).
Smarter, Better, Faster, Longer: A Modern Bidirectional Encoder
for Fast, Memory Efficient, and Long Context Finetuning and Inference.
Proceedings of ACL, Volume 1: Long Papers, pp. 2526–2547.
https://aclanthology.org/2025.acl-long.127/

[R7] Geifman, Y., and El-Yaniv, R. (2017).
Selective Classification for Deep Neural Networks.
Advances in Neural Information Processing Systems 30.
https://proceedings.neurips.cc/paper/2017/hash/4a8423d5e91fda00bb7e46540e2b0cf1-Abstract.html

[R8] Kontokosta, C., Hong, B., and Korsberg, K. (2017).
Equity in 311 Reporting: Understanding Socio-Spatial Differentials
in the Propensity to Complain.
Research preprint, arXiv:1710.02452;
presented at Data For Good Exchange 2017.
https://arxiv.org/abs/1710.02452

### Technical and institutional sources

[R9] scikit-learn. Working with text documents.
Official documentation.
https://scikit-learn.org/stable/auto_examples/text/index.html

[R10] FastAPI. Features.
Official documentation.
https://fastapi.tiangolo.com/features/

[R11] mySociety. FixMyStreet.
Official source repository and project description.
https://github.com/mysociety/fixmystreet

[R12] Akimat of Astana. About iKOMEK109.
Published 19 October 2022; page states an update on 3 June 2026.
https://www.gov.kz/org/astana/press/article/details/99399?lang=ru
