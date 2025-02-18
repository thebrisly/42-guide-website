# ft\_strdup

### Subject

{% code overflow="wrap" %}
```
STRDUP(3) (simplified)

NAME
    strdup -- save a copy of a string
SYNOPSIS
    char *strdup(const char *s1);
DESCRIPTION
    The strdup() function allocates sufficient memory for a copy of the string s1, does the copy, and returns a pointer to it. The pointer may subsequently be used as an argument to the function free(3).
    If insufficient memory is available, NULL is returned and errno is set to ENOMEM.
```
{% endcode %}

### Understandable explanation

For once, the man is really clear on what the function does. So I don't think I need to explain it with more details.

### Hints

We have to use malloc for this since the returned value of this function must be 'freeable' with the free function.

{% code title="ft_strdup.c" overflow="wrap" lineNumbers="true" %}
```c
char *ft_strdup(const char *s1)
{
    /* use malloc to allocate enough space for s1 
     * we will have to copy it completely
     * so we need enough space for it
     */
     /* loop over s1 and copy each character in the new string you
      * just allocated
      */
     /* return the allocated and copied string */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_strdup</summary>

{% code title="ft_strdup.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

char *ft_strdup(const char *s1)
{
    char *dest;
    size_t i;
    
    /* allocating enough memory for s1 + 1 character
     * for the NUL-terminating character
     */
    dest = (char *) malloc(ft_strlen(s1) + 1);
    if (!dest)
        return (NULL);
    i = 0;
    /* looping over the whole s1 string */
    while (s1[i])
    {
        /* copying the current s1 character into the same
         * position in the dest string we allocated above
         */
        dest[i] = s1[i];
        i++;
    }
    /* setting the NUL-terminating character */
    dest[i] = 0;
    /* finally, we return the newly created string */
    return (dest);
}
```
{% endcode %}

</details>
