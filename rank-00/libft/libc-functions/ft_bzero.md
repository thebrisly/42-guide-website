# ft\_bzero

### Subject

{% code overflow="wrap" %}
```
BZERO(3) (simplified)

NAME
    bzero -- write zeroes to a bye string
SYNOPSIS
    void bzero(void *s, size_t n);
DESCRIPTION
    The bzero() function writes n zeroed bytes to the string s. If n is zero, bzero() does nothing.
```
{% endcode %}

### Understandable explanation

This function works the same way as the `memset()` function, except you don't have to specify what character to write, it'll always be `0` (`NUL` character).

This function does not return anything and if the number of characters to write you passed as `size_t n` is `0`, `bzero` does nothing.

### Hints

{% code title="ft_bzero.c" overflow="wrap" lineNumbers="true" %}
```c
void    ft_bzero(void *s, size_t n)
{
    /* declare a temporary pointer */
    /* make the temporary pointer equal to *s converted to a char * */
    /* loop on the temporary pointer while we didn't reach n characters */
        /* in that loop, set the current byte equal to 0 */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_bzero</summary>

{% code title="ft_bzero.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void    ft_bzero(void *s, size_t n)
{
    /* declaring our temporary pointer */
    char    *tmp_ptr;
    
    /* making our temporary pointer equal to b converted to char * */
    tmp_ptr = (char *) s;
    /* looping on our temporary pointer while we didn't reach n */
    while (n > 0)
    {
        /* assigning 0 to the current byte in our temporary pointer */
        *(tmp_ptr++) = 0;
        /* reducing the n by one so we only set n bytes to 0 */
         n--;
    }
}
```
{% endcode %}

</details>
