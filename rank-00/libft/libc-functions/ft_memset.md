# ft\_memset

### Subject

{% code overflow="wrap" %}
```
MEMSET(3) (simplified)

NAME
    memset -- fill a byte string with a byte value
SYNOPSIS
    void *memset(void *b, int c, size_t len);
DESCRIPTION
    The memset() function writes len bytes of value c (converted to an unsigned char) to the string b.
RETURN VALUES
    The memset() function returns its first argument.
```
{% endcode %}

### Understandable explanation

As the man description says, this function writes `len` bytes of value `c` to the string `b`.

The value of `c` will be converted to an `unsigned char`, so to set this value in the `b` string, we'll have to convert the `b` string to a pointer to `unsigned char`. But remember the return value, we have to return the first parameter of the function, the `void *b` string.&#x20;

So how do we convert this parameter without changing the original one ? Think about temporary variables.

### Hints

To build this function, we'll have to declare a temporary variable, an `unsigned char *`. We'll then make all our manipulation on this pointer, without touching the original `void *b` string.

{% code title="ft_memset.c" overflow="wrap" lineNumbers="true" %}
```c
void    *ft_memset(void *b, int c, size_t len)
{
    /* declare a temporary unsigned char * */
    /* make this temporary variable equals to void *b converted to unsigned char */
    /* loop on the temporary variable while we didn't reach len */
        /* in that loop, set the current byte equal to c converted to unsigned char */
    /* return void *b */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_memset</summary>

{% code title="ft_memset.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void    *ft_memset(void *b, int c, size_t len)
{
    /* declaring our temporary pointer */
    unsigned char    *tmp_ptr;
    
    /* making our temporary pointer equal to b converted to unsigned char * */
    tmp_ptr = (unsigned char *) b;
    /* looping on our temporary pointer while we didn't reach len */
    while (len > 0)
    {
    /* assigning the unsigned char value of c to the current byte in our temporary pointer */
        *(tmp_ptr++) = (unsigned char) c;
        /* reducing the len by one so we only set len bytes */
        len--;
    }
    /* return the function's first parameter, void *b */
    return (b);
}
```
{% endcode %}

</details>
