---
title: Publishing your Model
description: 
published: true
date: 2023-09-18T00:46:31.838Z
tags: 
editor: markdown
dateCreated: 2023-09-18T00:46:31.838Z
---

# Publishing your model

So you have done it, you have setup a training software, put together your dataset and trained an awesome model and you want to share it with the world. This page guides you through making it available to the world!

## Licensing

Not the thing most people think about or want to think about, but extremely important, a license tells the user what they are allowed to do with your model. Without one, they technicallz arenẗ even allowed to use one at all.

Now you could write your own license, but for most people, selecting one using [this short wizard is more than enough](https://creativecommons.org/choose/). It takes a few seconds, then you are done.

## File Host

It is time to upload your model, we will list some potential filehosts below:

- [Google Drive]
Cons: If a file is accessed very frequently, users need to log in and import the model into their own cloud to download it.

- [MEGA]
Cons: Used to be a great option, but since a few years ago, there is now a 5GB limit that takes hours to refresh for users that want to download your files, annoying for people that want to download more, but a potential barrier for people using a VPN or behind a [CG-NAT](https://en.wikipedia.org/wiki/Carrier-grade_NAT)

- Discord
If the model is small enough or you enjoy Discord's Nitro subscription, then uploading your models to Discord is an option.

	Cons: There is no guarantee that files will stay up.

## Publishing

There are two places you can publish your model in our community after you have uploaded it and chose a license:

1. The #model-releases channel on our [Discord Server](https://discord.gg/cpAUpDK)
2. Directly on the [OpenModelDB](https://openmodeldb.info/)

### Discord

Just open Discord and if you have never released a model before, ping or DM one of the mods to give you the model author role, after that, just go to the model releases channel and use the following template to post your model and common metadata about it:

```markdown
@news @Wiki Editor
**Name:** ModelNameThatIsCreative
**License:** CC BY-NC-SA 4.0 for example
**Link:** <Link.to.the.model.com>
**Model Architecture:** ESRGAN / PPON / PSNR / SR / ...
**Scale:** 1, 2, 3, 4, 8 or 16
**Purpose:** The kind of images the model is intended to process.

**Iterations:** Your Iterations
**batch_size:** Your batch_size
**HR_size:** Probably either 128 or 192
**Epoch:** The amounts of Epochs you trained your model for.
**Dataset:** What source images you trained you model on. Feel free to use links.
**Dataset_size:** How many images were in your training HR folder
**OTF Training** Yes / No
**Pretrained_Model_G:** What model did you use as a base

**Description:** Your Description
```

### OpenModelDB

Now this is a little more involved.
#TODO
