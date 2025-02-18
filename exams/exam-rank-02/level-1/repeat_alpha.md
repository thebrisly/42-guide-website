# repeat\_alpha

### Subject

{% code overflow="wrap" %}
```
Assignment name  : repeat_alpha
Expected files   : repeat_alpha.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program called repeat_alpha that takes a string and display it
repeating each alphabetical character as many times as its alphabetical index,
followed by a newline.

'a' becomes 'a', 'b' becomes 'bb', 'e' becomes 'eeeee', etc...

Case remains unchanged.

If the number of arguments is not 1, just display a newline.

Examples:

$>./repeat_alpha "abc"
abbccc
$>./repeat_alpha "Alex." | cat -e
Alllllllllllleeeeexxxxxxxxxxxxxxxxxxxxxxxx.$
$>./repeat_alpha 'abacadaba 42!' | cat -e
abbacccaddddabba 42!$
$>./repeat_alpha | cat -e
$
$>
$>./repeat_alpha "" | cat -e
$
$>
```
{% endcode %}

### Commented solution

<details>

<summary>repeat_alpha</summary>

{% code title="repeat_alpha" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char *av[])
{
    int i;
    int j;
    
    /* check the number of argument
     */
    if (ac == 2)
    {
        i = 0;
        /* loop over the whole string
         */
        while (av[1][i])
        {
            /* if the character is an upper-case letter
             */
            if (av[1][i] >= 65 && av[1][i] <= 90)
            {
                j = 0;
                /* loop while the j is smaller than the alphabetical
                 * index of the current character
                 * - 64 is to get the alphabetical index
                 * A in ASCII => 65, so 65 - 64 = 1
                 * Z in ASCII => 90, so 90 - 64 = 26
                 */
                while (j < av[1][i] - 64)
                {
                    write(1, &av[1][i], 1);
                    j++;
                }
            }
            else if (av[1][i] >= 97 && av[1][i] <= 122)
            {
                j = 0;
                /* loop while the j is smaller than the alphabetical
                 * index of the current character
                 * - 96 is to get the alphabetical index
                 * a in ASCII => 97, so 97 - 96 = 1
                 * z in ASCII => 122, so 122 - 96 = 26
                 */
                while (j < av[1][i] - 96)
                {
                    write(1, &av[1][i], 1);
                    j++;
                }
            }
            else
                /* if the current character is not a letter
                 * simply write the character
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
