# snake\_to\_camel

### Subject

```
Assignment name  : snake_to_camel
Expected files   : snake_to_camel.c
Allowed functions: malloc, free, realloc, write
--------------------------------------------------------------------------------

Write a program that takes a single string in snake_case format
and converts it into a string in lowerCamelCase format.

A snake_case string is a string where each word is in lower case, separated by
an underscore "_".

A lowerCamelCase string is a string where each word begins with a capital letter
except for the first one.

Examples:
$>./snake_to_camel "here_is_a_snake_case_word"
hereIsASnakeCaseWord
$>./snake_to_camel "hello_world" | cat -e
helloWorld$
$>./snake_to_camel | cat -e
$
```

### Commented solution

{% code title="snake_to_camel.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int toUpper(int c)
{
    if (c >= 'a' && c <= 'z')
        return (c - 32);
    return (c);
}

int ft_putchar(char c)
{
    return write(1, &c, 1);
}

int main(int ac, char **av)
{
    int i;
    
    // do things only if there is only one argument
    if (ac == 2)
    {
        i = 0;
        // looping over the whole string
        while (av[1][i])
        {
            // If we encounter a _, we have to make the
            // next letter uppercase and not print the _
            // so we only print the uppercase letter
            if (av[1][i] == '_')
                // here we use the ++i operator to
                // increment i before accessing the value
                // that way we skip the _
                ft_putchar(toUpper(av[1][++i]));
            else
                // in all other cases, we simply write
                // the character to the screen
                ft_putchar(av[1][i]);
            i++;
        }
    }
    // and finally, we have our newline
    // putting it here makes us only need one in all the 
    // cases 
    ft_putchar('\n');
}
```
{% endcode %}
