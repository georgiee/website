+++
title = "Friendly Birds"
description = "A not so angry birds clone with webgl, box2d and liquid fun"
date = 2016-05-25T05:00:00Z
+++
# Introduction
This was my journey into Angry Birds. I focused on the following components and challenges:

+ Camera System for PIXI
+ Minimap View on the scene
+ Box2D Integration in PIXI (there is some code from Phaser's Box2D)
+ Fluid Integration (Liquid Fun), the build of box2d already contains liquid fun (see here
+ Polygon Rendering in PIXI (this wasn't possible then)
+ Custom Water Shader for the particles
+ Raycasting in Box2D
+ Building a Slingshot with Trajectory projection

<div class='old-code-warning'>
  👻Attention. This is old code. Very manual. Require JS, no npm versioning. 👻
</div>

# Running example
+ Use the minimap to pan the scene
+ Click, hold and drag around the slingshot to perform a shot
+ Use your mousewheel to zoom.
+ I don't think this will be usable on a mobile or tablet.
+ Ah and don't forget to expand the controls in the upper right corner.


{{< example
  repository="lab-friendly-birds"
  preview="/images/preview-friendly-birds.png"
  content="http://georgiee.github.io/lab-friendly-birds/chromeless.html" >}}

<div class='lab-sources'>Based on pixi, box2d and liquid fun</div>
