# paramsum

### Subject

```
Assignment name  : paramsum
Expected files   : paramsum.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that displays the number of arguments passed to it, followed by
a newline.

If there are no arguments, just display a 0 followed by a newline.

Example:

$>./paramsum 1 2 3 5 7 24
6
$>./paramsum 6 12 24 | cat -e
3$
$>./paramsum | cat -e
0$
$>
```

### Commented solution

<details>

<summary>paramsum</summary>

{% code title="paramsum.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

// Simple putnbr function, we don't need negatives since there
// will never be less than 0 arguments to a program
void ft_putnbr(int nbr)
{
    if (nbr >= 10)
        ft_putnbr(nbr / 10);
    char c = nbr % 10 + '0';
    write(1, &c, 1);
}

int main(int ac, char **av)
{
    // Casting argv argument to void to get rid of it
    // since we'll not use it
    (void) av;
    // Writing the number of arguments from argc minus 1
    // The first argument counted is the executable name so
    // not an argument as for this subject
    ft_putnbr(ac - 1);
    write(1, "\n", 1);
    return (0);
}
```
{% endcode %}

</details>
