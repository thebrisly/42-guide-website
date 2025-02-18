# ▪️ Building the thing

Firstly, I have to say that I won't be able to comment all my code and explain all of my code on here, there's too much files and things linked to one another that it would be impossible to do.

What I'll do is create for you multiple checklists, that corresponds to different part of the project and that you can follow in order to build a complete game in C using [MiniLibX](../../minilibx/). All the code for my game is available on my [Github](https://github.com/Laendrun/42/tree/main/so_long), if you have any question on it, don't hesitate to [contact](../../team.md) me (Simon) and it would be a pleasure for me to answer all the questions you might have.

so\_long being a video game, that is something pretty personal, and you surely don't want to do exactly the same thing as I did (and I don't want you to neither), that's why, checklists is the best way to go. You'll have some ideas on where to start and what to do, and you still have to search for information and learn new things.

Now that all that is said, let's get to work.

### Map checklist

* [ ] Parse the map\
  When parsing the map you can already check some errors, before even going further
  * [ ] Does the map file exist ?
  *   [ ] Is the map rectangular ?

      All the lines should be the same length.
  * [ ] Is there something in the map file ?
  * [ ] Is the map enclosed in walls ?
    * [ ] Check the first and last lines and columns, they should all be `1`
  * [ ] Is there only one exit ?
    * [ ] Simply count how many `E` you find on the map.
  * [ ] Is there only one start position ?
    * [ ] Simply count how many `P` you find on the map.
  * [ ] Is there at least one collectibles ?
    * [ ] Simply count how many `C` you find on the map.

All these checks can be made directly when you parse the map file. Now, if all these checks are ok, there's two more things you have to check on the map : is the exit accessible from the start position, and are all the collectibles accessible from the start position.

Remember that you have to collect all collectibles to unlock the exit, so if not all collectibles are accessible, the map is invalid.

The way that I checked that in my code is by using a sort of flood fill algorithm, starting on the start position. I check every tiles and what type they are, I update a counter each time the type of the tile is a collectible, same for the exit.

At the end I can easily check if the collectibles counter is equal to the number of collectibles that I found when parsing the map, if they are different, not all collectibles are accessible, thus the map is invalid.\
I do the same thing for the exit, if the exit counter is 0, this means the exit is inaccessible, thus the map is invalid.

An other way to check if the map is valid is to use a backtracking algorithm from the exit to the start position, and from all the collectibles to the start position. If any one of them couldn't reach the start position, the map is invalid.

### Game checklist

* [ ] Create a window using MiniLibX
  * [ ] Create the required structure to store all the necessary information
* [ ] Load all the required sprites (images) for your game and store them into memory
* [ ] Create the different hooks
  * [ ] key\_handler
  * [ ] mouse\_handler (if necessary)
  * [ ] close\_handler, this is a hook on the red cross that closes the program correctly
  * [ ] loop\_hook (=> you game loop)

### Render checklist

* [ ] Draw the background
* [ ] Draw the not movable parts of the map
* [ ] Draw the player

### Key handler

The key handler (at least in my game), is mainly used to call the update\_player\_position function when W, A, S or D is pressed or to close the program correctly when we press the ESC key.

There's some things you have to think about before updating the player position.

* [ ] Is the requested new position a Wall ?
  * [ ] if the new position is a Wall, don't do anything. The subject says that the player should not be able to go through walls
* [ ] Is the requested new position inside the map ?
  * [ ] if the new position is outside the map, don't do anything. Normally this shouldn't happen since the map is enclosed in walls but hey, never too sure.
* [ ] Is the requested new position a Collectible ?
  * [ ] if yes, update the collected items counter and check
    * [ ] check if all collectibles have been collected
      * [ ] if yes, unlock the exit
    * [ ] update your map 2D array and replace the collectible by a "floor" tile so that it is not drawn in the next iteration of the game loop.
* [ ] If the requested new position is not a wall, nor a collectible, nor outside the map, simply set the player position to the requested new position.

### Final word

You have to assemble all these checklist to get the game working, and adapt it to your style of coding. As said earlier, if you want to see some code, take a look at my Github and ask me questions.

That's basically all that you have to do to have a working game, but the big part is to find assets that fit the theme you want for your game.&#x20;

You can find a lot of free assets on [itch.io](https://itch.io/) (as said in the subject). You can also draw them yourself.&#x20;

You could use a program like [Aseprite](https://www.aseprite.org/) to draw some pixel art assets yourself, it's not free but it works great !
