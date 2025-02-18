# ft\_lstdelone

### Subject

{% code overflow="wrap" %}
```
FT_LSTDELONE (simplified)

NAME
    ft_lstdelone -- removes one element from the list
SYNOPSIS
    void ft_lstdelone(t_list *lst, void (*del)(void *));
DESCRIPTION
    Free the memory of the element passed as parameter using the 'del' function then free(3). The memory of 'next' must not be freed.
PARAMETERS
    lst: the element to free
    del: address of the function that can delete the element's content
RETURN VALUES
    None
AUTHORIZED EXTERNAL FUNCTIONS
    free(3)
```
{% endcode %}

### Understandable explanation

This function takes a list element as parameter and deletes its content as well as free the allocated memory using the `del` function passed as parameter too.

### Hints

{% code overflow="wrap" %}
```c
/* use the delete function on the element's content */
/* free the element */
```
{% endcode %}

### Commented solution

<details>

<summary>ft_lstdelone</summary>

{% code title="ft_lstdelone.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void ft_lstdelone(t_list *lst, void (*del)(void *))
{
    /* use the del function on the element's content */
    del(lst->content);
    /* free the element */
    free(lst);
}
```
{% endcode %}

</details>
