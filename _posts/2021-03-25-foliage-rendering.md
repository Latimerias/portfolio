---
layout:     post
title:      "Foliage Rendering in Houdini Karma"
active: notes
date:       2021-03-25
header-img: "img/postcover/renaming-files-thumbnail.jpg"
tags: []
categories: []
comments: false
---

## LookDev for Vegetation Assets

USD references files on disk which can make it difficult to LookDev assets like vegetation which can have very scene specific parameters like SSS. A ease of life workaround is
that when you use point instancing you can control shader parameters with point attributes. So for example I have an external USD asset of a tree, the base asset has no SSS making it look dead in my scene but instead of going back into my asset file and rewriting out the material I can create an attribute called `sss` which matches the parameter name on the principled shader and set it to any value which will activate SSS.