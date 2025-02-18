# reverse\_bits

### Subject

```
Assignment name  : reverse_bits
Expected files   : reverse_bits.c
Allowed functions:
--------------------------------------------------------------------------------

Write a function that takes a byte, reverses it, bit by bit (like the
example) and returns the result.

Your function must be declared as follows:

unsigned char	reverse_bits(unsigned char octet);

Example:

  1 byte
_____________
 0010  0110
     ||
     \/
 0110  0100
```

### Commented solution

<details>

<summary>reverse_bits.c</summary>

{% code title="reverse_bits.c" overflow="wrap" lineNumbers="true" %}
```c
unsigned char	reverse_bits(unsigned char octet)
{
	unsigned int	i;
	unsigned char	res = 0;

	i = 8;
	while (i--)
	{
		// shift all the bits of res by 1 to the left
		// i.e. res: 0000 0101 => 0000 1010
		// perform a bitwise AND on LSB of octet AND 1
		// Least Significant Bit is the right most one
		// i.e octet: 0000 0101 => 1
		// it then performs a bitwise OR between the 
		// two LSB and stores the result in res
		// 0000 1010 | 0000 0001 => res: 0000 1011
		res = (res << 1) | (octet & 1);
		// shifting the original octet by 1 to the right
		// so that in next iteration we have the next bit
		octet = octet >> 1;
	}
	return (res);
}

// If you want to test the code:
int	main(void)
{
	unsigned char bit = 0;
	// by changing the number on the next line, you change
	// the bits that are sent to the reverse_bits function
	// 5 => 0000 0101, the result should be 1010 0000
	unsigned char res = reverse_bits((unsigned char)5);

	int i = 8;
	while (i--)
	{
		bit = (res >> i & 1) + 48;
		printf("%c", bit);
	}
}
```
{% endcode %}

</details>
