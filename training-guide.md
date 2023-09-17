---
title: Training Guide
description: This is a short guide to cover everything you need to know to train your own model. In this tutorial, we will be using NeoSR.
published: true
date: 2023-09-17T22:31:19.375Z
tags: 
editor: markdown
dateCreated: 2023-09-17T22:30:39.055Z
---

# Training Guide

## Getting Started

*This guide assumes you already know how to download/clone repositories from GitHub and that you are familiar with python and pip.*

### Choosing a Fork

First of all, we maintain a list of [currently maintained forks here](Maintained_BasicSR_Forks "wikilink"). As of right now, the recommended one we will use here is NeoSR.

### Installing Dependencies

The documentation of NeoSR will be more up to date than instructions here, so we will keep it minimal and suggest to follow the [README installation instructions here](https://github.com/muslll/neosr#installation).

To get started you will need to install the version of Python supported by NeoSR, on Windows that can be done either by downloading it [here](https://www.python.org/downloads/windows/), or by creating an environment for it using [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html) or [mamba](https://mamba.readthedocs.io/en/latest/mamba-installation.html). On Linux those same tools work, but we suggest you install them with your system's package manager. Training on macOS has been relatively unexplored by our community, it might work on metal on the later arm macs released after 2023, you will probably need to modify your BasicSR fork of choice, if you want to explore it, we suggest you go onto our discord server.

### Creating a Dataset
It
All super resolution models are trained using low-resolution images, often called LR (Low Resolution) for short or LQ (Low Quality), and high-resolution images, often called HR (High Resolution) or GT (Ground Truth). For a 4x scale model, this means that your LR images will be 4x smaller in both vertical and horizontal resolution compared to your HR images.

It is important to create the best dataset you can for your upscale task. Many pre-existing datasets exist, such as nomos8k, nomosUni, DF2, Manga109 or many others, but a dataset can be any collection of images. Your HRs could be high quality frames of a TV show, for example, with the LRs being the same images scaled down by 4. This would then create a model that is good at upscaling small images that are visually similar to the LRs you created. The dataset is one of the most important part of training a model. Without a good dataset, your model will not work well.

Datasets don't have to just be downscaled images, though. You can use images with compression artifacts, or images with noise for the LR/GT frames. This will train your model to remove such artifacts. Most modern forks make this very simple, we'll discuss it lower down in the guide.

#### Examples of bad datasets in general

- A dataset with only 5 images
- A dataset where every image is almost exactly the same

#### Examples of bad HR images

- Images with lots of artifacts, such as those that come with high JPEG compression
- Images that have already been upscaled and as such look very blurry or overly sharpened.

#### Examples of good datasets

- 800+ high-quality pictures of mountains
- 3,000 exported frames of a 1080p cartoon
- 500 images of cropped-out faces

A few things to note:

- Your HR images and LR images must have exactly matching names
- Your HR images must be exactly 4x (or whatever scale you are training) the resolution of your LRs. This means you must crop your HR images so that each dimension (width and height) are multiples of 4, most forks do this for your automatically.
- The more images you have, the better the model will become (to an extent)

Once you have your dataset set up, you may want to create a validation set. This can just be a few images taken from your LR and HR folders and placed into separate HR and LR directories. These images are just used as a reference to see how your model is doing during training. This could be a crop of the target you are training your model for. **Note: These images will NOT affect training in any way. Also avoid using images in the training dataset for validation**

### Configuring NeoSR

This configuration setup for NeoSR is pretty straightforward and well documented [here](https://github.com/muslll/neosr/wiki/Configuration-Walkthrough). We suggest looking at it's documentation as it is likely more up to date than this article.

NeoSR provided templates used for training [here](https://github.com/muslll/neosr/tree/master/options) in `./options/`. Copy the template of the architecture and task of your choice. We strongly suggest not to modify those files directly, instead copy the config you want to use into the root of your repository and give it a project name, ideally the same as you want to use for your model, that way if you train another model, you can reference what changed between them. A choice selection of common parameters:

- `name`
This will be your model name. Typically, these also include the scale. Example: 4xBox, 2xFaithful.

- `scale`
This is the scale of your model. You should already know what this is if you have already created your dataset. Typically this is just 4.

- `dataroot_gt`
This is the path to your dataset's HR folder

- `dataroot_lq`
This is the path to your dataset's LR folder

- `num_worker_per_gpu`
This is the number of threads that will be used to load images per GPU. Typically this is just the number of cores/threads your CPU has.

- `batch_size`
This is the number of images that will be looked at in each iteration. Typically this is set to the highest it will go before running out of VRAM. It seems to yield more stable results while training.

- `gt_size`
This is the resolution that your dataset will be automatically croped to. This number may be lowered to reduce VRAM usage.

- `dataroot_gt (validation)`
This is the path to your dataset's validation HR folder (not required)

- `dataroot_lq (validation)`
This is the path to your dataset's validation LR folder (not required)

- `root`
The direct path to the directory of the repository you downloaded

- `pretrain_network_g`
The model that your model will use as a sort of base to get started with. We suggest using the closest model that already exists for your task of the architecture of your choice, you can [find models on the OpenModelDB](https://openmodeldb.info/).

- `val_freq`
The frequency that your model will be run on your validation dataset in iterations. Typically this is set to 5000.

- `save_checkpoint_freq`
Your model will be saved every this iterations. You may desire a lower save frequency if power outages, ... are a problem or a higher one if disk space is a concern.

### Training

To start training, open your command-line interface of choice, navigate to the root of the NeoSR repository, refered to as `./` here, and type
```bash
python train.py -opt your_train_config.yml
```
Just replace your_train_config.yml with whatever your training config is named. If all goes well, it should spit out a bunch of info and then start training from iteration 0, epoch 0. If you set everything up correctly, you should have a new folder in your `./experiments/` folder that is named after your model.

To pause training, press CTRL+C. It should save the latest state and model. If you spam it, press it at the wrong time, or have Powershell quick edit mode, there is a possibility it will not work properly. In this case you would fall back to the latest save/resume state which is specified on save_checkpoint_freq (ie: 7200.state). These files are saved in the experiments folder. To resume, edit the training config and remove the \# before resume_state. Then link to the .state file. To continue, simply use the command from the previous paragraph.

### Common errors

```
CUDA out of memory
```

This means you need to decrease your batch size. If you can't decrease your batch size any more, decrease your crop_size.

- If you're getting this error during validation, it means your validation images are too large. Try cropping them or splitting them into multiple images.

```
Module not found
```

This means you did not install the required libraries through pip. Try again or see if your path file is pointing to a different python installation

```
Could not broadcast shape \_\_\_\_ to shape \_\_\_\_
```

This could mean a few things, most likely your LR and HR sizes are mismatched. Make sure they are clean multiples of each other.