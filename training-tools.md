---
title: Training Tools
description: This page lists tools useful for training
published: true
date: 2023-09-17T22:59:09.971Z
tags: 
editor: markdown
dateCreated: 2023-09-17T22:58:20.269Z
---

# Training Tools

## Currently Maintained BasicSR Forks

Most training repositiries are based upon BasicSR. We will list the recommended ones below, then list the ones that used to be recommended at some point in time, but that you should better avoid now.

### [NeoSR](https://github.com/muslll/neosr)

The latest Fork by musl, it has AMP training support, and an opinionated choice of losses and architectures integrated to avoid those losses and architectures that don't add a meaningful benefit to the training process. It supports all of the relevant modern architectures and as such is the recommended fork as of September 2023.

### [traiNNer-redux FJ](https://github.com/FlotingDream/traiNNer-redux-FJ)

A fork of Joey's fork, adding additional architectures, ...

### [traiNNer-redux](https://github.com/joeyballentine/traiNNer-redux)

A fork of BasicSR made by Joey to add some additional losses such as the CX Loss and Color loss, as well as adding a few additional architectures such as swinirgan, 2c2esrgan, RealSwinIRGAN, compact-2c2, OmniSR and a few augmentations.

### [Xinntao's Original BasicSR](https://github.com/xinntao/BasicSR)

This is the original BasicSR repository. It was updated to v1 officially, however, it is not recommended as it lacks many of the features the community generally finds useful, and only creates x4 scale new-arch models.

### [Colab-traiNNer](https://github.com/styler00dollar/Colab-traiNNer)

Sudo's fork that contains a ton of architectures and losses, you can see him experimenting and expanding it on our discord.

## Dead BasicSR Forks

### [Victorca25's traiNNer](https://github.com/victorca25/BasicSR)

This used to be the recommended fork, It includes many features including contextual loss, enhanced degredation pipelines (augmentations), and support for many architectures (SOFVSR, for example).

### [BlueAmulet's Fork](https://github.com/BlueAmulet/BasicSR)

This fork added many features like auto-backups, YAML training configs, and Frequency Separation.

It is no longer maintained.

### [DinJerr's Fork](https://github.com/DinJerr/BasicSR)

This fork has lots of cool On The Fly training options added through ImageMagick. This includes different types of dithering and a Kuwahara filter.

It seems to be unmaintained as of late 2021.