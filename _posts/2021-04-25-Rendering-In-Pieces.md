---
layout:     post
title:      "Rendering in Pieces"
active: notes
date:       2021-04-25
image:
  feature: "splitrender-thumbnail.jpg"
header-img: "img/postcover/splitrender-thumbnail.jpg"
tags: [tag01, tag02]
categories: [cat01, cat02]
comments: false
---

# EDIT #

With mantra being fused out and Karma taking over a new NDC (normal device coordinates) system taking over this is much simpler. The values are represented as minx, maxx, miny, maxy. If you want to render the top quarter of the image you just need values of -1, 0, 0, 1 as the total image dimension in NDC are 2x2 with 1 being the max and -1 being the min and 0,0 the center.

Default values for a 1:1 aspect ration with 86 px overlap (this cuts of 86 pixels from the original render but saves the full resolution vertically)

- tl = -1, 0, 0, 1

- tr = 0, 1, 0, 1

- bl = -1, 0, -.89, .11

- br = 0, 1, -.89, .11

