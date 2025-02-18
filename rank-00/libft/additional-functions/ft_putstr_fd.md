# ft\_putstr\_fd

### Subject

```
FT_PUTSTR_FD (simplified)

NAME
    ft_putstr_fd -- write a string on a specified file descriptor
SYNOPSIS
    void ft_putstr_fd(char *s, int fd);
DESCRIPTION
    Write the string s on the file descriptor fd.
PARAMETERS
    s: string to write
    fd: file descriptor on which to write
RETURN VALUES
    ft_putstr_fd() does not return anything
AUTHORIZED EXTERNAL FUNCTIONS
    write(2)
```

### Understandable explanation

This one is pretty straight forward, you already know how to write the `ft_putstr()` function, if you don't remember, look back at what you did during your Piscine.

### Hints

Take a look at the man for the `write(2)` function, the first parameter is... you guessed it ! A file descriptor, so I mean, do you really need to have the code for this ?

I hope you can figure it out.

### Commented solution

<details>

<summary>ft_putstr_fd</summary>

{% code title="ft_putstr_fd.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void    ft_putstr_fd(char *str, int fd)
{
    int i;
    
    i = 0;
    while (str[i])
    {
        write(fd, &str[i], 1);
        i++;
    }
}
```
{% endcode %}

</details>
