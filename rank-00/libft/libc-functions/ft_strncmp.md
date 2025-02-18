# ft\_strncmp

### Subject

{% code overflow="wrap" %}
```
STRNCMP(3) (simplified)

NAME
    strncmp -- compare strings
SYNOPSIS
    int strncmp(const char *s1, const char *s2, size_t n);
DESCRIPTION
    The strncmp() function lexicographically compare the null-terminated strings s1 and s2.
    The strncmp() function compares not more than n characters. Because strncmp() is designed for comparing strings rather than binary data, characters that appear after a '\0' character are not compared.
RETURN VALUES
    The strncmp() function returns an integer greater than, equal to, or less than 0, according as the string s1 is greater than, equal to, or less than the string s2. The comparison is done using unsigned characters, so that '\200' is greater than '\0'.
```
{% endcode %}

### Understandable explanation

`strncmp()` compares string in a lexicographic order, this means that it compares each characters by their corresponding ASCII values.

`strncmp()` compares maximum `n` characters in both strings.

The returned value depends on what difference is found.\
If the two strings are the same, the returned result will be `0` since there is no difference.

If there is a difference, and the first different character in `s2` is greater than the character at the same place in `s1`, the returned result will be negative.

If there is a difference, and the first different character in `s2` is less than the character at the same place in `s1`, the returned result will be positive.

### Hints

{% code title="ft_strncmp.c" overflow="wrap" lineNumbers="true" %}
```c
int ft_strncmp(const char *s1, const char *s2, size_t n)
{
    /* loop over both string until we reach n characters */
    /* check if current s1 character is different than
     * current s2 character
     */
         /* if characters are different, return the difference
          * between both characters
          */
      /* if we read both strings until n characters and no difference
       * were found, return 0 as there is no difference
       */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_strncmp</summary>

{% code title="ft_strncmp.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int ft_strncmp(const char *s1, const char *s2, size_t n)
{
    size_t i;
    
    i = 0;
    while ((s1[i] || s2[i]) && i < n)
    {
        if ((unsigned char) s1[i] != (unsigned char) s2[i])
            return ((unsigned char) s1[i] - (unsigned char) s2[i]);
        i++;
    }
    return (0);
}
```
{% endcode %}

</details>
