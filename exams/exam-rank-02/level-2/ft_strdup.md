# \*ft\_strdup

### Subject

{% code overflow="wrap" %}
```
Assignment name  : ft_strdup
Expected files   : ft_strdup.c
Allowed functions: malloc
--------------------------------------------------------------------------------

Reproduce the behavior of the function strdup (man strdup).

Your function must be declared as follows:

char    *ft_strdup(char *src);
```
{% endcode %}

### Commented solution

<details>

<summary>ft_strdup()</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <stdlib.h>

char    *ft_strdup(char *src)
{
	char	*tmp; //we will duplicate str into this variable
	int	len; 
	int	i;

	len = 0;
	i = 0;
	while (src[len]) //we calculate the length of src to create a place with enough memory
		len++;
	tmp = malloc(sizeof(char) * len + 1); //we allocate some space thanks to malloc. + 1 because the string need some space for the extra "\0" at the end (don't forget it !)
	if (!tmp) //malloc protection
		return (NULL);
	while (src[i]) //loop to complete the new string
	{
		tmp[i] = src[i];
		i++;
	}
	tmp[i] = 0; //adding the null character at the end
	return (tmp);
}


#include <stdio.h>

int main()
{
	char	*a;
	a = "Hello World";
	printf("%s\n", ft_strdup(a));
}
```
{% endcode %}

</details>
