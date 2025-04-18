# rostring

### Subject

{% code overflow="wrap" %}
```
Assignment name  : rostring
Expected files   : rostring.c
Allowed functions: write, malloc, free
--------------------------------------------------------------------------------

Write a program that takes a string and displays this string after rotating it
one word to the left.

Thus, the first word becomes the last, and others stay in the same order.

A "word" is defined as a part of a string delimited either by spaces/tabs, or
by the start/end of the string.

Words will be separated by only one space in the output.

If there's less than one argument, the program displays \n.

Example:

$>./rostring "abc   " | cat -e
abc$
$>
$>./rostring "Que la      lumiere soit et la lumiere fut"
la lumiere soit et la lumiere fut Que
$>
$>./rostring "     AkjhZ zLKIJz , 23y"
zLKIJz , 23y AkjhZ
$>
$>./rostring "first" "2" "11000000"
first
$>
$>./rostring | cat -e
$
$>

```
### Commented solution

<details>

<summary>rostring</summary>

{% code title="rostring.c" overflow="wrap" lineNumbers="true" %}
```c
#include "unistd.h"

void	rostring(char *str)
{
	int	i;
	int	j;

	i = 0;
	while (str[i] && str[i] == ' ' || str[i] == '\t')
		i++;
	j = i;
	while (str[i])
	{
		while (str[i] && str[i] != ' ' && str[i] != '\t')
			i++;
		while (str[i] && (str[i] == ' ' || str[i] == '\t'))
			i++;
		while ((str[i] && (str[i] != ' ' && str[i] != '\t')) && (str[i
				- 1] == ' ' || str[i - 1] == '\t'))
		{
			while (str[i] && (str[i] != ' ' && str[i] != '\t'))
			{
				write(1, &str[i], 1);
				i++;
			}
			write(1, " ", 1);
			i++;
		}
	}
	while (str[j] && (str[j] != ' ' && str[j] != '\t'))
	{
		write(1, &str[j], 1);
		j++;
	}
}

int	main(int ac, char **av)
{
	if (ac >= 2)
	{
		rostring(av[1]);
	}
	write(1, "\n", 1);
	return (0);
}
```
{% endcode %}

</details>