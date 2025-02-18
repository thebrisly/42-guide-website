# ft\_itoa

### Subject

{% code overflow="wrap" %}
```
FT_ITOA (simplified)

NAME
    ft_itoa -- convert an int to a string
SYNOPSIS
    char *ft_itoa(int n);
DESCRIPTION
    Allocate (with malloc(3)) and returns a string representing n.
    Negative numbers must be handled.
PARAMETERS
    n: int to convert
RETURN VALUES
    ft_itoa() returns the string representing n; NULL if the memory allocation failed.
AUTHORIZED EXTERNAL FUNCTIONS
    malloc(3)
```
{% endcode %}

### Understandable explanation

The `ft_itoa` function does the opposite work of `ft_atoi`, converting a number to a string.

### Hints

Since we need to allocate some memory for the new string created from the int value we received, we have to count how much memory we have to allocate.

We have a function that count the length of a string, so for this one we'll build one counting the number of characters representing a number.

{% hint style="warning" %}
Remember that `-` is also a character for negative numbers, so don't forget to count it when counting.
{% endhint %}

Once we know the number of characters representing the value we received, we need to allocate enough memory for it plus the NUL-terminating character.

Once that is done, we can start converting our number to string, the easiest way to do it is to go from right to left, since we know how much character the string will be, and we can use the modulo operator to get the last character of the number. And then we can simply divide the number by ten to remove the last character from it.

Remember this :

{% code lineNumbers="true" %}
```c
int a = 124;
int b = 10;
int c = a / b;
printf("%d\n", c); => 12
```
{% endcode %}

Since both values are integers, the division will effectuated as an integer division, meaning that there's no remainder nor floating point values in the result, that's why we get 12 by dividing 124 by 10.

### Commented solution

<details>

<summary>ft_itoa</summary>

{% code title="ft_itoa.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

static int int_len(long nbr);
static char *pre_conv(int len);

char *ft_itoa(int n)
{
    int len;
    int i;
    char *result;
    long nbr;
    
    /* here I convert the int n received as parameter to a long
     * this is only done so that INT_MIN and INT_MAX are not a problem
     * and I can treat them the exact same way as all other numbers
     */
    nbr = n;
    /* getting the length of the number */
    len = int_len(nbr);
    /* allocating the string with the correct size and 
     * settings result[0] = '0'
     */
    result = pre_conv(len);
    if (!result)
        return (NULL);
    /* if the number is less than 0, we do the same thing as in the
     * int_len function, we set the number equals to minus itselft. 
    if (nbr < 0)
        nbr = -nbr;
    /* we then set i = len - 1, len take into account the NUL-terminating
     * character and we don't want to overwrite ti.
    i = len - 1;
     /* then we can make the conversion from int to character */
    while (nbr != 0)
    {
        result[i] = ((nbr % 10) + 48);
        nbr = nbr / 10;
        i--;
    }
    /* if the original number was negative, we set the first character equals to null/ 0;8/
    if (n < 0)
        result[0] = '-';
    result[len] = 0;
    /* At the very end, we can return the string we just craeated \*
    return (result);
}

static char *pre_conv(int len)
{
    char *tmp;
    
    /* we allocate enough memory for len + 1 character so we
     * don't skip the NUL-terminating character
     */
    tmp = malloc((len + 1) * sizeof(char));
    if (!tmp)
        return (NULL);
    /* here I set the index 0 of the newly allocated string to be 
     * character 0.
     * I do this here, because in the ft_itoa function, if the number
     * is 0, it will result in no condition working, and if I don't
     * set the first character working, we would have whatever value
     * was in memory at tmp[0], maybe the character 0, but most often
     * this will be some random junk value
     */
    tmp[0] = '0';
    return (tmp);
}

static int_len(long nbr)
{
    int count;
    
    count = 0;
    /* the number is less than 0, we add one to the count to take
     * into account the - we'll have to add at the end
     * and we set the number equal to minus itself so it becomes 
     * positive
     */
    if (nbr < 0)
    {
        count++;
        nbr = -nbr;
    }
    /* if the number equals 0, we have to add 1 to the count
     * you could skip this check by starting the count variable at 1
     * instead of 0
     */
    if (nbr == 0)
        count++;
    /* if we get to this point, the number will be different than 0
     * we then divide the number by ten and add 1 to the count each
     * time through the loop
     */
    while (nbr != 0)
    {
        nbr /= 10;
        count++;
    }
    /* we can finally return the count that is how much characters are
     * needed to represent this number as string
     */
    return (count);
}
```
{% endcode %}

</details>
