---
layout:     post
title:      "Karma Guide"
active: notes
date:       2023-08-07
header-img: "gallery/archive/uvl/greenhouse_shot_001.jpg"
tags: []
categories: []
comments: false
---

# Notes for Karma

- Houdini does not render out images with the ACEScg space by default. To set it up you need to change your "Render Working Space" in Edit > OCIO Editor to ACEScg. You also need to set "Output Colorspace" to be ACEScg on the Karma Render Settings LOP under Image Output > AOVs > Output Colorspace. If you fail to do this and log your render you will see at the end all image planes are converted to linear srgb.  

If you're confused about ACES there are a couple things to keep in mind when performing color transforms to assure accuracy.

  1. Data maps like roughness, normal, displacement should be transformed from Utility - Raw into ACEScg. This preserves the values of each pixel so there are consistent reads. You may think that normal maps have color though? While this is true, the value of each channel R,G,B is grayscale and represents the corresponding X,Y,Z meaning any color transforms would modify the positions defined by the normal map. 

  2. Color data like your diffuse map or subsurface color are a bit more complex because they are in a certain color space which needs to be transformed into the desired color space, usually ACEScg. In order to choose the proper transform you need to know the source color space of the texture. 99% of the time it will be sRGB with sRGB gamma that can be checked with a tool like exiftool. If you texture is coming from sRGB and has not already been linearized you can use Utility-sRGB-Texture into ACEScg. This will result in a much darker texture, which is from the linearization. This is fine however because you will never view ACEScg images, they will have a ODT that transforms them into their appropriate output device like sRGB, rec.709, P3-DCI etc.. on a monitor. This lets the computer and the user work with predictable, linear values while viewing non-linear, realistic outputs.

  3. HDRIs don't tend fall into either of these categories. Like color data, the texture already exist in some color space that is most likely sRGB. However unlike color data, the texture should already be linearized (assuming its from a reliable source) because it is holding data we want to use to light our scenes. So what you have is an sRGB texture that is linear. This can be transformed with Utility-Linear-sRGB into ACEScg. This will result in very small changes in color as the sRGB colors are transformed into the ACEScg gamut. 



