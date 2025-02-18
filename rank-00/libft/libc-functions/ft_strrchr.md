# ft\_strrchr

### Subject

{% code overflow="wrap" %}
```
STRRCHR(3) (simplified)

NAME
    strrchr -- locate character in string
SYNOPSIS
    char *strrchr(const char *s, int c);
DESCRIPTION
    The strrchr() function is identical to strchr(), except it locates the last occurence of c.
RETURN VALUES
    The function strrchr() returns a pointer to the located character, or NULL if the character does not appear in the string.
```
{% endcode %}

### Understandable explanation

This function is fairly easy to understand, it does the same thing as `strchr()`, but locates the last occurence of c.

### Hints

{% code title="ft_strrchr.c" overflow="wrap" lineNumbers="true" %}
```c
char *ft_strrchr(const char *s, int c)
{
    /* we can use basically the same code as ft_strchr() but not returning
     * the value as soon as we find the character, just setting a variable
     * each time, and returning it at the end of the function
     */
    /* loop over the whole string */
    /* check if current character is equal to the one we have to find */
    /* once we looped over the whole string, check again for the character
     * in case the character we have to find is '\0'
     */
    /* if we didn't find c in the string, return NULL */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_strrchr</summary>

{% code title="ft_strrchr.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

char *ft_strrchr(const char *s, int c)
{
    unsigned int i;
    char *res;
    char cc;
    
    /* we convert c to a char as we got it as an int */
    cc = (char) c;
    /* we set res as NULL at the beginning so if we don't find 
     * any occurence of c, the function will return NULL
     */
    res = NULL;
    i = 0;
    /* looping over the whole string s */
    while (s[i])
    {
         /* if the current character is equal to cc 
         * this means we found an occurence of cc in the string
         * therefore, we set res as the address of the character
         */
        if (s[i] == cc)
            res = (char *) &s[i];
        /* we then advance in the string to search for another
         * occurence of cc
         */
        i++;
    }
    /* once we looped over the whole string, if we didn't find an
     * occurence of cc, we have to check if cc is equal to '\0'
     * so we check once again if the current character is equal to cc
     * if this is the case, we set res as the address of the '\0' char
     */
    if (s[i] == c)
        res = (char *) &s[i];
    /* when we reach the end of the function, we return res
     * since we looped over the whole string and set res as the address
     * of the last occurence of c we found, this will return a pointer 
     * to the last occurence of c
     * and if we didn't find any occurence of c, since res was set to 
     * NULL at the very beginning of the function, the function will
     * return NULL
     */
    return (res);
}
```
{% endcode %}

</details>
