---
layout:     post
title:      "Karma XPU Memory Optimization"
active: notes
date:       2022-04-25
header-img: "img/postcover/design-resources-thumbnail.jpg"
tags: []
categories: []
comments: false
---



According to [SideFX](https://www.sidefx.com/docs/houdini/solaris/karma_xpu.html) Karma XPU does not flush textures from the GPU except between frames when rendering an image sequence. The test cases below show how to reduce memory usage. 

- Using a single texture in multiple materials

  As long as the texture is in a single place on disk, using it in multiple materials will not load the texture into memory more than a single time. 

- Using a the same texture with different paths

  If you have the same texture but it is referenced from different directories (exists in multiple places on disk), karma XPU will not be able to identify that they are the same and will load them all into memory.

