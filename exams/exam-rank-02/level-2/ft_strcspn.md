# ft\_strcspn

### Subject

{% code overflow="wrap" %}
```
Assignment name	: ft_strcspn
Expected files	: ft_strcspn.c
Allowed functions: None
---------------------------------------------------------------

Reproduce exactly the behavior of the function strcspn
(man strcspn).

The function should be prototyped as follows:

size_t	ft_strcspn(const char *s, const char *reject);
```
{% endcode %}

### Man Page

```
STRCSPN(3) (simplified)

NAME
    strcspn -- span a string
LIBRARY
    Standard C Library (libc, -lc)
SYNOPSIS
    #include <string.h>
    size_t strcspn(const char *s, const char *charset);
DESCRIPTION
    The strcspn() function spans the initial part of the null-terminated
string s as long as the characters from s do not occur in the null-
terminated string charset (it spans the complement of the charset). In
other words, it computes the string array index of the first character
of s which is also in charset, else the index of the first null character.
RETURN VALUES
    The strcspn() functions return the number of characters spanned.
```

### Commented solution

For this one, I'll give you two different examples, one will be done using indexes in the string `s` and `reject`. And the second example will use pointers directly.

<details>

<summary>Indexes</summary>

{% code title="ft_strcspn.c" overflow="wrap" lineNumbers="true" %}
```c
// Needed for size_t
#include <stdio.h>

size_t ft_strcspn(const char *s, const char *reject)
{
    size_t i;
    size_t j;
    
    i = 0;
    // Looping over the whole string
    while(s[i++])
    {
        j = 0;
        // Check the current string char against every char in charset
        while (reject[j])
        {
            // If character found, return index in current string
            if (s[i] == reject[j++])
            	return (i);
        }
    }
    // If we spanned the whole string, return i, in that case the
    // rejected char found is the NULL-terminating one
    return (i);
}
```
{% endcode %}

</details>

<details>

<summary>Pointers</summary>

{% code title="ft_strcspn.c" overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>

size_t ft_strcspn(const char *s, const char *reject)
{
    // Save a pointer to the start of s
    const char *og = s;
    const char *s2;
    
    // Looping over the whole string 
    while (*s++)
    {
        // Set s2 to be the start of reject
        // that way we keep the reject pointer to its original position
        // Then loop over the whole charset
        s2 = reject;
        while (*s2)
        {
            // If current string charcter found in charset, return the
            // number of characters spanned
            if (*s == *s2++)
                // Here we make use of the original pointer to calculate
                // the number of char. spanned
                return (s - og);
        }
    }
    // Same as above, we use the original pointer to calculate the number
    // of character spanned
    return (s - og);
}
```
{% endcode %}

</details>
