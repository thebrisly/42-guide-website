# print\_bits

### Subject

{% code overflow="wrap" %}
```
Assignment name  : print_bits
Expected files   : print_bits.c
Allowed functions: write
--------------------------------------------------------------------------------

Write a function that takes a byte, and prints it in binary WITHOUT A NEWLINE
AT THE END.

Your function must be declared as follows:

void	print_bits(unsigned char octet);

Example, if you pass 2 to print_bits, it will print "00000010"
```
{% endcode %}

### Commented solution

<details>

<summary>print_bits.c</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <unistd.h>

void print_bits(unsigned char octet)
{
    int i = 8; // Initialize a counter variable i to 8
    unsigned char bit = 0; // Initialize a variable bit to 0

    while (i--) // Loop through each bit of octet
    {
        bit = (octet >> i & 1) + 48; // Shift the bit of octet to the right i times and use the bitwise AND operator with 1 to get the bit value. Then add 48 to convert the bit value to its ASCII representation ('0' or '1')
        write (1, &bit, 1); // Write the ASCII representation of the bit to the standard output (stdout)
    }
}


/* if you want to test your code : */
int main()
{
	unsigned char octet = 3;
	print_bits(octet);
}

```
{% endcode %}

</details>
