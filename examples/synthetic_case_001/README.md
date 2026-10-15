# Synthetic case 001

This folder contains the first repetition of the simulated example in Figure 4. It compares complementary questioning with equal questioning, using the requested parser alias `gpt-6-sol` and reasoning effort `xhigh`. The model parses a complete prerecorded conversation. The questions and answers are fixed before parsing.

The customer was selected after scoring because its complementary five-level loss, averaged over two repetitions, was the lowest among twelve simulated customers. This selected example illustrates the pipeline and does not establish an average policy advantage. The dialogue is simulated and contains no real customer personal data.

| File | Contents |
| --- | --- |
| `complementary.request.zh.md` | Complete original Chinese request for complementary questioning, preserved byte for byte. |
| `equal.request.zh.md` | Complete original Chinese request for equal questioning, preserved byte for byte. |
| `*.request.en.md` | English translations for reading. These were not submitted to the model. Literal vocabulary aliases are retained. |
| `complementary.response.json` | Original parser response for complementary questioning, preserved byte for byte. |
| `equal.response.json` | Original parser response for equal questioning, preserved byte for byte. |
| `example.json` | Parser input description, full-precision directions and signals, parsed values, scoring rules, and final numerical outputs. |

Read either Chinese request first, or its English translation. Compare the corresponding JSON response with the opening and the five answers. Each response quotes the evidence supporting its parsed values. The opening yields `mu0 = [-1, 0, 1, 0, 0]`, color `burgundy`, and fabric `chiffon_lace` under both policies.

Then read `example.json`. Its `parser_visible` section describes the model input; the hidden ideal appears only in `evaluation`. The simulator's raw signals and shared noise are separate from the actual requests. Each policy lists all five exchanges and the final posterior, covariance, continuous designs, projected designs, categories, and losses under both response scales.

The parser actually received fine-scale answers, with one step equal to 0.25 units. The five-level answers were subsequently computed from stored raw signals. They were not the answers supplied to the model. The resulting values are:

| Scoring scale | Complementary minimum loss | Equal minimum loss |
| --- | ---: | ---: |
| Fine scale | 0.2500 | 0.6944 |
| Five levels | 0.0000 | 0.4444 |

Projection treats attribute codes within $10^{-9}$ of the minimum absolute distance as tied and chooses the lower code. The original hidden ideal stores the A-line coordinate as `0.3333333333`; the corresponding grid code is $1/3$. Their tiny difference produces the stored complementary five-level loss of approximately $1.11 \times 10^{-21}$, shown as zero in the table and paper. Full-precision values are retained in `example.json`.

The trial IDs in the original requests and responses identify simulated experimental conditions. They do not identify real people. This release provides the recorded example and its numerical outputs; it contains no policy search or optimization implementation.
