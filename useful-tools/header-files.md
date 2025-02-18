---
description: This page will describe some of the concepts used in header files
---

# 🏁 Header files

### What is a header file ?

A header file is a file with extension .h which contains C function declarations and macro definitions to be shared between several source files.

Note that a header file contains only function declaration and not the definitions of these functions.

{% code overflow="wrap" lineNumbers="true" %}
```c
void    ft_putchar(char c);
void    ft_putstr(char *str);
size_t    ft_strlen(char *str);
```
{% endcode %}

The declaration is only the prototype of the function.\
When we compile a C source file that includes a header file, these prototypes tell our source file that the functions declared in the header exist, what are their parameters, and what type of data do they return.

The definitions of these functions can be written in as many C source files as you want to.

i.e. the `LIBFT` project has one header file that contains the declaration of all the functions, but each function is written in a separate file so that the code remains readable and we include the same header file in all of them.

### Header protection

There's a lot of chance that you had some problems with your header files when trying to pass the Norm, for something called "HEADER PROT" (or something like that) but what the f\*\*\* is that ?

Header protection is the code that wraps your entire header file :

{% code title="header_example.h" overflow="wrap" lineNumbers="true" %}
```c
#ifndef HEADER_EXAMPLE_H
# define HEADER_EXAMPLE_H

// your functions prototypes go here
// your structures / typedefs go here as well

#endif
```
{% endcode %}

Before telling you exactly what this code do, I have to show you what a source file in which you include a header looks like when you compile it.

Let's keep `LIBFT` as an example

{% code title="libft.h" overflow="wrap" lineNumbers="true" %}
```c
size_t ft_strlen(char *s);
int ft_isdigit(int c);
```
{% endcode %}

{% code title="ft_strlen.c" overflow="wrap" lineNumbers="true" %}
```c
// This is what the code looks like before compilation

#include "libft.h"

size_t ft_strlen(char *s)
{
    size_t i;
    
    i = 0;
    while (s[i])
        i++;
    return (i);
}
```
{% endcode %}

{% code title="ft_isdigit.c" overflow="wrap" lineNumbers="true" %}
```c
// This is what the code looks like before compilation

#include "libft.h"

int ft_isdigit(int c)
{
    return (c >= 48 && c <= 57);
}
```
{% endcode %}

Above, I wrote 3 files, one header, and two source files that both include the same header file. Above is what the files look like before compilation, below, the same files after compilation.

{% code title="ft_strlen.c" overflow="wrap" lineNumbers="true" %}
```c
size_t ft_strlen(char *s);
int ft_isdigit(int c);

size_t ft_strlen(char *s)
{
    size_t i;
    
    i = 0;
    while (s[i])
        i++;
    return (i);
}
```
{% endcode %}

{% code title="ft_isdigit.c" overflow="wrap" lineNumbers="true" %}
```c
size_t ft_strlen(char *s);
int ft_isdigit(int c);

int ft_isdigit(int c)
{
    return (c >= 48 && c <= 57);
}
```
{% endcode %}

As you can see, the whole content of the header file was pasted at the top of each file (where we put the include statement before compilation). But since both our files will be compiled together in the same library, we don't have to include it in both files (or as many files as we included the header in), only including it in one of our source file is enough. That's the whole point of header protection, including headers only once.

If I write the same header with header protection like so :

{% code title="libft.h" overflow="wrap" lineNumbers="true" %}
```c
#ifndef LIBFT_H
# define LIBFT_H

size_t ft_strlen(char *s);
int ft_isdigit(int c);

#endif
```
{% endcode %}

Our source files after compilation will look like this :

{% code title="ft_strlen.c" overflow="wrap" lineNumbers="true" %}
```c
size_t ft_strlen(char *s);
int ft_isdigit(int c);

size_t ft_strlen(char *s)
{
    size_t i;
    
    i = 0;
    while (s[i])
        i++;
    return (i);
}
```
{% endcode %}

{% code title="ft_isdigit.c" overflow="wrap" lineNumbers="true" %}
```c
int ft_isdigit(int c)
{
    return (c >= 48 && c <= 57);
}
```
{% endcode %}

Why was the header included only once this time ?&#x20;

The header protection has a weird syntax, let's go over it line by line.

```c
#ifndef LIBFT_H
```

This first line means `if not defined LIBFT_H`, the preprocessor checks if the macro `LIBFT_H` is defined or not. If it is not defined, it takes into account everything that is between this statement and the last statement of our header file.

```c
# define LIBFT_H
```

This is a macro definition, as you would do for any other values, the name of this macro must follow a specific format, check the Norm to find what it should be, but remember that the name of the file is `libft.h` and the macro for `example_header.h` is `EXAMPLE_HEADER_H`, I'm sure you can figure it out.

Why do we define it ? So that next time we include the header file, this macro will be defined, so everything between `ifndef` and `endif` will be skipped as if it was never there. This way we only include the content of the header file at the top of one of all the source files.

And finally, the last statement of the header protection:

```c
#endif
```

This statement ends the `if` we opened at the top of the header file with `ifndef`.

#### TLDR

Header protection is a wrapper around all our header file content to include the content of this header only in one of the source file and not in every file.

The syntax of the header protection is the following:

```c
#ifndef FILENAME_H
# define FILENAME_H

// other includes (stdio.h, stdlib.h, etc)
// your function declarations
// structrures declarations

#endif
```

### Macros

A macro in a header file is what you declare with the `#define` statement.

You could, for example, define a macro called `WIN_H` that holds the height of the window you want to create, or `BUFFER_SIZE` to tell the program how much characters it has to read every time you call the function `read()` (that's what you have to do for [`get_next_line`](../rank-01/get_next_line/)).

Here are these examples:

{% code title="example_header.h" overflow="wrap" lineNumbers="true" %}
```c
#ifndef EXAMPLE_HEADER_H
# define EXAMPLE_HEADER_H
# define WIN_H 720
# define WIN_W 1280
# define BUFFER_SIZE 42

char *get_next_line(int fd);

#endif
```
{% endcode %}

You could have multiple screen resolutions pre-defined and choose one or another by commenting a define statement or not like so:

{% code title="example_header.h" overflow="wrap" lineNumbers="true" %}
```c
#ifndef EXAMPLE_HEADER_H
# define EXAMPLE_HEADER_H
//# define 720P
# define 360P
# define BUFFER SIZE 42

# ifdef 720P
#  define WIN_W 1280
#  define WIN_H 720
# endif

# ifdef 360P
#  define WIN_W 640
#  define WIN_H 360
# endif

# include <stdio.h>

char *get_next_line(int fd);

#endif
```
{% endcode %}

The above header file will set the `WIN_W` macro to `640` and the `WIN_H` macro to `360`.

#### What are macros used for ?

A defined macro can be used in every source files where the header is included.

To use it, it is really simple, if we take the example of a window size we could write this:

{% code title="main.c" overflow="wrap" lineNumbers="true" %}
```c
#include "example_header.h"

int main(void)
{
    printf("Window Height: %d\n", WIN_H);
    printf("Window Width : %d\n", WIN_W);
    return (0);
}
```
{% endcode %}

What will happen when you compile the above source file is that the preprocessor will replace the macros name with the values you set in the header file.

In this example WIN\_H will be replaced by 360 and WIN\_W by 640. So the expected result of running this program will be this:

{% code overflow="wrap" %}
```shell
$> ./a.out
$> Window Height: 360
$> Window Width : 640
$>
```
{% endcode %}
