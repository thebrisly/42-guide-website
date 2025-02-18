---
description: This page will showcase some helper functions for the MiniLibX library.
---

# MiniLibX Helper Function

### Simple put\_pixel function

This is a simple function to put a pixel to the screen by its `x` and `y` coordinates.

I based this function on what I found [here](https://harm-smits.github.io/42docs/libs/minilibx/getting_started.html#writing-pixels-to-a-image), and modified it a bit to make sure we only put a pixel that is inside the screen, without this check, the program could `segfault` if we try to set a value somewhere outside the window.

{% code overflow="wrap" lineNumbers="true" %}
```c
void ft_put_pixel(t_data *data, int x, int y, int color)
{
    char *pxl;
    
    if (x >= 0 && x < WINDOW_WIDTH && y >= 0 && y < WINDOW_HEIGHT
    {
        pxl = data->addr + (y * data->line_length + x * (data->bits_per_pixel / 8));
        *(unsigned int *)pxl = color;
    }
}
```
{% endcode %}

<details>

<summary>Final code to draw a pixel</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include "mlx.h"
#define	WINDOW_WIDTH 1920
#define WINDOW_HEIGHT 1080

typedef struct	s_data {
	void	*img;
	char	*addr;
	int		bits_per_pixel;
	int		line_length;
	int		endian;
}				t_data;

void ft_put_pixel(t_data *data, int x, int y, int color)
{
    char *pxl;

    if (x >= 0 && x < WINDOW_WIDTH && y >= 0 && y < WINDOW_HEIGHT)
    {
        pxl = data->addr + (y * data->line_length + x * (data->bits_per_pixel / 8));
        *(unsigned int *)pxl = color;
    }
}

int	main(void)
{
	void	*mlx;
	void	*mlx_win;
	t_data	img;

	mlx = mlx_init();
	mlx_win = mlx_new_window(mlx, 1920, 1080, "Hello world!");
	img.img = mlx_new_image(mlx, 1920, 1080);
	img.addr = mlx_get_data_addr(img.img, &img.bits_per_pixel, &img.line_length,
								&img.endian);
	ft_put_pixel(&img, WINDOW_WIDTH/2, WINDOW_HEIGHT/2, 0xFF0000);
	mlx_put_image_to_window(mlx, mlx_win, img.img, 0, 0);
	mlx_loop(mlx);
}

```
{% endcode %}

If you look closely, this will draw a red pixel at the very center of the window.

</details>

### Draw Line function (\~Naive line algorithm)

There is no function in MiniLibX to draw a line between two points, but this will be particularly useful when you try to code `FdF`, you'll have to join all your points by lines, so, here you go.

{% hint style="warning" %}
This function uses some function of the math library so make sure you can use it in your project and include it (`#include <math.h>`).\
For `FdF`, `Fractol` and `so-long`, all the math library are authorized.
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```c
void ft_draw_line(t_data *data, int x1, int y1, int x2, int y2, int color)
{
    int step;
    int x;
    int y;
    int i;
    int delta_x;
    int delta_y;
    
    delta_x = x2 - x1;
    delta_y = y2 - y1;
    if (abs(delta_x) >= abs(delta_y))
        step = abs(delta_x);
    else
        step = abs(delta_y);
    delta_x = delta_x / step;
    delta_y = delta_y / step;
    x = x1;
    y = x2;
    i = 0;
    while (i < step)
    {
        ft_put_pixel(data, x, y, color);
        x += delta_x;
        y += delta_y;
        i++;
    }
}
```
{% endcode %}

{% hint style="info" %}
You will have to find a way to make it pass the Norm, you can check how I did this [here](https://github.com/Laendrun/42/blob/main/fdf/src/draw.c#L27).
{% endhint %}
