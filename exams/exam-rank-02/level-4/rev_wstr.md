# rev\_wstr

### Subject

{% code overflow="wrap" %}
```
Assignment name  : rev_wstr
Expected files   : rev_wstr.c
Allowed functions: write, malloc, free
--------------------------------------------------------------------------------

Write a program that takes a string as a parameter, and prints its words in
reverse order.

A "word" is a part of the string bounded by spaces and/or tabs, or the
begin/end of the string.

If the number of parameters is different from 1, the program will display
'\n'.

In the parameters that are going to be tested, there won't be any "additional"
spaces (meaning that there won't be additionnal spaces at the beginning or at
the end of the string, and words will always be separated by exactly one space).

Examples:

$> ./rev_wstr "You hate people! But I love gatherings. Isn't it ironic?" | cat -e
ironic? it Isn't gatherings. love I But people! hate You$
$>./rev_wstr "abcdefghijklm"
abcdefghijklm
$> ./rev_wstr "Wingardium Leviosa" | cat -e
Leviosa Wingardium$
$> ./rev_wstr | cat -e
$
$>
```
### Commented solution

<details>

<summary>rev_wstr</summary>

{% code title="rev_wstr.c" overflow="wrap" lineNumbers="true" %}
```c
#include "unistd.h"

int	main(int ac, char **av)
{
	int i;
	int j;
	int first_word;

	i = 0;
	first_word = 0;
	if (ac == 2)
	{
		while (av[1][i] != '\0')
			i++;
		i--;
		while (i >= 0)
		{
			while (i >= 0 && (av[1][i] == ' ' || av[1][i] == '\t'))
				i--;
			j = i;
			while (j >= 0 && av[1][j] != ' ' && av[1][j] != '\t')
				j--;
			if (first_word)
				write(1, " ", 1);
			write(1, &av[1][j + 1], i - j);
			first_word = 1;
			i = j;
		}
	}
	write(1, "\n", 1);
	return (0);
}
```
{% endcode %}

</details>