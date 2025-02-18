# search\_and\_replace

### Subject

{% code overflow="wrap" %}
```
Assignment name  : search_and_replace
Expected files   : search_and_replace.c
Allowed functions: write, exit
--------------------------------------------------------------------------------

Write a program called search_and_replace that takes 3 arguments, the first
arguments is a string in which to replace a letter (2nd argument) by
another one (3rd argument).

If the number of arguments is not 3, just display a newline.

If the second argument is not contained in the first one (the string)
then the program simply rewrites the string followed by a newline.

Examples:
$>./search_and_replace "Papache est un sabre" "a" "o"
Popoche est un sobre
$>./search_and_replace "zaz" "art" "zul" | cat -e
$
$>./search_and_replace "zaz" "r" "u" | cat -e
zaz$
$>./search_and_replace "jacob" "a" "b" "c" "e" | cat -e
$
$>./search_and_replace "ZoZ eT Dovid oiME le METol." "o" "a" | cat -e
ZaZ eT David aiME le METal.$
$>./search_and_replace "wNcOre Un ExEmPle Pas Facilw a Ecrirw " "w" "e" | cat -e
eNcOre Un ExEmPle Pas Facile a Ecrire $
```
{% endcode %}

### Commented solution

<details>

<summary>search_and_replace</summary>

{% code title="search_and_replace.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char *av[])
{
    if (ac == 4)
    {
        int i;
        
        i = 0;
        /* loop over the whole string only if the second and 
         * third argument are only one character
         */
        while (av[1][i])
        {
            /* if the current character is the one we have to
             * replace, we replace it by the third argument
             */
            if (av[1][i] == av[2][0])
                av[1][i] = av[3][0];
            /* then we write the current character
             */
            write(1, &av[1][i], 1);
            i++;
        }
    }
    /* at the very end we write a new line, that way we write
     * the new line everytime, whether we have enough argument or not
     */
    write(1, "\n", 1);
}
```
{% endcode %}

</details>
