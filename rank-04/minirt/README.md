# MiniRT

42's MiniRT project is a programming challenge that aims to model images using a technique called raytracing. The aim is to create realistic images representing a given scene, viewed from a specified angle.&#x20;

Here is an example:&#x20;

{% embed url="https://www.youtube.com/watch?v=1JoTZg4Ulo0" %}
Example of a MiniRT (try hard version)
{% endembed %}

Obviously, you can do it a little simpler. In the video above he did all the extras and really did a try-harder job (spoiler: mine will not be so great)

To achieve this, **MiniRT uses a raytracing protocol**. Raytracing is a 3D image rendering method that simulates the behavior of light by tracing light rays from the virtual camera, and calculating the interaction of these rays with objects in the scene. _We will see it more in details later._

The scene modeled in MiniRT is made up of simple geometric objects such as spheres, planes or triangles. Each of these objects has its own properties, such as position, color and lighting system. Lighting systems can include ambient, diffuse or specular light sources, which contribute to the way objects are rendered.

MiniRT's ultimate goal is to produce realistic images that capture the effects of shadow, reflection and refraction of light in the scene. This requires the implementation of efficient raytracing algorithms to simulate these light interactions.

So... here we go. Now you are ready to dig into this big project. RayTracing will have no secrets for you in a few days ;)&#x20;

