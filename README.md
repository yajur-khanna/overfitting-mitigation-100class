# Overfitting Mitigation in 100-Class Sports Image Classification

This repository presents an empirical study of **overfitting in high-capacity convolutional neural networks trained from scratch**. A ResNet-101 model is trained on a curated sports image dataset containing **100 different sports**, where images are cropped to the primary action or object of interest. Despite the relative visual simplicity of the dataset, the baseline model exhibits **severe overfitting**, motivating a systematic investigation into mitigation strategies.

---

## Motivation

Large neural networks are often pretrained on massive datasets before fine-tuning. In this project, the goal is deliberately different:

- Train a **ResNet-101 from random initialization**
- Observe how a high-capacity model behaves on a **high-cardinality but semantically simple** classification task
- Understand **why overfitting occurs so aggressively**
- Systematically reduce overfitting using controlled interventions

This setup isolates **generalization behavior** from the benefits of transfer learning.

---

## Dataset

- **Domain:** Sports image classification  
- **Classes:** 100 different sports  
- **Preprocessing:** Images are cropped to the main focus of the sport/action  
- **Task difficulty:** Visually straightforward, but high class count

The dataset design makes the classification task relatively easy in terms of semantics, while still stressing generalization due to the number of classes.

---

## Baseline Model

- **Architecture:** ResNet-101
- **Initialization:** Random (no pretraining)
- **Training setup:** Standard supervised classification
- **Loss:** Cross-entropy
- **Metrics:** Accuracy, macro F1 score, loss curves

### Baseline Observation
The model rapidly achieves high training accuracy but fails to generalize, showing a clear **train–validation performance gap** characteristic of overfitting in over-parameterized networks.

---

## Overfitting Mitigation Strategies

To reduce overfitting, multiple strategies are applied and evaluated, including:

- **Data augmentation**
  - Random crops, flips, and geometric transformations
- **Regularization**
  - Weight decay
  - Dropout
  - Label smoothing
- **Training controls**
  - Learning rate scheduling
  - Early stopping
  - Batch size adjustments

Each strategy is introduced in a controlled manner to study its individual and combined effect on generalization.

---

## Experimental Analysis

Performance is analyzed using:
- Training vs validation accuracy
- Training vs validation loss
- Macro F1 score across classes
- Learning dynamics over epochs

The experiments demonstrate how even visually simple datasets can lead to severe overfitting when model capacity is high, and how targeted regularization can significantly improve generalization.

---

## Key Takeaways

- High-capacity models can overfit **even easy datasets** when trained from scratch
- Overfitting is amplified in **high-class-count** settings
- Regularization and augmentation are essential when transfer learning is not used
- Studying failure cases provides deeper insight than starting from pretrained models

---

## Project Structure

```text
├── data/                 # Dataset loaders and splits
├── models/               # ResNet-101 implementation
├── training/             # Training and validation loops
├── evaluation/           # Metrics and analysis scripts
├── experiments/          # Ablation studies
├── utils/                # Helper functions
└── README.md
