# ft\_memcpy

### Subject

{% code overflow="wrap" %}
```
MEMCPY(3) (simplified)

NAME
    memcpy -- copy memory area
SYNOPSIS
    void *memcpy(void *dst, const void *src, size_t n);
DESCRIPTION
    The memcpy() function copies n bytes from memory area src to memory area dst. If dstt and src overlap, behavior is undefined. Applications in which dst and src might overlap should use memove(3) instead.
RETURN VALUES
    The memcpy() function returns the original value of dst
```
{% endcode %}

### Understandable explanation

The `memcpy` function copies maximum n bytes from `src` to `dst`. The man talks about memory overlapping, I'll explain this with details on the `memmove` function page.

As for `memset` and `bzero` we'll need some temporary pointers to manipulate our data.

This functions works like the `strcpy` function, except that `memcpy` accepts `void *` as parameters, so we can give it any type of pointer we want to copy.

### Hints

{% code title="ft_memcpy.c" overflow="wrap" lineNumbers="true" %}
```c
void    *ft_memcpy(void *dst, const void *src, size_t n)
{
    /* declare a temporary pointer for dst */
    /* declare a temporary pointer for src */
    
    /* if src and dst are NULL, return dst */
    /* make dst tmp pointer equal to dst converted to unsigned char * */
    /* make src tmp pointer equal to src converted to unsigned char * */
    /* loop over the dst tmp pointer while we didn't reach n */
        /* set the current byte of dst tmp pointer equal to current byte of src tmp pointer */
        /* return dst */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_memcpy</summary>

{% code title="ft_memcpy.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void    *ft_memcpy(void *dst, const void *src, size_t n)
{
    /* declaring both our temporary pointers */
    unsigned char    *tmp_dst;
    unsigned char    *tmp_src;
    
    /* if both dst and src are NULL pointers we can directly return
     * dst since we won't do anything on it
     */
    if (dst == (void *)0 && src == (void *)0)
        return (dst);
    /* assigning both our temporary pointers to the converted
     * values of the "real" pointers
     */
    tmp_dst = (unsigned char *) dst;
    tmp_src = (unsigned char *) src;
    /* looping on both our temporary pointer until we reach 
     * n bytes
     */
    while (n > 0)
    {
        /* making current byte of tmp_dst = current byte of
         * tmp_src 
         */
        *(tmp_dst++) = *(tmp_src++);
        /* reducing n by one so we only copy n bytes */
        n--;
    }
    /* returning original dst, not our temporary pointer */
    return (dst);
}
```
{% endcode %}

</details>
