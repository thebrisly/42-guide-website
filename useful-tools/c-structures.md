---
description: What are C structures
---

# 🧱 C Structures

### Introduction

**Structures** are a way to group several related variables into one place.\
Each variable in the structure is known as a **member** of the structure.

To make it clearer, I will use the example of a library that wants to store information about books :

* Book title
* Book author
* Book ID

### Difference between array and structures

Arrays allow you to store multiple variables of the same data type, an array of `int`, an array of `char`, etc.

Structures allow you to store multiple variables of **different** data types. You could have one `int` member, one `char` member, multiple `double` members, etc.

### Create a Structure

Structures are generally declared in a header file so it is usable everywhere the header file is included.

They are created using the **struct** keyword like this :

{% code title="main.h" lineNumbers="true" %}
```c
struct [structure tag]
{
   member definition;
   member definition;
   ...
   member definition;
} [one or more structure variables];
```
{% endcode %}

#### Using structure tag and variables

Structure tag and structure variables are concepts that are easily explained with examples.&#x20;

I'll explain the difference between the two usage.

{% code lineNumbers="true" %}
```c
// With Structure Tag s_st1
struct s_st1
{
    int x;
    char c;
} a = {100, 'a'}, b = {50, 'b'};

// Without Structure Tag
struct
{
    int x;
    char c;
} c = {100, 'a'}, d = {50, 'b'};
```
{% endcode %}

`a` and `c` will have the same content, as expected.\
`b` and `d` will also have the same content, as expected.

The difference lies in the fact that you can create new variables based on the struct `s_st1` whenever you want in your code, but won't be able to do so for the anonymous structure.

If you want to create a new variable based on the structure you'll have to do the following :

<pre class="language-c" data-line-numbers><code class="lang-c">// Declaring new variable for the s_st1 structure.
<strong>// You can do this whenever you want in your code.
</strong><strong>struct s_st1 e;
</strong>e = {25, 'e'};
<strong>
</strong><strong>// Declaring new variable for the anonymous structure.
</strong><strong>// => go to the original structure declaration
</strong>struct
{
    int x;
    char c;
} c = {100, 'a'}, d = {50, 'b'}, f;
// Add a new variable to the list (i.e. 'f')
// once that's done you can assign values to the variable f
f = {25, 'f'};
</code></pre>

As you can see, using a named structure can be easier if you need to declare a new variable later in your code.

For example, our s\_book structure would be declared like this :

{% code overflow="wrap" lineNumbers="true" %}
```c
struct s_book
{
    char title[50];
    char author[50];
    int  book_id;
};

// later in the code we could use this line to declare new Books
struct s_book LOTR1 = {"The Lord of the Rings 1", "J.R.R. Tolkien", 44003415};
struct s_book LOTR2;

strcpy(LOTR2.title, "The Lord of the Rings 2");
strcpy(LOTR2.author, "J.R.R. Tolkien");
LOTR2.book_id = 44003416;
```
{% endcode %}

{% hint style="info" %}
Note that I named the structure since we would be using it to create multiple books in our code.
{% endhint %}

### Accessing structure members

To access a member of a structure, we have to use the **member access operator `.`.**

To use it, we have to put a `.` between the structure variable name and the member we want to access. See the example below to find out how it's used in a program.

{% code title="main.c" overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <string.h>

struct s_book
{
    char title[50];
    char author[50];
    int  book_id;
};

int main(void)
{
    // declaring 2 new books
    struct s_book book1;
    struct s_book book2;

    // Setting book1 members
    strcpy(book1.title, "The Lord of the Rings 1");
    strcpy(book1.author, "J.R.R. Tolkien");
    book1.book_id = 44003415;
    
    // Setting book2 members
    strcpy(book1.title, "The Lord of the Rings 2");
    strcpy(book1.author, "J.R.R. Tolkien");
    book1.book_id = 44003416;
    
    // Printing books information
    printf("%s - %s - %d\n", book1.title, book1.author, book1.book_id);
    printf("%s - %s - %d\n", book2.title, book2.author, book2.book_id);
    
    return (0);
}
```
{% endcode %}

When the above code is compiled and executed it produces the following result :

{% code overflow="wrap" %}
```
The Lord of the Rings 1 - J.R.R. Tolkien - 44003415
The Lord of the Rings 2 - J.R.R. Tolkien - 44003416
```
{% endcode %}

### Accesing structure pointer members

To access a member of a structure pointer, we have to use another **member access operator `->`.**

To use it, we have to put a `->` between the structure variable name and the member we want to access. See the example below to find out how it's used in a program.

{% code title="main.c" overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <string.h>

struct s_book
{
    char title[50];
    char author[50];
    int  book_id;
};

void printBook(struct s_book *book);

int main(void)
{
    // declaring 2 new books
    struct s_book book1;
    struct s_book book2;

    // Setting book1 members
    strcpy(book1.title, "The Lord of the Rings 1");
    strcpy(book1.author, "J.R.R. Tolkien");
    book1.book_id = 44003415;
    
    // Setting book2 members
    strcpy(book1.title, "The Lord of the Rings 2");
    strcpy(book1.author, "J.R.R. Tolkien");
    book1.book_id = 44003416;
    
    printBook(&book1);
    printBook(&book2);
    
    return (0);
}

void printBook(struct s_book *book)
{
   printf("%s - %s - %d\n", book->title, book->author, book->book_id);
}
```
{% endcode %}

When the above code is compiled and executed it produces the following result :

```
The Lord of the Rings 1 - J.R.R. Tolkien - 44003415
The Lord of the Rings 2 - J.R.R. Tolkien - 44003416
```

### Defining a type for your structure (typedef)

We use the `typedef` keyword to create an alias name for data types. It is commonly used with structures to simplify the syntax of declaring variables.

Look at the following example :

{% code overflow="wrap" lineNumbers="true" %}
```c
struct s_point
{
  int  x;
  int  y;  
};

int main(void)
{
  struct s_point p1, p2;
}
```
{% endcode %}

We can use `typedef` to write an equivalent with a simplified syntax :

{% code overflow="wrap" lineNumbers="true" %}
```c
typedef struct s_point
{
    int x;
    int y;
} t_point;

int main(void)
{
    t_point p1, p2;
}
```
{% endcode %}

### Naming convention

To respect the 42 Norm, we have to name our `structures` and `typedef` in a certain way.

This also makes it a lot easier to follow.

Structure names must start with `s_` and typedefs must start with `t_`.

```c
// incorrect structure
struct point_structure
{
    int x;
    int y;
};

// correct structure
struct s_point
{
    int x;
    int y;
};

// incorrect typedef
typedef struct s_point
{
    int x;
    int y;
} point;

// correct typedef
typedef struct s_point
{
    int x;
    int y;
} t_point;
```

### Why structs ?

Suppose you want to store information about, to keep the same example, a book : title, author, id. You can create different variables `title`, `author`, `id` to store this information.

What if you need to store information of more that one book ? Now, you need to create different variables for each informaiton per book : `title2`, `author2`, `id2`, etc.

A better approach would be to have a collection of all related information under a single named `s_book` structure and use it for every book.

#### Sources

{% embed url="https://www.tutorialspoint.com/cprogramming/c_structures.htm" %}

{% embed url="https://www.programiz.com/c-programming/c-structures" %}

{% embed url="https://www.geeksforgeeks.org/structures-c/" %}

{% embed url="https://stackoverflow.com/questions/44180120/what-is-the-use-of-struct-tag-name-in-c-programming" %}
