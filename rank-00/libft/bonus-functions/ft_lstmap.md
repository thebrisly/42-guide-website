# ft\_lstmap

### Subject

{% code overflow="wrap" %}
```
FT_LSTMAP (simplified)

NAME
    ft_lstmap -- creates a new list resulting from the application of f to each element
SYNOPSIS
    t_list *ft_lstmap(t_list *lst, void (*f)(void *), void (*del)(void *));
DESCRIPTION
    Iterate over the list 'lst' and apply the function 'f' to the content of each elements. Create a new list resulting of the successive applications of 'f'. The function 'del' is used to destroy the content of an element if necessary.
PARAMETERS
    lst: pointer address to one element
    f: the address of the function to apply
    del: the address of the function that can delete an element's content
RETURN VALUES
    None
AUTHORIZED EXTERNAL FUNCTIONS
    None
```
{% endcode %}

### Understandable explanation

This functions works similarly as the `ft_lstiter` function, but it creates a new list resulting of the successive applications of `f` on each element's content.

### Hints

```c
/* check if lst or f or del is NULL */
/* loop over lst */
    /* create a new element */
    /* if new elem is null, clear the new list */
/* add the new element to the back of the list */
/* finally, return the new list */
```

### Commented solution

<details>

<summary>ft_lstmap</summary>

```c
#include "libft.h"

t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))
{
    t_list *new_list;
    t_list *new_obj;
    
    if (!lst || !f || !del)
        return (NULL);
    new_list = NULL;
    /* loop over the existing list */
    while (lst)
    {
        /* create a new object with the content being the result
         * of the application of the function f on the current element's
         * content
         */
        new_obj = ft_lstnew(f(lst->content));
        if (!new_obj)
        {
            /* if the new object is null, clear the new list */
            ft_lstclear(&new_list, del);
            return (NULL);
        }
        /* if there is a new object, add it to the back of the new list */
        ft_lstadd_back(&new_list, new_obj);
        lst = lst->next;
    }
    /* finally, we return the new list */
    return (new_list);
}
```

</details>
