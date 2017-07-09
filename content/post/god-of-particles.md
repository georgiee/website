---
title: God of Particles
date: 2016-06-01
description: WebGL/ThreeJS based GPGPU pixel simulations in space or feeling like god commanding so many pixels. 👽👊
---

# Introduction
Work in progress. A GPGPU particle system based on kinematic equations. Acceleration, velocity and speed.
I worked through the excellent source of {% link webgl-particles2 https://github.com/nopjia/webgl-particles2  %} and created my very own understanding of particles in space. At the moment it looks really the same as the inspirational source. But under the hood it's a different and more manageable beast.

## First Change: Make velocity explicit
The original is based on implicit velocity calculated by the delta of previous and current positions. I wanted it to be more explicit so I can use it more easily for other algorithms. I'm thinking of boids and agent systems.
To do so, I created a second data texture to hold the velocity and a third data texture to hold target positions- as this is going to be used very often by me. I rewrote the shaders and the initialization step.

## Simulator Box
After understanding the whole implementation I ripped it apart and isolated the core system:
This [system](https://github.com/georgiee/lab-space-pixels/blob/a31055d4bd5e12dd60509bc2259c9a855b63dcfa/src/js/spacepixels/simulator.js) holds the position and velocity in a [ping-pong buffer](https://github.com/georgiee/lab-space-pixels/blob/a31055d4bd5e12dd60509bc2259c9a855b63dcfa/src/js/spacepixels/core/buffer-ping-pong.js) (read & write must be separated for gpus)
and sends those through a calculating shader - one for each step. Of course most happens in the [velocity step](https://github.com/georgiee/lab-space-pixels/blob/a31055d4bd5e12dd60509bc2259c9a855b63dcfa/src/js/spacepixels/shaders/source/simulate-velocity.frag)
The available target positions are not necessarily be used or filled with useful data at this point. We are going to use them later for displaying meshes and other pre-calculated positions. After the simulation we can take the calculated positions and do whatever we want. Like here: Rendering our [particle system](https://github.com/georgiee/lab-space-pixels/blob/a31055d4bd5e12dd60509bc2259c9a855b63dcfa/src/js/spacepixels/spacepixels.js#L24)

## Mesh Plotter
From the beginning I wondered how the animated mesh was implemented. After testing, reading and debugging I finally understood it and created own [core class](https://github.com/georgiee/lab-space-pixels/blob/a31055d4bd5e12dd60509bc2259c9a855b63dcfa/src/js/spacepixels/mesh-plotter.js) just for doing this part. It's doing the same as in the original implementation but it's completely rewritten, isolated and most important: (well) understood 😄

### This is the recipe:
+ Make a new shader step to encode the static or morphed position of a vertex into a color and place it at the original uv position.
+ This results in a colorful texture in the shape of the uvs.
+ Every point in this texture which holds a vertex part of the model has been set to alpha = 1 the rest is alpha = 0
+ This data texture is passed to the simulation step as target positions.
+ Now we can distinguish between mesh vertices and unoccupied/unused positions
+ Take each mesh vertex and use it as a target position. The position is encoded as the color (like in every data texture)

## Smooth Paths
I also included a path builder to use smooth Catmull-Rom Splines as a path. Depending on the time I can read the current position and pass it to the simulation as a target position for the whole system - and do some agent or predator stuff.

## Boids
I am now in the process of implementing flocking with the established simulation structure. I love boids/flocking!
I want to use a spatial data structure for a first basic optimization. Later I want to try [Improving Boids Algroithm in GPU using Estimated Self Occlusion](http://www2.dcc.ufmg.br/projetos/cggt/lib/exe/fetch.php?id=publications&cache=cache&media=sbgames08-boids.pdf)

# Running example

{{< example
  repository="lab-friendly-birds"
  preview="/images/preview-space-pixels.png"
  content="https://georgiee.github.io/lab-space-pixels/index.html" >}}

<div class='lab-sources'>
Based on <a href='https://github.com/mrdoob/three.js'>ThreeJS</a> and of course <a href='https://github.com/nopjia/webgl-particles2'>webgl-particles2</a>

</div>
