# ft\_toupper

### Subject

{% code overflow="wrap" %}
```
TOUPPER(3) (simplified)

NAME
    toupper -- lower case to upper case letter conversion
SYNOPSIS
    int toupper(int c);
DESCRIPTION
    The toupper() function converts a lower-case letter to the corresponding upper-case letter. The argument must be representable as an unsigned char or the value of EOF.
RETURN VALUES
    If the argument is a lower-case letter, the toupper() function returns the corresponding upper-casse letter if there is one; otherwise, the argument is returned unchanged.
```
{% endcode %}

### Understandable explanation

I don't think I'll need to explain with more details what this function does, the man is pretty self-explanatory on this point.

### Hints

{% code title="ft_toupper.c" overflow="wrap" lineNumbers="true" %}
```c
int    ft_toupper(int c)
{
    if (/* c is lower-case letter */)
        return (/* corresponding upper-case letter */);
    return (c);
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_toupper</summary>

{% code title="ft_toupper.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int    ft_toupper(int c)
{
    /* this checks if the character is a lower-case letter
     * with the decimal ASCII values (97 => a; 122 => z)
     */
    if (c >= 97 && c <= 122)
        /* in the ASCII table, upper-case letter are indexed 32 
         * less than lower-case letter, so to get the corresponding
         * upper-case letter, we substract 32 to the lower-case
         * letter
         */
        return (c - 32);
    /* As said in the man, if the character is not a lower-case
     * letter, the argument is returned unchanged, that's why we
     * return c directly
     */
    return (c);
}
```
{% endcode %}

</details>
