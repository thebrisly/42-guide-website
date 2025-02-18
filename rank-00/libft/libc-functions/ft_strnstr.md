# ft\_strnstr

### Subject

{% code overflow="wrap" %}
```
STRNSTR(3) (simplified)

NAME
    strnstr -- locate a substring in a string
SYNOPSIS
    char *strnstr(const char *haystack, const char *needle, size_t len);
DESCRIPTION
    The strnstr() function locates the first occurence of the null-terminated string needle in the string haystack, where not more than len characters are searched.
    Characters that appear after a '\0' character are not searched.
RETURN VALUES
    If needle is an empty string, haystack is returned; if needle occurs nowhere in haystack, NULL is returned; otherwise a pointer to the first character of the first occurence of needle is returned.
```
{% endcode %}

### Understandable explanation

The `strnstr()` function works in the same way as `strchr()` but searches for a complete substring in max `n` characters instead of a single character.

### Hints

{% code title="ft_strnstr.c" overflow="wrap" lineNumbers="true" %}
```c
char *ft_strnst(const char *haystack, const char *needle, size_t len)
{
    /* check if needle is empty */
        /* return haystack */
    /* loop over haystack */
        /* while current character of haystack is equal to the corresponding
         * character in needle */
             /* check if we have the complete needle */
}
```
{% endcode %}

I can also tell you that you'll need two different counters.

### Commented solution

<details>

<summary>ft_strnstr</summary>

{% code title="ft_strnstr.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

char *ft_strnstr(const char *haystack, const char *needle, size_t len)
{
    size_t i;
    size_t j;
    
    i = 0;
    j = 0;
    /* checking if needle is empty */
    if (needle[0] == 0)
        return ((char *) haystack);
    /* loop over haystack while we haven't looped over the whole
     * thing or until i = len
     */
    while (haystack[i] && i < len)
    {
        /* inside this first while loop
         * we are looping over the haystack as long as 
         * the current character is the correct character
         * in the needle
         */
        while (haystack[i + j] == needle[j] && haystack[i + j] && i + j < len)
        {
            /* we are inside this loop while the current
             * haystack character is the correct character in the 
             * needle so we just increment j to offset our haystack
             */
            j++;
            /* if needle[j] == 0, this means we read the whole
             * needle, so we found it in the haystack
             * we can return a pointer to the first character of
             * the needle
             * that why we used 2 counters, now we can offset our 
             * haystack pointer by i, which is the position of the
             * first character of the needle
             */
            if (needle[j] == 0)
                return ((char *) haystack + i);
        }
        i++;
        /* don't forget to set j to 0 again, otherwise you will
         * be offsetted in the needle beginning from the second
         * haystack character
         */
        j = 0;
    }
    return (0);
}
```
{% endcode %}

</details>
