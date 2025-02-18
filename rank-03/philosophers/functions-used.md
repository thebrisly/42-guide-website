# ▪️ Functions used

Remember `printf` ? Yeah right you recoded it yourself, that's good, but for this project, you can use the `stdlib` one, the real one.

And you also have access to a lot of other functions, but you **can't** use your `libft` for this project.

Some of these functions are only used for the bonus part, I didn't used them so I'll let you search how to use them. For this project you'll have to compile your programm with the `-pthread` flag.

### usleep()

```c
int usleep(useconds_t usec);
```

`usleep()` is a function in the C standard library that causes the calling process to sleep for a specified number of microseconds.

<details>

<summary>usleep() example</summary>

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

</details>

### gettimeofday()

```c
int gettimeofday(struct timeval *restrict tv, struct timezone *restrict tz);
```

The _**gettimeofday()**_ function gets the system’s clock time. The current time is expressed in elapsed seconds and microseconds since 00:00:00, January 1, 1970 (Unix Epoch).

<details>

<summary>gettimeofday()</summary>

```c
#include <sys/time.h>
#include <stdio.h>

int main() {
  struct timeval current_time;
  gettimeofday(&current_time, NULL);
  printf("seconds : %ld\nmicro seconds : %ld",
    current_time.tv_sec, current_time.tv_usec);

  return 0;
}
```

The 1st parameter is a pointer to a `timeval` structure. The `timeval` structure is defined as below in the `<sys/time.h>` header file.

```c
struct    timeval  {
  time_t        tv_sec ;   //used for seconds
  suseconds_t       tv_usec ;   //used for microseconds
}
```

The second argument should **always** be set to `NULL`. This second argument is obsolete and is only there for backwards compatibility.

</details>

You can find more information about **gettimeofday()** [here](https://man7.org/linux/man-pages/man2/settimeofday.2.html).

### pthread\_create()

```c
int pthread_create(pthread_t *restrict thread,
       const pthread_attr_t *restrict attr,
       void *(*start_routine)(void *),
       void *restrict arg);
```

The `pthread_create()` function starts a new thread in the calling process. The new thread starts execution by invoking `start_routine()`; `arg` is passed as the sole argument of `start_routine()`.

You can find more information about `pthread_create()` [here](https://man7.org/linux/man-pages/man3/pthread_create.3.html).

### pthread\_join()

```c
int pthread_join(pthread_t thread, void **retval);
```

```
       The pthread_join() function waits for the thread specified by
       thread to terminate.  If that thread has already terminated, then
       pthread_join() returns immediately.  The thread specified by
       thread must be joinable.
```

The `pthread_join()` function waits for the thread specified by `thread` to terminate. If that thread has already terminated, then `pthread_join()` returns immediately.

<details>

<summary>pthread_create() &#x26; pthread_join() example</summary>

```c
#include <pthread.h>
#include <stdlib.h>
#include <stdio.h>

void *thread(void *arg) {
  char *ret;
  printf("thread() entered with argument '%s'\n", arg);
  if ((ret = (char*) malloc(20)) == NULL) {
    perror("malloc() error");
    exit(2);
  }
  strcpy(ret, "This is a test");
  pthread_exit(ret);
}

main() {
  pthread_t thid;
  void *ret;

  if (pthread_create(&thid, NULL, thread, "thread 1") != 0) {
    perror("pthread_create() error");
    exit(1);
  }

  if (pthread_join(thid, &ret) != 0) {
    perror("pthread_create() error");
    exit(3);
  }

  printf("thread exited with '%s'\n", ret);
}
```

In this example, we use the pthread\_create() function to create a new thread that is initiated with the function called thread().

We then wait for the thread to terminate before printing the return value of the thread.

</details>

You can find more information about `pthread_join()` [here](https://man7.org/linux/man-pages/man3/pthread_join.3.html).

### pthread\_mutex\_init()

{% code overflow="wrap" %}
```c
int pthread_mutex_init(pthread_mutex_t *restrict mutex, const pthread_mutexattr_t *restrict attr);
```
{% endcode %}

The `pthread_mutex_init()` function initializes the mutex referenced by `mutex` with the attributes specified by `attr`. If `attr` is `NULL`, the default mutex attributes are used. When the `mutex` is successfully initialized, the mutex state becomes `initialized` and `unlocked`.

<details>

<summary>pthread_mutex_init() example</summary>

```c
#include <pthread.h>

int main(void)
{
    pthread_mutex_t mutex;

    // Initializing the mutex
    pthread_mutex_init(&mutex, NULL);
}
```

The above example uses the `pthread_mutex_init()` function to initialize a new `mutex` that can be used from all threads that we want to.

</details>

You can find more information about `pthread_mutex_init()` [here](https://man7.org/linux/man-pages/man3/pthread_mutex_destroy.3p.html).

### pthread\_mutex\_destroy()

```c
int pthread_mutex_destroy(pthread_mutex_t *mutex);
```

`The pthread_mutex_destroy()` function destroys the mutex object referenced by `mutex`. The `mutex` object becomes uninitialized and can be reinitialized with `pthread_mutex_init()` if needed.

<details>

<summary>pthread_mutex_init() &#x26; pthread_mutex_destroy() example</summary>

{% code overflow="wrap" %}
```c
#include <pthread.h>
#incluce <stdio.h>

int main(void)
{
    pthread_mutex_t mutex;
    
    // Initializing the mutex
    pthread_mutex_init(&mutex, NULL);
    
    printf("You can use the mutex from now on");
    
    // Destroying the mutex
    pthread_mutex_destroy(&mutex);
}
```
{% endcode %}

</details>

You can find more information about `pthread_mutex_destroy()` [here](https://man7.org/linux/man-pages/man3/pthread_mutex_destroy.3p.html).

### pthread\_mutex\_lock()

```c
int pthread_mutex_lock(pthread_mutex_t *mutex);
```

The `pthread_mutex_lock()` function locks the mutex referenced by `mutex`.

You can find more information about `pthread_mutext_lock()` [here](https://man7.org/linux/man-pages/man3/pthread_mutex_lock.3p.html).

### pthread\_mutex\_unlock()

```c
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

The `pthread_mutex_unlock()` function unlocks the mutex referenced by `mutex`.

<details>

<summary>pthread_mutex_lock() &#x26; pthread_mutex_unlock() example</summary>

```c
#include <pthread.h>
#include <stdio.h>

int main(void)
{
    pthread_mutex_t fork_mutex;
    
    pthread_mutex_init(&fork_mutex, NULL);
    
    pthread_mutex_lock(&fork_mutex);
    set_unavailable(fork);
    pthread_mutex_unlock(&fork_mutex);
    
    pthread_mutex_destroy(&fork_mutex);
    
    return (0);
}
```

</details>

You can find more information about `pthread_mutex_unlock()` [here](https://man7.org/linux/man-pages/man3/pthread_mutex_lock.3p.html).
