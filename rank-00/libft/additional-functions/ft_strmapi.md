# ft\_strmapi

### Subject

{% code overflow="wrap" %}
```
FT_STRMAPI() (simplified)

NAME
    ft_strmapi -- apply a function to each character of a string
SYNOPSIS
    char *ft_strmapi(const char *s, char (*f)(unsigned int, char));
DESCRIPTION
    Apply the function 'f' to each characters in the string 's' to create a new string (with malloc(3)) resulting of the successive applications of 'f'.
PARAMETERS
    s: string over which to iterate
    f: function to apply to each character
RETURN VALUES
    ft_strmapi() returns a new string resulting of the successive applications of 'f'; NULL if the memory allocations failed.
AUTHORIZED EXTERNAL FUNCTIONS
    malloc(3)
```
{% endcode %}

### Understandable explanation

This functions takes two parameters, the first one is a string, and the second one is a function.

What `ft_strmapi` does is apply the function `f` to every character of the string `s`.

It passes the index of the character in the string, and the character to the function `f`.

The result of the function `f` is placed in the new string at index `i`.

At the end, we return the new string resulting of the application of `f` on every character of the string.

### Hints

First, we have to allocate enough memory for the whole string plus one for the NUL-terminating character.

Then we can loop over the string `s`, and call the function `f` on each character of `s`.

### Commented solution

<details>

<summary>ft_strmapi</summary>

{% code title="ft_strmapi.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

char *ft_strmapi(const char *s, char (*f)(unsigned int, char))
{
    unsigned int i;
    char *res;
    
    /* allocating the memory for the new string */
    res = malloc((ft_strlen(s) + 1) * sizeof(char));
    if (!res)
        return (NULL);
    i = 0;
    /* looping over the whole string s */
    while (i < ft_strlen(s))
    {
        /* applying the function f to each character of s
         * and storing the result in the new string res
         */
        res[i] = (*f)(i, s[i]);
        i++;
    }
    /* setting the NUL-terminating character */
    res[i] = 0;
    /* finally, we return res */
    return (res);
}
```
{% endcode %}

</details>
