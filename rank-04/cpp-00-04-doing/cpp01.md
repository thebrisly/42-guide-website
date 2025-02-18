# CPP01

### Main topics

Let's go over the main topics that are present on the first page of the subject :

```
Memory allocation, pointers to members, references, switch statement
```

### Memory allocation

Remember that C++ basically is an extension of C, yeah so memory allocation also exists in C++. It's mainly not done in the same way as in C.

In C we have `malloc` and `free`, in C++ we have `new` and `delete`. Let's take an example comparing C and C++ since you already know C memory management pretty well.

{% code title="C Code" overflow="wrap" lineNumbers="true" %}
```c
#include <stdlib.h>
#include <stdio.h>

int main(void)
{
    int *ptr; // declare the pointer
    
    ptr = malloc(sizeof(int)); // allocate the memory
    *ptr = 45; // assign a value
    printf("ptr value: %d\n", *ptr); // print the value
    free(ptr); // deallocate the memory
    return (0);
}
```
{% endcode %}

{% code title="C++ Code" overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

int main(void)
{
    int *ptr; // declare the pointer
    
    ptr = new int; // allocate memory
    *ptr = 45 // assign a value
    std::cout << "ptr value: " << *ptr << std::endl; // print the value
    delete ptr; // deallocate memory
    return (0);
}
```
{% endcode %}

In this case, both codes are exactly the same, now let's look at how you would do that for a dynamically allocated array.

{% code title="C Code" overflow="wrap" lineNumbers="true" %}
```c
#include <stdlib.h>

int main(void)
{
    int *ptr;
    
    ptr = malloc (10 * sizeof(int));
    free(ptr);
    return (0);
}
```
{% endcode %}

{% code title="C++ Code" overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

int main(void)
{
    int *ptr;
    
    ptr = new int[10];
    delete [] ptr;
    return (0);
}
```
{% endcode %}

### Pointers to members

First of all, what are pointers to members ?

Remember that in C, we have pointers to variable and pointers to functions. These also exists in C++ but there's also 2 new pointer types in C++ to introduce the class concept into pointers.

I'll put down here the code example from the intra video on pointers to members.

{% code overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>
#include <Sample.hpp>

int main()
{
    Sample instance; // instance of Sample class on the stack
    Sample *instancep = &instance; // pointer to the instance of Sample

    int Sample::*p = NULL; // pointer to member attribute of Sample class
    // adding the Sample:: specifies that it will point to a member attribute of the Sample class
    void (Sample::*f)(void) const; // pointer to member function of Sample class
    
    p = &Sample::foo; // Setting Sample::*p to be the address of the foo member attribute
    
    std::cout << "Value of member foo: " << instance.foo << std::endl;
    instance.*p = 21; // this line sets the value of the member attribute pointed to by *p in the instance `instance` to 21

    std::cout << "Value of member foo: " << instance.foo << std::endl;
    instancep->*p = 42; // this line sets the value of the member attribute pointed to by *p in the instance pointed to by the `instancep` pointer
    std::cout << "Value of member foo: " << instance.foo << std::endl;
    
    f = &Sample::bar;
    
    (instance.*f)(); // calling the member function Bar in the instance `instance` of the Sample class
    (instancep->*f)(); // same thing as above, but this time with a pointer to the instance
}
```
{% endcode %}

#### .\* operator

> Refers to line 16 in the above example

We set `Sample::*p` to point to a member `foo` in the `Sample` class. The thing is, we could have multiple instances of the `Sample` class, so we have to specify on which instance we want to use the pointer by using the following syntax: `instance.*pointerToMemberAttribute`.

This is because the `foo` member attribute can exist in multiple class instances.

#### - >\* operator

> Refers to line 19 in the above example

Here we are not using the `Sample` instance directly anymore, we have to use the `->*` operator instead of the `.*` operator. It works exactly the same way but it adds a level of dereference in between.

This syntax: `instancePtr->*pointerToMemberAttribute` where `instancePtr` points to an `instance` of the `Sample` class, does the same thing as the `.*` operator used on instance variable directly.

#### Call member function from pointer to member function

> Refers to line 24 and 25 in the above example

For pointers to member functions, it works in the same way as pointer to member attributes.

We first set to which member function we want the pointer to point, and when we want to call the function, we have to specify on which instance of the class we'll call the function.

In the same way as pointer to member attributes, we have the two operators, `.*` and `->*`.

The `.*` operator is used when we use the instance variable directly, and the `->*` is used when we have a pointer to an instance variable.

### References

References are a new concept, that does not exist in `C`, it's close as what the pointers do in `C`.

The more accurate definition of a reference is the following:

> A reference is a pointer that is constant and is always dereferenced, it can never be `void`\\

Let's take the first example from the intra video

{% code title="c++ Refs UnCommented" overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

int main(void)
{
    int numberOfBalls = 42;
    
    int *ballsPtr = &numberOfBalls;
    int &ballsRef = numberOfBalls;
    
    std::cout << numberOfBalls << " " << *ballsPtr << " " << ballsRef << std::endl;
    
    *ballsPtr = 21;
    std::cout << numberOfBalls << std::endl;
    ballsRef = 84;
    std::cout << numberOfBalls << std::endl;
    
    return (0);
}
```
{% endcode %}

With just the definition given above, can you guess the output of the above code ?

<details>

<summary>Code result</summary>

```sh
$> 42 42 42
$> 21
$> 84
```

</details>

Now, we'll take the same example, but this time, I'll comment it so that we can understand what is being done in this code.

{% code title="c++ Refs commented" overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

int main(void)
{
    int numberOfBalls = 42; // assigning 42 to the numberOfBalls variable
    
    int *ballsPtr = &numberOfBalls; // assigning the address of the numberOfBalls variable to the ballsPtr pointer
    int &ballsRef = numberOfBalls; // assigning ballsRef to be a reference to the numberOfBalls variable
    // note that for reference, we assign it directly another variable and not the adress of another variable
    // Now that the reference is set, we cannot change what it is referencing.
    // This means that I could not do this later on: ballsRef = otherIntValue;
    
    std::cout << numberOfBalls << " " << *ballsPtr << " " << ballsRef << std::endl;
    // The above line first prints the value of the numberOfBalls variable
    // it then prints the value pointed to by ballsPtr by dereferencing the pointer using the * operator
    // it then prints the value of ballsRef which is a reference to the numberOfBalls variable
    
    *ballsPtr = 21;
    // dereference the pointer to modify the value pointed to by ballsPtr
    std::cout << numberOfBalls << std::endl;
    // should print 21
    ballsRef = 84;
    // modify the value referenced by ballsRef
    std::cout << numberOfBalls << std::endl;
    // should print 84

    return (0);
}
```
{% endcode %}

#### Things to note about references in C++

* A reference is somehow like a dereferenced pointer
* Once it's defined it will always be referencing the same value
* You cannot declare a reference without assigning it a value directly
* References are constant, you can't change what it references after the declaration
* A reference cannot be `void`, unlike a pointer that can be void

Some things of the above list in the form of code, as it can be better visualize by some:

{% code overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

int main(void)
{
    int intValue = 0;
    int secondValue = 10;
    
    int &valRef = intValue; // Will always reference intValue
    int &valRef2; // this will not work as references have to be directly assigned a variable to reference
    valRef = secondValue; // this will not work as valRef was already set to reference intValue
    int &valRef3 = NULL; // this will not work, first because references cannot be void, but also because we will not be able to set it to reference something else later since they are constant
}
```
{% endcode %}

### Switch statement

There's already something about the `switch` statement that you can read [here](../../useful-tools/switch-statement.md).
