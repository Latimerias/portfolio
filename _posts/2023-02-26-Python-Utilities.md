---
layout:     post
title:      "Houdini Python Scripts Utilities"
active: notes
date:       2023-02-25
header-img: "img/postcover/renaming-files-thumbnail.jpg"
tags: []
categories: []
comments: false
---

## Find Texture Locations im materialX Image VOPs
Useful for when you have a large scene that is returning missing texture references but you don't know where. You can also use houdini "Find Node" search option with the evaluated parameter filter and type filter.


    import hou
    import os

    texture = hou.ui.readInput(message="Texture Name.ext")

    nodes = hou.vopNodeTypeCategory().nodeType("mtlximage").instances()

    for node in nodes:
        if os.path.basename(node.parm("file").eval()) == texture[1]:
            print(node.path())
