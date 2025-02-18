# ft\_strjoin

### Subject

{% code overflow="wrap" %}
```
FT_STRJOIN (simplified)

NAME
    ft_strjoin -- concatenate 2 strings in a new string
SYNOPSIS
    char *ft_strjoin(const char *s1, const char *s2);
DESCRIPTION
    Allocate (with malloc(3)) and returns a new string resulting from the concatenation of s1 and s2.
PARAMETERS
    s1: prefix string
    s2: suffix string
RETURN VALUES
    ft_strjoin() returns the new string; NULL if the memory allocation failed.
AUTHORIZED EXTERNAL FUNCTIONS
    malloc(3)
```
{% endcode %}

### Understandable explanation

This function works basically the same way as `ft_strlcat` does, but instead of passing it a `destination` `string` that has to be correctly allocated as a parameter, we only pass two `strings` and `ft_strjoin` will allocate the required memory for both of them plus the NUL-terminating character.

`s1` will be the first string in the result, `s2` the second one.

### Hints

We have to get the length of both strings so we can allocate enough memory for both of them.

So that's the first thing to do. Then we can allocate enough memory for both string plus the NUL-terminating character.

We then copy `s1` into our newly allocated string, then we copy `s2`, and finally we can set the last character as `NUL`.

### Commented solution

<details>

<summary>ft_strjoin</summary>

{% code title="ft_strjoin.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

char *ft_strjoin(const char *s1, const char *s2)
{
    char *res;
    int i;
    int j;
    
    i = 0;
    j = 0;
    /* allocating the required memory */
    res = (char *) malloc((ft_strlen(s1) + ft_strlen(s2) + 1) * sizeof(char));
    if (!res)
        return (NULL);
    /* copying s1 into our res string */
    while (s1[i])
        res[j++] = s1[i++];
    /* we have to reset i to 0, otherwise we won't copy s2
     * from the start
     */
    i = 0;
    /* copying s2 into our res string */
    while (s2[i])
        res[j++] = s2[i];
    /* !! don't forget to NUL-terminate the string !! */
    res[j] = 0;
    /* finallly, we can return the new string */
    return (res);
}
```
{% endcode %}

</details>
