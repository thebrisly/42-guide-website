# ft\_lstadd\_back

### Subject

{% code overflow="wrap" %}
```
FT_LSTADD_BACK (simplified)

NAME
    ft_lstadd_back -- adds a new node at the end of the list
SYNOPSIS
    void ft_lstadd_back(t_list **lst, t_list *new);
DESCRIPTION
    Add the 'new' element at the end of the list
PARAMETERS
    lst: pointer address of the first element of the list
    new: pointer address of the new element to add to the list
RETURN VALUES
    None
AUTHORIZED EXTERNAL FUNCTIONS
    None
```
{% endcode %}

### Understandable explanation

This function lets us add a new element to the end of an existing list.

### Hints

```c
/* get the last element of the list */
/* set the last->next variable to point to the new element */
/* if last is NULL, make the list pointer point to the new element */
```

### Commented solution

<details>

<summary>ft_lstadd_back</summary>

{% code title="ft_lstadd_back.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void ft_lstadd_back(t_list **alst, t_list *new)
{
    t_list *last;
    
    /* using ft_lstlast to get the last element of the list
     */
    last = ft_lstlast(*alst);
    /* if last is NULL, there is no list, so we set the list pointer
     * to point to the new element
     */
    if (!last)
        *alst = new;
    /* we set the last's next variable to point to the new element
     */
    last->next = new;
}
```
{% endcode %}

</details>
