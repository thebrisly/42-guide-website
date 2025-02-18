# ft\_lstnew

### Subject

{% code overflow="wrap" %}
```
FT_LSTNEW (simplified)

NAME
    ft_lstnew -- create a new list node element
SYNOPSIS
    t_list *ft_lstnew(void *content);
DESCRIPTION
    Allocate (with malloc(3)) and return the new element. The member variable 'content' is initialized with the value of the 'content' parameter. The 'next' variable is initialized to NULL.
PARAMETERS
    content: The content of the new element
RETURN VALUES
    The new element.
AUTHORIZED EXTERNAL FUNCTIONS
    malloc(3)
```
{% endcode %}

### Understandable explanation

This function allocates memory for a new element of type `t_list`, setting its `content` to be the `content` parameter, and setting the `next` variable to `NULL`.

Then it returns the newly allocated / created element of the list.

### Hints

{% code title="ft_lstnew" overflow="wrap" lineNumbers="true" %}
```c
/* declare a new list element */
/* allocate memory for it */
/* set the new element variables 
 * new->content = content
 * new->next = NULL
 */
/* return the new element */
```
{% endcode %}

### Commented solution

<details>

<summary>ft_lstnew</summary>

{% code title="ft_lstnew.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

t_list *ft_lstnew(void *content)
{
    /* declaring the new list element
     */
    t_list *elem;
    
    /* allocating the memory for the new element
     */
    elem = malloc(sizeof(t_list));
    if (!elem)
        return (NULL);
    /* setting the content of the new element
     * to the 'content' parameter
     * and setting the 'next' to NULL
     */
    elem->content = content;
    elem->next = NULL;
    /* finally, we return the created element
     */
    return (elem);
}
```
{% endcode %}

</details>
