---
layout:     post
title:      "CRS Conversion Formulas"
active: notes
date:       2023-12-15
image:
  feature: 
header-img: "img/postcover/splitrender-thumbnail.jpg"
tags: []
categories: []
comments: false
---

# EPSG 4326 to EPSG 3857(GOOGLE MAPS)
```
float lon = @P.x;
float lat = @P.z;

float x = lon*20037508.34/180;
float y = (log(tan((90+lat)*PI/360))/(PI/180))*(20037508.34/180);

@P.x = x;
@P.z = y;
```