# Dataset and setup

## Sources

[SolDef_AI on Kaggle](https://www.kaggle.com/datasets/mauriziocalabrese/soldef-ai-pcb-dataset-for-defect-detection), by Maurizio Calabrese; [dataset paper](https://www.mdpi.com/2504-4494/8/3/117), Fontana et al. (2024), DOI 10.3390/jmmp8030117. The paper describes a broader dataset; this classifier uses only 228 labelled V1 images, not the full collection or the paper's Mask R-CNN pipeline.

Public Kaggle metadata checked 13 October 2026 lists version 1, last updated 5 March 2024, and licence `GPL 3`. The exact historical local download date is unknown. The archive has 2,545 members, including 428 JSON annotations across views. The selected V1 metadata independently yields 112 Good and 116 Incorrect images from CS1–CS6, with annotation dimensions 2560×1440.

## Required archive layout

The notebook requires `archive.zip` beside it and starts with `DATA = Path('archive.zip')`. Do not place an extra wrapper directory inside the archive. Expected member patterns include:

```text
SolDef_AI/Dataset/CS1/R0805/V1/Setup1/<image>.jpg
SolDef_AI/Labeled/<image>.json
SolDef_AI/Labeled/<image>.jpg
```

Raw basenames must identify one dataset image. Annotation JSON must contain one `good` or `no_good` shape, polygon `points`, and `imageWidth`/`imageHeight`. The labelled JPG must match the raw JPG bytes. The loader selects `V1` based on raw image path and asserts 228 selected samples. Changing archive format, labels or contents can invalidate these assumptions.

Independent metadata checks counted selected annotations and labels; all image/pixel duplicate, orientation and geometry assertions were not rerun during packaging. Dataset files are not distributed. Saved figure examples contain dataset photographs with attribution in the third-party notices.

## Environment and behavior

Saved metadata: Python 3.12.10. Saved import output: TensorFlow 2.21.0, Keras 3.14.0. Original package list has no pins. `requirements.txt` lists direct dependencies and JupyterLab. Installation and full training in a fresh environment are untested; no tested compatibility lockfile is provided.

The notebook reads archive contents in memory rather than extracting them. TensorFlow may download/cache ImageNet weights and use available accelerators. Running cells 17 and 21 builds/trains models; running all cells is not a read-only operation. Saving the notebook or exporting reports writes files. The archive is 1,178,779,597 bytes; RAM and runtime were not benchmarked. The model remains in memory; there is no checkpoint-export code.

## Labels and units

Good = 0; Incorrect (`no_good`) = 1. Labels and polygons come from the source annotations, not newly created project labels. Board counts are in [board-class-counts.csv](results/board-class-counts.csv). The task concerns component placement; it does not claim detection of every solder-joint defect, PCB trace defect or unannotated component.
