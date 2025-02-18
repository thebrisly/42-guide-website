# \*ft\_strlen

### Subject

{% code overflow="wrap" %}
```
Assignment name  : ft_strlen
Expected files   : ft_strlen.c
Allowed functions:
--------------------------------------------------------------------------------

Write a function that returns the length of a string.

Your function must be declared as follows:

int	ft_strlen(char *str);
```
{% endcode %}

### Commented solution

<details>

<summary>ft_strlen</summary>

I don't think I need to add any explanation, you know how this works, at least I hope so.

{% code title="ft_strlen.c" overflow="wrap" lineNumbers="true" %}
```c
int ft_strlen(char *str)
{
    int i;
    
    i = 0;
    while (str[i])
        i++;
    return (i);
}
```
{% endcode %}

</details>
