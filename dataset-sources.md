---
title: Dataset Sources
description: 
published: true
date: 2023-09-18T00:58:39.521Z
tags: 
editor: markdown
dateCreated: 2023-09-18T00:58:39.521Z
---

# Dataset Sources

To train your own model, you need a dataset of images. Here are some sources to get you started.

| Name | Price | Files | Description |
|------|-------|-------|-------------|
| [DIV2K](http://data.vision.ee.ethz.ch/cvl/DIV2K/DIV2K_train_HR.zip) | Free | 0.8K | 800 HQ real-world images|
| [https://github.com/bloc97/SYNLA-Dataset SYNLA] | Free | ~2K | This dataset is designed to simulate complex line art.|
| [https://quixel.com/megascans/library Quixel Megascans] | Limited Free | 9.89K | Discover a world of unbounded creativity. Explore a massive asset library, and Quixel’s powerful tools, plus free in-depth tutorials and resources.|
| [https://stock.adobe.com/ Adobe Stock] | $29.99+/Month | "Millions" | Stock photos, royalty-free images, graphics, vectors & videos|
| [https://www.pexels.com/ Pexels] | Free | Unknown | Free stock photos you can use everywhere. ✓ Free for commercial use ✓ No attribution required|
| [https://www.poliigon.com/ Poliigon] | $16+/Month | 3.069K |- todo -|
| [https://cc0textures.com/ CC0 Textures] | Free | A lot | Textures with Normal Maps, Displacement Maps and others in form of JPGS. Most seem to be 8K. The name of the website comes from the license.|
| [https://www.textures.com/ Textures.com] | Limited Free | 134.872K | Textures for 3D, Graphic Design and Photoshop 15 Free downloads every day!|
| [https://texturehaven.com/ texturehaven] | Free | 0.133K | 100% Free High Quality Textures for Everyone|
| [https://www.reddit.com/r/DHExchange/comments/ay0w3c/s_highres_scans_of_gustave_dor%C3%A9s_1866_bible/ Gustave Doré's 1866 Bible Illustrations] | Free | 0.241K | High-Res Scans of Gustave Doré's 1866 Bible Illustrations|
| [http://texturelib.com/ texturelib] | Limited Free | 6.605K | Library of quality high resolution textures. Free for personal and commercial use.|
| [http://toflow.csail.mit.edu/ Vimeo-90k] | Free | 89.8K | This dataset consists of 89,800 video clips downloaded from vimeo.com, which covers large variety of scenes and actions. It is designed for the following four video processing tasks: temporal frame interpolation, video denoising, video deblocking, and video super-resolution. |
| [http://toflow.csail.mit.edu/  Triplet (for temporal frame interpolation)] | Free | 73.171K | The triplet dataset consists of 73,171 3-frame sequences with a fixed resolution of 448 x 256, extracted from 15K selected video clips from [http://toflow.csail.mit.edu/ Vimeo-90k]. This dataset is designed for temporal frame interpolation.|
| [http://toflow.csail.mit.edu/  Septuplets] | Free | 91.701K| The septuplet dataset consists of 91,701 7-frame sequences with fixed resolution 448 x 256, extracted from 39K selected video clips from [http://toflow.csail.mit.edu/ Vimeo-90k]. This dataset is designed to video denoising, deblocking, and super-resolution. |
| [https://drive.google.com/open?id=1f25paYZvzULHsBRIjrqcVWTjiekupZQP falcoon300] | Free | 1.233K | LyonHrt: As it has been mentioned, here is the almost complete works of falcoon, as used in the falcoon300 model, this has a selection of 1233 images from original source, I should add there are some scantly clad woman, so nsfw lol.|
| [https://www.gwern.net/Danbooru2018 Danbooru2018] | Free | 3330K |  Danbooru2018 is a large-scale anime image database with 3.33m+ images annotated with 99.7m+ tags; it can be useful for machine learning purposes such as image recognition and generation.|
| [https://yingqianwang.github.io/Flickr1024/ Flickr1024] | Free | 2.048K | Flickr1024 is a large stereo dataset, which consists of 1024 high-quality images pairs and covers diverse scenarios. This dataset can be employed for stereo image super-resolution (SR). |
| [https://cv.snu.ac.kr/research/EDSR/Flickr2K.tar Flickr2K] | Free | ? | Huge dataset that is being used to train a lot of models. |
| [http://www.mohamedaly.info/datasets/caltech-games Caltech Game Covers] | Free | 11.4K | Found a dataset of game covers, but there's a ton of duplicates. If I can figure out how to parse the text files and remove the dupes, I'll upload the trimmed down version.|
| [https://drive.google.com/drive/folders/16PIViLkv4WsXk4fV1gDHvEtQxdMq6nfY outdoor scene training] | Free | 8.137K | outdoor scene training is huge, just the first file has 2,187 pictures (8,137 total)|
| [https://mega.nz/file/SL5jwYSR#nkVWxRMazz1QO72338ZEl1Ts0BLJjtYFxr9Ne-jmf7A Nomos2k] | Free | 2536 | A dataset made by musl on the Game Upscale Discord server. Description: A dataset containing 2536 images of 2000px. I hand selected it from multiple sources, based on the following criteria:
- High signal-to-noise ratio (low noise)
- Diverse. 
- Sharp (no motion blur, shallow DOF is ok)
- Contains mixed and complex textures/shapes that cover most part of the image
Raw images were processed on rawtherapee using prebayer deconvolution, AMaZe and AP1 color space. Sources: Adobe-MIT-5k, RAISE, FFHQ, DIV2K, DIV8k, Flickr2k, Rawsamples, SignatureEdits, Hasselblad raw samples and Unsplash. 
KernelGAN was trained using DLIP on all images, with scale 4x and up to 5k iter, instead of 3k. Hopefully it increases the accuracy of kernels. All files are provided on "kernelgan" folder. Note: in order to use it on traiNNer, you have to give dataroot_kernels path, along with enabling realistic under the resizing presets. 
I've also made available my selected noise patches. They were extracted from multiple images "in the wild", with unknown degradation:
[https://mega.nz/file/WSZjjYRI#jgJYQTxJQyJjW5cbDJdUte0szfOpyeiDRrWmMzIkxZ0 Noise Patches]
I encourage everyone to give it a try and, if possible, mirror the dataset. For now it was made available on MEGA, but I plan to mirror it on other solutions.
[https://cdn.discordapp.com/attachments/579685650824036387/904201202546380820/nomos2k.mp4 Sample Video]|

## Other sources
If you have some time consider adding them to this list here.
[http://homepages.inf.ed.ac.uk/rbf/CVonline/Imagedbase.htm http://homepages.inf.ed.ac.uk/rbf/CVonline/Imagedbase.htm]
[https://caffe2.ai/docs/datasets.html https://caffe2.ai/docs/datasets.html]
[https://pastebin.com/vU7P8Vmi https://pastebin.com/vU7P8Vmi]