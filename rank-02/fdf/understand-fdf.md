# 🗡️ Understand FdF

FdF is a graphic project in which you need to have new knowledge and master many new tools. In particular the minilibx of 42. But the subject can also be complex to understand... how to do it properly? Well, this is what we will see in this page

### From 3D to 2D

In the subject we are given an example of a map. This map corresponds to coordinates in a space (x,y,z). However, the screen of our computer is a surface with only two dimensions (x,y). We must therefore make a projection of the 3D points on a 2D plane.&#x20;

Here is an illustration to better visualize what I say:

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Projection of a 3D cube on a 2D plane</p></figcaption></figure>

Above, you have an example of 4 different projections. For this project, they only ask you to do the "**isometric projection**".&#x20;

Let's take a more concrete example and start from scratch.&#x20;

\[insert scheme of fdf to better understand what we need to do - cube 3d (with 3 axes and cube 2d with 2 axes that represent a screen)]

### Putting the dots in the right spots

If we have a map of 8 points:

<mark style="color:blue;">(col = 0, 1, 2, 3 = x)</mark>\
&#x20;          1  2  3  4 <mark style="color:blue;">(line = 0 = y)</mark>\
&#x20;          5  6  7  8 <mark style="color:blue;">(line = 1 = y)</mark>

With this, we can define 8 points. For example:

* (x,y,z) = (0,0,1)    |    (x,y,z) = (1,0,2)    |    (x,y,z) = (1,1,6)     |   ... and so on

However, your computer screen only has two coordinates (x and y). You can't see in 3D on your computer. You have to place the points in a certain way to create this 3D effect.&#x20;

Fortunately, this can be done with mathematical formulas. For one degree of projection we use:

```
destination.x = source.x + cos(angle) * source.z
destination.y = source.y + sin(angle) * source.z
```

Since in the data it is asked to create an **isometric projection**, we will have to use another formula. The isometric projection is a perspective representation of an object, where the three main edges (which correspond to the three dimensions of the object) form equal angles of 120°. Here is the one I used:

$$
destination.x = source.x * cos(a) + source.y * cos(a + 2) + source.z * cos(a - 2)
$$

$$
destination.y = source.x * sin(a) + source.y * sin(a + 2) + source.z * sin(a - 2)
$$

There are other formulas to reach the same result. I encourage you to do some tests so you can see the differences



### Connecting the dots

Once you understand the above theory and have placed all the dots on your screen, you must now connect them.&#x20;

To do this, you will need to code an algorithm that allows you to connect two points together. There are several types of algorithms that have already been done and you can use them as inspiration. Here are some of them:

* **DDA Line Algorithm**: [\[doc here\]](https://www.thecrazyprogrammer.com/2017/01/dda-line-drawing-algorithm-c-c.html)
* **Linear Interpolation:** [\[doc here\]](https://en.wikipedia.org/wiki/Linear_interpolation)
* **Bresenham:** [\[doc here\]](https://en.wikipedia.org/wiki/Bresenham's_line_algorithm)

Personally I used the DDA because it is the simplest and less complicated to achieve the same result.&#x20;



### To summarize

* [ ] First you have to convert all your three-dimensional points (x,y,z) into two-dimensional points (x,y).
* [ ] Once this is done, place the points on your screen (one point = one pixel).
* [ ] Code an algorithm that connects the points together and draw all the pixels that connect them.

This is not a complete checklist for the project. Afterwards, you have to pay attention to several other things that you will find in the final checklist. This one is just to help you understand the essential points of a projection.

