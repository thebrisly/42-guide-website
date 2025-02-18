# CPP02

### Main topics

```
Ad-hoc polymorphism, operator overloading and Orthodox Canonical class form
```

Before diving into ad-hoc polymorphism and operator overloading, let's take a look at the new rules given in the subject of this module.

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-25 at 20.40.15.png" alt=""><figcaption><p>CPP02 - New rules</p></figcaption></figure>

Orthodox Canonical Form, oh man that sounds complicated and... it's actually not that difficult.

It simply adds mandatory member functions to your classes, we'll see that in details in a few lines.

The second new rule, maybe you already did that, if not, look at the examples below and I think you'll get the idea pretty quickly.

Okay, so let's get to Orthodox Canonical Form...

### Orthodox Canonical Form

As the subject says, to respect the OCF (Orthodox Canonical Form), you have 4 mandatory members functions, let's take an example of what it should look like:

{% code title="example.hpp" overflow="wrap" lineNumbers="true" %}
```cpp
#ifndef EXAMPLE_HPP
# define EXAMPLE_HPP

class Example
{
    public:
        Example(void);
        Example(const Example& ex);
        Example &operator=(const Example& e);
        ~Example(void);
}

#endif
```
{% endcode %}

The class declaration itself is not that hard except maybe for this line:

`Example &operator=(const Example& e);`

When I first saw that I was like _Excuse me wtf,_ but it starts to make sense pretty quickly. It is "only" a way to tell your program how to act when you write the following code:&#x20;

{% code title="main.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
#include "Example.hpp"

int main(void)
{
    Example a;
    Example b;
    
    a.num = 10;
    a.name = "Simon";
    
    b = a; 
    // What values should be equal to which ?
    // this is what the operator overload let's us define
}
```
{% endcode %}

In the 4 mandatory member functions, you already know at least 2 of them, the default constructor and the destructor. Let's take a quick look at what the two other do.

First, the copy constructor. The copy constructor takes a reference to an object and constructs a new one based on the values of the referenced one.

{% code title="Example.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
#include "Example.hpp"

Example::Example(const Example& ex) : _val1(ex._val1) /* ... */
{
    return ;
}
```
{% endcode %}

I think you get the gist, the name _copy constructor_ is pretty clear.

Secondly, let's look at the assignment operator overload.&#x20;

> This is also connected to the _Operator overload_ main topic.

{% code title="Example.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
#include "Example.hpp"

Example &Example::operator=(const Example& ex)
{
    // in this case, we can't use the initialization list since
    // it's not a constructor function
    this->_val1 = ex._val1;
    return (*this);
}
```
{% endcode %}

### Ad-hoc polymorphism

I'm not insulting you, I promise. Let me explain.

_What the f\*\*\* is ad-hoc polymorphism ?_

Remember that, like in C, C++ is a typed language, so if you write a function taking an `int` as parameter, you'll not be able to pass it a `unsigned int`. But, there's something you can do in C++ that you can't in C, called `function overloading`, and that's how ad-hoc polymorphism is built.

First, try to compile the following C code.

{% code title="main.c" overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>

void print(int i);
void print(unsigned int j);

int main(void)
{
    int i = 10;
    unsigned int j = 100;
    
    print(i);
    print(j);
    
    return (0);
}

void print(int i)
{
    printf("Value is: %d\n", i);
}

void print(unsigned int j)
{
    printf("Value is: %u\n", j);
}
```
{% endcode %}

If everything's good, you should get an error like

`main.c:4:6: error: conflicting types for 'print'`

And that's totally normal, you have to functions with the same name but taking different argument types, and that's not possible in C.

Now, let's try the following C++ code.

{% code title="main.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

void print(int i);
void print(unsigned int j);

int main(void)
{
    int i = 10;
    unsigned int j = 100;
    
    print(i);
    print(j);
    print(i, j);
    
    return (0);
}

void print(int i)
{
    std::cout << "Value is: " << i << std::endl;
}

void print(unsigned int j)
{
    std::cout << "Value is: " << j << std::endl;
}

void print(int i, unsigned int j)
{
    std::cout << "Values are: " << i << " and " << j << std::endl;
}
```
{% endcode %}

And now... surprise, no errors at compile time, not in C++ and why is that ?

That's because function overloading is authorised in C++. Function overloading allows us to define two or more function with the same name in the same scope.

Ad-hoc polymorphisme works with function overloading, this will lead to code duplication. For each type you want your function to work with, you have to write it completely from 0 with another type.&#x20;

{% hint style="info" %}
There's also something called `Parametric polymorphism`, but that's another topic for a later time (-> CPP07)
{% endhint %}

### Operator overloading

And now, let's get to the last topic of this module, operator overloading.

As you saw in the last part, you can overload function in C++ by defining two or more function with the same name. Now, I'll show you how you can overload operators like `=`, `>=`, `<=`, `==`, and a lot of others.&#x20;

I'll only show example with some operator overloads, the other types works mostly the same with a little twist in the declaration but I'll let you search for the specific twists needed when you reach exercise 02 of this module.

{% code title="Example.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
#include "Example.hpp"

// Assignment operator
Example &Example::operator=(const Example& ex) {...} // you already saw that one

// Comparison operator (only one of the many available)
bool Example::operator>(const Example& ex)
{
    return (this->_val > ex._val);
}

// Arithmetic operator
Example Example::operator+(const Exammple& ex) const
{
    return (Example(this->_val + ex._val));
}

// Output stream operator
std::ostream &operator<<(std::ostream &o, const Example &ex)
{
    o << "Value is: " << ex._val << std::endl;
    return (o);
}
```
{% endcode %}

As said before, I won't show you all the operator overload available (see below), but only the main ones and this gives you an idea of most of the declarations. A little Google search will get you to what you want easily now that you have the correct terms to look for.

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-26 at 23.26.01.png" alt=""><figcaption><p>All the available operator that you can overload... - <a href="https://en.cppreference.com/w/cpp/language/operators">cppreference.com</a></p></figcaption></figure>

#### Helper Script

If you read through everything and got there, you deserve some kind of "treat", click [here](https://github.com/Laendrun/ocf_script) to find a bash script that will generate the files and template the required functions for Orthodox Canonical Form automatically for you.
