# ft\_strchr

### Subject

{% code overflow="wrap" %}
```
STRCHR(3) (simplified)

NAME
    strchr -- locate character in string
SYNOPSIS
    char *strchr(const char *s, int c);
DESCRIPTION
    The strchr() function locates the first occurence of c (converted to a char) in the string pointed to by s. The terminating null character is considered to be part of the string; therefor if c is '\0', the function locate the terminating '\0'.
RETURN VALUES
    The function strchr() return a pointer to the located character, or NULL if the character does not appear in the string.
```
{% endcode %}

### Understandable explanation

The `strchr()` function searches for one character in a string. If it finds the character, it returns a pointer to the first occurence of this specific character.

If it don't find any occurence of this character, it returns `NULL`.

We also have to return a pointer to the character if the character is `\0`.

### Hints

{% code title="ft_strchr.c" overflow="wrap" lineNumbers="true" %}
```c
char *ft_strchr(const char *s, int c)
{
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

<summary>ft_strchr</summary>

{% code title="ft_strchr.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

char *ft_strchr(const char *s, int c)
{
    unsigned int    i;
    char            cc,
    
    /* we convert c to a char as we got it as an int */
    cc = (char) c;
    i = 0;
    /* looping over the whole string s */
    while (s[i])
    {
        /* if the current character is equal to cc 
         * this means we found an occurence of c in the string
         * therefore, we return the address of the char as a char pointer
         */
        if (s[i] == cc)
            return ((char *) &s[i]);
        /* if the current character is not equal to cc
         * we advance in the string
         */
        i++;
    }
    /* once we looped over the whole string, if we didn't find an
     * occurence of cc, we have to check if cc is equal to '\0'
     * so we check once again if the current character is equal to cc
     * if this is the case, we return the address of '\0' as a char
     * pointer
     */
    if (s[i] == cc)
        return ((char *) &s[i]);
    /* if we reach this point, this means we didn't find any
     * occurence of cc in the string so we return NULL as
     * stated in the man
     */
    return (NULL);
}
```
{% endcode %}

</details>
