---
tags:
  - deeplearning
date: 2024-10-28
source: "[[COMPSCI 194]]"
---

Tool suits the Task

CNNs are translational equivariant, like our eyes.
CNNs tend to have a propensity for textural bias, over shape.

NLP - Transformers:
- Self attention

Calculating attention - QKV


Tool suits Multiple Tasks

Computer Vision - ViT
- Deviate very little from NLP transformer architecture
- Generate embedding of each token via linear projections

Properties:
- Position information is learned by model
- Classification head MLP to predict class
- other NLP-transformer-esque components ([[LayerNorm]], [[Multi-Head Attention]])

ViT vs CNN

- ViT's self-attention layers are global - global receptive field
- To a transformer, an embedding is an embedding irrespective of nature or type
- Reduces inductive bias



Occam's Razor
- On smaller data CNNs outperform transformers. On larger data transformer's shine.
- Transformers model human nature better.
- ViT's are more robust against adversarial attacks


Drawbacks of ViT
- Scalability: Extraction of patches is a problem specific to images not text
- For bigger images, number of tokens increases $O(n^{4})$
- Not good for fine-grained tasks like segmentation

## Shifted Window (Swin Transformer)

- Use non-overlapping windows to perform self-attention
- Develops a hierarchal feature map that yields improved global representation of the image
- Linear complexity
- Flexible to CV tasks like image classification, detection, semantic segmentation