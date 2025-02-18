# ▪️ Building the thing

For this function, this won't be a step by step building because describing each step that you need to take to build the function is pretty hard.

I'll give you hints on what you have to do to achieve it.

### LIBFT functions

For this project,  I used some of the LIBFT functions you already know and built.

I won't tell you exactly where and when you need to use them, but I'll give you what functions I used, maybe it'll give you some ideas on where to start or will unlock you if you're stuck on something.

* FT\_STRCHR
* FT\_STRDUP
* FT\_STRLEN
* FT\_SUBSTR
* FT\_STRJOIN

### Additional functions

Apart from these 5 functions, I used 3 other functions :

* `char *get_next_line(int fd)`
* `char *_fill_line_buffer(int fd, char *left_c, char *buffer)`
* `char *_set_line(char *line_buffer)`

### Explaining the functions

Each of these 3 functions have a specific use in the project, I will here describe what each function does, this could give you an idea on what to do. Also, you'll see better where I could have used the LIBFT functions.

<details>

<summary><code>char *get_next_line(int fd)</code></summary>

The main function get\_next\_line mainly makes some check about the file descriptor and the different memory allocation that could go wrong.

Once all checks are done, it calls the `_fill_line_buffer` function to read in the file descriptor until it find a `\n` or `\0` character.

Once the line variable is filled, we free the buffer so we don't have any memory leaks, since it's not used after that.

Once the buffer is freed, we set the line with the `_set_line` function and we return the line, storing the return value of `_set_line` in a static variable so that next time we call the `get_next_line` function we have access to the first characters of the line that may have been read before.

i.e. our file contains `1\n234\0`, our `BUFFER_SIZE` is 4.\
The first time we'll read through the file we'll read `1\n23` so what we are going to store in our static variable is `23` because the next time we call the function on the same file descriptor it will start reading at the `4` character in the file.

</details>

<details>

<summary><code>char *_fill_line_buffer(int fd, char *left_c, char *buffer)</code></summary>

This function fills the `line` buffer.

It will read BUFFER\_SIZE characters in each iteration until there's a `\n` or `\0` character in the line buffer.

Each time through the loop, it will check if there is already data in the `left_c` buffer, if there is, it will append the new read characters to it. If not, it will duplicate the content of the read buffer into the `left_c` buffer.

If a `\n` is found, it will break out of the loop and return the `left_c` buffer after appending the read characters to it.

</details>

<details>

<summary><code>char *_set_line(char *line_buffer)</code></summary>

This function take the line buffer as parameter, it reads in it until a `\n` or `\0` character is found, meaning the end of a line, or the end of the file.

This function sets the `line_buffer` a `\0` at the end of the line inside of it and it returns a substring of the buffer from the end of the line, to the end of the buffer.\
This substring is returned as `left_c`.

</details>

These are the main functions for this project, I hope these explanation of what they each do in my project, can help you working on your own.

In the next part you'll find the complete commented code for these 3 functions. I won't explain the other functions because you should have already corrected them and understood them.&#x20;
