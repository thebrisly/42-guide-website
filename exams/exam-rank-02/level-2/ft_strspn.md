# ft\_strspn

### Subject

{% code overflow="wrap" %}
```
Assignment name	: ft_strspn
Expected files	: ft_strspn.c
Allowed functions: None
---------------------------------------------------------------

Reproduce exactly the behavior of the strspn function 
(man strspn).

The function should be prototyped as follows:

size_t	ft_strspn(const char *s, const char *accept);
```
{% endcode %}

### Man Page

```
STRSPN(3) (simplified)

NAME
    strspn -- span a string
LIBRARY
    Standard C Library (libc, -lc)
SYNOPSIS
    #include <string.h>
    size_t strspn(const char *s, const char *charset);
DESCRIPTION
    The strcspn() function spans the initial part of the null-terminated 
string s as long as the characters from s occur in the null-terminated 
string charset. In other words, it computes the string array index of the 
first character of s which is not in charset, else the index of the first 
null character
RETURN VALUES
    The strspn() functions return the number of characters spanned.
```

### Commented solution

<details>

<summary>ft_strspn.c</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <stdlib.h>

size_t	ft_strspn(const char *s, const char *accept)
{
	int i;
	int	j;
	int check;

	i = 0;
	while (s[i])
	{
		j = 0;
		check = 0;
		while (accept[j])
		{
			if (s[i] == accept[j])
				check = 1;
			j++;
		}
		if (check == 0)
			return (i);
		i++;
	}
	return (i);
}

/*#include <stdio.h>
int main()
{
	char *s = "hello";
	const char *accept = "jfkhpell";
	printf("%zu\n", ft_strspn(s, accept));
}*/
```
{% endcode %}

</details>
