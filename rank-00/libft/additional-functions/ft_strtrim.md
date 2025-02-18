# ft\_strtrim

### Subject

{% code overflow="wrap" %}
```
FT_STRTRIM (simplified)

NAME
    ft_strtrim -- trims character set from string
SYNOPSIS
    char *ft_strtrim(const char *s1, const char *set);
DESCRIPTION
    Allocate (with malloc(3)) and returns a copy of s1, without the characters specified in set at the beginning and the end of s1.
PARAMETERS
    s1: string to trim
    set: characters to trim
RETURN VALUES
    ft_strtrim() returns a trimmed copy of s1; NULL if the memory allocation failed.
AUTHORIZED EXTERNAL FUNCTIONS
    malloc(3)
```
{% endcode %}

### Understandable explanation

The `ft_strtrim()` function takes a string and trims it.

What does trimming mean you might ask ? Let me explain.

Trimming means removing the characters specified in the `set` string from the start AND the end of the string `s1`, without removing the characters from the `set` that are in the middle of `s1`.

If we have the string `ababaaaMy name is Simonbbaaabbad` and our set is `ab`, we'll get this result out of the `ft_strtrim()` function : `My name is Simon`.

We removed every `a` and `b` from the start and the end of `s1`, without touching at the a in the middle of `s1`.

### Hints

We have to remove characters from the start AND the end of s1, so why don't we just loop over the string, advance while we have a character to remove.

And then, do the same thing from the end of the string, leaving us with a start and an end index for our trimmed string.

That's basically how I did it, and how my code works.

### Commented solution

<details>

<summary>ft_strtrim</summary>

{% code title="ft_strtim.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.hss"

static int to_trim(const char *set, char c);
static char *new_str(const char *s1, size_t start, size_t end);

char *ft_strtrim(const char *s1, const char *set)
{
    int i;
    int j;
    
    i = 0;
    j = ft_strlen(s1) - 1;
    /* if the string has a length of 0, we don't have anything
     * to trim, so we return an empty string that will be freeable
     */
    if (ft_strlen(s1) == 0)
        return (ft_strdup(""));
    /* we first loop from the start of the string until we find the first
     * character that is not part of the set to trim
     */
    while (to_trim(set, s1[i]))
        i++;
    /* we then do the same but from the end of the string this time.
     */
    while (to_trim(set, s1[j]))
        j--;
    /* Now, that is what the values correspond to :
     * i : the start index of the trimmed string in the full string
     * j : the end index of the trimmed string in the full string
     * Here what the values would be with the example I talked about
     * above.
     * s1 : "ababaaaMy name is Simonbbaaabbad"
     * ft_strlen(s1) : 33
     * after looping both ways, we have this :
     * i : 8
     * j : 23
     * but since we don't pass the end index, we pass the length of 
     * the new string we have to some "maths" 
     * j - (i - 1) : 23 - (8 - 1) = 23 - 7 = 16
     */
    return (new_str(s1, i, j - (i - 1));
}

/* this is a function helper, it creates and allocates a new
 * string based on the three input passed as parameter
 */
static char *new_str(const char *s1, size_t start, size_t len)
{
    char *str;
    size_t i;
    
    /* first, we check if the len of the string to create is 0
     * or if the start of the new string is after the end of the
     * original string
     * if that is the case, we call ft_strdup to create an empty string
     * that can be freed later
     */
    if (len <= 0 || start >= ft_strlen(s1))
        return (ft_strdup(""));
    /* we then call ft_calloc to allocate enough memory for the new
     * string plus the NUL-terminating character
     * we use calloc instead of malloc so we don't have to think about
     * NUL-terminating the string at the end of our function
     */
    str = ft_calloc(len + 1, sizeof(char));
    if (!str)
        return (NULL);
    i = 0;
    /* looping over i while it is smaller than the length of
     * our new string
     */
    while (i < len)
    {
        /* here we copy the content of s1 at index start + i into
         * our new string at index i, why is that ?
         * try to find by yourself, there is also a schema below to
         * explain this.
         */
        str[i] = s1[start + i];
        i++;
    }
    /* returning the new string that we created
     */
    return (str);
}

/* This helper function return 1 if the character c is part of the
 * set of characters to trim and 0 if it is not part of it
 */
static int to_trim(const char *set, char c)
{
    int i;
    
    i = 0;
    /* looping over the whole set so that we check the character c
     * against every character in the set of characters to trim
     */
    while (set[i])
    {
        if (c == set[i])
            return (1);
        i++;
    }
    return (0);
}
```
{% endcode %}

</details>
