# ▪️ Functions used

You are allowed to use several functions in this project. You already know some of them like write, ft\_printf (<mark style="color:red;">yours!</mark>), malloc, free and all the functions from your libft. However, other important functions that have never been used before will be **essential** to the success of this project. Let's look at them together.



### signal()

```c
sighandler_t signal(int signum, sighandler_t handler);
```

The `signal` function in C is a way to specify a function, called a signal handler, to be called when a specific signal is received by a running program. A signal is a message from the operating system to a program indicating that some event has occurred. The `signal` function allows you to specify a function to be called when a particular signal is received, so that you can take some action in response to the signal.

<details>

<summary>signal() example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>

void signal_handler(int signum) 
{
  printf("Received SIGINT!\n", signum);
  exit(0);
}

int main() 
{
  // Set the signal handler for the SIGINT and SIGTERM signals
  // to the signal_handler function
  
  signal(SIGINT, signal_handler);
  signal(SIGTERM, signal_handler);

  while (1) {
    // Do some work here...
  }

  return 0;
}
```
{% endcode %}

In this example, we've set the signal handler for both the `SIGINT` and `SIGTERM` signals to the `signal_handler` function. The `SIGINT` signal is generated when the user presses `CTRL+C`, and the `SIGTERM` signal is generated when the program is terminated by the operating system (e.g. by running the `kill` command). When either of these signals is received, the `signal_handler` function will be called, and it will print a message to the console and exit the program.

This example also demonstrates a common use case for the `signal` function: setting a signal handler to gracefully terminate a program when a certain signal is received. By setting a signal handler for the `SIGINT` and `SIGTERM` signals, we can ensure that the program will exit cleanly when it is terminated, rather than leaving resources in an undefined state.

</details>

### sigemptyset()

```c
int sigemptyset(sigset_t *set);
```

The `sigemptyset` function is used to initialize a signal set to the empty set, which means that it does not contain any signals. Signal sets are used by some functions, such as `sigaction`, to define the signals to be processed. The `sigemptyset` function takes a pointer to a set of signals as an argument and empties this set by adding no signal to it. This function is often used in conjunction with the `sigaddset` function, which adds a specified signal to a signal set.

### sigaddset()

```c
int sigaddset(sigset_t *set, int signum);
```

This function allows to add a signal to a set of signals. The `sigaddset` function takes two arguments: a pointer to a set of signals and the number of the signal to add to the set.&#x20;

Here is an example of using `sigaddset` to add the signal SIGINT to a set of signals and `sigemptyset`:

<details>

<summary>sigemptyset() &#x26; sigaddset() example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <signal.h>

int main(void)
{
    sigset_t signal_set;

    // Initialize an empty signal set
    sigemptyset(&signal_set);

    // Add SIGINT to the signal set
    sigaddset(&signal_set, SIGINT);
```
{% endcode %}

</details>

### sigaction()

{% code overflow="wrap" %}
```c
int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);
```
{% endcode %}

The `sigaction` function in C is used to specify the action to be taken when a specific signal is received by a process. It is defined in the `signal.h` header file.

The `signum` argument specifies the signal for which the action is being specified. The `act` argument is a pointer to a `struct sigaction` that specifies the action to be taken when the signal is received. The `oldact` argument is a pointer to a `struct sigaction` that is used to retrieve the previous action for the specified signal.

<details>

<summary>sigaction() example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>

void signal_handler(int signum) {
  printf("Received signal %d\n", signum);
}

int main(void) {
  struct sigaction action;
  action.sa_handler = signal_handler;
  sigemptyset(&action.sa_mask);
  action.sa_flags = 0;

  sigaction(SIGINT, &action, NULL);

  while (1) {
    // Do some work
  }

  return 0;
}
```
{% endcode %}

In this example, the `signal_handler` function is specified as the action to be taken when the `SIGINT` signal is received. When the signal is received, the `signal_handler` function will be called, which will print a message to the console. The `sigemptyset` function is used to initialize the signal mask, which specifies the signals that should be blocked while the signal handler is executing. The `sa_flags` field is set to 0, which specifies the default behavior for the signal action.

</details>



### kill()

```c
int kill(pid_t pid, int sig);
```

In C, the `kill` function **is a system call that sends a signal to a process**. It is defined in the `signal.h` header file.

The `pid` argument specifies the process ID of the process you want to communicate with. The `sig` argument specifies the signal to be sent to the process. There are various signals that can be sent, each corresponding to a different purpose. For example, the `SIGKILL` signal is used to terminate processes that are unresponsive or stuck in an infinite loop.

<details>

<summary>kill() example</summary>

Here is an example of using the `kill` function to terminate a process with the `SIGKILL` signal:

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

int main() {
  pid_t pid = getpid();  // get the process ID of the current process
  int result = kill(pid, SIGKILL);  // send the SIGKILL signal to the process
  if (result == 0) {
    printf("Process terminated successfully.\n");
  } else {
    perror("Error terminating process");
  }
  return 0;
}
```
{% endcode %}

Note that using the `kill` function to terminate a process should generally be avoided, as it can leave resources allocated to the process in an undefined state. Instead, it is usually better to allow the process to terminate gracefully by providing it with an opportunity to clean up and release resources before exiting.

</details>

### getpid()

```c
pid_t getpid(void);
```

In C, the `getpid` function **returns the process ID of the current process**. It is declared in the `unistd.h` header file.&#x20;

<details>

<summary>What are the process ID for?</summary>

In an operating system, a process is **an instance of a program that is being executed**. A process ID (PID) is a unique identifier assigned to each process by the operating system when it is created.

Process IDs are useful for a variety of purposes in coding. Here are a few examples:

1. Identifying and tracking processes: As mentioned earlier, the process ID is a unique identifier for a process, so it can be used to identify and track specific processes within the system.
2. Sending signals to processes: The `kill` function in C allows you to send a signal to a process, and you can specify the process to send the signal to using the process ID. This can be useful for controlling and interacting with processes from your code.
3. Process communication: Process IDs can be used as a way for processes to communicate with each other. For example, one process might create a new process using the `fork` function, and then pass the child process's ID back to the parent process so that the parent can communicate with the child.
4. Debugging: Process IDs can be helpful in debugging, as they can be used to identify which processes are causing problems or behaving unexpectedly.

Overall, process IDs are a useful tool for managing and interacting with processes in your code.

</details>

<details>

<summary>getpid() example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <unistd.h>

int main(void) {
  pid_t pid;

  pid = getpid();
  printf("The process ID is %d\n", pid);

  return 0;
}
```
{% endcode %}

This program will print the process ID of the current process to the console. The process ID is a unique identifier assigned to each process by the operating system. It is used to identify and track processes within the system.

</details>

### pause()

```c
int pause(void);
```

`pause()` is a function in the C standard library that causes the calling process to sleep until a signal is received. The process remains blocked until a signal handler is executed or the signal is ignored

<details>

<summary>pause() example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <unistd.h>

int main(void) {
    printf("Entering pause...\n");
    pause();
    printf("Exiting pause.\n");
    return 0;
}

```
{% endcode %}

</details>

### sleep()

```c
unsigned int sleep(unsigned int seconds);
```

`sleep()` is also a function in the C standard library that causes the calling process to sleep for a specified number of seconds.

<details>

<summary>sleep() example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <unistd.h>

int main(void) {
    printf("Sleeping for 3 seconds...\n");
    sleep(3); // The program waits 3 seconds
    printf("Done sleeping.\n");
    return 0;
}

```
{% endcode %}

</details>

### usleep()

```c
int usleep(useconds_t usec);
```

`usleep()` is a function in the C standard library that causes the calling process to sleep for a specified number of microseconds.

<details>

<summary>usleep() example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <unistd.h>

int main(void) {
    printf("Sleeping for 500000 microseconds...\n");
    usleep(500000);
    printf("Done sleeping.\n");
    return 0;
}

```
{% endcode %}

</details>

### exit()

```c
void exit(int status);
```

`exit()` is a function in the C standard library that terminates the calling process immediately. It takes an integer argument that specifies the exit status of the process. A value of 0 indicates successful termination, while non-zero values indicate an error.

<details>

<summary>exit() example</summary>

{% code overflow="wrap" lineNumbers="true" %}
```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    printf("Exiting with status 0...\n");
    exit(0);
}

```
{% endcode %}

</details>



And... that's it. You should be able to make some tests alone right now ;) If you don't know how to do it, see you in the next step.
