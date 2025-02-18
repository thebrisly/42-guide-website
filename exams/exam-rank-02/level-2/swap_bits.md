# swap\_bits

### Subject

{% code overflow="wrap" %}
```
Assignment name  : swap_bits
Expected files   : swap_bits.c
Allowed functions:
--------------------------------------------------------------------------------

Write a function that takes a byte, swaps its halves (like the example) and
returns the result.

Your function must be declared as follows:

unsigned char	swap_bits(unsigned char octet);

Example:

  1 byte
_____________
 0100 | 0001
     \ /
     / \
 0001 | 0100
```
{% endcode %}

### Commented solution

<details>

<summary>swap_bits.c</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
// Function to swap the four most significant bits (left four bits) with the four least significant bits (right four bits) of an 8-bit octet
unsigned char swap_bits(unsigned char octet)
{
    // Shift the four most significant bits to the right to the position of the four least significant bits, and OR them with the four least significant bits shifted to the left to the position of the four most significant bits
    return ((octet >> 4 | octet << 4));
}

```
{% endcode %}

</details>
