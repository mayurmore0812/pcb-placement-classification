# Model and preprocessing

Notebook cell references are one-based positions including Markdown.

| Stage | Implementation | Cells |
|---|---|---|
| Input checks | RGB/orientation, binary labels, annotation correspondence, box bounds, exact file/pixel duplicate assertions | 6 |
| Partition | Seed 42; stratified image-level 160/34/34 | 11 |
| Crop | Annotation-centred 2:1 crop, 25% margin each side, boundary adjustment, Lanczos resize to 320×160 | 13 |
| Augmentation | Training-only flips, brightness and contrast variation | 13, 15 |
| Backbone | ImageNet MobileNetV2, global average pooling, fine-tune from block_14_expand, BatchNormalization frozen | 17 |
| Head | Dropout 0.30, sigmoid Dense(1), no classifier L2 | 17 |
| Optimizer/loss | Adam 0.00005; binary cross-entropy | 17 |
| Training | Batch 16; maximum 30 epochs; validation-loss early stopping, patience 6, restored best weights | 4, 21 |
| Prediction | Average original/horizontal/vertical/both-flip probabilities | 13, 17 |
| Threshold | Median of validation thresholds within 0.01 of maximum balanced accuracy | 21 |

The saved model has 2,259,265 total parameters and 1,512,001 trainable parameters. Annotation geometry is required for cropping. Random augmentation is disabled at inference and backbone calls use `training=False`; BatchNormalization statistics stay fixed.

The 24-configuration validation search varies learning rate, dropout, fine-tuning boundary and L2. It is represented by archived scores and a hard-coded plotting table; the public notebook trains the selected G19 configuration rather than rerunning the complete search.
