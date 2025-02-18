# \*ft\_strcmp

### Subject

{% code overflow="wrap" %}
```
Assignment name  : ft_strcmp
Expected files   : ft_strcmp.c
Allowed functions:
--------------------------------------------------------------------------------

Reproduce the behavior of the function strcmp (man strcmp).

Your function must be declared as follows:

int    ft_strcmp(char *s1, char *s2);
```
{% endcode %}

### Man Page

```
STRCMP(3) (simplified)

NAME
    strcmp -- compare strings
SYNOPSIS
    #include <string.h>
    int strcmp(const char *s1, const char *s2);
DESCRIPTION
    The strcmp() and strncmp() functions lexicographically compare the null-
terminated strings s1 and s2.
RETURN VALUES
     The strcmp() and strncmp() functions return an integer greater than,
 equal to, or less than 0, according as the string s1 is greater than,
 equal to, or less than the string s2.  The comparison is done using
 unsigned characters, so that ‘\200’ is greater than ‘\0’.
```

### Commented solution

<details>

<summary>ft_strcmp</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
int ft_strcmp(char *s1, char *s2)
{
    int i;
    
    i = 0;
    // looping over both string while both of them are equal
    // and at least one of them is not finished
    while ((s1[i] || s2[i]) && s1[i] == s2[i])
        i++;
    // when we can't loop anymore, we return the substraction
    // of the last compared characters in both string, this will
    // result in either a negative, zero or positive value
    return (s1[i] - s2[i]);
}
```
{% endcode %}

</details>
