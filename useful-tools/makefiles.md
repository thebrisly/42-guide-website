---
description: >-
  Since makefiles are some kind of mystic shit, I'll try my best to explain some
  basics.
---

# 📄 Makefiles

### Introduction

{% hint style="warning" %}
I will mainly use the term _executable_ in the following examples, note that Makefiles can also be used to create a library.\
The steps to create a Makefile for a library are described later in this page.
{% endhint %}

{% hint style="warning" %}
Note that if you copy paste a Makefile example from this gitbook, you'll have to change every 4 spaces tabs, to single tabs as gitbook automatically converts a tab to a 4 spaces tab.
{% endhint %}

{% hint style="info" %}
You'll need a Makefile for alot of 42 projects, I think it's better if you understand what it does and how to modify it rather than just copying it from a Github.
{% endhint %}

### What is a Makefile / make ?

Makefiles are basically sophisticated shell scripts that automate the repetitive tasks of compiling/recompiling many files.&#x20;

Make Is a Unix utility that is designed to start execution of a makefile.\
A Makefile is a special file that you create name _Makefile_, it contains shell commands. While in the directory containing this Makefile, you will run the _make_ command and the commands written in the Makefile will be executed.

Make keeps track of the last time files (normally object files) were updated and only updates those files which are required to keep the sourcefile up-to-date.\
If you have a program with a lot of source and/or header files, when you change a file on which others depend, you must recompile all the dependent files. This is an extremely time-consuming task.

A Makefile contains a list of _rules_.\
These rules tell the system what commands you want to execute. Most of the time, these rules are commands to compile, or recompile, a series of files.&#x20;

The rules are in two parts. The first line is called a _dependency line_ and the following line(s) are called _actions_ or _commands_. The action line(s) must be indented with a tab.

Rule syntax:

```
RULE: DEPENDENCY LINE
    [tab]ACTION LINE(S)
```

The dependency line is also made of two parts. The first part, before the colon, is the _target_ file and the second part, after the colon, are the _prerequisites._ \
It is called a _dependency line_ because the first part depends on the second part.\
Multiple _prerequisites_ files must be separated by a space.

After the Makefile has been created, a program can be (re)compiled by typing _make._ _Make_ then reads the Makefile, creates a dependency tree and take whatever action is necessary.\
It will not necessarily do all the rules in the Makefile as all dependencies may not need to be updated. It will rebuild _target_ files if they are missing or older than the dependency file(s).

Unless directed otherwise, make will stop when it encounters an error during the build process.

### Simple Makefile example

Let's start of with the following three files, _hello.c, hellofunc.c_ and _hello.h._

<details>

<summary>hello.c</summary>

{% code lineNumbers="true" %}
```c
#include "hello.h"

int    main(void)
{
    printHello(void);

    return (0);
}
```
{% endcode %}

</details>

<details>

<summary>hellofunc.c</summary>

<pre class="language-c" data-overflow="wrap" data-line-numbers><code class="lang-c"><strong>#include "hello.h"
</strong>
void    printHello(void)
{
    printf("Hello World!\n);
}
</code></pre>

</details>

<details>

<summary>hello.h</summary>

```c
#ifndef HELLO_H
# define HELLO_H
# include <stdio.h>

void    printHello(void);
#endif
```

</details>

Normally, you would compile these files by executing the following command :\
`gcc -Wextra -Wall -Werror hello.c hellofunc.c -I. -o hello`

{% hint style="info" %}
The `-I.` is included so that gcc wil look in the current directory (.) for the include file _hello.h_&#x20;
{% endhint %}

This command compiles the two .c files and creates an executable named _hello_.

The simplest Makefile you could create for these file would look something like :

{% code title="Makefile" lineNumbers="true" %}
```makefile
hello: hello.c hellofunc.c
    gcc -Wextra -Wall -Werror hello.c hellofunc.c -I. -o hello
```
{% endcode %}

Next, I will describe what rules are present in every Makefiles, these are conventions rules, and are required by the 42 Norm.

More complex Makefile will be described later.

### Rules conventions

As said above, there are some rules conventions, these are rules that are not mandatory but present in almost all Makefiles, this makes compiling and building, as well as cleaning easier. Plus, these rules are required in the 42 Norm.

<table><thead><tr><th width="203">Rule name</th><th>Description</th></tr></thead><tbody><tr><td>all</td><td>Since the first rule encountered in the Makefile is executed when using the <code>make</code> command without any specific rule, the <em>all</em> rule has to be placed first in the Makefile, it usually calls the $(NAME) rule as a dependency (see example below).</td></tr><tr><td>$(NAME)</td><td>This is the main rule, it has for target the name of the executable we want to create and it will link all object files in an executable.</td></tr><tr><td>%.o: %.c</td><td>This rule is not required in the 42 Norm but makes reading the Makefile much easier.<br>This rule has for target any .o file, and for dependency the .c file with the same name.</td></tr><tr><td>clean</td><td>This rule is a simple cleaning rule that will delete all object files created during the build process, but leave the created executable untouched.</td></tr><tr><td>fclean</td><td>This rule is also a cleaning rule, it is dependent on the <em>clean</em> rule to delete all object files. Once all object files are deleted, this rule will delete the created executable.</td></tr><tr><td>re</td><td>This rule will rebuild everything, it is dependent on the <em>fclean</em> rule, which deletes every object file and the executable.<br>Once all the object files and the executable are deleted, the <em>re</em> rule calls the <em>all</em> rule to rebuild everything.</td></tr></tbody></table>

<details>

<summary>Simple Makefile respecting the convention (everything described)</summary>

{% code title="Makefile" lineNumbers="true" %}
```makefile
# This Makefile example contains some variables and automatic variables
# Below is the same Makefile without the variables and automatic variables
# NAME is a variable containing the name of the executable
# we want to create.
NAME = excutableName

# SRC is a variable containing all .c files required to build the project
# Note that every file name has to be separated by a space and that I 
# didn't use a wildcard (*.c) to get every file.
# While the usage of a wildcard would be simpler, it is not authorized by
# the 42 Norm as it is easier to input an unwanted file in the build 
# process by simply adding it in the src folder.
SRC = main.c test.c

# OBJ is a variable containing all .o files.
# As you can see I wrote OBJ := and not OBJ =
# The difference between := and = is that = is an assignement like we know
# in C. := tells make to append the result to the variable
# We have to append the result because what's on the right will be run for
# every .c file
# Whats on the right basically means : "for every .c file you find in the
# SRC variable, give me the corresponding .o file".
# This will then append the result for each .c file to the OBJ variable.
# It simply replaces the .c in each files in the SRC variable by .o
OBJ := $(SRC:%.c=%.o)

# ALL is the first rule in the Makefile, making it the default rule when
# calling the make command without specifying the rule.
# As said in the description table above, this rule has the $(NAME) rule
# as dependency and will therefore, call the $(NAME) rule
all: $(NAME)

# $(NAME) is, as said above, the main rule of the Makefile.
# This rule has the OBJ variable as dependency, which means, if one or
# more .o files are missing, make will try to build them (if a rule for
# that exists) before running the $(NAME) commands. 
# When all the dependency are there, the commands will be executed.
# This commande takes two automatic variables, $^ and $@
#
# $^: The name of all the prerequisites, with space between them
# $@: This corresponds to the name of the target, in this case this will
#    be executableName.
$(NAME): $(OBJ)
    gcc -Wextra -Wall -Werror $^ -o $@

# %.o rule will compile one .c file to its correspondig object (.o) file
# The %.o: %.c pattern specifies that in order to build something whose
# file name ends with .o, you need to have a file that has the same prefix
# but then ends with .c rather than .o.
# $<: The name of the first prerequisite.
# $@: This corresponds to the name of the target, in this case this will
#    be executableName.
%.o: %.c
    gcc -Wextra -Wall -Werror -c $< -o $@

# CLEAN rule has no prerequisites
# What it does is run the rm -f shell command followed by the content of
# the OBJ variable, that is, every .o filenames.
# This results in all the .o files being deleted.
clean:
    rm -f $(OBJ)

# FCLEAN rule has as prerequisite the CLEAN rule, which means that the 
# CLEAN rule will be run first. 
# When the CLEAN rule is done, the fclean commands will be run.
# This results in all the .io files being deleted, as well as the created
# library because it has the name $(NAME)
fclean: clean
    rm -f $(NAME)

# RE rule has as prerequisites the FCLEAN and ALL rules.
# As the prerequisite are read from left to right, the first rule to be
# executed will be the FCLEAN rule, then we'll have the ALL rule
# Since there are no commands for the RE rule, once the ALL rule is done,
# the RE rule will also be done.
re: fclean all
```
{% endcode %}

</details>

<details>

<summary>Simple Makefile respecting the convention (expanded variables)</summary>

{% code title="Makefile" lineNumbers="true" %}
```makefile
NAME = excutableName

SRC = main.c test.c
OBJ := $(SRC:%.c=%.o)

all: executableName

executableName: main.o test.o
    gcc -Wextra -Wall -Werror main.o -o executableName

main.o: main.c
    gcc -Wextra -Wall -Werror -c main.c -o main.o

test.o: test.c
    gcc -Wextra -Wall -Werror -c test.c -o test.o

clean:
    rm -f main.o test.o

fclean: clean
    rm -f executableName

re: fclean all
```
{% endcode %}

</details>

### Variables naming convention

There's a rule convention, for which rules are expected in every Makefile, and there's also a naming convention for variable. I'll describe here the variables that are expected in a Makefile, and explain why it's named this way for the ones that are not very clear.

<table><thead><tr><th width="172">Variable</th><th>Description</th></tr></thead><tbody><tr><td>NAME</td><td>The buid target name (executable / library / other)</td></tr><tr><td>CC</td><td>This variable contains the compiler<br>gcc for C<br>g++ for C++</td></tr><tr><td>CCFLAGS</td><td>This variable contains the compiler flags.<br>i.e. for 42 we have to use -Wall -Werror -Wextra</td></tr><tr><td>CPPFLAGS</td><td>This variable contains the compiler preprocessor flags.<br>i.e. : <br>-I to specify the include directory (see complete examples below)<br>-D MACRO=value to define a macro at compiling time (used in Get Next Line)</td></tr></tbody></table>

{% hint style="info" %}
Note that CPPFLAGS doesn't mean it's the C++ compiler flags, here the "PP" part stands for PreProcessor
{% endhint %}

### Automatic variables

There's a lot of so-called _automatic variables_ that you can use in your Makefiles, I'll describe and explain (with examples) only the most used ones (=> the ones that will be the most useful for you in the 42 Cursus).

<table><thead><tr><th width="193">Automatic vairable</th><th>Descrption</th></tr></thead><tbody><tr><td>$@</td><td>The file name of the target of the rule.</td></tr><tr><td>$&#x3C;</td><td>The name of the first prerequisite.</td></tr><tr><td>$?</td><td>The names of all the prerequisites that are newer than the target, with spaces between them.<br>If the target does not exist, all prerequisites will be included.</td></tr><tr><td>$^</td><td>The names of all the prerequisites, with spaces between them.</td></tr></tbody></table>

{% hint style="info" %}
You can find more specific descriptions for Automatic Variables here :\
[https://www.gnu.org/software/make/manual/html\_node/Automatic-Variables.html](https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html)
{% endhint %}

<details>

<summary>List of all other automatic variables</summary>

* $%
* $+
* $|
* $\*
* $(@D)
* $(@F)
* $(\*D)
* $(\*F)
* $(%D)
* $(%F)
* $(\<D)
* $(\<F)
* $(^D)
* $(^F)
* $(+D)
* $(+F)
* $(?D)
* $(?F)

</details>



### Complete Makefile example (EXECUTABLE)

Here under I will write a complete Makefile to compile an executable as well as describing each steps (as I for the simple Makefile).

This Makefile contains some _Filename functions_, that is another thing you can do in Makefiles to make them easier to maintain.

<details>

<summary>Complete executable Makefile example</summary>

{% code title="Makefile" lineNumbers="true" %}
```makefile
# This Makefile is a complete example to compile an executable.

# SRC is a variable containing all the mandatory source filenames.
# As you can see, I simply put the file names without the .c extension
# The .c extension is added to each filename with the addsuffix filename
# function.
# This filename function has the following prototype
# $(addsuffix suffix, names...)
# The suffix will be added to every filename you add as second argument.
SRC = $(addsuffix .c, main ft_isalpha ft_isdigit ft_isalnum ft_isascii ft_isprint)

# OBJS is a variable containing all .o filenames.
# As you can see, I wrote OBJS := and not OBJS =
# The difference between := and = is that = is an assignement operator like
# we know in C. := tells make to append the result to the variable.
# We have to append the result because what's on the right will be run for
# every .c file one by one.
# Whats on the right basically means : "for every .c file you find in the
# SRC variable, give me the corresponding .o filename".
# This will then append the result for each .c file to the OBJ variable.
# It simply replaces the .c from each file in the SRC variable by .o
OBJS := $(SRC:%.c=%.o)

# BONUS_SRC is a variable containing all the bonus source filenames.
# As you can see, I simply put the filenames without the .c extension.
# The .c extension is added to each file with the addsuffix filename 
# function. I also use this filename function to add _bonus suffix that is
# required by most 42 subjects.
# This filename function has the following prototype
# $(addsuffix suffix, names...)
# The suffix will be added to every filename you add as second argument.
# Then I add an $(addprefix, names...) filename function around it to
# add a prefix for the bonus directory.
# The $(addprefix, names...) works like the addsuffix function but
# instead of adding the text at the end of each filename, it adds it to
# the start of each filename.
BONUS_SRC = $(addprefix bonus/, $(addsuffix _bonus.c, ft_lstnew ft_lstadd_back ft_lstadd_front))

# BONUS_OBJS is a variable containing all bonus .o filenames.
# This works the same way as the OBJS variable.
BONUS_OBJS := $(BONUS_SRC:%.c=%.o)

# SUPP_SRC is a variable containing all the additionnal source files.
# It works the same way as the BONUS_SRC variable, adding the .c suffix
# to every filename, then adding the supp/ prefix to every filename with
# the $(addsuffix suffix, names...) and $(addprefix prefix, names...)
# filename functions.
SUPP_SRC = $(addprefix supp/, $(addsuffix .c, ft_putchar ft_putstr ft_putnbr))

# SUPP_OBJS is a variable containing all additionnal .o filenames.
# It works the same way as the OBJS and BONUS_OBJS variables.
SUPP_OBJS := $(SUPP_SRC:%.c=%.o)

# As I did for the source and object files, I declared some variables for
# things I don't want to write each time.

# NAME is a variable containing the naem of the executable we want to 
# create
NAME = executable

# CC is a variable containing the compiler
# usually gcc for C and g++ for C++
CC = gcc

# CCFLAGS is a variable containing the compiler flags
# -Wall : this flag enables all the warnings about constructions
# -Wextra : this flag enables some extra warning flags that are not 
# 	enabled by -Wall
# -Werror : this flag turns all warning into errors to stop the compiler
#	when it encounters a warning.
# You can find what flags are actually enabled when using these flags
# by following this link, it also describes in more details what each
# flag does
# https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#Warning-Options
CCFLAGS = -Wall -Werror -Wextra

# INC_DIR is a variable containing the path of the include directory
# Include directory is used to put all the .h files included in your
# .c files.
# By including the include directory as a preprocessor flag when
# compiling your files, you don't have to specify the path each time
# you include a header file.
# You can simply write #include "main.h" instead of "../include/main.h"
INC_DIR = .

# CPPFLAGS is a variable containing the preprocessor flags
# In this example, it only contains the -I flag which speicifies the
# include directory path taken from the INC_DIR variable.
CPPFLAGS = -I$(INC_DIR)

# OBJS_BASBO is a variable containing all the object filenames for the
# mandatory source files as well as the bonus source files.
OBJS_BASBO = $(OBJS) $(BONUS_OBJS)

# OBJS_ALL is a variable containing all the object filenames for the
# mandatory, bonus and additionnal source files.
OBJS_ALL = $(OBJS_BASBO) $(SUPP_OBJS)

# RM is a alias variable for the rm -f shell command.
# I say alias variable because I can use this instead of writing
# rm -f each time I have to delete something.
# If I don't put the -f option, using the rm function will generate an
# error if a file does not exist, -f force the execution, wheter or not
# the file to delete exists.
RM = rm -f

# ALL is the first rule in the Makefile, making it the default rule when
# calling the make command without specifying the rule.
# The rule has the $(NAME) rule as dependency and will therefore,
# call the $(NAME) rule.
all: $(NAME)

# $(NAME) is the main rule of the Makefile.
# This rule has the OBJS variable as a dependency, which means, if one
# or more .o files are missing, make will try to build them (if a rule
# for that exists) before running the $(NAME) commands.
# When all the dependency are there, the commands will be executed.
# The command executed is the gcc linking, it links all the .o files
# into an executable file called $(NAME)
$(NAME): $(OBJS)
	$(CC) $(CCFLAGS) $^ -o $@

# %.o rule will compile one .c file to its corresponding object (.o) file
# The %.o: %.c pattern specifies that in order to build something whose
# filename ends with .o, you need to have a file that has the same
# prefix but ends with .c rather than .o.
# $<: The name of the first prerequisite.
# $@: This corresponds to the name of the target : what is on the left
# 	side of the colon.
%.o: %.c
	$(CC) $(CPPFLAGS) $(CCFLAGS) -c $< -o $@


# CLEAN rule has no prerequisites
# What it does is use the $(RM) alias variable follow by the content of
# the OBJS_ALL variable, that is, every .o filenames.
# This results in all the .o files being deleted.
clean:
	$(RM) $(OBJS_ALL)

# FCLEAN rule has as prerequisite the CLEAN rule, which means that the
# CLEAN rule will be run first.
# When the CLEAN rule is done, the fclean commands will be executed.
# This results in all the .o files being deleted, as well as the created
# executable because it has the name $(NAME)
fclean: clean
	$(RM) $(NAME)

# RE rule has as prerequisites the FCLEAN and ALL rules.
# As the prerequisites are read from left to right, the first rule to be
# executed will be the FCLEAN rule, then we'll have the ALL rule.
# Since there are no commands for the RE rule, once the ALL rule is done,
# the RE rule will also be done.
re: fclean all

# BONUS rule works the same way as the $(NAME) rule but instead of 
# having the OBJS variable as dependency, it has the OBJS_BASBO variable
# Since the OBJS_BASBO variable contains the OBJS and the BONUS_OBJS
# variables, all the .o files contained in these two variables are
# dependencies for this bonus rule.
bonus: $(OBJS_BASBO)
	$(CC) $(CCFLAGS) $? -o $(NAME)

# EVERYTHING rule works the same way as the $(NAME) rule but instead of 
# having the OBJS variable as dependency, it has the OBJS_ALL variable.
# Since the OBJS_ALL variable contains the OBJS, BONUS_OBJS and
# SUPP_OBJS variables, all the .o files contained in these two variables
# are dependencies for this everything rule.
everything: $(OBJS_ALL)
	$(CC) $(CCFLAGS) $? -o $(NAME)

# .PHONY target specifies which targets are not file dependent
# Take a look at the ".PHONY targets" section below on this page
# for more details
.PHONY: all clean fclean re bonus everything
```
{% endcode %}

</details>

### Complete Makefile example (LIBRARY)

Here under I will write a complete Makefile to compile a library as well as describing each steps (as I did for the simple Makefile).

This Makefile contains some _Filename functions,_ that is another thing you can do in Makefiles to make them easier to maintain.

<details>

<summary>Complete library Makefile example</summary>

<pre class="language-makefile" data-title="Makefile" data-line-numbers><code class="lang-makefile"># This Makefile is a complete example to compile a C library.

# SRC is a variable containing all the mandatory source files
# As you can see, I simply put the file names without the .c extension
# the .c extension is added to each file with the addsuffix filename function
# this filename function has the following prototype
# $(addsuffix suffix, names…)
# The suffix will be added to every file name you add as second argument.
<strong>SRC = $(addsuffix .c, ft_isalpha ft_isdigit ft_isalnum ft_isascii ft_isprint)
</strong>
# OBJS is a variable containing all .o filenames.
# As you can see I wrote OBJS := and not OBJS =
# The difference between := and = is that = is an assignement operator 
# like we know in C. := tells make to append the result to the variable
# We have to append the result because what's on the right will be run for
# every .c file one by one.
# Whats on the right basically means : "for every .c file you find in the
# SRC variable, give me the corresponding .o filename".
# This will then append the result for each .c file to the OBJ variable.
# It simply replaces the .c from each file in the SRC variable by .o
OBJS := $(SRC:%.c=%.o)

# BONUS_SRC is a variable containing all the bonus source files
# As you can see, I simply put the file names without the .c extension
# the .c extension is added to each file with the addsuffix filename function
# this filename function has the following prototype
# $(addsuffix suffix, names...)
# The suffix will be added to every file name you add as second argument.
# Then I added an $(addprefix, names...) filename function around it to
# add a prefix for the bonus directory. 
# The $(addprefix, names...). works like the addsuffix function but
# instead of adding the text at the end of each filename, it adds it to
# the start of each filename.
BONUS_SRC = $(addprefix bonus/, $(addsuffix _bonus.c, ft_lstnew ft_lstadd_back ft_lstadd_front ))

# BONUS_OBJS is a variable containing all bonus .o filenames.
# This works the same way as the OBJS variable.
BONUS_OBJS := $(BONUS_SRC:%.c=%.o)

# SUPP_SRC is a variable containing all the additional source files
# It works the same way as the BONUS_SRC variable, adding the .c suffix
# to every filename, then adding the supp/ prefix to every filename
SUPP_SRC = $(addprefix supp/, $(addsuffix .c, ft_putchar ft_putstr ft_putnbr))

# SUPP_OBJS is a variable containing all additional .o filenames.
# It works the same way as the OBJS and BONUS_OBJS variables.
SUPP_OBJS := $(SUPP_SRC:%.c=%.o)

# As I did for the source and object files, I declared some variables for
# things I don't want to write each time.

# NAME is a variable containing the name of the archive we want to create
NAME = libft.a

# CC is a variable containing the compiler
# usually gcc for C and g++ for C++
CC = gcc

# CCFLAGS is a variable containing the compiler flags
# -Wall : this flag enables all the warnings about constructions
# -Wextra : this flag enables some extra warning flags that are not
#          enabled by -Wall
# -Werror : this flag turns all warning into errors to stop the compiler
#         when it encounters a warning.
# You can find what flags are actually enabled when using these flags
# by following this link, it also describes in more details what each
# flag does
# https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#Warning-Options
CCFLAGS = -Wall -Wextra -Werror

# INC_DIR is a variable containing the path of the include directory
# Include directory is used to put all the .h file needed by your 
# library.
# By including the include directory as a preprocessor flag when compiling
# your files, you don't have to specify the path each time you include a 
# header file. 
# You can simply write #include "main.h" instead of "../include/main.h".
INC_DIR = .

# CPPFLAGS is a variable containing the preprocessor flags
# In this example, it only contains the -I flag which specifies the 
# include directory path taken from the INC_DIR variable.
CPPFLAGS = -I$(INC_DIR)

# RM is an alias variable for the rm -f shell command.
# I say alias variable because I can use this instead of writing
# rm -f each time I have to delete something.
# If I don't put the -f option, using the rm function will generate an
# error if a file does not exist, -f force the execution, wheter or not the
# file to delete exists.
RM = rm -f

# ARNAME is an alias variable for the ar rcs $(NAME) shell command.
ARNAME = ar rcs $(NAME)

# RANNAME is an alias variable for the ranlib $(NAME) shell command.
RANNAME = ranlib $(NAME)

# OBJS_BASBO is a variable containing all the object filenames for the
# mandatory source files as well as the bonus source files.
OBJS_BASBO = $(OBJS) $(BONUS_OBJS)

# OBJS_ALL is a variable containing all the object filenames for the 
# mandatory, bonus and additionnal source files.
OBJS_ALL = $(OBJS_BASBO) $(SUPP_OBJS)

# ALL is the first rule in the Makefile, making it the default rule when
# calling the make command without specifying the rule.
# This rule has the $(NAME) rule as dependency and will therefore,
# call the $(NAME) rule.
all: $(NAME)

# $(NAME) is the main rule of the Makefile.
# This rule has the OBJS variable as a dependency, which means, if one or
# more .o files are missing, make will try to build them (if a rule for
# that exists) before running the $(NAME) commands.
# When all the dependency are there, the commands will be executed.
# The commands are what is described above in the variable declaration
# section :
# ARNAME : ar rcs $(NAME)
# RANNAME : ranlib $(NAME)
$(NAME): $(OBJS)
    $(ARNAME) $(OBJS)
    $(RANNAME)

# %.o rule will compile one .c file to its correspondig object (.o) file
# The %.o: %.c pattern specifies that in order to build something whose
# file name ends with .o, you need to have a file that has the same prefix
# but then ends with .c rather than .o.
# $&#x3C;: The name of the first prerequisite.
# $@: This corresponds to the name of the target : what is on the left
#     side of the colon.
%.o: %.c
    $(CC) $(CPPFLAGS) $(CCFLAGS) -o $@ -c $&#x3C;

# CLEAN rule has no prerequisites
# What it does is use the $(RM) alias variable followed by the content of
# the OBJS_ALL variable, that is, every .o filenames.
# This results in all the .o files being deleted.
clean:
    $(RM) $(OBJS_ALL)

# FCLEAN rule has as prerequisite the CLEAN rule, which means that the 
# CLEAN rule will be run first. 
# When the CLEAN rule is done, the fclean commands will be run.
# This results in all the .io files being deleted, as well as the created
# library because it has the name $(NAME)
fclean: clean
    $(RM) $(NAME)

# RE rule has as prerequisites the FCLEAN and ALL rules.
# As the prerequisite are read from left to right, the first rule to be
# executed will be the FCLEAN rule, then we'll have the ALL rule.
# Since there are no commands for the RE rule, once the ALL rule is done,
# the RE rule will also be done.
re: fclean all

# The bonus rule works the same way as the $(NAME) rule but instead of
# having the OBJS variable as dependency, it has the OBJS_BASBO variable.
# Since the OBJS_BASBO variable contains the OBJS and the BONUS_OBJS
# variables, all the .o files contained in these two variables are
# dependencies for this bonus rule.
# The commands are what is described above in the variable declaration
# section :
# ARNAME : ar rcs $(NAME)
# RANNAME : ranlib $(NAME)
bonus: $(OBJS_BASBO)
    $(ARNAME) $(OBJS_BASBO)
    $(RANNAME)

# The bonus rule works the same way as the $(NAME) rule but instead of
# having the OBJS variable as dependency, it has the OBJS_ALL variable.
# Since the OBJS_ALL variable contains the OBJS, the BONUS_OBJS and the
# SUPP_OBJS variables, all the .io files contained in these two variables
# are dependencies for this everything rule.
# The commands are what is described above in the variable declaration
# section :
# ARNAME : ar rcs $(NAME)
# RANNAME : ranlib $(NAME)
everything: $(OBJS_ALL)
    $(ARNAME) $(OBJS_ALL)
    $(RANNAME)
</code></pre>



</details>

### .PHONY targets

A phony target is a target that is not really the name of a file. It's just a name for a recipe to be executed when you make an explicit reuquest (i.e `make clean`).

There are two reasons to use a phony target :

* To avoid a conflict with a file of the same name.
* To improve performance.

If you write a rule whose recipe will not create the target file, the recipe will be executed every time the target comes up for remaking. Here is example :&#x20;

{% code title="Makefile" lineNumbers="true" %}
```makefile
clean:
    rm -f *.o
```
{% endcode %}

Because the rm command does not create a file named clean, probably no such file will ever exist.

Therefore, the rm command will be executed every time you say `make clean`.

In this example, the clean target will not work as expected if a file named clean is ever created in this directory. Since it has no prerequisites, clean would always be considered up to date and its recipe would not be executed.

To avoid this problem, you can explicitly declare the target to be phony by making it a prerequisite of the special .PHONY target as follows :

```
.PHONY: clean
clean:
    rm -f *.o
```

Once this is done, `make clean` will run the recipe regardless of whether there is a file named clean.

#### Sources

Everything I wrote there is available in greater details somewhere on this link.

{% embed url="https://www.gnu.org/software/make/manual/html_node/" %}
GNU Make documentation
{% endembed %}
