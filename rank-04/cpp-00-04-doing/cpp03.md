# CPP03

### Main topics

```
Inheritance
```

### Inheritance

Let's go and take a look at what _inheritance_ means.

Inheritance is the capacity of a class to derive properties to another class.

New classes are created from an existing class, the new class is called a _Child Class_ or _Derived Class_ and the class from which it was created is called the _Base Class_ or _Parent Class_.

#### When is inheritance useful

Let's say you have to create a little program to manage an inventory of vehicles. You'll go ahead and create a class for _Cars_, one for _Trucks_, one for _Motorbikes_, etc.

<figure><img src="../../.gitbook/assets/cpp-03-classes-1.svg" alt=""><figcaption><p>Classes without inheritance example</p></figcaption></figure>

As you can see above, all the different types of vehicles have the same basic properties, but some might require additional properties.

Do you really want to type the same properties over and over again each time you have to add a new vehicle type ? No, and that's what inheritance is for (amongst other things).

<figure><img src="../../.gitbook/assets/cpp-03-classes-2.svg" alt=""><figcaption><p>Classes with inheritance example</p></figcaption></figure>

Isn't it better like this ? \
What we are doing here is declaring a base class _Vehicle_, with some properties like any other class. Then, when we create our _Car_ class, we say it extends the available properties of _Vehicle_. If we declare a new _Car_, we can access and set all the properties from the base class since _Car_ extends it. Let's look at the following code.

{% code overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

// Declaring our base Vehicle class
class Vehicle
{
	public:
		Vehicle(std::string type);
		std::string type;
	private:
};

// Declaring our Car class that publicly extends our Vehicle class
class Car : public Vehicle
{
	public:
		Car(void);
	private:
};

// Simple operator overload for output stream
// as you can see, we say that we need a Vehicle on the right
// side of the << operator
std::ostream &operator<<(std::ostream &o, const Vehicle &v)
{
	o << "This is a vehicle of type " << v.type;
	return (o);
}

// Constructors
Vehicle::Vehicle(std::string type): type(type) {}
Car::Car(void) : Vehicle("Car") {}

int	main(void)
{
	Car car = Car();
	std::cout << car << std::endl;
	return (0);
}
```
{% endcode %}

In that code, our _Car_ is a sub-class of _Vehicle_. We can access all the properties and functions of the _Vehicle_ class from any sub-class derived from it. If we want to create another vehicle type, we can simply create another class, i.e. _Truck,_ and do the same as for the _Car_ class.

#### **Car Constructor**

The `Car` class has its own constructor which does not take any parameters. Its main role is to initialize the `Car` class and set its type by calling the parent `Vehicle` class constructor with the hardcoded string "Car".

```cpp
Car::Car(void) : Vehicle("Car") {}
```

This means that every time a `Car` object is created, it automatically gets the type "Car" through the `Vehicle` constructor. The `void` keyword indicates that no parameters are required for the `Car` constructor. The `Car` constructor uses an initialization list to call the parent `Vehicle` constructor with the predetermined type.

### Access Specifier

Access specifiers play a crucial role in object-oriented programming as they control the visibility and accessibility of class members. There are three types of access specifiers: `public`, `protected`, and `private`.

* `public` inheritance makes the public and protected members of the base class public and protected in the derived class respectively. This means that the same level of access is preserved in the derived class.
* `protected` inheritance will make the public and protected members of the base class protected in the derived class. This restricts the access to these members outside the class hierarchy, while keeping them accessible within the class and its derived classes.
* `private` inheritance will make both the public and protected members of the base class private in the derived class. This means that these members can no longer be accessed from objects of the derived class, only from within the derived class itself (essentially turning all inherited members into private members of the derived class).

Here is an example illustrating different access specifiers in inheritance:

```cpp
class Base {
public:
    int publicVar;
protected:
    int protectedVar;
private:
    int privateVar;
};

class PublicDerived : public Base {
    // publicVar is public
    // protectedVar is protected
    // privateVar is not accessible
};

class ProtectedDerived : protected Base {
    // publicVar is protected
    // protectedVar is protected
    // privateVar is not accessible
};

class PrivateDerived : private Base {
    // publicVar is private
    // protectedVar is private
    // privateVar is not accessible
};
```

It's essential to choose the right access specifier to ensure the encapsulation and proper hierarchical structure of your classes. This can have a significant impact on how your classes interact with one another and with the rest of your program.

### Advanced topics

#### Multiple Inheritance

Multiple inheritance is a feature of some object-oriented programming languages in which a class can inherit characteristics and behaviors from more than one parent class. This allows for the creation of a new class that aggregates multiple behaviors from various classes. In C++, multiple inheritance can lead to complex hierarchies and the potential for the diamond problem, where a class inherits the same base class through multiple paths. Here's a simple syntax example in C++:

```cpp
class Base1 {
public:
    void function1() {}
};

class Base2 {
public:
    void function2() {}
};

class Derived : public Base1, public Base2 {
    // Inherits function1 from Base1 and function2 from Base2
};

int main() {
    Derived derivedObject;
    derivedObject.function1(); // From Base1
    derivedObject.function2(); // From Base2
}
```

When using multiple inheritance, it's essential to manage complexities and potential ambiguities that can arise, ensuring the correct functions or properties are accessed.

#### Diamond Inheritance Problem

You do remember that the last exercise in this module is called `DiamondTrap` right ? There might be a link that you can make here.

Diamond inheritance occurs in Object-Oriented Programming when a subclass, or derived class, inherits from two classes that, in turn, inherit from a single base class. This creates a shape similar to a diamond when visualized in a class diagram.&#x20;

**Example:**

```cpp
class Base {
public:
    void baseMethod() {}
};

class Derived1 : public Base {
    // Inherits baseMethod from Base
};

class Derived2 : public Base {
    // Inherits baseMethod from Base
};

class SubDerived : public Derived1, public Derived2 {
    // Attempts to inherit baseMethod from both Derived1 and Derived2
    // This may cause ambiguity because baseMethod exists in two places in the hierarchy.
};
```

When `SubDerived` tries to use `baseMethod`, the compiler may not be sure which version of `baseMethod` to use - the one from `Derived1` or the one from `Derived2`. This ambiguity is the essence of the diamond problem.

**Virtual Inheritance as a Solution:**

Virtual inheritance allows you to specify that only a single instance of the base class should be inherited by any derived classes, thus preventing multiple "copies" of the base class being included in the extended class hierarchies.

```cpp
class Base {
public:
    void baseMethod() {}
};

class Derived1 : virtual public Base {
    // Virtually inherits baseMethod from Base
};

class Derived2 : virtual public Base {
    // Virtually inherits baseMethod from Base
};

class SubDerived : public Derived1, public Derived2 {
    // Inherits a single instance of baseMethod
};
```

Using virtual inheritance, `SubDerived` will only have one `baseMethod` inherited from the `Base` class, resolving the ambiguity and avoiding the diamond problem.

You can find more information about derivation here on [IBM](https://www.ibm.com/docs/en/zos/2.4.0?topic=reference-inheritance-c-only), our here on [geekforgeeks](https://www.geeksforgeeks.org/inheritance-in-c/).
