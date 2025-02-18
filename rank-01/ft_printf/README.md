---
description: 'The goal of this project is simple: replicate the printf function.'
---

# ft\_printf

In a nutshell, the printf function is a command to display a <mark style="color:red;">formatted</mark> string on the screen.&#x20;

{% hint style="info" %}
The word "format" means that format specifiers, which begin with the % character, indicate the location and method of converting a data element (such as a number) into characters.&#x20;
{% endhint %}

Let's take an example.&#x20;

First, to use the printf function on C, you must include the <mark style="color:purple;">"stdio" library</mark> (standard input/output).

{% code lineNumbers="true" %}
```c
#include <stdio.h>

int main()
{
	printf("hello my name is Laura and i'm 23 years old\n");
	printf("hello my name is %s and i'm %d years old\n", "Laura", 22);
}
```
{% endcode %}

On line 5 I did a printf of a simple string. On the next line, on line 6, I used the format specifiers so you can understand it better.&#x20;

**Both functions will return the same thing but it's in the construction that they differ.**&#x20;

<figure><img src="../../.gitbook/assets/Capture.PNG" alt=""><figcaption></figcaption></figure>

At the beginning of the sentence, each character is copied/written literally into the function's output. Then, when the function **finds a format specifier** (which starts with a % character), it will retrieve the argument that is in the same position and write it in a very specific way.

For example when it finds the first %, it looks at what type it is. In our example, the first one is "s" so it will treat the first argument as a string, and use a specific method to copy this element into the function output. It will do the same thing when it finds the next %. Etc.&#x20;

### Format specifiers

The character after a '%' has different meanings. Let's just look at the ones we need to realize this project for school 42.

<table><thead><tr><th width="128">Character</th><th>Description</th></tr></thead><tbody><tr><td>%</td><td>Prints a % character.</td></tr><tr><td>d, i</td><td><em>Print an int</em> as a signed <a href="https://en.wikipedia.org/wiki/Integer">integer</a>. %d and %i are synonymous for output, but are different when used with <a href="https://en.wikipedia.org/wiki/Scanf()"><code>scanf</code></a> for input (where using %i will interpret a number as hexadecimal if it's preceded by 0x, and octal if it's preceded by 0.)</td></tr><tr><td>u</td><td>Print decimal unsigned int.</td></tr><tr><td>x, X</td><td>Print an unsigned int as a <a href="https://en.wikipedia.org/wiki/Hexadecimal">hexadecimal</a> number. x uses lower-case letters and X uses upper-case.</td></tr><tr><td>s</td><td>Print a null-terminated (\0) string.</td></tr><tr><td>c</td><td>Print a single character (char).</td></tr><tr><td>p</td><td>Print the address of a pointer or any other variable. The output is displayed in hexadecimal value. It's a format specifier which is used if we want to print data of type (void *).</td></tr></tbody></table>



### Return value (int)

The prototype of the printf function is constructed like this:

```c
int	ft_printf(const char *format, ...);
```

As you can see, the `printf` function <mark style="color:red;">returns a value of type int</mark>. But why ?



In short, it is mainly about **checking for errors**. You can make sure that the operation was successful or not using the return value. Checking the return value of `printf` allows you to detect failure _early_ so you don't waste time attempting to write millions of lines when the first line already failed.

* If a positive value is returned (indicating the number of characters written) it means the operation was successful.&#x20;
* If a negative number is returned there was some error.



If you want to check what value the function returns, you can do a printf of your printf.

<pre class="language-c"><code class="lang-c"><strong>int main()
</strong><strong>{
</strong><strong>    int result = printf("Sentence to know how many %s\n", "characters were written");
</strong><strong>    
</strong>    printf("%d characters were written", result);
}
</code></pre>
