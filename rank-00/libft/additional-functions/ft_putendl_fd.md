# ft\_putendl\_fd

### Subject

{% code overflow="wrap" %}
```
FT_PUTENDL_FD (simplified)

NAME
    ft_putendl_fd -- write a string on a specified file descriptor, follow by a newline
SYNOPSIS
    void ft_putendl_fd(char *s, int fd);
DESCRIPTION
    ft_putendl_fd() writes the string s, followed by a newline, on the file descriptor fd
PARAMETERS
    s: string to write
    fd: the file descriptor on which to write
RETURN VALUES
    ft_putendl_fd() does not return anything
AUTHORIZED EXTERNAL FUNCTIONS
    write(2)
```
{% endcode %}

### Understandable explanation

This one is pretty straight forward, if you already built the `ft_putstr_fd()` function, you can work it out by yourself I think. It works the same way, it just adds a `newline` character at the end.

### Hints

As said above, take a look at how you did `ft_putstr_fd()`, it should be fairly easy from there.

### Commented solution

<details>

<summary>ft_putendl_fd</summary>

{% code title="ft_putendl_fd.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void    ft_putendl_fd(char *str, int fd)
{
    int    i;
    
    i = 0;
    while (str[i])
    {
        write(fd, &str[i], 1);
        i++;
    }
    write(fd, "\n", 1);    
}
```
{% endcode %}

</details>
