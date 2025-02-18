# ft\_lstsize

### Subject

{% code overflow="wrap" %}
```
FT_LSTSIZE (simplified)

NAME
    ft_lstsize -- returns the number of element in the list
SYNOPSIS
    int *ft_lstsize(t_list *lst);
DESCRIPTION
    Count the number of elements of the list
PARAMETERS
    lst: start of the list
RETURN VALUES
    The size of the list
AUTHORIZED EXTERNAL FUNCTIONS
    None
```
{% endcode %}

### Understandable explanation

I think the subject is clear on what this function does, we have to return the number of element of the list.

### Hints

{% code overflow="wrap" %}
```c
/* loop over the list */
/* return the count */
```
{% endcode %}

### Commented solution

<details>

<summary>ft_lstsize</summary>

{% code title="ft_lstsize.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int ft_lstsize(t_list *lst)
{
    /* I used a tmp variable so that we don't modify the 
     * existing list
     */
    t_list *tmp;
    int i;
    
    tmp = lst;
    i = 0;
    /* we loop as long as tmp is not equal to null
     * since the last element's next point to null
     * we will be iterating over all the elements of the list
     */
    while (tmp)
    {
        /* set the tmp to be its 'next' element */
        tmp = tmp->next;
        i++;
    }
    /* returning the count */
    return (i);
}
```
{% endcode %}

</details>
