---
description: >-
  This is the new concept that we learn during this project. It is essential to
  understand it well before moving on.
---

# ▪️ Variadic functions

The functions you have used and created so far in your course had fixed arguments. There could be several, but you always knew in advance what arguments you would need.

For example strlen only takes a string as input `(int ft_strlen(char *str))` and split takes two elements as input `(**ft_split(char const *s, char c))`. You get the idea.



A **variadic function** is a function which accepts a <mark style="color:red;">**variable number of arguments**</mark><mark style="color:red;">.</mark> It is characterized by the **"..."** in a function.&#x20;

```c
int	ft_printf(const char *format, ...);

// const char *format is the mandatory argument of printf
```

{% hint style="warning" %}
The variadic function must have at least one **mandatory argument.** There is no minimum for the number of variable arguments.
{% endhint %}



When someone calls the printf function, we don't know in advance how many elements the person wants to display. In other words, we don't know how many times the format specifier will be used.

```c
printf("hello my name is %s and i am %d old\n", "laura", 23);
```

In the above case, the function takes two other arguments, in addition to the initial string. If you knew in advance how many arguments you were using and of what type, the function could be rewritten in this way:&#x20;

```c
int	ft_printf(const char *format, char *string, int age);
```



Thankfully the C language is well done. There is no need to rewrite the printf function every time you change the number of arguments in input. You will just have to include the "stdarg" library which will allow you to use a new type of variable, **`va_list`**_,_ and 3 very useful _macros_: **`va_start`, `va_arg`** & **`va_end`**

```c
#include <stdarg.h>
```

Let's take a closer look at how to use them



## va\_list, va\_start, va\_end & va\_arg

### `va_list` - new object type

`va_list` is an <mark style="color:red;">**object type**</mark> suitable for holding the information needed by the macros `va_start`, `va_copy,` `va_arg`, and `va_end` (that you will understand in a few minutes). In other words, it is a list that will contain all the dynamic arguments.

To create a variable of this type, you will have to do it the same way as any other variable.

```c
va_list    any_name_you_want;

// we will call it args for the next example:
va_list    args;
```

This will create the list of dynamic arguments which can be illustrated as follows

<figure><img src="../../.gitbook/assets/va_list.PNG" alt=""><figcaption></figcaption></figure>

In this example, the printf function takes 2 extra arguments, in addition to the mandatory argument. These two arguments are the variable arguments and will be stored in the previously created variable of type v&#x61;_&#x6C;ist,_ thanks to `va_start`.



### **`va_start` - function macro**

The macro `va_start` function will somehow initialize everything, before we start moving through our variable argument list (va\_list). You have to write it like that:

```c
va_start( va_list var, parameterN );

// in our example, it would be:
va_start( args, format);
```

* `var` is a variable of type arg\_list (args for us)
* `parameterN` is the named parameter preceding the first dynamic parameter (in our case, with printf, it would be the initial string) - in other words, **it's the mandatory argument**

Its purpose is to set the stage and define which elements will be stable and which will vary. This is when your va\_list variable will have all the elements in the table.

{% hint style="warning" %}
`va_start` must be called before any use of `va_arg - otherwise your va_list variable/table will be empty.`
{% endhint %}



### **`va_arg` - function macro**

Now that everything is ready, you can start using and playing with your variable arguments. This can be done with va\_arg.

This macro allows access to the arguments of the variadic function. Each time `va_arg` is called, you move to the next argument.&#x20;

`va_arg` will take as argument first the list of dynamic arguments we had defined at the very beginning (va\_list object) and **the type** of the variable of the next argument.

```c
va_arg( va_list var, type_of_the_variable )
```



Let's go back to our example

<figure><img src="../../.gitbook/assets/va_list (1).PNG" alt=""><figcaption></figcaption></figure>

The length of our variable argument list (args) is 2. There is a string argument in first position and an int argument in second position.

If you want to access the first argument, you will have to call `va_arg` once and specify the type of the argument. In this case, the first argument is a string, that will be defined by a pointer.

If you want to access the second argument, you do the same thing. But this time the type of the argument is an "int".

{% code lineNumbers="true" %}
```c
// access the first argument (type "string")
va_arg( args,  char * ) // -> "Laura"

// access the second argument (type "int")
va_arg( args, int ) // -> 23
```
{% endcode %}

Obviously, this is just a theoretical example so that you can understand how va\_arg works. In practice, since we don't know in advance how many arguments the function will take, you can imagine that you will have to create conditions for each specified format.



### **`va_end` - function macro**

Once you have finished your program, don't forget to clean up the object you initialized by calling va\_start.

`va_end` can modify the object, which was called "args" in our previous exampl&#x65;**,** so that it is no longer usable.&#x20;

```c
va_end( va_list var );

// and in our example:
va_end (args);
```

`va_end()` will free the allocated memory.





Now that you have the basics and have understood the most complicated part (aka the variadic functions (scary huh ?)) you can try to create your own printf : the legendary ft\_printf. Let's do it together step by step.
