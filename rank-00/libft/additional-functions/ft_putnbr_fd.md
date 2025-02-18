# ft\_putnbr\_fd

### Subject

{% code overflow="wrap" %}
```
FT_PUTNBR_FD (simplified)

NAME
    ft_putnbr_fd -- write an int on a specified file descriptor
SYNOPSIS
    void ft_putnbr_fd(int n, int fd);
DESCRIPTION
    ft_putnbr_fd() writes the int n on the file descriptor fd
PARAMETERS
    n: int to write
    fd: file descriptor on which to write
RETURN VALUES
    ft_putnbr_fd() does not return anything
AUTHORIZED EXTERNAL FUNCTIONS
    write(2)
```
{% endcode %}

### Understandable explanation

This function works the same way as the `ft_putnbr()` function you had to do during the Piscine, it also takes the `fd` parameter, like `ft_putchar_fd()`, `ft_putstr_fd()`, `ft_putendl_fd()`.

I think that going from here you should be able to build it.

### Hints

Don't forget that the character `0` is not code `0` in the `ASCII` table, I think you can take a look at your Piscine code ([`C05 - Ex04`](https://github.com/Laendrun/piscine42/blob/main/c04/ex02/ft_putnbr.c)), it works the same.

### Commented solution

<details>

<summary>ft_putnbr_fd</summary>

{% code title="ft_putnbr_fd.c" overflow="wrap" lineNumbers="true" %}
```clike
#include "libft.h"

void    ft_putnbr_fd(int n, int fd)
{
    /* this checks for INT_MIN as INT_MAX is not 
     * just INT_MIN * -1, so if we have INT_MIN, we can
     * directly write it out
     */
    if (n == -2147483648)
        write(fd, "-2147483648", 11);
    /* if the number is less than 0, we have to write a '-'
     * followed by the number, so we write the '-'
     * then we multiply the number by -1 to make it positive
     * and we call the ft_putnbr_fd function with the positive
     * number
     */
    else if (n < 0)
    {
        write(fd, "-", 1);
        n = -n;
        ft_putnbr_fd(n, fd);
    }
    else
    {
        /* here the number will be positive
         * the first thing we have to do is transform the 
         * number into each of its digit
         * we do that by calling the function again with the
         * number / 10, that removes one digit from the end 
         * of it since its an integer division
         * once we have done that, we can call the function
         * with the number % 10 to get the remainder of the 
         * itneger division, that way we get each digit.
         * if the number we send to the function is still greater
         * than zero, we make the same thing, call the function
         * with the number divided by 10, then again with 
         * with the number modulo 10
         */
        if (n > 9)
        {
            ft_putnbr_fd(n / 10, fd);
            ft_putnbr_fd(n % 10, fd);
        }
        else
        {
            /* if we get here, this means n is only one digit
             * when n is only one digit, we can convert it to 
             * its corresponding character in the ASCII table
             * and write it.
             * as for the other functions, we set the first
             * parameter of the write function to fd
             */
            digit = n + 48;
            write(fd, &digit, 1);
        }
    }
}
```
{% endcode %}

</details>
