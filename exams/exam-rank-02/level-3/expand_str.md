# expand\_str

### Subject

```
Assignment name  : expand_str
Expected files   : expand_str.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes a string and displays it with exactly three spaces
between each word, with no spaces or tabs either at the beginning or the end,
followed by a newline.

A word is a section of string delimited either by spaces/tabs, or by the
start/end of the string.

If the number of parameters is not 1, or if there are no words, simply display
a newline.

Examples:

$> ./expand_str "vous   voyez   c'est   facile   d'afficher   la   meme   chose" | cat -e
vous   voyez   c'est   facile   d'afficher   la   meme   chose$
$> ./expand_str " seulement          la c'est      plus dur " | cat -e
seulement   la   c'est   plus   dur$
$> ./expand_str "comme c'est cocasse" "vous avez entendu, Mathilde ?" | cat -e
$
$> ./expand_str "" | cat -e
$
$>
```

### Commented solution

<details>

<summary>expand_str</summary>

{% code title="expand_str.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

void ft_putchar(char c)
{
    write(1, &c, 1);
}

int is_space(char c)
{
    if (c <= 32)
        return 1;
    return 0;
}

int main(int ac, char **av)
{
    if (ac == 2)
    {
        int i = 0, space = 0;
        // skipping all leading blank chars
        while (is_space(av[1][i]))
            i++;
        while (av[1][i])
        {
            // if there is a blank char, make the space flag 1
            // if there are multiple blank, it will be set
            // to 1 each time
            if (is_space(av[1][i]))
                 space = 1;
            // if current char is not a blank char
            // write 3 spaces if flag is on
            // set the space flag back to 0
            // write current char
            if (!is_space(av[1][i]))
            {
                if (space)
                    write(1, "   ", 3);
                space = 0;
                ft_putchar(av[1][i]);
            }
            i++;
        }
    }
    ft_putchar('\n');
}
```
{% endcode %}

</details>
