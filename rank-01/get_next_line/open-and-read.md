# ▪️ open() & read()

To start this project you must first be able to open a text file. Once opened, we will be able to read it. This can be done using the open() and read() functions.



{% hint style="danger" %}
PS: If you don't know what it is is a file descriptor (fd), you can check this page before continuing:
{% endhint %}

{% content-ref url="../../useful-tools/file-descriptors-fd.md" %}
[file-descriptors-fd.md](../../useful-tools/file-descriptors-fd.md)
{% endcontent-ref %}

##

## open ()

For the function to work, you must first implement the following library

```c
#include <fcntl.h>
```

This function will allow you to open and access a file. It is prototyped this way:

```c
int open (const char* path, int flags [, int mode ]);
```

#### Path

It corresponds to title of the file that you would like to open/create.&#x20;

It also refers to the file’s location. If you are not working in the same directory as the file, you can provide an absolute path that begins with “/”

#### Flags

You have to tell your function what kind of access you want. This is done with flags. Here is the list with the information of each flag:

* **O\_RDONLY**: In read-only mode, open the file.
* **O\_WRONLY**: In a write-only mode, open the file
* **O\_RDWR**: Open the file in reading and write mode
* **O\_CREAT**: This flag is applied to create a file if it doesn’t exist in the specified path or directory
* **O\_EXCL**: Prevents the file creation if it already exists in the directory or location.

#### Return Value

The return value of open() is a file descriptor, a small, nonnegative integer that is an index to an entry in the process's table of open file descriptors. If there is an error somewhere, the function will return -1 as a synonym of failure.

<details>

<summary>Example</summary>

There has to be a `text.txt` file so you can open it.

```c
int main()
{
    int fd;
    fd = open("text.txt", O_RDONLY);
}
```

</details>

For the moment it will not show you anything because the function is only used to open a file. You will have to use an additional function to make it useful. For example the read() function that we will see together now.



## read ()

The function is prototyped this way:&#x20;

```c
ssize_t read(int fildes, void *buf, size_t nbyte);
```

This function attempts to read `nbyte` bytes of data from the object referenced by the descriptor `fildes` into the buffer pointed to by `buf`.  The read() function starts at a position given by the pointer associated with `fildes`. At the end, the pointer is incremented by the number of bytes (`nbyte`) actually read.

It is well explained in the below video, so I will not get through it once again:

{% embed url="https://www.youtube.com/watch?t=2s&v=-Mt2FdJjVno" %}

It is in french but it has english subtitles !



Now that you know how these two functions work, let's move on to the next step: [understanding static variables](static-variables.md). A concept that will be used a lot in other projects! See you there :smile:
