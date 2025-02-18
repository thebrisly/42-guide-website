# pgcd

### Subject

```
Assignment name  : pgcd
Expected files   : pgcd.c
Allowed functions: printf, atoi, malloc, free
--------------------------------------------------------------------------------

Write a program that takes two strings representing two strictly positive
integers that fit in an int.

Display their highest common denominator followed by a newline (It's always a
strictly positive integer).

If the number of parameters is not 2, display a newline.

Examples:

$> ./pgcd 42 10 | cat -e
2$
$> ./pgcd 42 12 | cat -e
6$
$> ./pgcd 14 77 | cat -e
7$
$> ./pgcd 17 3 | cat -e
1$
$> ./pgcd | cat -e
$
```

### Commented solution

<pre class="language-c" data-overflow="wrap" data-line-numbers><code class="lang-c"><strong>#include &#x3C;stdio.h>
</strong><strong>#include &#x3C;stdlib.h>
</strong><strong>
</strong><strong>int main(int ac, char **av)
</strong>{

    if (ac == 3)
    {
        // I won't explain the whole thing
	// but if we take 14 and 77 as input we would
	// have the following (each iteration separated by ;)
	// 14; 14; 14; 14; 14; 14; 7
	// 77; 63; 49; 35; 21; 7;  7
        int number1 = atoi(av[1]);
        int number2 = atoi(av[2]);
        
        if (number1 > 0 &#x26;&#x26; number2 > 0)
<strong>        {
</strong><strong>            while (number1 != number2)
</strong><strong>            {
</strong><strong>                if (number1 > number2)
</strong><strong>                    number1 = number1 - number2;
</strong><strong>                else
</strong><strong>                    number2 = number2 - number1;
</strong><strong>            }
</strong><strong>            printf("%d", number1);
</strong><strong>        }
</strong>    }
    printf("\n");
}
</code></pre>
