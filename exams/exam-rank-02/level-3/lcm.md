# lcm

### Subject

```
Assignment name  : lcm
Expected files   : lcm.c
Allowed functions:
--------------------------------------------------------------------------------

Write a function who takes two unsigned int as parameters and returns the
computed LCM of those parameters.

LCM (Lowest Common Multiple) of two non-zero integers is the smallest postive
integer divisible by the both integers.

A LCM can be calculated in two ways:

- You can calculate every multiples of each integers until you have a common
multiple other than 0

- You can use the HCF (Highest Common Factor) of these two integers and
calculate as follows:

	LCM(x, y) = | x * y | / HCF(x, y)

  | x * y | means "Absolute value of the product of x by y"

If at least one integer is null, LCM is equal to 0.

Your function must be prototyped as follows:

  unsigned int    lcm(unsigned int a, unsigned int b);
```

### Commented solution

<details>

<summary>lcm</summary>

{% code title="lcm.c" overflow="wrap" lineNumbers="true" %}
```c
unsigned int lcm(unsigned int a, unsigned int b)
{
    unsigned int g = (a > b) ? a : b;
    
    // Check if any of the integer is null
    if (a == 0 || b == 0)
    	return (0);
    
    while (1)
    {
    	// if g is perfectly divisible by both a and b
    	// this is the lcm
        if ((g % a == 0) && (g % b == 0))
            return (g);
        g++;
    }
}
// Un-comment the following to test
// #include <stdio.h>
// #include <stdlib.h>
// int main(int ac, char **av)
// {
// 	if (ac == 3)
// 	{
// 		unsigned int m = lcm(atoi(av[1]), atoi(av[2]));
// 		printf("LCM: %u\n", m);
// 	}
// }
```
{% endcode %}

</details>
