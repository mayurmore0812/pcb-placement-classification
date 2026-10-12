# Evaluation and limitations

## Saved results

| Split | Images | Good | Incorrect | Board designs |
|---|---:|---:|---:|---|
| Training | 160 | 79 | 81 | CS1–CS6 |
| Validation | 34 | 16 | 18 | CS1–CS6 |
| Test | 34 | 17 | 17 | CS1–CS6 |

Saved best epoch is 3, threshold 0.50. Validation balanced accuracy/F1: 0.7639/0.7778. Test balanced accuracy/F1: 0.8529/0.8571. Confusion matrix rows actual Good/Incorrect and columns predicted Good/Incorrect: `[[14,3],[2,15]]`. Balanced accuracy equals `(14/17 + 15/17)/2`; Incorrect F1 equals `2×15/(2×15 + 3 + 2)`. These arithmetic checks agree with the saved values, but are not an independent reproduction of predictions or training.

Notebook cell 23 saves 2,000-replicate stratified bootstrap intervals: balanced accuracy 0.7059–0.9706; F1 0.7273–0.9697. Cell 25 lists five errors, with maximum distance 0.177 from threshold. Saved outputs, plots and error tables are historical evidence; no fresh training run was performed.

## Configuration selection and historical test exposure

[Validation ranking](results/validation-grid.csv) contains 24 configurations. G19 and G22 tie on validation balanced accuracy/F1; G19 uses no classifier L2. The selected notebook and archived ranking describe validation as the selection basis.

[Historical test diagnostics](results/historical-test-diagnostics.csv) contain test scores for ten configurations, including G19. They establish that the same project test partition was inspected during experimentation. Therefore a project-wide claim that this test was never inspected or used only once is unsupported, even though the current training/threshold code uses validation.

An archived status note reports a separate formal-refit score of 0.8235 balanced accuracy and 0.8333 F1. The current canonical notebook saves 0.8529 and 0.8571, matching the G19 historical diagnostic counts. These are distinct saved records; exact run-to-run cause is not established. The canonical values are labelled as that notebook's saved result, not as fresh confirmation.

## Evaluation boundaries

- Every board design appears in all partitions. Results concern new images of known designs, not new board designs or factories.
- The test has only 34 images. Bootstrap intervals cover fixed-test resampling, not all training-seed, selection or board-design uncertainty.
- Annotation-based cropping assumes localization is supplied; there is no detector in this pipeline.
- No calibrated probability evaluation, factory throughput, latency benchmark, financial impact or field deployment is shown.
- Dataset class balance is nearly even; it does not mimic an established production defect prevalence.
- Exact duplicates are checked in code, but physical-component or near-duplicate grouping across image splits is not independently established here.

The saved figures and tables support a bounded academic classification experiment, not autonomous manufacturing quality assurance.
