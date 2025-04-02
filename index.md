---
layout: post
title: Digital Rain C++ Project
tags: Cillian Jennings
categories: test
---



# Introduction
This is the blog of my C++ Programming project on Digital Rain. The aim of this project was to create a digital rain as seen in the movie "The Matrix". 
I used the object oriented programming style in this project. This is what the final product looks like:

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/DigitalRain.gif" width="400" height="300">

# Design and Test
The design of this project was assisted by ai tools, where I discovered console screen buffering or double buffering, [Microsoft Screen Buffering](https://learn.microsoft.com/en-us/windows/console/createconsolescreenbuffer).
This works by creating two seperate memory buffers, one is visible (active buffer) while the other (inactive buffer) is used for drawing the next frame.
Once the new frame is completely drawn in the inactive buffer, the program swaps the roles of the two buffers. The inactive buffer becomes active and is displayed, 
while the previously active buffer becomes the new drawing surface.
The purpose of double buffering it to eliminate flickering in the console. My first version of digital rain was very flickery and not very pleasant to look at, and double buffering solved that.
![image](https://github.com/user-attachments/assets/c5dc0e9c-c5d7-46d2-8dd1-83c56e1af738)


# The Algorithm


# Problem Solving


# Modern C++ insight & reflection



Font can be *Italic* or **Bold**.


Hyperlinks look like this: [GitHub Help](https://help.github.com/).

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/DigitalRain.png" width="400" height="300">
