# Industrial Defect Detection on Stay Cable Bridges

Applied Data Science Case Study – Computer Vision for Infrastructure Inspection

Domain: Bridge inspection (robot video → frames)

Task: Defect detection + 5-class categorization

Scale: ~1,500 annotated images (boundingboxes + polygons)

Models: YOLOv8, Mask R-CNN, EfficientNet

Constraints: NDA (no code/data/metrics)

##  Abstract

This project presents an applied computer vision solution for automated defect detection on stay cable bridges using deep learning. The objective was to support industrial bridge inspection processes by analyzing robot-captured video footage and detecting structural defects on steel cable joints and weld regions.
Approximately 1,500 annotated images were extracted from inspection robot video recordings and used to benchmark multiple deep learning architectures. The system was designed to assist pre-screening of inspection data in a safety-critical environment, with particular emphasis on recall and F1-score.
Due to confidentiality agreements, source code, dataset, and exact performance metrics cannot be publicly shared. This repository provides a technical overview of the methodology and engineering decisions.

## Verification & Public References

- Certificate of completion (VSL AG collaboration):  
  [View Certificate](./certificate_vsl_industrial_ai.pdf)

- Public Academy Blog Summary:  
  [Read Blog Post](https://nexademy.org/blog/data-science-capstone-projects-batch-33)

##  1. Problem Definition

Bridge inspections traditionally rely on manual visual inspection, which is time-intensive and potentially hazardous.
This project aimed to:
Detect structural defects on steel stay cable bridges
Identify welding joint defects, surface cracks, dents, and related anomalies
Classify defects into five defined categories
Support engineers through automated pre-screening of inspection footage
Full automation was not within project scope. The goal was to provide trained models and technical documentation for potential integration into inspection workflows.

##  2. Data Description

~1,500 images extracted from robot-recorded inspection video
Outdoor industrial environment
Mixed lighting conditions (day/night variability)
Images captured along continuous cable traversal
Multi-class defect labeling (5 classes)
Annotations included bounding boxes and polygon masks
Class imbalance addressed through targeted augmentation
Dataset split:
70% Training
20% Validation
10% Test

##  3. Methodology
### 3.1 Preprocessing

Frame extraction from inspection video
Image resizing for training consistency
Geometric augmentation:
Random scaling
Controlled rotations
Cropping
Photometric augmentation:
Brightness adjustment
Contrast variation
Gaussian blur
Augmentation strategy focused on robustness against lighting variability and small-object detection challenges.

### 3.2 Model Architectures Benchmarked

The following architectures were evaluated using pretrained weights (COCO):
YOLOv8 (Multi-class object detection)
Mask R-CNN (Segmentation-based detection)
EfficientNet (Binary anomaly classification)
EfficientNet was trained using transfer learning with progressive layer unfreezing to improve performance on domain-specific data.
Training conducted on GPU environment (Google Colab), batch size = 32.

##  4. Evaluation Strategy

Given the safety-critical context, evaluation prioritized:
Recall (minimizing missed defects)
F1-score (precision-recall balance)
Confusion matrix analysis
False negatives were considered more critical than false positives due to potential safety implications.
Models were compared based on:
Class-wise detection behavior
Sensitivity to small defects
Stability across lighting conditions
Overfitting behavior on validation set

##  5. Observations & Model Behavior

Key observations:
YOLO demonstrated strong performance for certain defect classes with efficient detection speed.
Mask R-CNN provided improved granularity in segmentation-based scenarios.
EfficientNet performed effectively in binary anomaly detection tasks.
Progressive layer unfreezing improved transfer learning results.

##  6. Failure Case Analysis

Observed challenges included:
Lighting variability between bridges
Annotation inconsistencies
Small defect regions under low contrast
Domain shift between inspection sites
These factors significantly influenced generalization performance.

##  7. Proposed Two-Stage Architecture (Outlook)

A modular two-stage pipeline was proposed:
Stage 1:
Binary anomaly detection (EfficientNet)
Stage 2:
Multi-class defect detection (YOLO or Mask R-CNN)
This architecture was suggested to potentially improve precision and reduce computational overhead in real-world deployment scenarios.

##  8. Deployment Scope

Trained model weights and documentation were delivered to the client.
System integration, automation, and deployment were outside project scope.

##  9. Key Learnings

Transfer learning significantly improved performance with limited dataset size.
Annotation consistency strongly impacts model stability.
Recall optimization is essential in safety-critical inspection systems.
Lighting variability is a major challenge in outdoor industrial computer vision tasks.

##  10. Confidentiality Notice

This project was conducted in collaboration with VSL AG.
Due to confidentiality agreements:
Source code
Dataset
Internal performance metrics
cannot be publicly disclosed.

This repository serves as a technical case study overview.
