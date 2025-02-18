# \*ft\_strcpy

### Subject

{% code overflow="wrap" %}
```
Assignment name  : ft_strcpy
Expected files   : ft_strcpy.c
Allowed functions:
--------------------------------------------------------------------------------

Reproduce the behavior of the function strcpy (man strcpy).

Your function must be declared as follows:

char    *ft_strcpy(char *s1, char *s2);
```
{% endcode %}

### Commented solution

<details>

<summary>ft_strcpy</summary>

{% code title="ft_strcpy.c" overflow="wrap" lineNumbers="true" %}
```c
// man strcpy=> char *strcpy(char *dest, const char *src)

char    *ft_strcpy(char *s1, char *s2)
{
    unsigned int i;
    
    i = 0;
    /* loop over the source string (s2)
     * if the source is empty, we don't even have to enter the loop
     */
    while (s2[i])
    {
        /* set the chracter at index i in the destination (s1) to be
         * equal to the character at index i in the source (s2)
         */
        s1[i] = s2[i];
        i++;
    }
    /* set the character at index i in the destination (s1) to 0
     * this is done to NUL-terminate the destination (s1) if we copied 
     * something inside
     * or to set the destination (s1) as empty if the source (s2) is empty
     */
    s1[i] = 0;
    return (s1);
}
```
{% endcode %}

</details>

{% hint style="success" %}
Thanks Veronique for the correction :smile:
{% endhint %}
