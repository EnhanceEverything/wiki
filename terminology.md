---
title: Terminology
description: Common terms you might stumble across
published: true
date: 2023-09-17T23:48:02.402Z
tags: 
editor: markdown
dateCreated: 2023-09-17T23:48:02.402Z
---

# Terminology
This page gives you an overview of the terminology and abbreviations you might see in relation with ESRGAN.

# General AI Terms

- **GAN - Generative Adversarial Network**
An AI network that works by having a generator that tries to fool the discriminator. During training, the generator tries to generate realistic fakes of the training data, while the discriminator tries to tell which images are real and which are fake. Both of these two elements keep improving each other during training.

- **Dataset**
The collection of data you train your AI model on. For super resolution, it's a pair of low-resolution and high-resolution images.

- **Batch Size**
The amount of images the trainer looks at in one iteration. Generally a higher batch size makes the training more stable and prevents sudden degressions.

- **Iterations**
The amount of times your AI model updates itself with new data. Multiply with your batch size to get the total amount of images that have been processed.
    
  For example: If your model is at 10,000 iterations with batch size 4, it has seen 40,000 training images.

- **Epochs**
How often your entire dataset was processed. Important: One epoch does not mean your model has finished training! It can still improve, even after seeing the same data many times.

- **Fine-Tuning**
Training a model using another model as a "template" instead of training from scratch. You usually do this with ESRGAN models.

- **Pretrain Model**
The model used for fine-tuning. Should be similar to what you want your fine-tuned model to be, or very neutral.

- **Checkpoint**
A model that was saved during training.

# Hardware and Software

- **GPU**
Synonymous with "Graphics Card", though this technically only refers to the actual processor chip on your graphics card.

- **VRAM**
Video RAM, the amount of memory your GPU has. Most AI related applications need as much VRAM as they can get.

- **CUDA**
Nvidia's software stack that allows all kinds of software to run on your GPU.

- **Python**
The language most AI applications are written in. The runtime needs to be installed before you can run any python scripts.

# Other common Training Specific Terms

- **Tile Size, Crop Size or GT Size**
During training, images are usually split into tiles to avoid running out of VRAM. The tile size defines how large these tiles are. For example 128 would usually mean 128x128 GT tiles and if the scale is 4, 32x32 LQ tiles.

  Larger tiles are not automatically better, but they can provide the model with more context. However, usually smaller tiles work just as well and may even be preferrable for workloads that don't require a lot of context, such as jpg decompression.

  The higher the resolution of both the LQ and GT tiles, the more VRAM is required.

- **LQ or LR - Low Quality / Resolution**
The part of your training data that resembles the type of images you want to use your model on.

- **GT / HR - Ground Truth / High Resolution**
The part of your training data that resembles what you want your model to output.

- **Augmentation**
The process of making your LR images intentionally "worse" in order to make the AI learn to improve them.

  Examples: JPEG compression, dithering, blur, noise

- **Batch Size**
The amount of images process per training iteration. Higher number means slower training and higher memory usage, but usually better results.

- **AMP**
Automatic Mixed Precision - Speeds up training on modern GPUs (cards with Tensor Cores like the Tesla V100 or RTX 2080 Ti)

- **Validation**
The process of "benchmarking" your model during training and calculating certain metrics to help you see how the model performs. **This is purely optional and has no impact on the model.**

- **Discriminator**
The part of the AI that tries to tell whether the generator's image is real or fake. BasicSR offers **VGG**, **PatchGAN**, and **Multiscale** PatchGAN.

- **Loss Function**
The generated image get's compared with the ground truth image. A loss function returns how close it is.

- **Learning Rate**
How fast the model trains. By default, it slowly decays (decreases) in order to make the model more stable with time.