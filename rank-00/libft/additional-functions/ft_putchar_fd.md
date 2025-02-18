# ft\_putchar\_fd

### Subject

{% code overflow="wrap" %}
```
FT_PUTCHAR_FD (simplified)

NAME
    ft_putchar_fd -- write character c on a specified file descriptor
SYNOPSIS
    void ft_putchar_fd(char c, int fd);
DESCRIPTION
    The ft_putchar_fd() function writes the character c on the file descriptor fd.
PARAMETERS
    c: character to write
    fd: file descriptor on which to write
RETURN VALUES
    ft_putchar_fd() does not return anything.
AUTHORIZED EXTERNAL FUNCTIONS
    write(2)
```
{% endcode %}

### Understandable explanation

This one is pretty straight forward, you already know how to write the `ft_putchar()` function, if you don't remember, look back at what you did during your Piscine.

### Hints

Take a look at the man for the `write(2)` function, the first parameter is... you guessed it ! A file descriptor, so I mean, do you really need to have the code for this ?

I hope you can figure it out.

### Commented solutions

<details>

<summary>ft_putchar_fd</summary>

{% code title="ft_putchar_fd.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void    ft_putchar_fd(char c, int fd)
{
    /* first parameter is the file descriptor
     * second parameter is the address to the character
     */
    write(fd, &c, 1);
}
```
{% endcode %}

</details>
