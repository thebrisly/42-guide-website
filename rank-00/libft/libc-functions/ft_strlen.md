# ft\_strlen

### Subject

{% code overflow="wrap" %}
```
STRLEN(3) (simplified)

NAME
    strlen -- find length of string
SYNOPSIS
    size_t(const char *s);
DESCRIPTION
    The strlen() function computes the length of the string s.
RETURN VALUES
    The strlen() function returns the number of characters that precede the terminating NUL character.
```
{% endcode %}

### Understandable explanation

For this function, the man is pretty self-explanatory on what the function does, but some things are new, we never seen some things before.

The `strlen()` function returns the number of characters before the terminating `NUL` (`\0`) character of the string.

#### What does this mean ?

If our string is `abcde\0`, `strlen()` will return `5`.

The string we pass as parameter has the keyword `const` before it, this means we can't modify this string inside our function, since it's a constant value.

The returned value of `strlen()` is of type `size_t`, what is it ? Let me explain.

As said on [geeksforgeeks.org](https://geeksforgeeks.org/size_t-data-type-c-language), the `size_t` data type is a type which is used to represent the size of objects in bytes and is therefore used as the return type by the `sizeof` operator. It is guaranteed to be big enough to contain the size of the biggest object the host system can handle. Basically the maximum permissible size is dependent on the compiler; if the compiler is 32 bit then it is simply a typedef (i.e., alias) for `unsigned int` but if the compiler is 64 bit then it would be a typedef for `unsigned long long`. The `size_t` data type is never negative.

### Hints

{% code title="ft_strlen.c" overflow="wrap" lineNumbers="true" %}
```c
size_t    ft_strlen(const char *s)
{
    while( /* we are not reading \0 character */)
        /* increment a counter and read next char */
    return (/* the counter */);
}
```
{% endcode %}

### Commented solution

{% hint style="danger" %}
Come on ! You wrote this function like a hundred times during the Piscine, you really need to see the code ?
{% endhint %}

<details>

<summary>ft_strlen</summary>

{% code title="ft_strlen.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

size_t    ft_strlen(cont char *s)
{
    /* usually we declare our counter as an int, but for this one
     * we'll declare it as a size_t since size_t is bigger than int
     */
    size_t    i;
    
    i = 0;
    /* we then iterate over all the characters in the s array
     * you might think there's no exit condition on this loop but
     * there is. If the character we read is \0 then the loop
     * condition will evaluate to false, therefore not going into
     * it again.
     */
    while (s[i])
        i++;
    /* as said in the hint, we return the counter, it will be equal
     * to the number of character before the terminating \0
     * character
     */
    return (i);
}
```
{% endcode %}

</details>
