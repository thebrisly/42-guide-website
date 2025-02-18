# Building the thing

This project was divided into 4 parts

1. The first part concerns **parsing and reading input files**
2. The second part is a little more mathematical and concerns **intersections and ray tracing**
3. Then the **management of light, shadows and colors**
4. And finally all the **graphic management** (windows, hooks, etc.). **with the minilibx**

Let's look at each of the 4 parts in detail



## Parsing

Parsing isn't very complicated, but it does take a long time... a very long time! Here is the list of almost everything that you need to check:

* [ ] File management (non-existent, empty files, etc.)
* [ ] The types correspond to the requested types and nothing else&#x20;
* [ ] There is a MAXIMUM of one camera, one diffused light and one ambient light (there can be 0 or one, but no more!)
* [ ] Each line corresponding to a type must have the right number of elements
* [ ] If it's a color, it has to be in the right range (0 - 255) and the same goes for orientation vectors (-1,1), etc. Make sure all digits are in the correct range for each type.
* [ ] For each object, you also need to pay attention to its specific characteristics (whether the diameter or height of a cylinder is non-negative, for example, or other things).

Visually it would look like this:

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

There are a LOT of parameters to take into account. Just try to make sure it doesn't segfault when you take a scene in the parameter of your program ! :)



## Intersections and raytracing

Here, the focus shifts to a core challenge: finding intersections. The goal is to determine where the rays cast from the camera hit different objects in the scene.&#x20;

This process involves intricate steps to calculate intersections with various shapes like spheres, planes, and cylinders.&#x20;

* For spheres, it requires solving quadratic equations to find the points where the ray and the sphere's surface meet.&#x20;
* Planes involve straightforward geometric calculations to determine where the ray intersects the plane.&#x20;
* Cylinders require a bit more complexity, involving calculations to find where the ray crosses the cylindrical surface.&#x20;

Successfully mastering these calculations is essential as it forms the foundation for accurately tracing rays and creating the visual representation of the scene.

To sum up, here's a little to-do list of what you can do:



* [ ] Send rays from the camera position to each pixel of the screen.
* [ ] Determine where each ray intersects with the objects in the scene (spheres, planes, cylinders).
* [ ] Calculate the precise points of intersection by solving equations or using geometric methods.
  * [ ] Intersection with a sphere
  * [ ] Intersection with a plane
  * [ ] Intersection with a cylinder
* [ ] Evaluate the distance between the camera and the intersection points to understand what's closest.
* [ ] Decide which object the ray hits first by comparing distances to the intersection points
* [ ] Once the closest object is identified we can try to find out what color the pixel will be and how bright it will be (next step)



## Lights and shadows

In this step, we make things look real with light and shadows. We check if objects are lit or in shadow by sending rays to light sources. We use angles to decide how bright things should be. Background light and distance effects are also added.

* [ ] Once the closest object is identified, cast new rays from the intersection point towards light sources.
* [ ] If one of these rays intersects with another object before it reaches the light source, it's like catching the object casting a shadow on itself. This shadow indicates that the point is not directly illuminated by the light.
* [ ] Conversely, if the ray reaches the light source without obstruction, the point basks in direct illumination – it's in the light.
  * [ ] When a point is in the light, assess the angle at which the light strikes the object's surface. This angle helps determine how intense the light's effect should be on the point (or any other method if you find a better one)
* [ ] Introduce the concept of ambient light, which mimics the soft, indirect illumination from all directions in the environment. This is like a gentle, uniform glow that helps prevent overly dark shadows.
* [ ] Contemplate how light attenuates, growing weaker as it travels. Objects farther from the light source receive less light intensity, which influences their brightness.
* [ ] Blend all these factors together, calculating how they contribute to the final color of the pixel at that point on the screen. This color is a result of intricate interactions between light and the object's characteristics.

## Graphic Management

This part involves creating a graphical interface using the minilibx library to display the rendered image. The library provides tools to open windows, handle keyboard inputs, and interact with the user. Here's a breakdown of the steps:



* [ ] Initialize minilibx
* [ ] Create a window
* [ ] Handler user inputs / hooks (close the program/window with the cross or by pressing ESC)
* [ ] Render the image (call your raytracing function)
* [ ] Display the image (put your pixels one by one)



And that's it ! Don't forget other basic things such as error handling and leaks management ;)\
\
I really hop that you'll have as much fun as we've had on this project! And we wish you good luck and a lovely adventure. don't forget that if you have any questions, you can come and [ask me](https://www.linkedin.com/in/laura-fabbiano/).
