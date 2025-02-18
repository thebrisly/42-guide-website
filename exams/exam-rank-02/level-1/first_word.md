# first\_word

### Subject

{% code overflow="wrap" %}
```
Assignment name  : first_word
Expected files   : first_word.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes a string and displays its first word, followed by a
newline.

A word is a section of string delimited by spaces/tabs or by the start/end of
the string.

If the number of parameters is not 1, or if there are no words, simply display
a newline.

Examples:

$> ./first_word "FOR PONY" | cat -e
FOR$
$> ./first_word "this        ...    is sparta, then again, maybe    not" | cat -e
this$
$> ./first_word "   " | cat -e
$
$> ./first_word "a" "b" | cat -e
$
$> ./first_word "  lorem,ipsum  " | cat -e
lorem,ipsum$
$>
```
{% endcode %}

### Commented solution

<details>

<summary>first_word</summary>

{% code title="first_word.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char *av[])
{
    /* checking the number of arguments
     */
    if (argc == 2)
    {
        unsigned int i;
        
        i = 0;
        /* looping over the string to remove the possible starting
         * spaces (32) and tabulations (9)
         */
        while (av[1][i] == 32 || av[1][i] == 9)
            i++;
        /* then start printing the characters from the string
         * until we find either a space, a tabulation, or a \0
         */
        while ((av[1][i] != 32 && av[1][i] != 9) && av[1][i])
            write(1, &av[1][i++], 1);
    }
    /* writing a \n at the end, because in every case we have to put a 
     * \n at then end, either when we wrote something or not
     */
    write(1, "\n", 1);
    return (0);
}
```
{% endcode %}

</details>
