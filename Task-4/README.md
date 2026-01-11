Task-4: CNNs, Transfer Learning, and Fine-Tuning Experiments
Overview

This task investigates convolutional neural networks and transfer learning across three image classification datasets of increasing complexity:

    Fashion-MNIST – Custom CNN from scratch

    DeepWeeds – Transfer learning with progressive fine-tuning

    FER2013 – Transfer learning for facial expression recognition

The experiments emphasize architecture design, data augmentation, fine-tuning strategies, and rigorous metric reporting, with conclusions drawn from controlled comparisons.



1. Fashion-MNIST — Custom CNN from Scratch
Dataset

    28×28 grayscale images

    10 clothing categories

    Balanced dataset

    Model Architecture

A custom CNN designed from scratch using PyTorch:

    3 convolutional layers (Conv → ReLU → MaxPool)

    Fully connected classifier

    Dropout for regularization

Training Strategy

    Train / validation / test split

    Adam optimizer

    Cross-entropy loss

    No pretrained weights used

Evaluation Metrics

    Accuracy

    Macro Precision

    Macro Recall

    Macro F1-score

    Confusion Matrix

Results (Test Set)

    Accuracy: ~90–91%

    Macro F1: ~0.91

Key Observations

    CNN learns discriminative texture and shape features effectively

    Most confusion occurs between visually similar classes (e.g., Shirt vs T-shirt)

    Confirms suitability of CNNs for low-resolution image classification

2. DeepWeeds — Transfer Learning Study
Dataset

    17,509 RGB images

    9 weed classes (including “Other”)

    Real-world background clutter

    Official CSV-based train/val/test splits

Model Choice

    ResNet-50 (ImageNet pretrained)

Justification:

    Deep residual architecture supports stable fine-tuning

    Strong performance on texture-rich natural images

    Modular layers enable controlled unfreezing

Fine-Tuning Strategies Compared
A. Frozen Backbone (FC-only Training)

    All convolutional layers frozen

    Only final classification head trained

Results

    Accuracy: ~0.76

    Macro F1: ~0.68

Interpretation

    High precision, low recall

    ImageNet features insufficient for weed-specific discrimination

B. Partial Fine-Tuning (Layer4 + FC)

    ResNet backbone frozen except layer4

    Classification head trained

Results

    Accuracy: ~0.92

    Macro F1: ~0.90

Interpretation

    Significant improvement in recall

    High-level semantic adaptation critical for plant morphology

C. Full Fine-Tuning (End-to-End)

    Entire ResNet-50 trainable

    Lower learning rate to preserve pretrained knowledge

Results

    Accuracy: ~0.94

    Macro F1: ~0.92

Interpretation

    Best overall performance

    Marginal gains over partial fine-tuning at higher computational cost

DeepWeeds Key Findings

    Frozen backbones underperform on domain-specific tasks

    Partial fine-tuning provides the best trade-off 

    Full fine-tuning yields maximum accuracy but diminishing returns    

    “Other” class remains the most challenging

3. FER2013 — Facial Expression Recognition
Dataset

    48×48 grayscale face images

    7 emotion classes

    Subtle inter-class visual differences

Model Choice

    ResNet-18 (ImageNet pretrained)

Justification:

    Lower parameter count suitable for FER resolution

    Residual design enables controlled fine-tuning

    Widely used baseline in FER literature

Fine-Tuning Strategies Compared
A. Frozen Backbone (FC-only)

    Only classifier trained

Results

    Accuracy: ~0.44

    Macro F1: ~0.38

Interpretation
    
    Severe class collapse
    
    ImageNet features poorly aligned with emotion semantics

B. Partial Fine-Tuning (Layer4 + FC)

    High-level features adapted

Results

    Accuracy: ~0.61

    Macro F1: ~0.59

Interpretation

    Large improvement over frozen baseline

    Still limited by frozen low-level filters

C. Full Fine-Tuning (End-to-End)

    Entire network trainable

Results

    Accuracy: ~0.64

    Macro F1: ~0.62

Interpretation

    Best recall and class balance

    Gains smaller than DeepWeeds due to task ambiguity

FER2013 Key Findings

    Emotion recognition requires low-level feature adaptation
    
    Partial fine-tuning yields most of the gains
    
    Full fine-tuning improves minority emotion recognition

    Confusions persist between similar emotions (Fear–Surprise, Angry–Disgust)

Global Observations
    Transfer learning effectiveness depends on domain similarity
    
    Progressive unfreezing is essential for complex semantics
    
    Macro-averaged metrics are critical under class imbalance
    
    Partial fine-tuning often offers the best cost-performance trade-off

Final Conclusion

        This task demonstrates the importance of progressive fine-tuning when applying deep CNNs to real-world vision problems. While frozen pretrained models provide a useful baseline, adapting high-level—and in some cases low-level—features is essential for achieving strong performance. Across datasets, partial fine-tuning consistently delivers substantial gains, while full fine-tuning yields optimal results when computational resources permit.