---
layout:     post
title:      "Karma XPU Bugs and Limitations"
active: notes
date:       2023-08-10
header-img: "gallery/archive/uvl/greenhouse_shot_001.jpg"
tags: []
categories: []
comments: false
---

## Intro

This is a list of all the bugs or limitations I have encountered with Karma XPU, sometimes with solutions or confirmations of incompletion from SideFX. 

## Custom AOVs do not support 64-bit primvars

When writing out custom AOVs sourced from primvars XPU does not support 64-bit primvars. When creating an primvar in an attribute wrangle you can change this in the bindings tab which will determine the USD data type from the VEX data type. 

