# alpha\_mirror

### Subject

{% code overflow="wrap" %}
```
Assignment name  : alpha_mirror
Expected files   : alpha_mirror.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program called alpha_mirror that takes a string and displays this string
after replacing each alphabetical character by the opposite alphabetical
character, followed by a newline.

'a' becomes 'z', 'Z' becomes 'A'
'd' becomes 'w', 'M' becomes 'N'

and so on.

Case is not changed.

If the number of arguments is not 1, display only a newline.

Examples:

$>./alpha_mirror "abc"
zyx
$>./alpha_mirror "My horse is Amazing." | cat -e
Nb slihv rh Znzarmt.$
$>./alpha_mirror | cat -e
$
$>
```
{% endcode %}

### Commented solution

<details>

<summary>alpha_mirror</summary>

{% code title="alpha_mirror.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char *av[])
{
    int i;
    
    if (ac == 2)
    {
        i = 0;
        while (av[1][i])
        {
            if (av[1][i] >= 65 && av[1][i] <= 90)
            /* we remove the ASCII code of the letter from the ASCII
             * code of the last upper-case letter, then add the ASCII
             * code of the first upper-case letter
             * 90 - 65(A) = 35, 35 + 65 = 90(Z)
             * 90 - 66(B) = 34, 34 + 65 = 89(Y)
             */ 
                av[1][i] = 90 - av[1][i] + 65;
            else if (av[1][i] >= 97 && av[1][i] <= 122)
            /* we remove the ASCII code of the letter from the ASCII
             * code of the last lower-case letter, then add the ASCII
             * code of the first lower-case letter
             * 122 - 97(a) = 35, 35 + 97 = 122(z)
             * 122 - 98(b) = 34, 34 + 97 = 121(y)
             */ 
                av[1][i] = 122 - av[1][i] + 97;
            /* finally, we can writethe current character to the screen
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
