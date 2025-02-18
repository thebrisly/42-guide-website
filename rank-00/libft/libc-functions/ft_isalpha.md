# ft\_isalpha

### Subject

{% code overflow="wrap" %}
```
ISALPHA(3) (simplified)

NAME
    isalpha -- alphabetic character test
SYNOPSIS
    int isalpha(int c)
DECRIPTION
    The isalpha() function tests for any character for which isupper(3) or islower(3) is true. The value of the argument must be resprensentable as an unsigned char or the value of EOF.

RETURN VALUES
    The isalpha() function return zero if the character tests false and returns non-zero if the character tests true.
```
{% endcode %}

### Understandable explanation

For this function, the man is self-explanatory, but I'll still explain it in other words.

The `isalpha()` function returns a non-zero value if the character passed as an `int` parameter is an alphabetical letter (lowercase or uppercase).

If the character is not alphabetical, the `isalpha()` function returns `0`.

### Hints

{% code title="ft_isalpha.c" overflow="wrap" lineNumbers="true" %}
```c
int    ft_isalpha(int c)
{
    if (/* c value is one of the lowercase letter in the ASCII table  or if c value is one the uppercase letter in the ASCII table*/)
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

<summary>ft_isalpha</summary>

{% code title="ft_isalpha.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int    ft_isalpha(int c)
{
    /* the first part of the condition checks if c is uppercase */
    /* the second part of the condition checks if c is lowercase */
    if ((c >= 65 && c <= 90) || (c >= 97 && <= 122))
        return (c); // here I'm returning c, as if it's alphabetical it'll be non-zero
    return (0); // if we reach this point, c isn't alphabetical
}
```
{% endcode %}



</details>
