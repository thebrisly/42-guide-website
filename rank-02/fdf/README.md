---
description: >-
  FdF is a project in which we convert a file with a grid of height values into
  a 3d wireframe using a simple graphics library called MiniLibX.
---

# FdF

Well, if you are here it means that you have survived GNL and maybe already push swap... FdF is much less bad than these two projects. You will have to go back to math, but nothing too complicated, don't worry

### Goal

<details>

<summary>Project-specific guidelines</summary>

* The result should be displayed using an **isometric projection**.
* Your program must display an image in a window.
* The management of the window should remain smooth (change the window, minimize it, etc.).
* Pressing the ESC key should close the window and exit the program cleanly.
* Clicking on the cross at the top of the window should close the window and exit the program cleanly.
* Using the MiniLibX images is mandatory.

</details>

Of course! FdF is the abbreviation of "Fil de Fer", which means "Wireframe" in French. The FdF project is one of the first graphics projects. The goal of the FdF project is to create a software that can read a file containing information about a 3D object and display it as a wireframe model on the screen.

You have to go from a representation like this:

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption><p>2D representation of the "42.fdf" map</p></figcaption></figure>

Where the rows represent the x-axis, the columns the y-axis and the values the z-axis (the altitude).

To a graphic representation like this:

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption><p>3D representation of the "42.fdf" map</p></figcaption></figure>

The subject is simple and clear. In practice it is a bit more complicated than that because many new concepts are introduced. But by separating each step and looking at one element after the other, you will be able to do this project very easily.



### Visual Final Example

To give you an idea, here is what the final project should look like:

{% embed url="https://www.youtube.com/watch?v=kH58QaKAPOU" %}

Well, the guy is a genius and he did more things than requested in the project - but you get the general idea :-)



This project will have more pages than the others. There will be a theoretical part about the new things you have to learn in this project (and an explanation of all the new functions), a mathematical part to understand the transformation process and a practical part, where you will code FdF thanks to everything you will have learned and to checklists we will define.

Okay, let's get to the heart of the matter now
