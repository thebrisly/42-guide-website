# ft\_lstadd\_front

### Subject

{% code overflow="wrap" %}
```
FT_LSTADD_FRONT (simplified)

NAME
    ft_lstadd_front -- Adds a new element at the front of the list
SYNOPSIS
    void ft_lstadd_front(t_list **lst, t_list *new);
DESCRIPTION
    Add the 'new' element at the front of the list
PARAMETERS
    lst: pointer address to the first element of the list
    new: pointer address of the new element to add to the list
RETURN VALUES
    None
AUTHORIZED EXTERNAL FUNCTIONS
    None
```
{% endcode %}

### Understandable explanation

This function lets us add a new element to the front of an existing list.

We receive the new element and the existing list.

### Hints

<pre class="language-c" data-title="ft_lstadd_front" data-overflow="wrap" data-line-numbers><code class="lang-c"><strong>/* set the new element's next address to point 
</strong><strong> * to the start of the existing list
</strong><strong> */
</strong><strong>/* set the existing list pointer to point to the new element
</strong><strong> */
</strong></code></pre>

### Commented solution

<details>

<summary>ft_lstadd_front</summary>

{% code title="ft_lstadd_front.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

void ft_lstadd_front(t_list **alst, t_list *new)
{
    /* setting the new element's next address to point
     * to the start of the existing list
     */
    new->next = *alst;
    /* set the existing list pointer to point to the new element
     */
    *alst = new;
}
```
{% endcode %}

</details>
