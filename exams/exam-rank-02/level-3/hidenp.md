# hidenp

### Subject

```
Assignment name  : hidenp
Expected files   : hidenp.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program named hidenp that takes two strings and displays 1
followed by a newline if the first string is hidden in the second one,
otherwise displays 0 followed by a newline.

Let s1 and s2 be strings. We say that s1 is hidden in s2 if it's possible to
find each character from s1 in s2, in the same order as they appear in s1.
Also, the empty string is hidden in any string.

If the number of parameters is not 2, the program displays a newline.

Examples :

$>./hidenp "fgex.;" "tyf34gdgf;'ektufjhgdgex.;.;rtjynur6" | cat -e
1$
$>./hidenp "abc" "2altrb53c.sse" | cat -e
1$
$>./hidenp "abc" "btarc" | cat -e
0$
$>./hidenp | cat -e
$
$>
```

### Commented solution

<details>

<summary>hidenp</summary>

{% code title="hidenp.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char **av)
{
    int i = 0, j = 0;
    
    if (ac == 3)
    {
        // Looping over s2 only if there is something
        // in s1
        while (av[2][j] && av[1][i])
        {
            // If current char of s2 equals current char
            // of s1, advance in s1
            if (av[2][j] == av[1][i])
                i++;
            // advance in s2 every time
            j++;
        }
        // if we reached the end of s1, it's hidden in s2
        if (av[1][i] == 0)
            write(1, "1", 1);
        else
            write(1, "0", 1);
    }
    write(1, "\n", 1);
}
```
{% endcode %}

</details>
