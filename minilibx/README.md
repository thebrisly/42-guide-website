# 🖌️ MiniLibX

### Introduction

In this pages I will cover some information about MiniLibX, the library you'll be using for (at least) the three rank 2 graphical project (so\_long, FdF, Fract-ol).

I found most of the information I needed to use MiniLibX on this [page](https://harm-smits.github.io/42docs/libs/minilibx/getting_started.html).

I didn't find much other documentation online, and this one has some examples on how to do the basics things but I'd like to improve some of their explanation a bit and add some more examples that I really missed when trying to understand better how MiniLibX works.&#x20;

### Installation

{% hint style="warning" %}
I did a big part of the project using MiniLibX on the school computer, so if you're running Window or Linux, go check this [link](https://harm-smits.github.io/42docs/libs/minilibx/getting_started.html#installation) to install it correctly on your machine.
{% endhint %}

Here's the Makefile I used for my so\_long project (adapted a bit from the one I really used).

{% code title="Makefile" overflow="wrap" lineNumbers="true" %}
```
NAME = so_long
SRC = $(addprefix src/, main.c utils.c draw.c map_parser.c path_checker.c game_utils.c map_parser_utils.c free.c)
GNL_SRC = $(addprefix gnl/, gnl.c gnl_utils.c)
PRINTF_SRC = $(addprefix ft_printf/, ft_print_c.c ft_print_d.c ft_print_p.c ft_print_s.c ft_print_u.c ft_print_x.c ft_printf.c)

OBJ := $(SRC:%.c=%.o)
GNL_OBJ := $(GNL_SRC:%.c=%.o)
PRINTF_OBJ := $(PRINTF_SRC:%.c=%.o)

CC = gcc
CCFLAGS = -Wextra -Wall -Werror

all: $(NAME)

$(NAME): $(OBJ) $(GNL_OBJ) $(PRINTF_OBJ)
    $(CC) $(CCFLAGS) $^ -Lmlx -lmlx -framework OpenGL -framework AppKit -o $(NAME)

%.o: %.c
	gcc $(CCFLAGS) -Imlx -Iincludes -c $< -o $@

clean:
	rm -f $(OBJ) $(GNL_OBJ) $(PRINTF_OBJ)

fclean: clean
	make clean -C mlx/
	rm -f $(NAME)

re : fclean all
```
{% endcode %}
