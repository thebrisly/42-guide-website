# rot\_13

### Subject

{% code overflow="wrap" %}
```
Assignment name  : rot_13
Expected files   : rot_13.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes a string and displays it, replacing each of its
letters by the letter 13 spaces ahead in alphabetical order.

'z' becomes 'm' and 'Z' becomes 'M'. Case remains unaffected.

The output will be followed by a newline.

If the number of arguments is not 1, the program displays a newline.

Example:

$>./rot_13 "abc"
nop
$>./rot_13 "My horse is Amazing." | cat -e
Zl ubefr vf Nznmvat.$
$>./rot_13 "AkjhZ zLKIJz , 23y " | cat -e
NxwuM mYXVWm , 23l $
$>./rot_13 | cat -e
$
$>
$>./rot_13 "" | cat -e
$
$>
```
{% endcode %}

### Commented solution

<details>

<summary>rot_13</summary>

{% code title="rot_13.c" overflow="wrap" lineNumbers="true" %}
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
            /* checking if the character is between Aa - Mm
             * if it's the case, we can add 13 to it to get
             * the character 13 places in front of it
             */
            if ((av[1][i] >= 65 && av[1][i] <= 77) || (av[1][i] >= 97 && av[1][i] <= 109))
                av[1][i] += 13;
            /* checking if the character is between Nn - Zz
             * if it's the case, we can substract 13 to it to get
             * the character 13 places in front of it
             */
            else if ((av[1][i] >= 78 && av[1][i] <= 90) || (av[1][i] >= 110 && av[1][i] <= 122))
                av[1][i] -= 13;
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
