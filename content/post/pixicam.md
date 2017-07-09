+++
title = "Pixicam"
date = 2015-12-01
tags = ["pixi", "camera", "canvas"]
description = "A camera and minimap system for PIXI JS"
+++
# Introduction
Place all your objects in a world which is rendered based on 2d camera transformation. So you can zoom & translate your world with any size (think of platformer, tilemap).

This world is a simple container so you can maintain other layers to render a HUD or menu on top of of your camera renderer world.

# Camera use cases
+ Zoom to a target
+ Zoom to fit a view area
+ Follow Target
+ Constrained View
+ Change Zoom Pivot

# Running example
+ Use the minimap to pan the scene
+ Use your mousewheel to zoom.
+ I don't think this is usable on a mobile or tablet at the moment.
+ Ah and don't forget to expand the controls in the upper right corner.


{{< example
  preview="/images/preivew-pixicam.png"
  content="http://georgiee.github.io/lab-pixicam/chromeless.html" >}}

<div class='lab-sources'>
  Based on <a href='https://github.com/GoodBoyDigital/pixi.js'>PIXI</a> and some code taken from <a href='https://github.com/photonstorm/phaser'>Phaser</a>
  Assets by <a href='http://kenney.nl/'>Kenny</a>

  <iframe src="https://ghbtns.com/github-btn.html?user=georgiee&repo=pixicam&type=star&size=large" frameborder="0" scrolling="0" width="160px" height="30px"></iframe>
</div>
