# ft\_strpbrk

This solution has been proposed by Duc Nguyen ([Find his Github link here ](https://github.com/nguyenduc-03/42Student))

### Subject

{% code overflow="wrap" %}
```
Assignment name	: ft_strpbrk
Expected files	: ft_strpbrk.c
Allowed functions: None
---------------------------------------------------------------

Reproduce exactly the behavior of the function strpbrk
(man strpbrk).

The function should be prototyped as follows:

char	*ft_strpbrk(const char *s1, const char *s2);
```
{% endcode %}

### Man page

```
STRPBRK(3) (simplified)

NAME
     strpbrk –- locate multiple characters in string
LIBRARY
     Standard C Library (libc, -lc)
SYNOPSIS
     #include <string.h>
     char *strpbrk(const char *s, const char *charset);

DESCRIPTION
     The strpbrk() function locates in the null-terminated string s the first
     occurrence of any character in the string charset and returns a pointer to this
     character.  If no characters from charset occur anywhere in s strpbrk()
     returns NULL.
RETURN VALUES
     The strpbrk() function return a pointer to the first occurence of any character
     in the string,if no characters occur anywhere in s, strpbrk() returns NULL.
```

### Commented solution

<details>

<summary>ft_strpbrk()</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
char *ft_strpbrk(const char *s1, const char *s2)
{
    int i = 0;
    int j = 0;
    char *re = (char *)s1;

    while (s1[i])
    {
        j = 0;
        while (s2[j])
        {
            if (s1[i] == s2[j])
                return re;
            j++;
        }
        i++;
        re++;
    }
    return NULL;
}
```
{% endcode %}

</details>

#### Explanation of  `char *re = (char *)s1;`

In this function, the variable `re` is a temporary pointer that is initially set to the start of the input string `s1`. It is used to track the current position in `s1` as we iterate through it using an index (`i`). Every time we move to the next character in `s1`, we also increment `re`, so that it always points to the same character as `s1[i]`.

When a character from `s1` is found in `s2`, `re` is returned. This ensures the function returns a **pointer to the matching character** in `s1`, which is the correct behavior for a `strpbrk`-like function.

