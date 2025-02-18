---
description: >-
  Explanations of certain concepts to reduce confusion during the realization of
  the project
---

# 🗡️ Graphics programming

I had a lot of difficulty at the beginning to distinguish between all the terms I had just found on the web. This new chapter is a big one. Let's try to get some practice on this brand new chapter which is graphic programming (it's really fun, trust me :-) )



### Display VS Window VS Image

When you start coding, the first thing you'll do is initialize your workspace. There are these three terms that I find very similar and I couldn't tell them apart, but in the end they are very different:

#### **Display**

A display is something that shows visual information. In the context of graphical programming, it refers to the physical device that displays the graphical user interface. For example, when you are using a computer, the display could be a monitor or a TV connected to the computer via HDMI.

#### **Window**&#x20;

A window is a graphical element that **represents a rectangular area on the display**. It is used to display content, such as text, images, or videos.  For example, a window might contain a text editor, a web browser, or a video player.

#### **Image**

An image is a **two-dimensional array of pixels** that can be displayed on the display. It can be a static image, such as a photograph, or a dynamic image, such as a video. In graphical programming, images are often used to display graphical elements, such as icons, backgrounds, or visual effects. They can be displayed by themselves or as part of a window.



Your displays, windows, and images can have several different sizes (defined in pixels). It's up to you to define which size best fits what you do and what you need. Here is a small diagram to better visualize:

\[insert scheme]

<details>

<summary>Example in C</summary>

Before starting to do graphic programming you should always think about initiating a display and one or more windows and images.

{% code overflow="wrap" lineNumbers="true" %}
```c
int	main(void)
{
	void	*mlx; //display
	void	*mlx_win; //window
	t_data	image; //image

	mlx = mlx_init(); //display init
	mlx_win = mlx_new_window(mlx, 1920, 1080, "Hello world!"); //window init
	image.img = mlx_new_image(mlx, 1920, 1080); //image init
}
```
{% endcode %}

</details>





### Interacting with your program (with hooks)

When you work on a graphic project, you will be able to interact with the window you are working on. You can for example close a window, zoom in/out and many other things. This can be done thanks to a thing called "hook".&#x20;

A **hook** in computer science is a way to intercept and modify the behavior of a function or system call. It is often used to add additional functionality or to customize the behavior of a program or operating system.

<details>

<summary>Simple example of a hook</summary>

Imagine that you have a program that displays a message on the screen every time you press a certain key on the keyboard. You might want to add some additional behavior to this program, such as changing the color of the message or playing a sound every time the key is pressed.

To do this, you could "hook" the function that handles the key press events. When the key is pressed, your hook function would intercept the event and perform the additional behavior you want, such as changing the color of the message or playing a sound. Then, it would pass the event along to the original function so that the message can be displayed as usual.

Here is some pseudocode that shows how this might work:

{% code overflow="wrap" lineNumbers="true" %}
```c
//Original function that handles key press events
void OnKeyPress(Key key)
{
    // Display a message
    DisplayMessage("You pressed the key: " + key);
}

// Hook function that intercepts key press events
void Hooked_OnKeyPress(Key key)
{
    // Perform additional behavior
    ChangeMessageColor(Color.Red);
    PlaySound("beep.wav");

    // Pass the event along to the original function
    OnKeyPress(key);
}

// Hook the OnKeyPress function
void HookOnKeyPress()
{
    // Replace the OnKeyPress function with our hook function
    OnKeyPress = Hooked_OnKeyPress;
}

// Main program loop
void Main()
{
    // Hook the OnKeyPress function
    HookOnKeyPress();

    // Wait for key press events
    while (true)
    {
        Key key = WaitForKeyPress();
        OnKeyPress(key);
    }
}

```
{% endcode %}

</details>

This concept will be really userful for the rest of the project.

