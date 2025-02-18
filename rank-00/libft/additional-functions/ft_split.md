# ft\_split

### Subject

{% code overflow="wrap" %}
```
FT_SPLIT (simplified)

NAME
    ft_split -- split a string into an array of words
SYNOPSIS
    char **ft_split(const char *s, char c);
DESCRIPTION
    Allocate (with malloc(3)) and returns an array of strings obtained by splitting s with the character c, used as delimiter.
    The returned array must be NUL-terminated.
PARAMETERS
    s: string to split
    c: delimiter character
RETURN VALUES
    ft_split() returns an array of strings resulting from the splitting of s; NULL if the memory allocation failed.
AUTHORIZED EXTERNAL FUNCTIONS
    malloc(3)
```
{% endcode %}

### Understandable explanation

You might have heard some things about `ft_split()` but don't worry, I'll explain everything the best I can.

{% hint style="info" %}
There's a reason why we chose ft\_split as one of our Halloween costume :joy:
{% endhint %}

The subject tells us that `ft_split()` must return an array of strings (=> an array of arrays, since strings are arrays of characters terminated by a NUL character).

We can also phrase that as an array of words, we take the string `s` and we split it to get an array containing each words of it. Each word is separated by one or more `c`, that's our word delimiter.

It's also said that our words array must be NUL-terminated. That means we have to allocate one more element in our array, that we can set to 0. By doing this we have an easy way to loop over our words array, the same as for a string: `while(words[i] != 0)`.

The subject is not that hard to understand, the more complex thing is to your code do all that.

### Hints

We don't have enough line in a single function to write `ft_split()` so we'll have to write multiple functions.

I'll quickly get over all the things we have to do to achieve a functioning `ft_split()` (the way I separate thing maybe is a sign ;))

* Count how many words there is in the string, depending on the delimiter
* Allocate an array of arrays (words array) big enough to hold all words + 1 that we can set to 0
* Allocate a string for each words in our words array and copy the words in it
* Free everything if we have a memory allocation error

{% code title="ft_split.c" overflow="wrap" lineNumbers="true" %}
```c
char **ft_split(const char *s, char c)
{
   /* allocate an array big enough to hold all the words in s */
   /* loop over the string and find the start of the word */
      /* find the end of the word */
         /* copy the world at the first free index in our words array */
   /* return our words array */   
}

int word_count(/* whatever parameter you need */)
{
   /* find and return the number of words in the string */
}

void ft_free(/* whatever argument you need */)
{
   /* free EVERYTHING you allocated */
   /* each element of the array as well as the array */
}

char *fill_word(/* whatever argument you need */)
{
   /* allocate enough room for the word */
   /* copy the word into the memory you allocated above */
   /* return the allocated word */
}
```
{% endcode %}

### Commented solution

<details>

<summary>ft_split</summary>

{% code title="ft_split.c" overflow="wrap" lineNumbers="true" %}
```c
#include "libft.h"

static int word_count(const char *str, char c);
static char *fill_word(const char *str, int start, int end);
static void *ft_free(char **strs, int count);
/* you'll probably find another way to do this than what I did
 * it's not the best thing I did, but it works
 */
static void ft_initiate_vars(size_t *i, int *j, int *s_word);

char **ft_split(const char *s, char c)
{
    char **res;
    size_t i;
    int j;
    int s_word;
    
    ft_initiate_vars(&i, &j, &s_word);
    /* allocate a table big enough to hold all the words */
    res = ft_calloc((word_count(s, c) + 1), sizeof(char *));
    if (!res)
        return (NULL);
    /* loop over the whole string */
    while (i <= ft_strlen(s))
    {
        /* this check let's us find the index of the first
         * character of the word in the string.
         * s_word acts as a trigger so that we don't update
         * the index each time around the loop
         */
        if (s[i] != c && s_word < 0)
            s_word = i;
        /* if we found the start of a word and then another
         * separator, we know that we reached the end of the word
         * this could also be the end of the string
         */
        else if ((s[i] == c || i == ft_strlen(s)) && s_word >= 0)
        {
            /* j is the index of the word in our words array
             * so here we give the full string, the start index 
             * of the word, and the current i, which is the end
             * of the word to the fill_word function which will
             * return an allocated word and set it to res[j]
             */
            res[j] = fill_word(s, s_word, i);
            /* if fill_word failed to allocate memory
            * we have to free everything, so we call the ft_free
            * function with the words array and j which is the 
            * number of word we already saved
            */
            if (!(res[j]))
                return (ft_free(res, j));
            /* when we saved our word, we reset our s_word to -1
             * so it can trigger the next word when we go back
             * around the loop
             */
            s_word = -1;
            j++;
        }
        i++;
    }
    return (res);
}

/* please find another way to do this, please */
static void ft_initiate_vars(size_t *i, int *j, int *s_word)
{
    *i = 0;
    *j = 0;
    *s_word = -1;
}

static void *ft_free(char **strs, int count)
{
    /* in this loop
     * we loop over each element of the words array 
     * and we free it
     */
    int i;
    
    i = 0;
    while (i< count)
    {
        free(strs[i]);
        i++;
    }
    /* when we freed every element
     * we can free the words array
     */
    free(strs);
    return (NULL);
}

static char *fill_word(const char *str, int start, int end)
{
    char *word;
    int i;
    
    i = 0;
    /* allocating enough memory to store the word */
    word = malloc((end - start + 1) * sizeof(char));
    if (!word)
        return (NULL);
    /* this loop copies the word from str to word
     */
    while (start < end)
    {
        word[i] = str[start];
        i++;
        start++;
    }
    /* we set the last character to 0 to NUL-terminate the string
     * and then we return the word
     * this word will be stored in our words array
     */
    word[i] = 0;
    return (word);
}

static int word_count(const char *str, char c)
{
    int count;
    int x;
    
    count = 0;
    x = 0;
    /* x is a trigger, we start counting the word only if it equals 0
     * this let's us skip all the separators, as while it is a separator
     * the x variable will still be 0
     * to make it clearer, we loop over the whole string, when we
     * encounter a character that is not a separator and our trigger is 0
     * we add one to our word count and set our trigger to 1 so it will
     * not count another word until we find another separator
     * when we found a separator, we set our trigger to 0 again so that
     * we can count another word if there's one
     * the trigger helps us take care of the strings that are only
     * composed of separator
     */
    while (*str)
    {
        if (*str != c && x == 0)
        {
            x = 1;
            count++;
        }
        else if (*str == c)
            x = 0;
        str++;
    }
    return (count);
}
```
{% endcode %}

</details>
