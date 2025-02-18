# ft\_list\_size

## Subject

```
Assignment name  : ft_list_size
Expected files   : ft_list_size.c, ft_list.h
Allowed functions:
--------------------------------------------------------------------------------

Write a function that returns the number of elements in the linked list that's
passed to it.

It must be declared as follows:

int	ft_list_size(t_list *begin_list);

You must use the following structure, and turn it in as a file called
ft_list.h:

typedef struct    s_list
{
    struct s_list *next;
    void          *data;
}                 t_list;
```

## Commented solution

{% hint style="warning" %}
Don't forget to turn in your `ft_list.h` file as well
{% endhint %}

<details>

<summary>ft_list_size()</summary>

{% code title="ft_list_size.c" overflow="wrap" lineNumbers="true" %}
```c
#include "ft_list.h"

int ft_list_size(t_list *begin_list)
{
    int i = 0;
    
    // Loop over list elements while the next element is not null
    while (begin_list->next)
    {
        // set the original pointer equal to a pointer to the
        // next element and increment our counter
        begin_list = begin_list->next;
        i++;
    }
    // return the counter
    return (i);
}
```
{% endcode %}

</details>
