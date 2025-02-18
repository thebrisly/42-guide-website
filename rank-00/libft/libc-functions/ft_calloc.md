# ft\_calloc

### Subject

{% code overflow="wrap" %}
```
CALLOC(3) (simplified)

NAME
    calloc -- memory allocation
SYNOPSIS
    void *calloc(size_t count, size_t size);
DESCRIPTION
    The calloc() function allocates memory.
    The allocated memory is aligned such that it can be used for any data type.
    The calloc() function contigously allocates enough space for count objects that are size bytes of memory each and returns a pointer to the allocated memory.
    The allocated memory is filled with bytes of value zero.
RETURN VALUES
    If successful, calloc() returns a pointer to allocated memory. If there is an error, they return a NULL pointer and set errno to ENOMEM.
```
{% endcode %}

### Understandable explanation

By now you should have understand what the `malloc()` function does, at least I hope. Otherwise, understand how `malloc()` works and come back here.\
I will mainly base my explanation on comparing `calloc()` to `malloc()`.

`calloc()` works in the same way as `malloc()` does, but the difference is that `calloc()` sets all the memory bytes are set to `0` instead of staying as the gibberish that was there in memory before we allocated it.

### Hints

{% code title="ft_calloc.c" overflow="wrap" lineNumbers="true" %}
```c
void *ft_calloc(size_t count, size_t size)
{
    /* declare a tmp unsigned char pointer */
    /* use malloc to allocate count * size in tmp */
    /* loop over tmp and set each byte to 0 */
    /* return tmp */
}
```
{% endcode %}

### Commented  solution

<details>

<summary>ft_calloc</summary>

{% code title="ft_calloc.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void *ft_calloc(size_t count, size_t size)
{
    unsigned char *tmp;
    size_t i;
    
    i = 0;
    /* allocating count * size bytes in memory with malloc */
    tmp = malloc(count * size);
    /* check if the memory was allocated */
    if (!tmp)
        return (NULL);
    /* loop over every allocated bytes and set it to 0 */
    while (i < count * size)
        tmp[i++] = 0;
    /* return the allocated memory */
    return (tmp);
}
```
{% endcode %}

</details>
