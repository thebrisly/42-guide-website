# ft\_isascii

### Subject

{% code overflow="wrap" %}
```
ISASCII(3) (simplified)

NAME
    isascii -- test for ASCII character
SYNOPSIS
    int isascii(int c)
DESCRIPTION
    The isascii() function tests for an ASCII character, which is any character between 0 and octal 0177 inclusive.
```
{% endcode %}

### Understandable explanation

For this function, the man is self-explanatory, even though it doesn't tell you what the return values are...

The `isascii()` function returns a non-zero value if the character passed as an `int` parameter is an ASCII character between 0 and octal 0177, this means characters between 0 and decimal 127, all characters displayed when you type the `man ascii` command.

If the character is not an ASCII character between 0 and octal 0177, the `isascii()` function return `0`.

### Hints

{% code title="ft_isascii.c" overflow="wrap" lineNumbers="true" %}
```c
int    ft_isascii(int c)
{
    if (/* c is between 0 and decimal 127 */)
        return (/* non-zero value of your choice */);
    return (0);
}
```
{% endcode %}

### Commente solution

{% hint style="warning" %}
This works mostly like the 3 other ones we built, there's a little catch though.
{% endhint %}

<details>

<summary>ft_isascii</summary>

{% code title="ft_isascii" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int    ft_isascii(int c)
{
    /* checking if c is between 0 and decimal 127 */
    if (c >= 0 && c <= 127)
        return (1);
    /* Note that I didn't return c for this one */
    /* why ? if the value of c is 0, this function as to return a non-zero value too, so we can't return c */
    return (0);
}
```
{% endcode %}

</details>
