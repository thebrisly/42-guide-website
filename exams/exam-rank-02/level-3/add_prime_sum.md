# add\_prime\_sum

### Subject

```
Assignment name  : add_prime_sum
Expected files   : add_prime_sum.c
Allowed functions: write, exit
--------------------------------------------------------------------------------

Write a program that takes a positive integer as argument and displays the sum
of all prime numbers inferior or equal to it followed by a newline.

If the number of arguments is not 1, or the argument is not a positive number,
just display 0 followed by a newline.

Yes, the examples are right.

Examples:

$>./add_prime_sum 5
10
$>./add_prime_sum 7 | cat -e
17$
$>./add_prime_sum | cat -e
0$
$>
```

### Commented solution

There's actually nothing really complicated in the fact of making a simple addition between some numbers, the real challenge is to build the supportive function, hope you remember how to build an `atoi` function.

<details>

<summary>add_prime_sum.c</summary>

{% code title="add_prime_sum.c" overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

void ft_putchar(char c);
void ft_putnbr(int nbr);
int is_prime(int nbr);
int ft_atoi(char *str);

void ft_putchar(char c)
{
    write(1, &c, 1);
}

void ft_putnbr(int nbr)
{
    unsigned int nb;
    
    if (nbr < 0)
    {
        ft_putchar('-');
        nb = -nbr;
    }
    else
    	nb = nbr;
    if (nb >= 10)
        ft_putnbr(nb / 10);
    ft_putchar(nb % 10 + '0');
}

// checking if a number is a prime number
int is_prime(int nbr)
{
    // first prime number is 3, if nbr smaller than that we
    // can return 0 to say it's not prime
    if (nbr < 2)
        return (0);
    // checking all factors up until half nbr
    // going over nbr/2 is useless, let's take an example
    // nbr = 10; nbr/2 = 5; If we check for 3, checking for 6
    // will give the same result
    int i = 2;
    while (i <= nbr / 2)
    {
        if (nbr % i == 0)
            return (0);
        i++;
    }
    return (1);
}

// You know how this works
int ft_atoi(char *str)
{
    int res = 0, sign = 1, i = 0;
    while (str[i] == ' ')
        i++;
    if (str[i] == '+' || str[i] == '-')
        if (str[i++] == '-')
            sign = -1;
    while (str[i] && str[i] >= 48 && str[i] <= 57)
    {
        res *= 10;
        res += str[i] - 48;
        i++;
    }
    res *= sign;
    return (res);
}

int main(int ac, char **av)
{
    if (ac != 2 || ft_atoi(av[1]) <= 0)
    {
        write(1, "0\n", 2);
        return (0);
    }
    int n = ft_atoi(av[1]);
    
    // The following is the actual logic for add_prime_sum
    // we check every number up until what's given via the
    // command line and if the number is prime, we add it
    // to the whole sum.
    int sum = 0;
    while (n > 1)
    {
        if (is_prime(n))
            sum += n;
        n--;
    }
    ft_putnbr(sum);
    ft_putchar('\n');
}
```
{% endcode %}

</details>
