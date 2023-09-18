---
title: Upscaling Build Engine Games
description: 
published: true
date: 2023-09-18T00:03:58.799Z
tags: 
editor: markdown
dateCreated: 2023-09-18T00:03:58.799Z
---

# Upscaling Build Engine Games

## Making Upscale Packs for Build Engine Games

Note that everything on this page assumes you are using either an Eduke32 or BuildGDX-derived port. This will not work on NightDive’s Blood Fresh Supply.

### Extracting tiles

Your first task is to extract tiles from the games ART files, for some games the ART files are already in the game’s main folder (Blood, Witchaven, TekWar) for others they are stored inside a GRP file (in case of Powerslave it is called STUFF.DAT but programs that support GRP files will also open that although you may need to change the file extension) which can be extracted by several tools, for example [SLADE](https://slade.mancubus.net/).

ART files can be opened in M210’s [BAFED](https://m210.duke4.net/index.php/downloads/download/8-java/41-build-art-files-editor), which is preconfigured with palettes for most Build Engine games. This may be more user friendly for the novice user and the resulting exported file will have transparency already applied. The downside is the exported tiles no longer retains the original color indices, which we’ll get to later.

Instead, my preferred method is a commandline tool called [ART2TGA](https://dukeworld.com/2001-current/rtcm/blood-tools-artedit/Wart2tga.zip). You can extract an ART file by dragging it onto the executable. However you may find the palette comes out wrong. To resolve this, place the file PALETTE.DAT from your game in the same directory as ART2TGA.

If you have many ART files to work with, a more convenient approach though is with a batch script

```cmd
for %%f in (*.art) do (art2tga %%f)
```

This will extract all the art files in the folder you run it in. They will be in TGA format so you will want to use the image processing tool of your choice to convert it to a format supported by ESRGAN. You will also notice the lack of transparency.

### DEF Files

Once you’ve made your upscales you need to define them in a DEF file. This is how you define a hightile:

```
texture 1170 { pal 0 { file "filename.png" nocompress nodownsize }}
```

Here 1170 is the tile number, pal 0 defines the new image as replacement using the base palette (which will also override any non-defined palette)

Note that tiles defined this way will only show up in Polymost (and for EDuke32 Polymer) renderers. In its current form, hightiles are unaffected by palette swaps, you have two options, either define a separate image for each palette swap, or use tints. This is how you define a tint in EDuke32-based ports:

```
tint { pal 5 red 255 green 255 blue 255 flags 1 }
```

pal 5 is the palette being tinted, while the three following values are multipliers for each channel, finally flags have special properties.

|Flag |                    |
|-----|--------------------|
| 0   | Nothing            |
| 1   | Greyscale          |
| 2   | Invert             |
| 3   | Greyscale + Invert |

The greyscale and inversion effects are applied before the RGB multipliers. Additional function flags described [here](https://wiki.eduke32.com/wiki/Definetint_(DEF)). For BuildGDX the syntax for defining tints is slightly different:

```
definetint 5 255 255 255 1
```

You can have both forms in the same file however. At the moment the function flags aren’t implemented in BuildGDX so you’re limited to the RGB multipliers (as such the example here does nothing)

Now, if you got 23000 tiles it’s a pain in the ass to write definitions individually, so here’s a helpful batch script

```cmd
setlocal EnableDelayedExpansion for %%f in (tile*.png) do (
set tmp=%%f
if "%%f"=="!tmp:~0,8!.png" (
echo texture !tmp:~4,4! { pal 0 { file "upscale/%%f" nocompress nodownsize }} >> new.def
) else (
echo texture !tmp:~4,4! { pal !tmp:~9,-4! { file "upscale/%%f" nocompress nodownsize }} >> new.def 
)
)
```

In this case, files need to follow the format tileXXXX_YY.png where XXXX is the tile number and YY the palette. The script also allows for omitting \_YY for tiles using the base palette. Place the files in the upscale folder. For compatibility with the BuildGDX you’ll want a def file specifically named for the port. Then you zip them up and place in the game’s autoload folder.

| Game                         | File         |
|------------------------------|--------------|
| Blood                        | bloodgdx.def |
| Duke Nukem 3D                | dukegdx.def  |
| Legend of the Seven Paladins | lspgdx.def   |
| Powerslave                   | psgdx.def    |
| Redneck Rampage              | rrgdx.def    |
| Shadow Warrior               | swgdx.def    |
| TekWar                       | twgdx.def    |
| Witchaven                    | whgdx.def    |
| Witchaven 2                  | wh2gdx.def   |

In BuildGDX-based ports, multiple ZIP files can use the default DEF file. Note that you do not need to include everything in the same DEF file, you can load a separate file inside the DEF file with the include command. EDuke32-based ports are more complicated, as only the last DEF file of a given name is parsed. Raze uses a loading method similar method to EDuke32-based ports, but also allows cumulative loading by tagging -raze to the end of the main def filename, for example blood-raze.def

### Palette swaps

> ![blood_cultist_palette_swap_comparison.png](/assets/images/blood_cultist_palette_swap_comparison.png)
> Upscale of Blood's Cultist with palette swap applied before vs. after upscaling

Most Build Engine games have some sort of palette swaps. Extracting them varies from game to game.

If you plan to define separate images for each palswap you have two choices

1.  Swap palette before upscaling
2.  Palettise your upscaled image and swap palette afterwards.

Both have their advantages and disadvantages. If you apply the palette swap before upscaling there is no risk of mismatch between similar colors with wildly different palette swap results, but you are also duplicating the amount of upscaling work that needs to be done. If you palette swap afterwards the upscale process generally has the benefit of having more colors to work with, however there’s the risk of mismatching. You’re also limiting the result to the colors in the palette.

#### Indexed hightiles

A recent addition is the indexed hightile functionality. This is currently only supported in Raze and special builds of EDuke32 and NBlood. Enable it by putting indexed at the end of each define, for example:

```
texture 0020 { pal 0 { file "upscale/tile0020.png" indexed }}
```

When using indexed hightiles you don't have to supply separate palette variants for each image, they are instead recolored in-engine.

#### Duke Nukem 3D

For most palette swaps, either the whole palette is tinted uniformly excluding fullbrights or just palette indices 64-95. Notable palettes are 21, used for the assault captain and red keycards, 22 used for the assault trooper, and 23 used for the yellow keycard.

Palette indices 240-254 are special. They are fullbrights, not affected by shading (this property does not apply to hightiles), and not swapped out in the various uniform palettes (1,2,6,7,8). If you are planning to use your upscales either as 8-bit tiles in a mod or doing palette swaps after upscaling I recommend making a copy of the game's palette excluding the fullbright colors and applying that to your sprites. In my upscales I made a separate copy of the sprites using fullbrights where everything but the fullbrights are made black, I then upscaled that and keyed in the result on the normal upscale.

Duke 3D's palette is shared with Redneck Rampage so this applies to those games as well.

[EDuke32 Wiki](https://wiki.eduke32.com/wiki/Palette_(environment)) has a full listing of the palettes and palette swaps used by the game.

#### Blood

While Blood has fewer palette swaps than Duke Nukem 3D and no fullbrights, they are a lot more complicated.

Palette indices 48-63 are changed in palettes 3 as well as 11-14, these are noteworthy as they are used for the various cultists as well as the player. Palette indices 64-79 are changed to blue in palette 3, used by the tommy gun wielding cultist.

As these are very similar in tone to each other as well as other colors in the palettes the likelihood of a color mismatch is high. For my upscale pack I made multiple palettised copies of affected upscaled sprites, each with a limited segment of the palette available, which were then combined using a series of masks. The method described for Duke Nukem 3D's fullbrights is usable here as well.

#### Powerslave

Powerslave has very limited use of palette swaps. The only one you really need to pay attention to is palette 5, REDBRITE. If you use PCExhumed it already defines a tint for it.

#### Witchaven

The palette swaps for Witchaven are very unintuitive.

Palette 10-12 swaps out palette indices 144-159. The red color used in the knight's cloak.

#### Ion Fury

[Forum post describing the effect of palettes](https://forums.duke4.net/topic/8181-ion-fury/page__st__3300__p__327678#entry327678)

### Global palette changes

This applies to Duke Nukem 3D, Blood and Redneck Rampage. While underwater and in certain other circumstances the game changes its global palette. This is simulated using tints in EDuke32, DukeGDX, RedNukem, NBlood and BloodGDX. RedneckGDX does not have this feature.

### Addon support

For BuildGDX you can conditionally load DEF files based on the addon/expansion loaded:

```
includeif vacation.grp vacation.def
```

You can use INI files instead of GRP for Blood addons. Note that other files defined in the main def file are still loaded.

### Legend of the Seven Paladins

Legend of the Seven Paladins is unique in that it has two ART files, one being used for the intro level and the rest for the game itself. This causes problems when defining hightiles as the same tile number is used for different tiles.