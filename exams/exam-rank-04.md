---
description: Minihell part 2 (oh nooo again ?!)
---

# Exam Rank 04

The Rank 4 exam of 42 is quite simple: **just recreate a micro shell**.&#x20;



## Subject&#x20;

`Allowed functions:`

> malloc, free, write, close, fork, waitpid, signal, kill, exit, chdir, execve, dup, dup2, pipe, strcmp, strncmp



Write a program that will behave like executing a shell command

* The command line to execute will be the arguments of this program
* Executable's path will be absolute or relative but your program must not build a path (from the PATH variable for example)
* You must implement "|" and ";" like in bash
  * we will never try a "|" immediately followed or preceded by nothing or "|" or ";"
* Your program must implement the built-in command cd only with a path as argument (no '-' or without parameters)
  * if cd has the wrong number of argument your program should print in STDERR "error: cd: bad arguments" followed by a '\n'
  * if cd failed your program should print in STDERR "error: cd: cannot change directory to path\_to\_change" followed by a '\n' with path\_to\_change replaced by the argument to cd
  * a cd command will never be immediately followed or preceded by a "|"
* You don't need to manage any type of wildcards (\*, \~ etc...)
* You don't need to manage environment variables ($BLA ...)
* If a system call, except execve and chdir, returns an error your program should immediatly print "error: fatal" in STDERR followed by a '\n' and the program should exit
* If execve failed you should print "error: cannot execute executable\_that\_failed" in STDERR followed by a '\n' with executable\_that\_failed replaced with the path of the failed executable (It should be the first argument of execve)
* Your program should be able to manage more than hundreds of "|" even if we limit the number of "open files" to less than 30.

Example that should work :&#x20;

```
$>./microshell /bin/ls "|" /usr/bin/grep microshell ";" /bin/echo i love my microshell
microshell
i love my microshell
$>

>./microshell 
```



<details>

<summary>One solution (that inspired me)</summary>

[https://github.com/shackbei/microshell-42/blob/main/microshell.c](https://github.com/shackbei/microshell-42/blob/main/microshell.c)

</details>
