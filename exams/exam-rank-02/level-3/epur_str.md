# epur\_str

### Subject

```
Assignment name  : epur_str
Expected files   : epur_str.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes a string, and displays this string with exactly one
space between words, with no spaces or tabs either at the beginning or the end,
followed by a \n.

A "word" is defined as a part of a string delimited either by spaces/tabs, or
by the start/end of the string.

If the number of arguments is not 1, or if there are no words to display, the
program displays \n.

Example:

$> ./epur_str "vous voyez c'est facile d'afficher la meme chose" | cat -e
vous voyez c'est facile d'afficher la meme chose$
$> ./epur_str " seulement          la c'est      plus dur " | cat -e
seulement la c'est plus dur$
$> ./epur_str "comme c'est cocasse" "vous avez entendu, Mathilde ?" | cat -e
$
$> ./epur_str "" | cat -e
$
$>
```

### Commented solution

<details>

<summary>epur_str</summary>

{% code title="epur_str.c" overflow="wrap" lineNumbers="true" %}
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
            // write a space if flag is on
            // set the space flag back to 0
            // write current char
            if (!is_space(av[1][i]))
            {
                if (space)
                    ft_putchar(' ');
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
