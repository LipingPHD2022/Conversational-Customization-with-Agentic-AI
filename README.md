# Conversational Customization: Parsing Prompts and a Synthetic Example

Companion materials for the research manuscript **Conversational Customization with Agentic AI: Coordinating Preference Learning and Design Recommendations**, by Yugang Yu and Liping Yang.

This repository documents how a language model converts a prerecorded garment customization conversation into structured preference inputs. It provides the actual parsing instructions, an output schema, attribute codes, and one complete synthetic customer example under complementary and equal questioning.

## Repository contents

| Location | Contents |
| --- | --- |
| [`prompts/`](prompts/) | Chinese parsing prompt template and its English translation. |
| [`schemas/`](schemas/) | JSON Schema for the parsed preferences, fixed requirements, answers, and supporting quotations. |
| [`protocol/`](protocol/) | Ordered attribute codes, Chinese and English labels, fixed color and fabric vocabulary, and answer conventions. |
| [`examples/synthetic_case_001/`](examples/synthetic_case_001/) | Actual requests and archived responses for one synthetic example, English translations, and numerical reference results. |
| [`CITATION.cff`](CITATION.cff) | Citation metadata for these materials and the associated manuscript. |

## Parsing task

The model receives the customer's opening description and all five prerecorded question–answer exchanges together. It extracts:

- The initial preference vector, in the order skirt length, silhouette, neckline openness, train length, and sleeve length.
- Fixed color and fabric requirements.
- Five numerical answer values, with a preference for B positive and a preference for A negative; each stated step represents 0.25 units.
- Quotations supporting the extracted values, taken from the opening or the corresponding answer.

An attribute absent from the opening receives an initial value of zero. An unreadable answer receives `null` and an explanation in its evidence field. The schema describes the response format; the evaluation protocol separately checks evidence and assigns a failure loss when required fields are missing or invalid.

Question directions are fixed before parsing. A deterministic controller performs posterior updates and computes the design recommendations. The historical requests use the Chinese instructions and fine-scale replies. The English files are translations for readers. The requested model alias for the included responses is GPT-6 Sol, with reasoning effort set to `xhigh`; the underlying model snapshot is unavailable.

## Using the materials

1. Read the attribute codes and fixed vocabulary in `protocol/`.
2. Fill the prompt template with an opening and five exchanges. Keep evaluation targets and response noise outside the model input.
3. Read the response schema and inspect the original request–response pairs in the example directory.
4. Compare the parsed values with the example's reference results. The example README identifies the fields visible to the parser and the fields used only for evaluation.

The original requests and responses retain their synthetic experiment identifiers. These identifiers connect the paired files and carry no real customer identity. Folder names distinguish complementary questioning from equal questioning.

## Interpreting the example

The example corresponds to Figure 4 of the manuscript. It was selected after evaluation because it has the lowest repeat-averaged complementary five-level loss among twelve fixed synthetic customers. This selection supports an illustration of the mechanism; it provides no estimate of average policy performance.

The model actually parsed fine-scale replies. Five-level replies were subsequently computed from the simulated raw signals by a fixed encoder. The example keeps these two response scales separate and provides reference results for both. Under five-level evaluation, the best complementary design has coded loss 0, and the best equal-questioning design has coded loss approximately 0.44. Fine-scale evaluation gives approximately 0.25 and 0.69, respectively.

Reference results follow the manuscript's uniform projection rule: attribute levels within $10^{-9}$ of the minimum distance qualify as tied, and the lowest numerical code is selected. Garment attributes and target preferences are specified for simulation. The example contains no observed customer conversation or customer outcome.

## Scope

This release covers the parsing interface and one synthetic example. Reproducing the manuscript's population comparisons, candidate selection, optimization searches, and robustness experiments requires additional computational materials. The release contains no model credentials, commercial system interfaces, catalogue images, or original partner dataset.

## Citation and contact

Please cite the associated manuscript when discussing or reusing these materials:

> Yu, Y., & Yang, L. *Conversational Customization with Agentic AI: Coordinating Preference Learning and Design Recommendations*. Research manuscript.

GitHub's **Cite this repository** feature provides the repository citation from `CITATION.cff`.

Corresponding author: **Liping Yang**, School of Management, University of Science and Technology of China. Email: [lipingphd@mail.ustc.edu.cn](mailto:lipingphd@mail.ustc.edu.cn).
