# 🗡️ Building the thing

What I'll do here is create for you multiple checklists, that corresponds to different part of the project and that you can follow in order to build it. All the code for my "FdF" is available on my [Github](https://github.com/thebrisly/42-Cursus-Piscine/tree/master/FdF). If you have any question on it, don't hesitate to [contact](../../team.md) me (Laura) and it would be a pleasure for me to answer all the questions you might have.

To realize FdF I created 6 `.c` files:

* `fdf.c`: the place where the `main` is located, error handling and memory allocation
* `start.c`: the place where I initialize my graphic variables and where I do preliminary checks
* `points.c`: the place where I create my three and two dimensional point tables
* `limits.c`: the place where I define which point should connect to another point
* `draw.c`: this is where I have all my formulas and functions that allow me to draw what I want
* `hooks.c`: the place where I give instructions to interact with the mouse and keyboard

and of course a `.h` called "`fdf.h`" where I have the most important and biggest structure.

We'll go through all these files via checklists so you can see what logic I applied.

{% hint style="danger" %}
There must be NO leaks. Check that you free the allocated memory each time !
{% endhint %}



Of course you can do otherwise than what I have shown you above. Here is a more global checklist to make the project your own and make it the best you can.

I didn't put everything otherwise it will not be understandable ^^ I hope it will be useful...



### (some) Checklists

#### Main Checklist

* [ ] Check that there are only 2 arguments
* [ ] Free the allocated memory (no leaks)

#### Map Checklist

* [ ] Get and store the map data somewhere (coordinates, height, length...)
* [ ] Error handling of the map
  * [ ] Empty map (should not segfault if given to you)
  * [ ] Map not rectangular (should not segfault if given to you)

#### Graphical Programmation Checklist

* [ ] Initialize the display, the window and the image&#x20;
* [ ] Initialize the infinite loop for your graphic environment&#x20;

### fdf.c

I created three functions in this file.&#x20;

One that handles errors (simply exit the program and display a message when called), one that frees the tables that I don't need any more and a main that can be defined by these tasks:

### points.c

This file is very simple. It simply initializes my array with three-dimensional points (x,y,z) and another array with two-dimensional points (x,y) that I create from the three-dimensional points.

* [ ] From the the data stored in start.c (the map data), i created a single list with all 3D points
* [ ] From the list containing all 3D points I created another single list with all 2D points
  * [ ] Check that you use the correct formula to convert your points

### hooks Checklist

* [ ] The window and the program should close properly when...&#x20;
  * [ ] You click on ESC&#x20;
  * [ ] You close the window by clicking on the cross
* [ ] **FdF BONUS**
  * [ ] When you use the mouse cursor downwards you zoom the image&#x20;
  * [ ] When you use the mouse cursor upwards you zoom out the image
  * [ ] When you press w,a,s,d (or the arrows) you can move&#x20;
  * [ ] When you click on another key you can rotate (change the angle of the image)
  * [ ] Add another bonus you like



I hope this helps! Let me know if you have any other questions.
