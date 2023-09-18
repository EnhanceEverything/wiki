---
title: Model Architectures
description: An overview of the currently in use and recommended Model Architectures
published: true
date: 2023-09-18T00:50:50.937Z
tags: 
editor: markdown
dateCreated: 2023-09-18T00:50:50.937Z
---

# Model Architectures

There are a lot of different neural networks, in fact there are new ones every day. But here is a *small* list of important ones:

## Relevant Networks

### [DAT](https://github.com/zhengchen1999/dat)

Transformer Architecture that is relatively lightweight. Considered a very good modern options.

### [DITN](https://github.com/yongliuy/DITN)

Transformer Architecture that is relatively lightweight.

### [OmniSR](https://github.com/Francis0625/Omni-SR)

Transformer Architecture that is relatively lightweight.

### [SRFormer](https://github.com/HVision-NKU/SRFormer)

Transformer Architecture that is relatively lightweight.

### [HAT](https://github.com/XPixelGroup/HAT)

Transformer based architecture. Especially good at handling text.

### [SwinIR](https://github.com/JingyunLiang/SwinIR)

Transformer based architecture.

### [compact / SRVGGNetCompact](https://github.com/XPixelGroup/BasicSR/blob/master/basicsr/archs/srvgg_arch.py)

Lightning fast architecture great for real time upscaling of videos if your GPU is fast enough.

### [ESRGAN](https://github.com/xinntao/ESRGAN)

[ESRGAN](https://github.com/xinntao/ESRGAN) is what most of us started with when our community was founded. There are a ton of models for basically every task you can imagine, andz on modern hardware, it also runs quite fast. You can check the [Model Database](https://openmodeldb.info) or our [Discord server](https://discord.gg/SxvYsgE) for model releases. The above model architectures are now considered superior, and ESRGAN is only included here due to the sheer number of specialised models available for it.

### [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)

Not really an architecture, but a set of augmentations applied during training to make the model more capable of handling various artifacts and degradations. With NeoSR, it can be applied to pretty much any architecture. The repo contains models trained with it based on the ESRGAN and compact architecture.

## Considered out of date

### [SFTGAN](https://github.com/xinntao/SFTGAN)

[SFTGAN](https://github.com/xinntao/SFTGAN) is from the same developers as ESRGAN. It works by segmenting an image before it upscales them.

### [waifu2x](https://github.com/nagadomi/waifu2x)

[waifu2x](https://github.com/nagadomi/waifu2x), [with GUI](https://github.com/lltcggie/waifu2x-caffe) quite old at this point, all the models above can deliver much higher quality outputs.
