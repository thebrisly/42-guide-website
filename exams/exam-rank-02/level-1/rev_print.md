# rev\_print

### Subject

{% code overflow="wrap" %}
```
Assignment name  : rev_print
Expected files   : rev_print.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes a string, and displays the string in reverse
followed by a newline.

If the number of parameters is not 1, the program displays a newline.

Examples:

$> ./rev_print "zaz" | cat -e
zaz$
$> ./rev_print "dub0 a POIL" | cat -e
LIOP a 0bud$
$> ./rev_print | cat -e
$
```
{% endcode %}

### Commented solution

<details>

<summary>rev_print</summary>

{% code title="rev_print.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char *av[])
{
    if (ac == 2)
    {
        int i;
        
        i = 0;
        /* looping over the whole string to find its length
         */
        while (av[1][i])
            i++;
        /* looping over the length of the string (length to 0)
         * and writing each character one by one
         */
        while (i--)
            write(1, &av[1][i], 1);
    }
    write(1, "\n", 1);
}
```
{% endcode %}

</details>
