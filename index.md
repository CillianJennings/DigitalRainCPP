---
layout: post
title: Digital Rain C++ Project
---

# Introduction
This is the blog of my C++ Programming project on Digital Rain. The aim of this project was to create a digital rain as seen in the movie "The Matrix". 
I used the object oriented programming style in this project. This is what the final product looks like:

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/DigitalRain.gif">

# Design and Test
The design of this project was assisted by ai tools, where I discovered console screen buffering or double buffering, [Microsoft Screen Buffering](https://learn.microsoft.com/en-us/windows/console/createconsolescreenbuffer).
This works by creating two seperate memory buffers, one is visible (active buffer) while the other (inactive buffer) is used for drawing the next frame.
Once the new frame is completely drawn in the inactive buffer, the program swaps the roles of the two buffers. The inactive buffer becomes active and is displayed, 
while the previously active buffer becomes the new drawing surface.
The purpose of double buffering it to eliminate flickering in the console. My first version of digital rain was very flickery and not very pleasant to look at, and double buffering solved that.

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/DoubleBuffering1.png" width="400" height="300">

The code snippet above where the two console screen buffers are created using the windows API function. It has various parameters that are required and are shown in the microsoft webpage linked above.
The first is the access, in this case both read and write. The second is the share mode, 0 meaning no sharing. The third is the security attributes, NULL being the default. The fourth is the buffer type which only has this one supported type. The fifth is reserved which should be NULL.

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/DoubleBuffering2.png">

The code snippet above configures the dimensions of the console screen buffers and the visible window size. BufferSize specifies how many colums and rows each buffer can hold. 
1 is taken away from the width and height to correctly cover the entire buffer without going out of bounds. For example the buffer width is 120 therfore the columns are numbered 0-119.
Buffer 0 is set as the currently displayed active buffer.

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/Initialise.png">

The code snippet above initialises columns with random positions and lengths. The length of the column is set to be between 6 and 10. The -10 in the last line is so the columns are drawn in above the top of the window.
In other words it's to prevent columns just appearing on the console instead of falling down from the top.

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/SetCursorPos.png">

This function moves the console cursor to the specified position. A COORD structure is created to hold the x and y coords. Then the x and y parameters are assigned to the structure.
Windows API function updates the consoles internal cursor position so that the text output will be at the specified coords.

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/DoubleBuffering3.png">

The above code first starts by determining which buffer is currently inactive. It then clears the entire buffer by filling it with space characters. Finally it sets the default colour of
the inactive buffer to dark green. This ensures that anything not drawn in another colour will appear dark green.

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/DoubleBuffering4.png">

This code simply swaps the console buffers, making the previously inactive buffer the new active buffer.

# The Algorithm

<img src="https://raw.githubusercontent.com/cillianjennings/DigitalRainCPP/main/docs/assets/images/Algorithm.png">

This is the main algorithm or piece of code that draws the "rain". The first for loop iterates through all columns where each column is one vertical stream of characters. 
The next for loop goes through the number of characters that make up the column. Then the actual vertical position on the screen is calculated by adding the columns top position and the character index.
The if statement checks of the character is within the visible console area (between row 0 and the height). The console cursor position function is called. Then the colour of the character is chosen. If its the last character in the column its white, otherwise it randomly chooses between light green and dark green. Next the character is chosen randomly from the characters listed in validChars, where it then writes to the inactive buffer.
Finally after drawing all the characters in the column, startY is increased so the column will appear one row lower on the next frame.

# Problem Solving

During the development of this digital rain project I encountered a few problems that needed to be tackled.

1. Screen flickering: The biggest problem I had at the beginning was definitely how flickery the screen was. It wasn't nice to look at and took away from the animation.
   The solution I found through the assitance of ai tools and the internet was double buffering. Which basically creates two buffers and draws the "rain" to the inactive buffer while the active
   buffer is shown on the console. The two buffers then just switch back and forth.
2. Incorrect Characters: At one point the characters being printed were only chinese/japanese characters which weren't what I had specified in validChars. What fixed the problem was switching from
   WriteConsole to WriteConsoleA which is the ANSI version. This made sure that single-byte char's are treated as ANSI/ASCII. It appeared the problem was WriteConsole may have been mapping to WriteConsoleW
   (wide version). Due to passing in 1-byte chars, this ended up displaying the wrong glyphs.


# Modern C++ insight & reflection



