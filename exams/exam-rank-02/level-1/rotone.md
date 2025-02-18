# rotone

### Subject

{% code overflow="wrap" %}
```
Assignment name  : rotone
Expected files   : rotone.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes a string and displays it, replacing each of its
letters by the next one in alphabetical order.

'z' becomes 'a' and 'Z' becomes 'A'. Case remains unaffected.

The output will be followed by a \n.

If the number of arguments is not 1, the program displays \n.

Example:

$>./rotone "abc"
bcd
$>./rotone "Les stagiaires du staff ne sentent pas toujours tres bon." | cat -e
Mft tubhjbjsft ev tubgg of tfoufou qbt upvkpvst usft cpo.$
$>./rotone "AkjhZ zLKIJz , 23y " | cat -e
BlkiA aMLJKa , 23z $
$>./rotone | cat -e
$
$>
$>./rotone "" | cat -e
$
$>
```
{% endcode %}

### Commented solution

<details>

<summary>rotone</summary>

{% code title="rotone.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char *av[])
{
    if (ac == 2)
    {
        int i;
        
        i = 0;
        /* looping over the whole string
         */
        while (av[1][i])
        {
            /* checking if the character is Z or z
             * if it's the case, we remove 25 to get A or a
             * respectively
             */
            if (av[1][i] == 90 || av[1][i] == 122)
                av[1][i] -= 25;
            /* checking if the character is between Aa - Yy
             * if it's the case, we can add 1 to it to get
             * the next character
             */
            else if ((av[1][i] >= 65 && av[1][i] <= 89) || (av[1][i] >= 95 && av[1][i] <= 121))
                av[1][i] += 1;
            /* finally, we can write the character and increment the
             * counter
             */
            write(1, &av[1][i], 1);
            i++;
        }
    }
    write(1, "\n", 1);
}
```
{% endcode %}

</details>
