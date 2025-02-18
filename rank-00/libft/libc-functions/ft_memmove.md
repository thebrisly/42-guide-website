# ft\_memmove

### Subject

{% code overflow="wrap" %}
```
MEMMOVE(3) (simplified)

NAME
    memmove -- copy byte string
SYNOPSIS
    void *memmove(void *dst, const void *src, size_t len);
DESCRIPTION
    The memmove() function copies len bytes from string src to string dst.
    The two strings may overlap; the copy is always done in a non-destructive manner.
RETURN VALUES
    The memmove() function returns the original value of dst.
```
{% endcode %}

### Understandable explanation

The `memmove()` function does the same thing as the `memcpy()` function but this time, the copy is made, as said in the man, in a non-destructive manner. This means that both strings (src and dst) can overlap in memory and this function does not overwrite part of, or the entirety of the string when making the copy.

#### What is memory overlapping ?

I found a really good explanation on [stackexchange.com](https://cs50.stackexchange.com/questions/14615/memory-overlap-in-c) so I'll copy it here to explain what is memory overlapping.

> Suppose we have an array of 5 chars, where each char is a byte long
>
> ```bash
> +++++++++++++++++++++++++++++++
> | 'a' | 'b' | 'c' | 'd' | 'e' |
> +++++++++++++++++++++++++++++++
>  0x100 0x101 0x102 0x103 0x104
> ```
>
> Now according to the man page of `memcpy`, it takes 3 arguments, a pointer to the destination block of memory, a pointer to the source block of memory, and the size of bytes to be copied.
>
> What if the destination is `0x102`, the source is `0x100` and the size is `3` ?\
> Memory overlapping happens here. That is, `0x100` would be copied into `0x102`, `0x101` would be copied into `0x103` and `0x102` would be copied into `0x104`.
>
> Notice that we first copied into `0x102` then we copied from `0x102` which means that the value which was originally in `0x102` was lost as we overwrote it with the value we copied into `0x102` before we copy from it. So we would end up with something like
>
> ```bash
> +++++++++++++++++++++++++++++++
> | 'a' | 'b' | 'a' | 'b' | 'a' |
> +++++++++++++++++++++++++++++++
>  0x100 0x101 0x102 0x103 0x104
> ```
>
> Instead of
>
> ```bash
> +++++++++++++++++++++++++++++++
> | 'a' | 'b' | 'a' | 'b' | 'c' |
> +++++++++++++++++++++++++++++++
>  0x100 0x101 0x102 0x103 0x104
> ```
>
> How does a function like `memmove` take care of memory overlapping ?
>
> According to its man page, it first copies the bytes to be copied into a temporary array then pastes them into the destination block as oppose to a function like `memcpy` which copies directly from the source block to the destination block.

That's for memory overlapping, it is also said that `memmove` copies the bytes to be copied into a temporary array then pastes them into the destination block. That's not the way I did it because as said in the subject of the LIBFT, we can't use `malloc()` for this function.

The way I did it without using `malloc()`, is to first check if the 2 memory blocks are overlapping or not. If they are overlapping we'll copy from the end of the source memory block until the start. If they are not overlapping we'll copy "normally", from start to end.

### Hints

ft\_memmove

{% code title="ft_memmove.c" overflow="wrap" lineNumbers="true" %}
```c
void    *ft_memmove(void *dst, const void *src, size_t len)
{
    /* declare 2 temporary pointer for src and dst */
    /* declare a counter */
    /* check if both src and dst are NULL */
    /* make dst tmp pointer equal to dst converted to char * */
    /* make src tmp pointer equal to src converted to char * */
    /* if src and dst are overlapping */
        /* loop while len is greater than 0 and copy src into dst */
    /* if src and dst are not overlapping */
        /* loop while our counter is less than len and copy src into dst */
    /* return dst */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_memmove</summary>

{% code title="ft_memmove.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void    *ft_memmove(void *dst, const void *src, size_t len)
{
    /* declaring our 2 temporary pointers and our counter */
    char    *c_src;
    char    *c_dst;
    size_t    i;
    
    /* if both src and dst are NULL, we directly return NULL */
    if (!dst && !src)
        return (NULL);
    /* assigning the converted values of src and dst to our temporary 
     * pointers so that we don't touch the original values
     */
    c_src = (char *) src;
    c_dst = (char *) dst;
    i = 0;
    /* checking if the address of the destination is greater than the
     * address of the source, if that's the case we'll copy from end to
     * start
     */ 
    if (c_dst > c_src)
        while (len-- > 0)
            c_dst[len] = c_src[len];
    /* if the address of the destination is not greater than the address
     * of the source, we'll copy from start to end, like we're used to
     */
    else
    {
        while (i++ < len)
            c_dst[i] = c_src[i];
    }
    return (dst);
}
```
{% endcode %}



</details>
