---
title: "A Simple Pinball Game with OpenGL"
tags: [technology]
layout: post
date: 2017-08-15
---

- overview of code structure
- physics engine in more detail
- modelling in more detail
- conclusions?

What's up, peeps. After 8 months of stress, I've finally found some time to write a new blog post. In this post, I want to show off the pinball game that I spent the last few weeks of my 4B term working on, through blood, sweat, and tears.

## Some Background 
Some of you may have heard about CS488, one of the big three CS courses at the University of Waterloo. The course is split into two main parts - the first involves OpenGL and the forward rendering of the graphics pipeline, which involves going from a model into a final rendering onto a screen. We had some assignments here involving manual transformations on a cube, and making a personal puppet with joints, but my favourite is probably the Minecraft clone. The next half of the course is focused on ray tracing, and is basically the reverse flow of the graphics pipeline, where from each pixel on the screen, the colour can be determined from tracing a ray into the world view and looking for collisions. More information about the course can be found on [UWFlow](https://uwflow.com/course/cs488) for anyone interested in self-afflicted pain. ;)

- insert my favourite picture of the graphics pipeline here

## What I Built 
An excerpt from my initial project proposal:

> The pinball project that I want to make is a simple OpenGL game. In this game, the user will be able to launch a ball from a launchpad into the pinball table. In this zone, there will be a variety of obstacles as well several flippers (player-controlled bats) that can rotate and collide with the ball to move it around. Upon the ball entering certain zones, specific particle and sound effects will be shown in order to be more visually appealing.
> 
> In order to do this, I will need to spend a significant portion of my time into refining the physics engine and object collision so that the ball can move realistically. In order to model this, factors such as gravity, elasticity, and mass will have to be taken into account. I will also have to spend additional time researching algorithms such as shadow mapping in order to implement dynamic shadows.
>   
> Creating a pinball game is not only challenging, but also very interesting. It involves me combining a lot of different graphical concepts together with gaming concepts in order to create one cohesive project. In addition, the physics and object detection will be implemented from scratch, which makes the project a lot more mathematical in nature and thus, more challenging.
>    
> My pinball game is a simple OpenGL game to demonstrate the knowledge that I have accumulated in the CS488 course, as well as give me a chance to research the things that I haven't learned in class. I will learn some basic physics in the process in order to deal with the physics engine. Additionally, I will learn and integrate with third party libraries in order to complete objectives such as texture mapping and audio implementation.

And my final result was the following:

- screenshot + youtube link?

Not too shabby, huh?

### Technologies I Used

- **Blender** - Blender is a a free tool for 3D modelling. It allowed me to easily model my 3D assets, and then export them into many formats for a variety of asset importing libraries. For this project, I exported it into the Wavefront (.obj) format for simplicity
- **OpenGL 3** - One of the two main API's for rendering graphics, with the other being DirectX. OpenGL allows you to take advantage of hardware-accelerated rendering by leveraging the GPU's processing power
- **glm** - GLM is the standard C++ library used for graphics related matrix math, with naming conventions and functionality that matches the GLSL spec. It's very convenient for common operations such as matrix transformations
- **Imgui** - Imgui is a simple, self-contained library for rendering common UI elements such as labels and buttons. I used it for my debugging menu which features several buttons and a framerate display
- **Assimp 3.3.1** - Assimp is a simple-to-use asset loader for 3D file formats, such as .obj. I used it into import my models from Blender into my own custom C++ class
- **IrrKlang 1.5.0** - IrrKlang is a cross platform sound library free for commerical use. I only use it to play 2D sound, but it's capable of much more

## Creating Assets with Blender
- UV mapping?
- weird on spheres
- simplest way to get started is to follow youtube tutorials to learn the tool, also ensures you do good practices. watching multiple videos for the same thing let's you have a better all around understanding. lots of people use blender in different ways
- to keep myself sane, I used the coordinate system on Blender's grid as my modelling coordinates and scale for after I import into my C++ program
- example table width & height were blah and blah, in program, those are their conceptual coordinates

![UV Mapping with Blender]({{ site.baseurl }}/assets/in_post_images/blender-uv-mapping.jpg)
![Blender]({{ site.baseurl }}/assets/in_post_images/blender.jpg)

## Overview of Code Structure

|-+-|
| Col1 | Col2 |
|-+-|
| content1adf | content2dflkjkl |
|-+-|

## Physics Engine in More Detail

## Afterthought

## Acknowledgments
blah blah learnopengl was a great source, provided some starting points for some helper classes that I derived my classes from
