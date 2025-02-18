# ft\_memcmp

### Subject

{% code overflow="wrap" %}
```
MEMCMP(3) (simplified)

NAME
    memcmp -- compare byte string
SYNOPSIS
    int memcmp(const void *s1, const void *s2, size_t n)
DESCRIPTION
    The memcmp() function compares byte string s1 against byte string s2.
    Both strings are assumed to be n bytes long.
RETURN VALUES
    The memcmp() function returns zero if the two strings are identical, otherwise returns the difference betwee the first two differing bytes (treated as unsigned char values, so that '\200' is greater than '\0', for example).
    Zero-length strings are always identical. This behaviour is not required by C and portable code should only depend on the sign of the returned value.
```
{% endcode %}

### Understandable explanation

`memcmp()` compares byte strings. It works similarly to the `strncmp()` function.

The difference here is that `memcmp()` works with bytes strings so it take void pointers as parameter, plus a third character, representing, as said in the man, the assumed length of both strings. This means that `memcmp()` will not compare more than `n` bytes.

The return value depends on what difference is found.

If there is no difference between both strings, the return value will be 0.

If there is a difference, and the first different character in `s2` is greater than the character at the same place in `s1`, the returned result will be negative.

If there is a difference, and the first different character in `s2` is less than the character at the same place in `s1`, the returned result will be positive.

### Hints

{% code title="ft_memcmp.c" overflow="wrap" lineNumbers="true" %}
```c
int ft_memcmp(const void *s1, const void *s2, size_t n)
{
    /* loop over both strings until we reach n bytes */
    /* check if current s1 byte is different than current
     * s2 byte
     */
           /* if bytes are different, return the difference
            * between both characters
            */
     /* if we read both byte strings until n bytes and no difference
      * were found, return 0 as there is no difference
      */h2
}
```
{% endcode %}

## Commented solution

<details>

<summary>ft_memcmp</summary>

{% code title="ft_memcmp.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int ft_memcmp(const void *s1, const void *s2, size_t n)
{
    unsigned char *str1;
    unsigned char *str2;
    size_t i;
 
    /* converting s1 and s2 to unsigned char */   
    str1 = (unsigned char) *s1;
    str2 = (unsigned char) *s2;
    i = 0;
    /* same loop as strcmp */
    while (i < n)
    {
       /* check if current byte is different in both strings */
        if ((unsigned char) str1[i] != (unsigned char) str2[i])
            /* return the difference between both chars */
            return ((unsigned char) str1[i] - (unsigned char) str2[i]);
    }
    /* if we read through both strings completely and there
     * were no difference, we return 0
     */
    return (0);
}
```
{% endcode %}

</details>
