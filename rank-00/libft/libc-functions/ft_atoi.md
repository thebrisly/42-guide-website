# ft\_atoi

### Subject

{% code overflow="wrap" %}
```
ATOI(3) (simplified)

NAME
    atoi -- convert ASCII string to integer
SYNOPSIS
    int atoi(const char *str);
DESCRIPTION
    The atoi() function converts the initial portion of the string pointed to by str to int representation.
```
{% endcode %}

### Understandable explanation

The `atoi()` function converts a string to its `int` representation.

Some things that the `atoi()` function does are not clearly said in the man. I'll quickly list them here.

* The string passed as parameter may begin with an arbitrary number of whitespaces as determined by `isspace(3)`
* After the arbitrary number of whitespaces, there can be one single optional '+' or '-' sign
* The remainder of the string will be converted to an int, stopping at the first character which is not a valid digit in the given base (in our case we only need to manage base 10, so the valid digits are 0-9)

I talked about the `isspace(3)` function, what is that function ? It works the same way as the `isdigit`, `isalpha`, etc. but returning a non-zero value when the character is one of the following

<details>

<summary>isspace(3)</summary>

* \t => tabulation
* \n => new line
* \v => vertical tabulation
* \f => form feed
* \r => carriage return
* ' ' => space

</details>

To make it easier, will be coding the `isspace(3)` function as a static helper function for our `atoi(3)` function.

### Hints

{% code title="ft_atoi.c" overflow="wrap" lineNumbers="true" %}
```c
int    ft_atoi(const char *str)
{
    while (/* character isspace */)
        /* advance in the string */
    if (/* character is + and next character is not - */)
        /* advance in the string */
    if (/* character is - */)
        /* save the sign as negative */
    while (/* there is something in the string and that is a digit 0-9 */)
        /* convert the current digit value to int value */
        /* don't overwrite what we already converted */
    /* multiply the int result by the sign */
    return (/* result */);
}

static int    ft_isspace(int c)
{
    if (/* c is one of the whitespace characters */)
        return (/* non-zero value of your choice */);
    return (0);
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_atoi</summary>

{% code title="ft_atoi.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int    ft_atoi(const char *str)
{
    int    result;
    int    sign;
    int    i;
    
    result = 0;
    sign = 1;
    i = 0;
    /* here we use our version of the isspace function to check if
     * the current character is a whitespace
     */
    while (ft_isspace(str[i]))
        i++;
    /* checking if the character is a + character and that the next
     * one is not a -
     * we don't have to check if the following character is another +
     * because if the following is also a + it won't enter the following
     * condition that checks for a - character
     * and if it doesn't enter the following condition it will not enter
     * the main while loop that only checks for digits 0-9
     */
    if (str[i] == '+' && str[i + 1] != '-')
        i++;
    /* if the current character is -, we make sign equal to -1 so 
     * we can simply multiply the final result by this sign
     * to get the negative or positive number
     */
    if (str[i] == '-')
    {
        sign = -1;
        i++;
    }
    /* while we are not at the end of the string and the character is 
     * a digit between 0 and 9 
     * we multiply the current result by 10 so we add another digit
     * to the result
     * then we add the decimal value of the current character - 48 to
     * the result. the -48 part comes from the ASCII table. The '0'
     * character as the decimal value 48, and we don't want to add 48 to
     * our int result, but 0, so we substract 48. 
     * Since all digits between 0 and 9 follow each other in the ASCII
     * table, this substract works for every one of them.
     * Then we move to the next character in the string
     */
    while (str[i] && str[i] >= 48 && str[i] <= 57)
    {
        /* take a look under this expandable, I made a clearer example
         * of how this part works
         */
        result *= 10;
	result += str[i] - 48;
	i++;
    }
    /* When we converted every digit to int, we multiply the end result
     * by the sign variable
     * if the number is negative, this means we'll be multiplying by -1
     * therefore getting the negative value of result
     * if the number is positive, since the sign variable was set to 1 at
     * the beginning of the function, we multiply the end result by one,
     * so the result value stays unchanged
     */
    result *= sign;
    return (result);
}

int    ft_isspace(int c)
{
    /* this checks if the character is one of the whitespaces */
    if (c == 9 || c == 10 || c == 11 || c == 12 || c == 13 || c == 32)
        /* we could return c here, if we reach this point the value of 
         * c will be a non-zero value
         */
        return (1);
    return (0);
}
```
{% endcode %}

</details>

<details>

<summary>Conversion example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
int main(void)
{
    int result;
    
    result = 0;              // result = 0
    result *= 10;            // result = 0
    result += '1' - 48;      // result = 1
    result *= 10;            // result = 10
    result += '5' - 48;      // result = 15
    result *= 10;            // result = 150
    result += '4' - 48;      // result = 154
}
```
{% endcode %}

I hope this will help you understand what happens in the while loop of our `ft_atoi()` function.

</details>
