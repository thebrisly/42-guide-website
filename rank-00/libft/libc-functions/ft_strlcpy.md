# ft\_strlcpy

### Subject

{% code overflow="wrap" %}
```
STRLCPY(3) (simplified)

NAME
    strlcpy -- size-bounded string copying
SYNOPSIS
    size_t strlcpy(char *dst, const char *src, size_t dstsize);
DESCRIPTION
    The strlcpy() function copy strings with the same input parameters and output result as snprintf(3). It is designed to be safer, more consistent, and less error prone replacement for the easily misused function strncpy(3)
    strlcpy() take the full size of the destination buffer and guarantee NUL-termination if there is room. Note that room for the NUL should be included in dstsize. Also note that strlcpy() only operate on true ''C'' strings. This means that for strlcpy() src must be NUL-terminated.
    strlcpy() copies up to dstsize - 1 characters from the string src to dst, NUL-terminating the result if dstsize is not 0.
    If the src and dst strings overlap, the behavior is undefined.
RETURN VALUES
    The strlcpy() function return the total length of the strings it tried to create. That means the length of src.
    If the return value is >= dstsize, the output string has been truncated.
    It is the caller's responsibility to handle this.
```
{% endcode %}

### Understandable explanation

What this function does is pretty simple in that it's made to copy one string to another but with a small catch, it **always** NUL-terminate the string.

If you give a `dstsize` long enough to NUL-terminate the string without truncating it, `strlcpy()` will simply copy the string, as you'd do with `strcpy()`. If you don't give a `dstsize` long enough, it will copy `dstsize - 1` characters from the source into the destination, adding the NUL-terminating character after that.

The `strlcpy()` function **always** returns the length of the string that it tried to create, this is the length of `src`, even if you have to truncate the string to NUL-terminate it.

### Hints

I implemented this the same way it is implemented in the Apple's C version. Check the sources for the link to the page.

{% code title="ft_strlcpy.c" overflow="wrap" lineNumbers="true" %}
```c
size_t	ft_strlcpy(char *dst, const char *src, size_t dstsize)
{
    /* get the length of src */
    /* check if dstsize is big enough to accomodate src length 
     * plus the NUL character
     */
    /* copy the whole src into dst */
    /* else */
    /* copy dstsize - 1 characters into dst */
    return (/* length of src */);
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_strlcpy</summary>

{% code title="ft_strlcpy.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

size_t    ft_strlcpy(char *dst, const char *src, size_t dstsize)
{
    size_t    src_len;
    
    /* getting the length of src with our ft_strlen function */
    src_len = ft_strlen(src);
    /* checking if dstsize is big enough to accomodate src_len plus
     * the terminating NUL character
     */
    if (src_len + 1 < dstsize)
        /* using ft_memcpy to copy the source into the destination */
        ft_memcpy(dst, src, src_len + 1);
    /* if dstsize is not big enough, we have to truncate the string
     * when copying it
     * note that we also check if dstsize is 0, if that is the case
     * we don't have to copy anything, so we just skip this part by
     * not entering the condition
     */
    else if (dstsize != 0)
    {
        /* we also use ft_memcpy, but instead of giving it
         * src_len + 1 as a maxsize, we give it dstsize - 1
         */
        ft_memcpy(dst, src, dstsize - 1);
        /* we then NUL-terminate the string */
        dst[dstsize - 1] = 0;
    }
    /* finally, we return the original length of the src */
    return (src_len);
}
```
{% endcode %}

</details>

### Sources

[Apple OpenSource strlcpy implementation](https://opensource.apple.com/source/xnu/xnu-4570.1.46/osfmk/arm/strlcpy.c.auto.html)
