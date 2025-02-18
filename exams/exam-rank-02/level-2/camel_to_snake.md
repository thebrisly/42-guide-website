# camel\_to\_snake

{% code overflow="wrap" %}
```
Assignment name  : camel_to_snake
Expected files   : camel_to_snake.c
Allowed functions: malloc, realloc, write
--------------------------------------------------------------------------------

Write a program that takes a single string in lowerCamelCase format
and converts it into a string in snake_case format.

A lowerCamelCase string is a string where each word begins with a capital letter
except for the first one.

A snake_case string is a string where each word is in lower case, separated by
an underscore "_".

Examples:
$>./camel_to_snake "hereIsACamelCaseWord"
here_is_a_camel_case_word
$>./camel_to_snake "helloWorld" | cat -e
hello_world$
$>./camel_to_snake | cat -e
$
```
{% endcode %}

### Commented solution

<details>

<summary>camel_to_snake</summary>

{% code title="camel_to_snake.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char *av[])
{
    int i;
    
    if (ac == 2)
    {
        i = 0;
        /* looping over the whole string
         */
        while (av[1][i])
        {
            /* if we encounter an upper-case letter
             * we have to make it lower-case and write a _ before it
             */
            if (av[1][i] >= 65 && av[1][i] <= 90)
            {
                /* here, we change the upper-case letter to its
                 * corresponding lower-case letter
                 */
                av[1][i] += 32;
                /* we write a _ to the screen
                 */
                write(1, "_", 1);
            }
            /* then we can write the current character, changed or not
             */
            write(1, &av[1][i], 1);
            i++;
        }
    }
    /* finally we can write the newline
     */
    write(1, "\n", 1);
}
```
{% endcode %}

</details>
