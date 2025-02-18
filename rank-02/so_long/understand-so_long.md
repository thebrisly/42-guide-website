# ▪️ Understand so\_long

### Goal

<details>

<summary>Project-specific guidelines</summary>

You have to build a simple 2D game (top-down or platformer)

* The goal of the game is to collect all objects present on the map to unlock an exit.
* We have to be able to use W, A, S and D to move around.
* The player can move in all four directions (up, down, right, left).
* The player can't go through walls.
* The total move count must be displayed at every move in the shell.
* Pressing the ESC key must close the window and exit the program correctly.
* Clicking on the red cross must close the window and exit the program correctly.
* Using MiniLibX Images is mandatory.

</details>

In short, you'll have to create a simple 2D game, top-down or viewed from the side.

The subject in itself is fairly clear on what you have to do, I'll take some time on the next page to explain some of the core concepts you'll have to know before starting to build your game.

### Before Starting

Before starting to work on this project and read what I wrote, I encourage you to take some time and read the documentation of the MiniLibX [here](https://harm-smits.github.io/42docs/libs/minilibx), that's not the "official" documentation but it is still better explained there.

There's also a [MiniLibX](broken-reference) section on this Gitbook where I put some helper functions that I used as well as some hooks that might be useful for this project.

You should also choose what type of games you want to build, a top-down view, or one that is viewed from the side (like a platformer).

{% hint style="info" %}
A 2D top-down game is a type of video game that is played from a top-down perspective, meaning that the camera is positioned above the game world and the player views the game from an overhead perspective. In a 2D top-down game, the game world is typically represented in two dimensions, meaning that the game world is shown as a flat plane rather than a fully three-dimensional space.

In a 2D top-down game, the player usually controls a character that is represented by a single sprite or 2D graphic, and moves the character around the game world by using the arrow keys or WASD keys on the keyboard, or by using a gamepad or joystick. The player typically interacts with the game world by moving the character around the game world, collecting items, solving puzzles, and defeating enemies.

2D top-down games are often used to create a sense of nostalgia or retro style, as they were popular in the early days of video gaming. They are also well-suited for certain types of gameplay, such as turn-based strategy games or games that involve a lot of exploration and puzzle-solving.
{% endhint %}

{% hint style="info" %}
A 2D platformer game is a type of video game that involves navigating a character through a series of levels or environments by running, jumping, and avoiding obstacles and enemies. In a 2D platformer game, the game world is typically represented in two dimensions, meaning that the game world is shown as a flat plane rather than a fully three-dimensional space and is shown from a side (Mario is a good example of that).

In a 2D platformer game, the player usually controls a character that is represented by a single sprite or 2D graphic, and moves the character around the game world by using the arrow keys or WASD keys on the keyboard, or by using a gamepad or joystick. The player typically interacts with the game world by moving the character around the game world, collecting items, solving puzzles, and defeating enemies.

2D platformer games often involve a series of levels that the player must progress through, with each level becoming increasingly difficult as the player advances. The player may also have the ability to earn power-ups or special abilities that can help them navigate through the levels more easily.

2D platformer games are a popular genre of video game, and have been around since the early days of video gaming. They are often known for their fast-paced action and challenging gameplay, and have been a staple of the video game industry for many years.
{% endhint %}

### Examples 2D games

Here are three well known example of 2D games that exist and from which you can inspire if you need ideas.

<figure><img src="../../.gitbook/assets/hotline_miami.avif" alt=""><figcaption><p>Hotline Miami</p></figcaption></figure>

{% hint style="info" %}
Learn more about Hotline Miami [here](https://en.wikipedia.org/wiki/Hotline_Miami)
{% endhint %}

<figure><img src="../../.gitbook/assets/super_mario_bros.jpg" alt=""><figcaption><p>Super Mario Bros.</p></figcaption></figure>

{% hint style="info" %}
I think you all know what Super Mario Bros. is but you can find information [here](https://en.wikipedia.org/wiki/Super_Mario_Bros.) and even play it online [here](https://supermario-game.com/).
{% endhint %}

<figure><img src="../../.gitbook/assets/terraria.jpg" alt=""><figcaption><p>Terraria</p></figcaption></figure>

{% hint style="info" %}
You can find more information about Terraria [here](https://en.wikipedia.org/wiki/Terraria).
{% endhint %}
