# PCB Component Placement Classification

> **Repository status:** README-only preview. The reviewed notebook, images, and model have not been published here yet.

## Project question

Can image classification help flag incorrect component placement on printed circuit boards for human inspection?

This academic prototype classifies cropped board images as acceptable or incorrect placement. It does not locate components automatically or replace a production inspection system for now.

## Approach

The reviewed experiment uses 228 labelled top-view images from six board designs. Annotation derived component regions are cropped and resized, then an ImageNet-pretrained MobileNetV2 is fine-tuned for binary classification. Model settings are compared on validation data, followed by an error review.

## Saved evaluation

The final notebook reports **0.853 balanced accuracy** on a **34-image test set**, with **15 of 17 incorrect placements** flagged. These are unseen images of board designs that also appear in training. Prior diagnostic analysis examined test data during development. Performance on entirely new board designs remains unknown on my research for now.

## Planned release

I plan to publish one canonical notebook, a checked environment file, selected permitted example images, validation results, and a short model card. The image dataset and historical artifacts will be reviewed for sharing rights and relevance before upload.

**Tools used:** Python, TensorFlow/Keras, MobileNetV2, Pillow, scikit-learn.

**Code, images, and trained models are not yet available in this repository.**
