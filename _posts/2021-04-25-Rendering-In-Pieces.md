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

---



Scene too large to render as a single piece? Luckily in houdini the fix is simple. First I will note that its impossible to split a render up by creating a new camera matrix which you may be inclined to do first, you must use a camera with identical matrix settings and be able to crop or pan its view.

To do this in houdini start off with your scene set up normally and create the camera you want to split into pieces. Once you have your main camera duplicate it 4 times to split the render into 4 pieces. We want to make sure that these cameras have the exact settings as the original. 

Next we just want to look at 2 settings, `screen window x/y` and `screen window size`. The settings are as follows. The camera you want in the top left corner will have a screen window x/y value of `-.25, .25`. The top right corner will have a value of `.25, .25`. The bottom left corner has a value of `-.25, -.25` and the bottom right is `.25, -.25`. The screen window size is set to a value of .5 for all cameras. For an explanation of these values read below.


The screen window size is simple, we put a value of .5 in because we split the image into 4 pieces. For example if our original image is 10 units by 6 units to get 1/4 of it we would create an image with the dimensions 5 units by 3 units. I refrain from using resolution here because even if you change the screen window size to .5 on a 1920x1080 render it will still render as 1080, you can think of it as zooming in. 

The screen window x/y specifies the center point of the cameras views and the screen window size is a multiplier of the camera window without reducing resolution. To understand these parameters its best to look at the camera window as a 2D screen with a center point of 0,0:x/y. If we shrunk our screen window size down to .5x.5 it is the correct size for a single piece but is still centered at the center of the original camera which is 0,0. We need to center it at it corresponding corner. If we wanted to center it at the top left corner we would move it -.25 along the x and .25 up. 

![screen](img\screen-layout.jpg)
The 1920x1080 rectangle represents our original camera view and the red rectangle is the scales camera with the screen window size set to .5x.5 and screen window x/y set to -.25x.25.

The parameters to set up a 1280x720 into 4 pieces are screen window x/y .214844/.215278 and window size of .570312999 which during compositing corresponds to a 158px overlap in x direction and 90px in y direction. This gives a final image of ~2243x1178.