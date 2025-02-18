# ft\_isdigit

### Subject

{% code overflow="wrap" %}
```
ISDIGIT(3) (simplified)

NAME
    isdigit -- decimal-digit character test
SYNOPSIS
    int isdigit(int c)
DESCRIPTION
    The isdigit() function tests for a decimal digit character.
    The value of the argument must be representable as an unsigned char or the value of EOF.
RETURN VALUES
    The isdigit() function return zero if the character tests false and return non-zero if the character tests true.
```
{% endcode %}

### Understandable explanation

For this function, the man is self-explanatory, but I'll still explain it in other words.

The `isdigit()` function return a non-zero value if the character passed as an `int` parameter is a decimal digit character (0 - 9).

If the character is not a decimal digit character, the `isdigit()` function return `0`.

### Hints

{% code title="ft_isdigit.c" overflow="wrap" lineNumbers="true" %}
```c
int    ft_isdigit(int c)
{
    if (/* c value is one of the decimal digit characters in the ASCII table */)
        return (/* non-zero value of your choice */);
    return (0);
}
```
{% endcode %}

### Commented solution

{% hint style="danger" %}
Come on ! You really need the code for that function ?
{% endhint %}

<details>

<summary>ft_isdigit</summary>

{% code title="ft_isdigit.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int    ft_isdigit(int c)
{
    /* this checks the character against the ASCII table if c is a decimal digit */
    if (c >= 48 && c <= 57)
        return (c); // here I'm returning c, as if it's a decimal digit it'll be non-zero
    return (0); // if we reach this point, c isn't a decimal digit
}
```
{% endcode %}

</details>
