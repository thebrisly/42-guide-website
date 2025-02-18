# CPP00

This CPP module is here to make you learn the basics of C++ and the main principles of this programming language.

I'll do my best to guide you through every topics that is mentioned in this module.

### Main topics

Let's go over the main topics that are present on the first page of the subject :

```
Namespaces, classes, member functions, stdio streams,
initialization lists, static, const, and some other basic
stuff
```

### Namespaces

A namespace is a way to scope a variable / method or anything else in your code.

Let's take a look at a simple example using a namespace in two different ways.

```cpp
#include <iostream>
using namespace std; 
// this line sets the namespace to std
// this means that we don't have to write std:: before 
// using any of the functions / variables in the iostream header

// this code is an example of using a namespace globally
int main(void)
{
    cout << "Hello World!" << endl;
    return (0);
}
```

```cpp
#include <iostream>
// notice that this time we don't add the 
// using namespace std;
// line

// this code does exactly the same thing as the one above
int main(void)
{
    std::cout << "Hello World!" << std::endl;
    return (0);
}
```

Those are two simple cases, to show you the difference between using a namespace globally and not using a namespace. In this case, that is not very interesting but take a look at the following code.

{% code overflow="wrap" lineNumbers="true" %}
```cpp
#include <iostream>

class FirstClass:
{
    public:
        FirstClass();
        ~FirstClass();
        void    print(std::string txt);
};

class SecondClass:
{
    public:
        SecondClass();
        ~SecondClass();
        void    print(void);
};

int main(void)
{
    // now if you want to call the print function, you'll have to specify a namespace
    // the namespace will correspond to the class of the print function 
    // you want to call
    // for example, to call the print(void) function, you'll have to write the following
    SecondClass::print(void);
    // and if you want to call the print(std::string txt) function
    FirstClass::print("My text");
    
    // if you try to do the following
    FirstClass::print(void);
    // it will not work, since the function FirstClass::print(void) does not
    // exist in the FirstClass namespace
    // the same goes for this
    SecondClass::print("Text");
    // for the same reason
    
    return (0);
}
```
{% endcode %}

{% hint style="warning" %}
Note that the above code will not compile, but it gives you an idea.
{% endhint %}

You can have multiple functions having the same name, then you can specify a namespace to call the correct function.

Go search some the internet for more information and try to build small C++ projects to understand how it works precisely.

Source: [https://learn.microsoft.com/en-us/cpp/cpp/namespaces-cpp?view=msvc-170](https://learn.microsoft.com/en-us/cpp/cpp/namespaces-cpp?view=msvc-170)

### Constructor functions & initialization lists

A constructor function is a special method inside a class that is automatically called whenever you create a new object of the class.

A simple constructor could be implemented like this:

{% code overflow="wrap" lineNumbers="true" %}
```cpp
class Class {     // The class
  public:           // Access specifier
    Class() {     // Constructor
      std::cout << "Hello World!";
    }
};

int main() {
  Class Obj;    // Create an object of Class, this will automatically call the constructor
  return 0;
}
```
{% endcode %}

{% hint style="warning" %}
A constructor always has the same name as the class itself and does not return anything.
{% endhint %}

Let's take another example.

{% code overflow="wrap" lineNumbers="true" %}
```cpp
class Car
{
    public:
        Car(); // Constructor declaration
        Car(std::string pbrand, std::string pmodel, int pyear); // second constructor
        std::string brand;
        std::string model;
        int year;
};

Car::Car(void)
{
    std::cout << "Hello world !" << std::endl;
    brand = "";
    model = "";
    year= 0;
    return ;
}

Car::Car(std::string pbrand, std::string pmodel, int pyear)
{
    brand = pbrand;
    model = pmodel;
    year = pyear;
    return ;
}

int main() {
  // Create Car objects and call the constructor with different values
  Car car1();
  Car car2("Ford", "Mustang", 1969);

  // Print values
  std::cout << car1.brand << " " << car1.model << " " << car1.year << std::endl;
  std::cout << car2.brand << " " << car2.model << " " << car2.year << std::endl;
  return 0;
}
```
{% endcode %}

In the main function, both car will be created as car objects, but one of them will directly have all the properties set to correct values, the other one will have default values.

Since the constructor functions are called when you create a new object of a specific class, you could specify some default values to be set directly in the constructor so you're sure they are correct when you try to use them.

These are constructors that I used in one of the modules:

{% code overflow="wrap" lineNumbers="true" %}
```cpp
// Default constructor, everything is set by the callee
ClapTrap::ClapTrap(void) : _name("Default"), _hp(10), _ep(10), _ad(0)
{
	std::cout << "Default ClapTrap constructor called for ";
	std::cout << _GREEN << this->_name;
	std::cout << _RESET << std::endl;
	return ;
}

// Named constructor, other values are set by the callee
ClapTrap::ClapTrap(std::string name) : _name(name), _hp(10), _ep(10), _ad(0)
{
	std::cout << "Named ClapTrap constructor called for ";
	std::cout << _GREEN << this->_name;
	std::cout << _RESET << std::endl;
	return ;
}

// Full constructor, everything is set by the caller
ClapTrap::ClapTrap(std::string name, uint hp, uint ep, uint ad) : _name(name), _hp(hp), _ep(ep), _ad(ad)
{
	std::cout << "Full ClapTrap Constructor called for ";
	std::cout << _GREEN << this->_name << _RESET;
	std::cout << " with " << _YELLOW << this->_hp << _RESET << " hp, ";
	std::cout << _YELLOW << this->_ep << _RESET << " ep, " << _YELLOW << this->_ad << _RESET << " ad.";
	std::cout << std::endl;
	return ;
}
```
{% endcode %}

Why is there a semi-colon and properties name after the constructor parameters ?&#x20;

Well, there another term that is related to constructor functions : `initialization lists`.

These are initialization lists, what it does is set the class attribute based on the value between the parentheses.

{% code overflow="wrap" %}
```cpp
ClapTrap::ClapTrap(std::string name, uint hp, uint ep, uint ad) : _name(name), _hp(hp), _ep(ep), _ad(ad)
```
{% endcode %}

This line is equivalent to the following code.

{% code overflow="wrap" lineNumbers="true" %}
```cpp
ClapTrap::ClapTrap(std::string name, uint hp, uint ep, uint ad)
{
    _name = name;
    _hp = hp;
    _ep = ep;
    _ad = ad;
}
```
{% endcode %}

It's an easier and better way to assign values inside the constructor function.

### Classes

If you didn't read the **w3schools** C++ introduction guide linked above, go ahead and read it, there's a lot of detailed information about classes since it's a central part of C++ and OOP.

Here I'll give you the file structure of this module. 42 Norm and C++ good practices will make you have something looking like this for every C++ project you'll build.

```
cpp00/
├─ ex00/
│  ├─ ...
├─ ex01/
│  ├─ Makefile
│  ├─ main.cpp
│  ├─ PhoneBook.cpp
│  ├─ PhoneBook.hpp
│  ├─ Contact.cpp
│  ├─ Contact.hpp
```

What you'll have at the end of projects using classes, is an `hpp` file containing the class definition, and a corresponding `cpp` file containing the class declaration.

### Member functions

Member functions are operators or functions declared as members of a class.\
In the code example for the [Namespaces](cpp00.md#namespaces), both `print` functions are member functions.

You could have more than that, take a look at the following class declaration (it might be a bit scary now, but it's actually pretty simple):

{% code overflow="wrap" lineNumbers="true" %}
```cpp
class	Bureaucrat
{
	public:
		Bureaucrat(void);
		Bureaucrat(std::string name);
		Bureaucrat(std::string name, int grade);
		Bureaucrat(const Bureaucrat &b);
		~Bureaucrat();
		Bureaucrat	&operator=(const Bureaucrat &b);

		void		setName(std::string name);
		void		setGrade(int grade);
		std::string	getName(void) const;
		int			getGrade(void) const;
		void		incrementGrade(void);
		void		decrementGrade(void);

		void		signForm(AForm &f);
		void		executeForm(AForm &f);
	private:
		std::string	_name;
		int			_grade;
};
```
{% endcode %}

In this example, you can see that there are 9 member functions, 4 constructor functions, 1 destructor function and 1 operator member.
