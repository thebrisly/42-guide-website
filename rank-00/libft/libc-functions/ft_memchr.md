# ft\_memchr

### Subject

{% code overflow="wrap" %}
```
MEMCHR(3) (simplified)

NAME
    memchr -- locate byte in byte string
SYNOPSIS
    void *memchr(const void *s, int c, size_t n);
DESCRIPTION
    the memchr() function locates the first occurence of c (convered to an unsigned char) in string s.
RETURN VALUES
    The memchr() function returns a pointer to the byte located, or NULL if no such byte exists within n bytes.
```
{% endcode %}

### Understandable explanation

The `memchr()` function works similarly as the `strchr()` function, the difference is that `memchr()` works with byte string (`void *`) where `strchr()` works with 'litteral' strings (`char *`).

This means we can send whatever type of data we want to `memchr()` and it'll still work.

`memchr()` also has a third parameter, `n`. This parameter tells the function how many bytes we want to search in. We need this parameter since `s` is not a 'litteral' string, it doesn't have a NUL-terminating character. If we didn't have this parameter, we would be reading a random number of bytes each time.

### Hints

{% code title="ft_memchr.c" overflow="wrap" lineNumbers="true" %}
```c
void *ft_memchr(const void *s, int c, size_t n)
{
    /* as said in the man, the search is done for c converted to
     * an unsigned char, so we have to convert both c and s to 
     * unsigned char
     */
    /* loop over the byte string until our counter is equal to n */
    /* compare the current byte to c */
        /* if they are the same, return the address of this byte as a
         * void *
         */
    /* if we searched n bytes and didn't find what we were looking for
     * return NULL
     */
    /* as you can see, this is very close to the strchr and strrchr
     * functions, so take a look at these before looking at the
     * solution
     */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_memchr.c</summary>

{% code title="ft_memchr.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void *ft_memchr(const void *s, int c, size_t n)
{
    unsigned char *str;
    size_t i;
    unsigned char uc;
    
    /* converting both s and c to unsigned char */
    str = (unsigned char *) s;
    uc (unsigned char) c;
    i = 0;
    /* looping over n bytes */
    while (i < n)
    {
        /* same check as strchr */
        if (str[i] == uc)
            /* there, we return a void pointer instead
             * of the char pointer we returned in strchr
             */
            return ((void *) &str[i]);
        i++;
    }
    /* if we reached this point, we didn't find any occurence
     * of c in n bytes, so we return NULL
     */
    return (NULL);
}
```
{% endcode %}

</details>
