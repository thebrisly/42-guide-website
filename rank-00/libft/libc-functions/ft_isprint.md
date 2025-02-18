# ft\_isprint

### Subject

{% code overflow="wrap" %}
```
ISPRINT(3) (simplified)

NAME
    isprint -- printing character test (space character inclusive)
SYNOPSIS
    int isprint(int c)
DESCRIPTION
    The isprint() function tests for any printing character, including space. The value of the argument must representable as an unsigned char or the value of EOF.
RETURN VALUES
    The isprint() function returns zero if the character tests false and returns non-zero if the character tests true.
```
{% endcode %}

### Understandable explanation

For this function, the man is pretty self-explanatory, but I'll give more details (i.e. what are the printing characters).

The `isprint()` function returns a non-zero value if the character passed as an `int` parameter is a printing character.

If the character is not a printing character, the `isprint()` function returns `0`.

The printing characters are all character between decimal 32 and decimal 126.

### Hints

{% code title="ft_isprint.c" overflow="wrap" lineNumbers="true" %}
```c
int    ft_isprint(int c)
{
    if (/* c is between 32 and 126 */)
        return (/* non-zero value of your choice */);
    return (0);
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_isprint</summary>

{% code title="ft_isprint.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int    ft_isprint(int c)
{
    /* check if c is between decimal 32 and decimal 126 (inclusive) */
    if (c >= 32 && c <= 126)
        return (c); // if we reach this point, c will be a non-zero value.
    return (0);
}
```
{% endcode %}

</details>
