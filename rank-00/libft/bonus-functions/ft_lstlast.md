# ft\_lstlast

### Subject

{% code overflow="wrap" %}
```
FT_LSTLAST (simplified)

NAME
    ft_lstlast -- get the last element of the list
SYNOPSIS
    t_list *ft_lstlast(t_list *lst);
DESCRIPTION
    Returns the last element of the list
PARAMETERS
    lst: the start of the list
RETURN VALUES
    Last element of the list
AUTHORIZED EXTERNAL FUNCTIONS
    None
```
{% endcode %}

### Understandable explanation

I think that for this one the subject is clear enough, we have to return a pointer to the last element of the list, it's pretty easy to understand.

### Hints

For this one, we basically have to do the same thing as for the `ft_lstsize` function but we don't need to count how many elements are in the list nor return the count, but we directly return the `tmp` element.&#x20;

### Commented solution

<details>

<summary>ft_lstlast</summary>

{% code title="ft_lstlast.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

t_list *ft_lstlast(t_list *lst)
{
    t_list *tmp;
    
    if (!lst)
        return (NULL);
    tmp = lst;
    /* instead of looping directly over the element, we check if
     * there is a next element in the list, if not, that means we
     * reached the end and we have to return the current pointer
     * if we looped over the element directly like for ft_lstsize
     * we would be returning NULL every time
     */
    while (tmp->next)
        tmp = tmp->next;
    return (tmp);
}
```
{% endcode %}

</details>
