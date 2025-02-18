# max

### Subject

{% code overflow="wrap" %}
```
Assignment name  : max
Expected files   : max.c
Allowed functions:
--------------------------------------------------------------------------------

Write the following function:

int		max(int* tab, unsigned int len);

The first parameter is an array of int, the second is the number of elements in
the array.

The function returns the largest number found in the array.

If the array is empty, the function returns 0.
```
{% endcode %}

### Commented solution

<details>

<summary>max.c</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
int		max(int* tab, unsigned int len)
{
	int count = 0;
	int result = 0;
	int i = 0;
	if (len > 0)
	{
		while (count < len)
		{
			if (tab[i] > result)
				result = tab[i];
			i++;
			count++;
		}
		return (result);
	}
	return (0);
}

#include <stdio.h>

int main()
{
	int int_tab[] = {1, 3, 2, 10, 9};
	printf("%d", max(int_tab, 5));
}
```
{% endcode %}

</details>
