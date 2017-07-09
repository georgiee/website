+++
title = "Pinball Simulation"
description = "Take P2JS physics and Phaser, some state machines and entities. Et voilà: a pinball machine."
date = 2016-05-01
tags = ["pinball", "simulation"]
+++
## Introduction

+ P2JS physics engine. Today I would use Box2D as it supports CCD which was a HUGE problem, there was a lot of tunneling on weak system.
+ Created a custom state machine to manage the state of all entities
+ Created a custom action system to trigger different predefined actions like light on, ball reset, start mission, trigger sound and so on.
+ A zone system so that only 1/4 of the involved table physics is active at one moment. only zones near the ball are activated.
+ The ramp on the right is actually an elevated area which is kind of a problem with a 2D physics engine. I placed some sensors on the entries so I can toggle between the base level and the ramp level. I use the physic bits of the engine (like in Box2D) to toggle the collisions pairs. This allows the ball to roll beneath the ramp when the ramp is not activated. Works like a charme.
+ webgl & canvas support
+ entities, actions, missions and assets are created from json files. So you could make your own pinball with the existing code- well in theory. I wouldn't hold my breath 🙃
+ Too bad but I wrote this back then in coffee script (oh WHY???💩) and I used middleman as my building pipeline. I'm not able to get the original files to run so I spare you the time.
The single compiled JS files are still readable.

👻Attention. This is like other code on my lab so far a little dated and build very manual. Require JS, no npm versioning. 👻

# Running example
Looks weird?? Yeah sorry.🤕
This was client work from some years ago. To make it public I had to clean it up, obfuscate the involved assets, remove all sounds (and replace it with one default sound). Also the dramatic music is missing.

{{< example
  repository="lab-pinball-simulation"
  preview="/images/preview-pinball-simulation.png"
  content="http://georgiee.github.io/lab-pinball-simulation/index.html" >}}

<div class='lab-sources'>Based on <a href='https://github.com/photonstorm/phaser'>Phaser (v2.04, pretty old now)</a> and <a href='https://schteppe.github.io/p2.js/'>P2JS</a><br>

</div>
