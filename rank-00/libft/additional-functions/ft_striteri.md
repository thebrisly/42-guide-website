# ft\_striteri

### Subject

{% code overflow="wrap" %}
```
FT_STRITERI (simplified)

NAME
    ft_striteri -- apply a function to each character of a string (index specified)
SYNOPSIS
    void ft_striteri(char *s, void (*f)(unsigned int, char*));
DESCRIPTION
    Apply the function 'f' to each characters of the string 's', passing its index as a first parameter.
    Each character is transmitted by address to 'f' so it can be modified if necessary.
```
{% endcode %}

### Understandable explanation

`ft_striteri` works the same way as `ft_strmapi` does, take a look at the explanation for `ft_strmapi` and then come back here.

The difference between `ft_striteri` and `ft_strmapi` is that `ft_striteri` doesn't return anything and works directly on the original string.

### Hints

This functions takes two parameters, the first one is a string, and the second one is a function.

What `ft_striteri` does is apply the function `f` to every character of the string `s`.

It passes the index of the character in the string, and a pointer to the character to the function `f`.

The function `f` directly modifies the value of the character in the original string.

At the end, we don't need to return anything but the original string will have been modified.

### Commented solution

<details>

<summary>ft_striteri</summary>

{% code title="ft_striteri.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void ft_striteri(char *s, void (*f)(unsigned int, char*))
{
    unsigned int i;
    
    i = 0;
    /* looping over the whole original string */
    while (s[i])
    {
        /* apply the function f to the character at index i
         * passing i and the address to s[i] as parameter to f
         * f will update the original string directly
         */
        (*f)(i, &s[i]);
        i++;
    }
}
```
{% endcode %}

</details>
