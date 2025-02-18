# ft\_lstiter

### Subject

{% code overflow="wrap" %}
```
FT_LSTITER (simplified)

NAME
    ft_lstiter -- apply a function to each element's content
SYNOPSIS
    void ft_lstiter(t_list *lst, void (*f)(void *));
DESCRIPTION
    Iterate over the list 'lst' and apply the function 'f' to the content of all elements.
PARAMETERS
    lst: pointer address to one element
    f: function to apply
RETURN VALUES
    None
AUTHORIZED EXTERNAL FUNCTIONS
    None
```
{% endcode %}

### Understandable explanation

This function iterates over the whole list and applies the function `f` to the content of each elements.

### Hints

```c
/* loop over the entire list */
/* apply the function 'f' to the content of each elements */
```

### Commented solution

<details>

<summary>ft_lstiter</summary>

{% code title="ft_lstiter.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void ft_lstiter(t_list *lst, void (*f)(void *)
{
    t_list *tmp;
    
    tmp = lst;
    /* loop while tmp is not null */
    while (tmp)
    {
        /* apply the function f to the content of the current
         * element
         */
        f(tmp->content);
        /* set tmp to point to the next element */ 
        tmp = tmp->next;
    }
}
```
{% endcode %}

</details>
