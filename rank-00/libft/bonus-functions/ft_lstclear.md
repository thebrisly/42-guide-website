# ft\_lstclear

### Subject

{% code overflow="wrap" %}
```
FT_LSTCLEAR (simplified)

NAME
    ft_lstclear -- removes the element passed as parameter and all the following elements
SYNOPSIS
    void ft_lstclear(t_list **lst, void (*del)(void *));
DESCRIPTION
    Deletes and free the memory of the element passed as parameter and all the following elements using 'del' and free(3). Finally, the initial pointer must be set to NULL.
PARAMETERS
    lst: pointer address to one element
    del: address of the function that can delete the element's content
RETURN VALUES
    None
AUTHORIZED EXTERNAL FUNCTIONS
    free(3)
```
{% endcode %}

### Understandable explanation

This functions works similarly as the `ft_lstdelone` function, but instead of removing only one element, it removes the element passed as parameter as well as all the following elements.

### Commented solution

<details>

<summary>ft_lstclear</summary>

{% code title="ft_lstclear.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void ft_lstclear(t_list *lst, void (*del)(void *))
{
    t_list *tmp;
    /* loop over the list */
    while (*lst)
    {
        /* set the tmp to point to the next element of the list */
        tmp = (*lst)->next;
        /* use ft_lstdelone on the current element */
        ft_lstdelone(*lst, del);
        /* set the list pointer equal to tmp, so that we have a 
         * pointer to the next element
         */
        *lst = tmp;
    }
    /* free the list pointer and set it to NULL */
    free(*lst);
    *lst = NULL;
}
```
{% endcode %}

</details>
