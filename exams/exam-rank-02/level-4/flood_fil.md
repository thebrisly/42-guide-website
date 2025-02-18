# flood\_fil

if you have never had to deal with this kind of problem, I advise you to watch this video which explains the principle VERY WELL!&#x20;

Just after that, you'll be able to code flood fill in 5 minutes ;)

{% embed url="https://www.youtube.com/watch?v=VuiXOc81UDM" %}

And here is the subject:

### Subject

{% code overflow="wrap" %}
```
Assignment name  : flood_fill
Expected files   : *.c, *.h
Allowed functions: -
--------------------------------------------------------------------------------
Write a function that takes a char ** as a 2-dimensional array of char, a 
t_point as the dimensions of this array and a t_point as the starting point.
Starting from the given 'begin' t_point, this function fills an entire zone 
by replacing characters inside with the character 'F'. A zone is an group of 
the same character delimitated horizontally and vertically by other characters
or the array boundry.
The flood_fill function won't fill diagonally.
The flood_fill function will be prototyped like this:
  void  flood_fill(char **tab, t_point size, t_point begin);
The t_point structure is prototyped like this:
  typedef struct  s_point
  {
    int           x;
    int           y;
  }               t_point;
Example:
$> cat test_main.c
#include "test_functions.h"
#include "flood_fill.h"
int main(void)
{
	char **area;
	t_point size = {8, 5};
	t_point begin = {2, 2};
	char *zone[] = {
		"1 1 1 1 1 1 1 1",
		"1 0 0 0 1 0 0 1",
		"1 0 0 1 0 0 0 1",
		"1 0 1 1 0 0 0 1",
		"1 1 1 0 0 0 0 1",
	}
	area = make_area(zone);
	print_tab(area);
	flood_fill(area, size, begin);
	putc('\n');
	print_tab(area);
	return (0);
}
$> gcc flood_fill.c test_main.c test_functions.c -o flood_fill; ./flood_fill
1 1 1 1 1 1 1 1
1 0 0 0 1 0 0 1
1 0 0 1 0 0 0 1
1 0 1 0 0 0 0 1
1 1 0 0 0 0 0 0
1 1 1 1 1 1 1 1
1 F F F 1 0 0 1
1 F F 1 0 0 0 1
1 F 1 0 0 0 0 1
1 1 0 0 0 0 0 0
$> 
------------------------------------------------------------------------------*/
```
{% endcode %}

### Commented solution

{% code overflow="wrap" lineNumbers="true" %}
```c
#include "flood_fill.h"

// Recursive function to flood fill an area of a 2D character array
void fill(char **tab, t_point size, char target, int row, int col)
{
    // Check if current row and column values are out of bounds
    if (row < 0 || col < 0 || row >= size.y || col >= size.x)
        return;
    
    // Check if current cell has already been filled or does not match the target character
    if (tab[row][col] == 'F' || tab[row][col] != target)
        return;

    // Mark current cell as filled
    tab[row][col] = 'F';

    // Recursively fill neighboring cells
    fill(tab, size, target, row -1, col); // fill cell above
    fill(tab, size, target, row +1, col); // fill cell below
    fill(tab, size, target, row, col - 1); // fill cell to the left
    fill(tab, size, target, row, col + 1); // fill cell to the right
}

// Function to initiate flood fill from a specified point
void flood_fill(char **tab, t_point size, t_point begin)
{
    char target = tab[begin.y][begin.x]; // Get the character to fill around
    fill(tab, size, target, begin.y, begin.x); // Start the flood fill from the specified point
}

```
{% endcode %}

You can then use the example of the subject to see if you did everything right :-)
