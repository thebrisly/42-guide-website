# ▪️ Understand Philosophers

{% hint style="warning" %}
We didn't do the bonuses so we will not explain anything about it.\
I'll let you do some research yourself ;)
{% endhint %}

### What is a process ?

> A process is a program that is running on your computer. This can be anything from a small background task, such as a spell-checker or system events handler to a full-blown application like Internet Explorer or Microsoft Word. All processes are composed of one or more [threads](https://techterms.com/definition/thread).

If you want a more precise example of what a process is, you can click [\[here\]](https://42-cursus.gitbook.io/guide/rank-02/minitalk/understand-minitalk#processes-and-signals). Laura created and showed a good example.

> Since most [operating systems](https://techterms.com/definition/operating_system) have many background tasks running, your computer is likely to have many more processes running than actual programs. For example, you may only have three programs running, but there may be twenty active processes. You can view active processes in Windows by opening the Task Manager (press Ctrl-Alt-Delete and click Task Manager). On a Mac, you can see active processes by opening Activity Monitor (in the Applications→Utilities folder).

Source : [techterms.com](https://techterms.com/definition/process)

### What is a thread ?

> What do a t-shirt and a computer program have in common? They are both composed of many threads! While the threads in a t-shirt hold the shirt together, the threads of a computer program allow the program to execute sequential actions or many actions at once. Each thread in a program identifies a process that runs when the program asks it to (unlike when you ask your roommate to do the dishes).
>
> Threads are typically given a certain priority, meaning some threads take precedence over others. Once the CPU is finished processing one thread, it can run the next thread waiting in line. However, it's not like the thread has to wait in line at the checkout counter at Target the Saturday before Christmas. Threads seldom have to wait more than a few milliseconds before they run. Computer programs that implement "multi-threading" can execute multiple threads at once. Most modern operating systems support multi-threading at the system level, meaning when one program tries to take up all your CPU resources, you can still switch to other programs and force the CPU-hogging program to share the processor a little bit.

Source: [techterms.com](https://techterms.com/definition/thread)



### Differences between threads and processes

Both processes and threads are independent sequences of execution. The typical difference is that threads (of the same process) run in a shared memory space, while processes run in separate memory spaces. (source: [stackoverflow](https://stackoverflow.com/questions/200469/what-is-the-difference-between-a-process-and-a-thread))

Here under are some points that I noted during my research :

#### Process

* Can have multiple threads
* When using fork(), duplicates everything
  * This means a variable is just copied, if we modify the variable in one process it won't be modified in the other one

#### Threads

* share memory space
  * if I declare a variable somewhere, and modify it inside of a thread, it will be changed for every other threads as well
* can run in what's called a "memory race"
  * since the memory is shared between threads, if multiple threads try to access the same variable at the same time, it's called a "memory race" since the "fastest" thread will modify the variable value, and then the other one will. But the value of the first modification could have useful somewhere.
  * we have to protect our program against "memory race", like we do for "memory leaks"

{% embed url="https://www.youtube.com/watch?v=FY9livorrJI" %}

### What is a mutex ? (pthread\_mutex)

A mutex is basically a lock. We can lock a variable so that only one thread can access the variable at a time. When the first thread finished its operation on the variable, we unlock the mutex so that the other thread can access the variable.

{% embed url="https://www.youtube.com/watch?feature=youtu.be&v=oq29KUy29iQ" %}

