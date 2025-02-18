# ft\_range

## Subject

```
Assignment name  : ft_range
Expected files   : ft_range.c
Allowed functions: malloc
--------------------------------------------------------------------------------

Write the following function:

int     *ft_range(int start, int end);

It must allocate (with malloc()) an array of integers, fill it with consecutive
values that begin at start and end at end (Including start and end !), then
return a pointer to the first value of the array.

Examples:

- With (1, 3) you will return an array containing 1, 2 and 3.
- With (-1, 2) you will return an array containing -1, 0, 1 and 2.
- With (0, 0) you will return an array containing 0.
- With (0, -3) you will return an array containing 0, -1, -2 and -3.
```

## Commented solution

<details>

<summary>ft_range.c</summary>

{% code title="ft_range.c" overflow="wrap" lineNumbers="true" %}
```c
int *ft_range(int start, int end)
{
    int i = 0;
    // Defining the lenght of the range
    // Since we don't have access to the abs function, we have
    // to make a manual absolute value
    int len = (end - start) < 0 ? ((end - start) * -1) + 1 : (end - start) + 1;
    // Allocating the range needed
    int *range = (int *) malloc(len * sizeof(int));
    
    // Fill in the range
    while (i < len)
    {
        // Next lines are for numbers going up
        if (start < end)
            range[i] = start++;
        // Next lines are for numbers going down
        else
            range[i] = start--;
        i++;
    }
    // Returning the filled range
    return (range);
}
```
{% endcode %}

</details>
