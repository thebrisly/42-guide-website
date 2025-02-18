# CPP07

### Main topics

```
C++ templates
```

I think it was the simplest CPP module to understand... It really is an intuitive concept that will save you a lot of time in your future projects! Let's directly dive into this topic :smile:

### Templates

Templates in C++ allow you to write generic code that can work with different data types without duplicating code. Let's use a super simple example:

**Imagine you want to create a function that swaps two values.**

Without templates, you might create a separate function for each data type you want to swap, like this:

{% code overflow="wrap" lineNumbers="true" %}
```c
void swapIntegers(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

void swapDoubles(double& a, double& b) {
    double temp = a;
    a = b;
    b = temp;
}
```
{% endcode %}

With templates, you can create a single function that works with various data types:

{% code overflow="wrap" lineNumbers="true" %}
```c
template <typename T>
void swapValues(T& a, T& b) {
    T temp = a;
    a = b;
    b = temp;
}
```
{% endcode %}

* `template <typename T>`: This line declares a template with a placeholder type `T`. It tells the compiler that we'll use `T` to represent different data types.
* `void swapValues(T& a, T& b)`: This is the generic function that can swap values of any data type represented by `T`. It takes two references as parameters (to modify the original values) and uses `T` for the temporary variable.

Now, you can use `swapValues` for integers, doubles, or any other data type without writing separate swap functions for each type:

{% code overflow="wrap" lineNumbers="true" %}
```c
int main() 
{
    int x = 5, y = 10;
    double a = 2.5, b = 7.3;

    swapValues(x, y);  // Swaps integers
    swapValues(a, b);  // Swaps doubles

    return 0;
}

```
{% endcode %}

And...that's it, basically. You'll also need to implement class templates :&#x20;

### Class templates

**Class templates** in C++ are a way to **create generic classes that can work with different data types or objects**. They are similar in concept to function templates, but instead of creating generic functions, you create generic classes.

Suppose you want to create a generic container class called `Box` that can hold different types of objects. You can use a class template to achieve this:

{% code overflow="wrap" lineNumbers="true" %}
```cpp
template <typename T>
class Box {
private:
    T content;

public:
    Box(const T& item) : content(item) {}

    T getItem() const {
        return content;
    }
};
```
{% endcode %}

* `template <typename T>`: This line declares a class template with a placeholder type `T`. It tells the compiler that `T` will represent different data types or object types.
* `class Box`: This is the declaration of the generic class named `Box` (a classical declaration - what you did in the other modules basically)
* `T content;`: This is a member variable of type `T`, which represents the content that the `Box` can hold.
* `Box(const T& item) : content(item) {}`: This is a constructor that takes an object of type `T` as a parameter and initializes the `content` member with that object.
* `T getItem() const { return content; }`: This is a member function that retrieves the content of the `Box`.

Now, you can use the `Box` class template to create instances for different types:

{% code overflow="wrap" lineNumbers="true" %}
```cpp
main() {
    Box<int> intBox(42);            // A Box that holds an integer
    Box<double> doubleBox(3.14);    // A Box that holds a double
    Box<std::string> stringBox("Hello, World!"); // A Box that holds a string

    int intValue = intBox.getItem();
    double doubleValue = doubleBox.getItem();
    std::string stringValue = stringBox.getItem();

    return 0;
}
```
{% endcode %}

Class templates are especially useful when you want to create reusable and type-safe container classes or data structures.



Anyway. Templates aren't a difficult concept to understand, and you'll soon get the hang of it ! But make sure you understand them, because we're going to need them for module 8, which deals with containers... see you there!
