# \*ft\_putstr

### Subject

{% code overflow="wrap" %}
```
Assignment name  : ft_putstr
Expected files   : ft_putstr.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a function that displays a string on the standard output.

The pointer passed to the function contains the address of the string's first
character.

Your function must be declared as follows:

void	ft_putstr(char *str);
```
{% endcode %}

### Commented solution

<details>

<summary>ft_putstr</summary>

{% code title="ft_putstr.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

void ft_putstr(char *str)
{
    // Define and initialize an unsigned integer variable 'i' to 0
    unsigned int i = 0;

    // Loop until the null character ('\0') is encountered in the string pointed to by 'str'
    while (str[i])
    {
        // Call the 'write' function to output the character at the current position in the string,
        // specified by the value of 'i', to standard output (stdout)
        write(1, &str[i], 1);

        // Increment 'i' by 1 after each iteration
        i++;
    }
}

```
{% endcode %}

</details>
