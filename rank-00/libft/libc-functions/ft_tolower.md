# ft\_tolower

### Subject

{% code overflow="wrap" %}
```
TOLOWER(3) (simplified)

NAME
    tolower -- upper case to lower case letter conversion
SYNOPSIS
    int tolower(int c);
DESCRIPTION
    The tolower() function converts an upper-case letter to the corresponding lower-case letter. The argument must be representable as an unsigned char or the value of EOF.
RETURN VALUES
    If the argument is an upper-case letter, the tolower() function returns the corresponding lower-case letter if there is one; otherwise, the argument is returned unchanged.
```
{% endcode %}

### Understandable explanation

I don't think I'll need to explain with more details what this function does, the man is pretty self-explanatory on this point.

### Hints

{% code title="ft_tolower.c" overflow="wrap" lineNumbers="true" %}
```c
int    ft_tolower(int c)
{
    if (/* c is an upper-case letter */)
        return (/* corresponding lower-case letter */);
    return (c);
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_tolower</summary>

{% code title="ft_tolower.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int    ft_tolower(int c)
{
    /* this checks if the character is an upper-case letter
     * with the decimal ASCII values (65 => A; 90 => Z)
     */
    if (c >= 65 && c <= 90)
        /* In the ASCII table, upper-case letters are indexed 32
         * less than lower-case letters, so to get the
         * corresponding lower-case letter, we add 32 to the
         * upper-case letter
         */
        return (c + 32);
    /* As said in the man, if the character is not an upper-case
     * letter, the argument is returned unchanged, that's why we 
     * return c directly
     */
    return (c);
}
```
{% endcode %}

</details>
