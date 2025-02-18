# CPP05

### Main topics

```
Repetition and Exceptions (try, throw & catch
```

In this module, you'll learn how to create exceptions and then use them in your code.&#x20;

First, let's talk FOOD (because i'm hungry): **Imagine you're baking a cake.**

1. **Mixing Bowl:** This is where you combine ingredients, like mixing flour, eggs, and sugar. When you're blending things together, sometimes a small mistake can happen.
2. **Eggshell:** If you accidentally drop an eggshell into your mix, you wouldn't want it in your cake, right? So, you remove the eggshell to keep the cake perfect. Similarly, in code, when something unexpected occurs, you "throw away" the issue by sending an error message.
3. **Safety Net:** Now, picture having a safety net under your mixing bowl. If an eggshell falls in (an error occurs), the safety net catches it. Then you can decide what to do with the eggshell, like discarding it or acknowledging the mistake. In code, the safety net is like the "catch" block, helping you handle unexpected problems that occur during your program's execution.

The metaphor may be a bit lame, but we're going to do exactly the same thing (well... almost) in C++.&#x20;

Let's take a very easy example and see step by step what it does to better understand these new concepts :)

Here we have :

{% code overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

int main() {
    int dividend, divisor, result;

    std::cout << "Enter the dividend: ";
    std::cin >> dividend;

    std::cout << "Enter the divisor: ";
    std::cin >> divisor;

    try 
    {
        if (divisor == 0) 
        {
            throw "Division by zero is not allowed!";  // Throw an exception
        }

        result = dividend / divisor;
        std::cout << "Result: " << result << std::endl;
    }
    catch (const char* errorMessage) 
    {
        std::cerr << "Error: " << errorMessage << std::endl;
    }

    return 0;
}
```
{% endcode %}

The code consists of **three main parts**. The "try" (miying bowl), "throw" (eggshell) & "catch"(safety net) blocks:

1. `try` block (l. 12-19): This is where you put code that might generate an exception. In this case, it checks if the divisor is zero, which would result in division by zero.
2. `throw (l.16 && also 14-17)`: If a condition inside the `try` block is met (in this case, if `divisor` is zero), the program throws an exception. This means it raises an error message ("Division by zero is not allowed!").
3. `catch` block: This block "catches" the exception if it's thrown. It's like a safety net that handles the error. In this code, it catches exceptions of type `const char*`, which is a pointer to a string (the error message).

So, in simple terms, if you try to divide by zero (which is not allowed in math), the code throws an exception with the error message. The `catch` block then catches this exception and displays the error message.

If you enter valid numbers, the division is performed, and no exception is thrown. In this case, the code displays the result.

This mechanism helps you gracefully handle errors and prevent your program from crashing when unexpected issues occur.



And... that's about it. All CPP05 exercises are about playing with exceptions.



**You'll also have to create your own exceptions**: class exceptions. It won't be too complicated, so I'll let you find the answer you to search on Internet. (Spoiler: the exception you create must inherit from the class... Exception ;-) )

\
