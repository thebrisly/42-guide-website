# ft\_isalnum

### Subject

{% code overflow="wrap" %}
```
ISALNUM(3) (simplified)

NAME
    isalnum -- alphanumeric character test
SYNOPSIS
    int isalnum(int c)
DESCRIPTION
    The isalnum() function tests for any character for which isalpha(3) or isdigit(3) is true. The value of the argument must be representable as an unsigned char or the value of EOF.
RETURN VALUES
    The isalnum() function returns zero if the character tests false and returns non-zero if the character tests true.
```
{% endcode %}

### Understandable explanation

For this function, the man is self-explanatory, but I'll still explain it in other words.

The `isalnum()` function returns a non-zero value if the character passed as an `int` parameter is alphabetical or a decimal digit character.

If the character is not alphabetical nor a decimal digit character, the `isalnum()` function returns `0`.

### Hints

{% code title="ft_isalnum.c" overflow="wrap" lineNumbers="true" %}
```c
int    ft_isalnum(int c)
{
    if (/* c isalpha or c isdigit */)
        return (/* non-zero value of your choice */);
    return (0);
}
```
{% endcode %}

### Commented solution

{% hint style="danger" %}
Come on ! You really need the code for that function ?
{% endhint %}

<details>

<summary>ft_isalnum (variant 1)</summary>

<pre class="language-c" data-title="ft_isalnum.c" data-overflow="wrap" data-line-numbers><code class="lang-c"><strong>#include "libft.h"
</strong><strong>
</strong><strong>int    ft_isalnum(int c)
</strong>{
    /* This checks makes use of the 2 preceeding functions we built */
    if (ft_isalpha(c) || ft_isdigit(c))
        return (c); //If we reach this point we can return c as it will be a non-zero value
    return (0);
}
</code></pre>

</details>

<details>

<summary>ft_isalnum (variant 2)</summary>

{% code title="ft_isalnum.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

int    ft_isalnum(int c)
{
    /* This check is the same as the variant one but without using the pre-existing functions, it's longer to write, it could be useful if you don't want to have it being dependant on other functions */
    if ((c >= 48 && c <= 57) || (c >= 65 && c <= 90) || (c >= 97 && c <= 122))
        return (c); // If we reach thi point we can simply return c as it will be a non-zero value
    return (0);
}
```
{% endcode %}

</details>
