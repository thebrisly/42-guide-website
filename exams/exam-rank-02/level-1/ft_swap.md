# ft\_swap

### Subject

{% code overflow="wrap" %}
```
Assignment name  : ft_swap
Expected files   : ft_swap.c
Allowed functions:
--------------------------------------------------------------------------------

Write a function that swaps the contents of two integers the adresses of which
are passed as parameters.

Your function must be declared as follows:

void	ft_swap(int *a, int *b);
```
{% endcode %}

### Commented solution

<details>

<summary>ft_swap</summary>

{% code title="ft_swap.c" overflow="wrap" lineNumbers="true" %}
```c
void ft_swap(int *a, int *b)
{
    /* we have to declare a temporary variable
     * to make a swap between 2 variables
     */
    int x;
    
    // set our temporary variable to be equal to the value of *a
    x = *a;
    // set the value of *a to be equal to the value of *b
    *a = *b;
    // set the value of *b to be equal to the value of x
    *b = x;
}
```
{% endcode %}

</details>
