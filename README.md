# cifar10-cnn-vit-lora
CIFAR-10 image classification with CNNs, Vision Transformers, and LoRA fine-tuning using PyTorch.
# CIFAR-10 Classification with CNNs, ViTs and LoRA

## Overview

This course project compares a CNN and a Vision Transformer trained
from scratch with an ImageNet-pretrained ViT on CIFAR-10.

I implemented the scratch models, completed the training and evaluation
code, and compared linear probing, LoRA and full fine-tuning.

## Methods

- CNN with three convolutional blocks
- Compact Vision Transformer trained from scratch
- Linear probing with a frozen pretrained ViT backbone
- LoRA fine-tuning of query and value attention projections
- Full fine-tuning of the pretrained ViT
- Controlled experiment comparing LoRA ranks 8 and 16

## Experimental Setup

- Dataset: CIFAR-10
- Split: 45,000 training / 5,000 validation / 10,000 test images
- The same split was used for all models
- Random seed: 328
- GPU: NVIDIA Tesla T4
- Scratch models: 30 training epochs
- Linear probe: 2 epochs
- LoRA and full fine-tuning: 3 epochs

## Results

| Model | Test accuracy | Trainable parameters |
|---|---:|---:|
| CNN baseline | 86.44% | 815,018 |
| ViT from scratch | 78.92% | 4,249,354 |
| Linear probe | 96.35% | 7,690 |
| LoRA rank 8 | 98.40% | 302,602 |
| Full fine-tuning | 98.04% | 85,806,346 |
| LoRA rank 16 | 98.00% | 597,514 |

The CNN baseline above is the rerun used for the Part 2 comparison.
The separate Part 1 CNN run achieved 86.06% test accuracy.

## Main Findings

The CNN outperformed the scratch ViT under the same epoch budget.
Pretraining improved accuracy substantially.

LoRA rank 8 achieved the highest test accuracy while updating about
0.351% of the model parameters. It also used less training time and
peak GPU memory than full fine-tuning in these runs.

Increasing LoRA rank from 8 to 16 did not improve accuracy.
Alpha was kept at 16, so alpha/r changed from 2 to 1.
Each configuration was tested once, and batch order was not identical.

## Evaluation

The notebook includes training curves, validation confusion matrices,
example predictions, and misclassified images. Training time and peak
GPU memory are also reported.

## Running the Notebook

Open the notebook in Google Colab, select a GPU runtime, and run the
cells from top to bottom.

The notebook installs its additional dependencies. Full experiments
require downloading CIFAR-10 and the pretrained Hugging Face checkpoint.
Any personal Google Drive setup should be adjusted or removed before running.

## Acknowledgments

Completed for CMPUT 328 at the University of Alberta using the
course-provided starter notebook.

ChatGPT was used to help understand the assignment, complete code
sections, debug errors, review outputs, and draft explanations.
