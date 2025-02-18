# ft\_strlcat

### Subject

{% code overflow="wrap" %}
```
STRLCAT(3) (simplified)

NAME
    strlcat -- size-bounded string concatenation
SYNOPSIS
    size_t strlcat(char *dst, const char *src, size_t dstsize);
DESCRIPTION
    The strlcat() function concatenate strings with the same input parameters and outuput result as snprintf(3). It is designed to be safer, more consistent, and less error prone replacements for the easily misused function strncat(3).
    strlcat() take the full size of the destination buffer and guarantee NUL-termination if there is room. Note that room for the NUL should be included in dstsize. Also note that strlcat() only operate on true ''C'' strings. This means that both src and dst must be NUL-terminated.
    strlcat() appends string src to the end of dst. It will append at most dstsize - strlen(dst) - 1 characters. It will then NUL-terminate, unless dstsize is 0 or the original dst string was longer than dstsize (in practice this should not happen as it means that either dstsize is incorrect or that dst is not a proper string).
    If the src and dst strings overlap, the behavior is undefinded.
RETURN VALUES
    Like snprintf(3), strlcat() function return the total length of the string it tried to create. That means the initial length of dst plus the length of src.
    If the return value is >= dstsize, the output string has been truncated.
    It is the caller's responsibility to handle this.
```
{% endcode %}

### Understandable explanation

What this function does is pretty simple in that it's made to concatenate two strings but with a small catch, it **always** NUL-terminate the string.

If you give a `dstsize` long enough to NUL-terminate the resulting concatenated string without truncating it, `strlcat()` will simply concatenate the two string, as you'd do with `strcat()`. If you don't give a `dstsize` long enough, it will concatenate `dstsize - strlen(dst) - 1` characters, adding the NUL-terminating character after that.

The `strlcat()` function **always** returns the length of the string it tried to create, this is the original length of `dst` plus the original length of `src`, even if you have to truncate the string to NUL-terminate it.

### Hints

I implemented this the same way it is implemented in the Apple's C version. Check the sources for the link to the page.

{% code title="ft_strlcat.c" overflow="wrap" lineNumbers="true" %}
```c
size_t	ft_strlcat(char *dst, const char *src, size_t dstsize)
{
    /* get the original length of src */
    /* get the original length of dst */
    /* if the length of dst is equal to dstsize */
    /* simply return the the length of dst + the length of src */
    /* if dstsize is big enough to accomodate both src and dst */
    /* concatenate src at the end of dst */
    /* else, concatenate dstsize character maximum */
    return (/* length of src + length of dst */);
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_strlcat</summary>

{% code title="ft_strlcat.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

size_t	ft_strlcat(char *dst, const char *src, size_t dstsize)
{
    size_t    src_len;
    size_t    dst_len;
    
    /* getting the original lenth of src and dst */
    src_len = ft_strlen(src);
    dst_len = ft_strlen(dst);
    /* this check can be ommited if you implement the strnlen function */
    if (dst_len >= dstsize)
        dst_len = dstsize;
    /* if the dst_len is equal to dst_size
     * this means that we don't need to concatenate anything since
     * the dst already contains the maximum number of characters
     */
    if (dst_len == dstsize)
        return (dstsize + src_len);
    /* if dstsize is big enough to accomodate both src and dst */
    if (src_len < dstsize - dst_len)
    /* we used ft_memcpy again, since it works directly on memory
     * addresses, we can offset the pointer of dst by dst_len so our
     * dst pointer is now set at the end of dst, then we tell ft_memcpy to
     * copy the content of src there for a maximum of src_len + 1
     * character
     */
        ft_memcpy(dst + dst_len, src, src_len + 1);
    else
    {
    /* in this case, we do the same thing as above, we offset the dst 
     * pointer by dst_len and then we copy src there
     * this time, we copy dstsize - dst_len - 1 character
     */
        ft_memcpy(dst + dst_len, src, dstsize - dst_len - 1);
    /* as with ft_strlcpy, we then NUL-terminate the string */
        dst[dstsize - 1] = '\0';
    }
    /* finally, we return the original length of src + dst */
    return (dst_len + src_len);
}
```
{% endcode %}

</details>

### Sources

[Apple OpenSource strlcat implementation](https://opensource.apple.com/source/Libc/Libc-997.1.1/string/strlcat.c.auto.html)
