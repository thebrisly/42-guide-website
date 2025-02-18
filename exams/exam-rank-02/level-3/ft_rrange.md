# ft\_rrange

### Subject

```
Assignment name  : ft_rrange
Expected files   : ft_rrange.c
Allowed functions: malloc
--------------------------------------------------------------------------------

Write the following function:

int     *ft_rrange(int start, int end);

It must allocate (with malloc()) an array of integers, fill it with consecutive
values that begin at end and end at start (Including start and end !), then
return a pointer to the first value of the array.

Examples:

- With (1, 3) you will return an array containing 3, 2 and 1
- With (-1, 2) you will return an array containing 2, 1, 0 and -1.
- With (0, 0) you will return an array containing 0.
- With (0, -3) you will return an array containing -3, -2, -1 and 0.
```

### Commented solution

<details>

<summary>ft_rrange()</summary>

{% code title="ft_rrange.c" overflow="wrap" lineNumbers="true" %}
```c
int *ft_rrange(int start, int end)
{
    int i = 0;
    // Defining the length of the range
    // Since we don't have access to the abse function, we have
    // to make a manual absolute value
    int len = (end - start) < 0 ? ((end - start) * -1) + 1 : (end - start) + 1;
    // Allocating the range needed
    int *range = (int *) malloc(len * sizeof(int));
    
    // Fill in the range
    while (i < len)
    {
        // Next lines are for numbers going up
        if (end < start)
            range[i] = end++;
        // Next lines are for numbers going down
        else
            range[i] = end--;
        i++;
    }
    // Returning the filled range
    return (range);
}
```
{% endcode %}

</details>
