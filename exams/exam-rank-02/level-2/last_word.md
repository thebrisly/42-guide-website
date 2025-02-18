# last\_word

### Subject

```
Assignment name  : last_word
Expected files   : last_word.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes a string and displays its last word followed by a \n.

A word is a section of string delimited by spaces/tabs or by the start/end of
the string.

If the number of parameters is not 1, or there are no words, display a newline.

Example:

$> ./last_word "FOR PONY" | cat -e
PONY$
$> ./last_word "this        ...       is sparta, then again, maybe    not" | cat -e
not$
$> ./last_word "   " | cat -e
$
$> ./last_word "a" "b" | cat -e
$
$> ./last_word "  lorem,ipsum  " | cat -e
lorem,ipsum$
$>
```

### Commented solution

<details>

<summary>last_word.c</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main (int ac, char **a)
{
	if (ac == 2)
	{
		int i = 0;

		// getting to the end of the string
		while (a[1][i])
			i++;
		i--;
		// looping over the whole string backwards
		// until we found a space
		while (a[1][i] > 32)
			i--;
		i++;
		// getting back to the end and writing the last word to
		// the screen
		while (a[1][i])
		{
			write(1, &a[1][i], 1);
			i++;
		}
	}
	write (1, "\n", 1);
}
```
{% endcode %}



</details>
