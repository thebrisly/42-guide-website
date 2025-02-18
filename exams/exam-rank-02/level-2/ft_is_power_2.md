# ft\_is\_power\_2

### Subject

{% code overflow="wrap" %}
```
Assignment name  : is_power_of_2
Expected files   : is_power_of_2.c
Allowed functions: None
--------------------------------------------------------------------------------

Write a function that determines if a given number is a power of 2.

This function returns 1 if the given number is a power of 2, otherwise it returns 0.

Your function must be declared as follows:

int	    is_power_of_2(unsigned int n);
```
{% endcode %}

### Commented solution

<details>

<summary>ft_is_power_2.c</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
int	    is_power_of_2(unsigned int n)
{

// we will initialize a test variable to 1, and we will multiply it by 2 until it is equal to or greater than the variable we have been given as a parameter (n). If the two variables are equal it means that it is a power of 2 (since we have always multiplied this number by 2)
	
	int test = 1;

	while (test <= n)
	{
		if (test == n)
			return  (1); // test is a power of 2
		test = test * 2;
	}
	// we will leave the loop if the test variable is greater than n. this means that it is not a power of 2 an we need to return 0.
	return (0);
}


#include <stdio.h>
int main()
{
	printf("%d", is_power_of_2(16));
}
```
{% endcode %}

</details>
