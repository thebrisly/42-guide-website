# ft\_list\_remove\_if

### Subject

{% code overflow="wrap" %}
```
Assignment name  : ft_list_remove_if
Expected files   : ft_list_remove_if.c
Allowed functions: free
--------------------------------------------------------------------------------

Write a function called ft_list_remove_if that removes from the
passed list any element the data of which is "equal" to the reference data.

It will be declared as follows :

void ft_list_remove_if(t_list **begin_list, void *data_ref, int (*cmp)());

cmp takes two void* and returns 0 when both parameters are equal.

You have to use the ft_list.h file, which will contain:

$>cat ft_list.h
typedef struct      s_list
{
    struct s_list   *next;
    void            *data;
}                   t_list;
$>
```
### Commented solution

<details>

<summary>ft_list_remove_if</summary>

{% code title="ft_list_remove_if.c" overflow="wrap" lineNumbers="true" %}
```c
// You have to use the ft_list.h file, which will contain: ft_list.h

typedef struct      s_list
{
    struct s_list   *next;
    void            *data;
}                   t_list;

#include "ft_list.h"
#include "stdlib.h"

void	ft_list_remove_if(t_list **begin_list, void *data_ref, int (*cmp)())
{
	t_list *tmp;

	if ((*begin_list == NULL) || (begin_list == NULL))
		return ;
	if (cmp((*begin_list)->data, data_ref) == 0x0)
	{
		tmp = *begin_list;
		*begin_list = (*begin_list)->next;
		free(tmp);
		ft_list_remove_if(begin_list, data_ref, cmp);
	}
	else
		ft_list_remove_if(&((*begin_list)->next), data_ref, cmp);
}
```
{% endcode %}

</details>