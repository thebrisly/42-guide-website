# ulstr

### Subject

{% code overflow="wrap" %}
```
Assignment name  : ulstr
Expected files   : ulstr.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a program that takes a string and reverses the case of all its letters.
Other characters remain unchanged.

You must display the result followed by a '\n'.

If the number of arguments is not 1, the program displays '\n'.

Examples :

$>./ulstr "L'eSPrit nE peUt plUs pRogResSer s'Il staGne et sI peRsIsTent VAnIte et auto-justification." | cat -e
l'EspRIT Ne PEuT PLuS PrOGrESsER S'iL STAgNE ET Si PErSiStENT vaNiTE ET AUTO-JUSTIFICATION.$
$>./ulstr "S'enTOuRer dE sECreT eSt uN sIGnE De mAnQuE De coNNaiSSanCe.  " | cat -e
s'ENtoUrER De SecREt EsT Un SigNe dE MaNqUe dE COnnAIssANcE.  $
$>./ulstr "3:21 Ba  tOut  moUn ki Ka di KE m'en Ka fe fot" | cat -e
3:21 bA  ToUT  MOuN KI kA DI ke M'EN kA FE FOT$
$>./ulstr | cat -e
$
```
{% endcode %}

### Commented solution

<details>

<summary>ulstr</summary>

{% code title="ulstr.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

int main(int ac, char *av[])
{
    /* checking the number of argument 
     */
    if (ac == 2)
    {
        int i;
        
        i = 0;
        /* looping over the whole string
         */
        while (av[1][i])
        {
            /* if the character is an upper-case letter
             * add 32 to it to get the corresponding lower-case
             * letter
             */
            if (av[1][i] >= 65 && av[1][i] <= 90)
                av[1][i] += 32;
            /* if the character is a lower-case letter
             * substract 32 from it to get the corresponding upper-case
             * letter
             */
            else if (av[1][i] >= 97 && av[1][i] <= 122)
                av[1][i] -= 32;
            /* we can then write the current character and 
             * increment i
             */
            write(1, &av[1][i], 1);
            i++;
        }
    }
    /* at the very end, we write a new line, that way if the number
     * of argument is not correct, we'll write a single newline
     */
    write(1, "\n", 1);
}
```
{% endcode %}

</details>
