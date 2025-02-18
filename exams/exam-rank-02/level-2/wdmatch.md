# wdmatch

### Subject

```
Assignment name  : wdmatch
Expected files   : wdmatch.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes two strings and checks whether it's possible to
write the first string with characters from the second string, while respecting
the order in which these characters appear in the second string.

If it's possible, the program displays the string, followed by a \n, otherwise
it simply displays a \n.

If the number of arguments is not 2, the program displays a \n.

Examples:

$>./wdmatch "faya" "fgvvfdxcacpolhyghbreda" | cat -e
faya$
$>./wdmatch "faya" "fgvvfdxcacpolhyghbred" | cat -e
$
$>./wdmatch "quarante deux" "qfqfsudf arzgsayns tsregfdgs sjytdekuoixq " | cat -e
quarante deux$
$>./wdmatch "error" rrerrrfiiljdfxjyuifrrvcoojh | cat -e
$
$>./wdmatch | cat -e
$
```

### Commented solution

<details>

<summary>wdmatch.c</summary>

{% code title="wdmatch.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char **av)
{
    if (ac == 3)
    {
        const char *s1 = av[1];
        const char *s2 = av[2];
        int len = 0, i = 0;
        
        while (s1[len])
            len++;
        
        // checking all characters of s1 in s2
        while (i < len && *s2)
        {
            // next line checks if current s1 char is
            // equal to s2 char, after the comparison is
            // done, we increment the s2 pointer
            // even if the condition doesn't match
            // if the condition match, we increment i to
            // check for next s1 char
            if (s1[i] == *s2++)
                i++;
        }
        if (i == len)
            write(1, s1, len);
    }
    write(1, "\n", 1);
    return (0);
}
```
{% endcode %}

</details>
