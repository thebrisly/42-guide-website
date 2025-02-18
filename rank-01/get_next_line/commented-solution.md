---
description: >-
  We propose you here one of the solutions that works. However, we recommend you
  to try not to look at the solution and read what we explained in part 3. Use
  this part only in case of emergency.
---

# ▪️ Commented solution

Below we will use my code (Simon) but you can also consult Laura's code, which is a little different from mine on some points. Here are our Github for this project:

* [Simon's get\_next\_line](https://github.com/Laendrun/42/tree/main/get_next_line)

{% hint style="danger" %}
<mark style="color:red;">**And again: Try to do it on your own and only consult the solutions in case of ultimate trouble! And if you want to look at the answers, try to understand what you are doing ;)**</mark>
{% endhint %}

I also made this project with the bonus, so you'll have both versions, I'll start with the normal version and you can try to find by yourself how to make the bonuses work.

{% hint style="info" %}
To make the bonus work I only had to add like 20 - 25 characters in total. The bonus for this project is easily achievable.
{% endhint %}

{% hint style="warning" %}
I won't be commenting the LIBFT functions, you have your own, I hope you know how they work.
{% endhint %}

<details>

<summary>get_next_line.c</summary>

{% code title="get_next_line.c" overflow="wrap" lineNumbers="true" %}
```c
#include "get_next_line.h"

static char    *_fill_line_buffer(int fd, char *left_c, char *buffer);
static char    *_set_line(char *line);
static char    *ft_strchr(char *s, int c);

char    *get_next_line(int fd)
{
    static char *left_c;
    char        *line;
    char        *buffer;
    
    buffer = (char *)malloc((BUFFER_SIZE + 1) * sizeof(char));
    /*
     * fd < 0 : this means the file descriptor is invalid
     * BUFFER_SIZE <= 0 : we'll read BUFFER_SIZE characters at a time,
     * we can't read 0 or less character
     * read(fd, 0, 0) < 0 : this check lets us see if the file exists and
     * that it has some content to read from, or event that the file is 
     * openable to read, maybe the file descriptor is more than 0, but it
     * was open in 'modify only', that means we can't read it.
     */
    if (fd < 0 || BUFFER_SIZE <= 0 || read(fd, 0, 0) < 0)
    {
        free(left_c);
        free(buffer);
        left_c = NULL;
        buffer = NULL;
        return (NULL);
    }
    if (!buffer)
        return (NULL);
    line = _fill_line_buffer(fd, left_c, buffer);
    /* We have to free the buffer variable here since we'll not be using
     * it later in the function, freeing it prevents memory leaks.
     */
    free(buffer);
    buffer = NULL;
    if (!line)
        return (NULL);
    left_c = _set_line(line);
    return (line);
}

static char *_set_line(char *line_buffer)
{
    char    *left_c;
    ssize_t    i;
    
    i = 0;
    /* This loop let's us find the end of the line
     * either when we encounter a \n or a \0
     */
    while (line_buffer[i] != '\n' && line_buffer[i] != '\0')
        i++;
    /* here we check if the current or next character is a \0
     * if this is the case, this means that the line is empty so
     * we return NULL, this is what the subject asks us, send NULL
     * if there is no next line
     */
    if (line_buffer[i] == 0 || line_buffer[1] == 0)
        return (NULL);
    /* here we take a substring from the end of the line to the end
     * of the whole line_buffer, that's what's left from our line
     */
    left_c = ft_substr(line_buffer, i + 1, ft_strlen(line_buffer) - i);
    if (*left_c == 0)
    {
        free(left_c);
        left_c = NULL;
    }
    /* don't forget to set the last character to \0 to NUL-terminate
     * the line
     */    
    line_buffer[i + 1] = 0;
    return (left_c);
}

static char	*_fill_line_buffer(int fd, char *left_c, char *buffer)
{
        /* ssize_t type works the same way as siyze_t type, but it can be
         * a negative number, something that size_t can't do.
         * Since most of the system function we'll be using return -1 to
         * signify errors, it could be useful to be able to store 
         * negative numbers
         */
	ssize_t	b_read;
	char	*tmp;

	b_read = 1;
	while (b_read > 0)
	{
		b_read = read(fd, buffer, BUFFER_SIZE);
		/* if b_read is -1, it means there was an error reading
		 * the file descriptor, so we free left_c and return NULL.
		 */
		if (b_read == -1)
		{
			free(left_c);
			return (NULL);
		}
		/* if b_read is 0, this surely means we read the whole
		 * file so there-s no need to stay in the loop
		 */
		else if (b_read == 0)
		/* if we didn't read anything, we can break out of the
		 * loop
		 */
			break ;
		/* don't forget to set the last character of the buffer
		 * to 0 to NUL-terminate the string
		 */
		buffer[b_read] = 0;
		/* there we check if the left_c static char * is empty
		 * because if it's empty, we can't use ft_strjoin on it
		 */
		if (!left_c)
			left_c = ft_strdup("");
		tmp = left_c;
		/* once we set left_c to be empty, if it was NUL
		 * or just that something was left in it from the
		 * last time we called get_next_line
		 * we can join the buffer we just read to left_c
		 */
		left_c = ft_strjoin(tmp, buffer);
		free(tmp);
		tmp = NULL;
		/* we search in the buffer we just read if we read
		 * a \n or not
		 * if yes, we can break out of the loop
		 * if not, we go in the loop once again to read more 
		 * from the file.
		 */
		if (ft_strchr(buffer, '\n'))
			break ;
	}
	/* at the end of this function, we return the left_c string
	 * it will contain everything we read and ensure there's is 
	 * either a \0 or a \n within it.
	 */
	return (left_c);
}

static char	*ft_strchr(char *s, int c)
{
	unsigned int	i;
	char			cc;

	cc = (char) c;
	i = 0;
	while (s[i])
	{
		if (s[i] == cc)
			return ((char *) &s[i]);
		i++;
	}
	if (s[i] == cc)
		return ((char *) &s[i]);
	return (NULL);
}
```
{% endcode %}

</details>

<details>

<summary>get_next_line_utils.c</summary>

{% code title="get_next_line_utils.c" overflow="wrap" lineNumbers="true" %}
```c
#include "get_next_line.h"

char	*ft_strdup(char *s1)
{
	char			*dest;
	unsigned int	i;

	dest = (char *) malloc(ft_strlen(s1) + 1);
	if (!dest)
		return (NULL);
	i = 0;
	while (s1[i])
	{
		dest[i] = s1[i];
		i++;
	}
	dest[i] = 0;
	return (dest);
}

size_t	ft_strlen(char *s)
{
	int	i;

	i = 0;
	while (s[i])
		i++;
	return (i);
}

char	*ft_substr(char *s, unsigned int start, size_t len)
{
	size_t	i;
	char	*str;

	if (!s)
		return (NULL);
	if (start > ft_strlen(s))
		return (malloc(1));
	if (len > ft_strlen(s + start))
		len = ft_strlen(s + start);
	str = malloc((len + 1) * sizeof(char));
	if (!str)
		return (NULL);
	i = 0;
	while (i < len)
	{
		str[i] = s[start + i];
		i++;
	}
	str[i] = 0;
	return (str);
}

char	*ft_strjoin(char *s1, char *s2)
{
	char			*res;

	res = (char *) malloc((ft_strlen(s1) + ft_strlen(s2) + 1) * sizeof(char));
	if (!res)
		return (NULL);
	fill_str(res, s1, s2);
	return (res);
}

void	fill_str(char *res, char *s1, char *s2)
{
	unsigned int	i;
	unsigned int	j;

	i = 0;
	j = 0;
	while (s1[j])
		res[i++] = s1[j++];
	j = 0;
	while (s2[j])
		res[i++] = s2[j++];
	res[i] = '\0';
}
```
{% endcode %}

</details>

<details>

<summary>get_next_line.h</summary>

{% code title="get_next_line.h" overflow="wrap" lineNumbers="true" %}
```c
#ifndef GET_NEXT_LINE_H
# define GET_NEXT_LINE_H
# ifndef BUFFER_SIZE
#  define BUFFER_SIZE 42
# endif
# include <stdlib.h>
# include <unistd.h>
# include <fcntl.h>

char    *get_next_line(int fd);
char    *ft_strdup(char *s);
size_t    ft_strlen(char *s);
char    *ft_substr(char *s, unsigned int start, size_t len);
char    *ft_strjoin(char *s1, char *s2);
void    fill_str(char *res, char *s1, char *s2);

#endif
```
{% endcode %}

</details>

### Bonus part

As said before, I made the bonus for this project, so here under I'll put the code for the bonus part.&#x20;

{% hint style="danger" %}
I encourage you to really try the bonus by yourself, they are easily achievable as said before.
{% endhint %}

<details>

<summary>get_next_line_bonus.c</summary>

{% code title="get_next_line_bonus.c" overflow="wrap" lineNumbers="true" %}
```c
#include "get_next_line.h"

static char		*_fill_line_buffer(int fd, char *left_c, char *buffer);
static char		*_set_line(char *line);
static char		*ft_strchr(char *s, int c);

char	*get_next_line(int fd)
{
	/* There's only a minimal difference to make the bonus
	 * work
	 * It's basically transforming our static char * variable
	 * to an array of char *
	 * as you can see I set the number of elements of the array to 
	 * the constant MAX_FD (see get_next_line.h to see what it is)
	 */
	static char	*left_c[MAX_FD];
	char		*line;
	char		*buffer;

	buffer = (char *)malloc((BUFFER_SIZE + 1) * sizeof(char));
	if (fd < 0 || BUFFER_SIZE <= 0 || read(fd, 0, 0) < 0)
	{
		/* as we changed our static char * to an array
		 * we have to specify wich index we wanna work on
		 * the easier thing to do is to set it to fd
		 */
		free(left_c[fd]);
		free(buffer);
		left_c[fd] = NULL;
		buffer = NULL;
		return (0);
	}
	if (!buffer)
		return (NULL);
	/* again here, we want to store the left characters in 
	 * the array at the index of the fd, so if we have another fd
	 * we won't be overwriting what was left from the other fd
	 */
	line = _fill_line_buffer(fd, left_c[fd], buffer);
	free(buffer);
	buffer = NULL;
	if (!line)
		return (NULL);
	/* and here again, we have to switch from left_c to left_c[fd]
	 * that's the last thing we have to change, all the other place
	 * we use left_c (in all other functions), we use it as a string
	 * therefore, because we are passing left_c[fd] as parameter
	 * we basically are passing strings as parameter
	 * so no problem there, and nothing to change.
	 */
	left_c[fd] = _set_line(line);
	return (line);
}

static char	*_set_line(char *line_buffer)
{
	char	*left_c;
	ssize_t	i;

	i = 0;
	while (line_buffer[i] != '\n' && line_buffer[i] != '\0')
		i++;
	if (line_buffer[i] == 0 || line_buffer[1] == 0)
		return (0);
	left_c = ft_substr(line_buffer, i + 1, ft_strlen(line_buffer) - i);
	if (*left_c == 0)
	{
		free(left_c);
		left_c = NULL;
	}
	line_buffer[i + 1] = 0;
	return (left_c);
}

static char	*_fill_line_buffer(int fd, char *left_c, char *buffer)
{
	ssize_t	b_read;
	char	*tmp;

	b_read = 1;
	while (b_read > 0)
	{
		b_read = read(fd, buffer, BUFFER_SIZE);
		if (b_read == -1)
		{
			free(left_c);
			return (0);
		}
		else if (b_read == 0)
			break ;
		buffer[b_read] = 0;
		if (!left_c)
			left_c = ft_strdup("");
		tmp = left_c;
		left_c = ft_strjoin(tmp, buffer);
		free(tmp);
		tmp = NULL;
		if (ft_strchr(buffer, '\n'))
			break ;
	}
	return (left_c);
}

static char	*ft_strchr(char *s, int c)
{
	unsigned int	i;
	char			cc;

	cc = (char) c;
	i = 0;
	while (s[i])
	{
		if (s[i] == cc)
			return ((char *) &s[i]);
		i++;
	}
	if (s[i] == cc)
		return ((char *) &s[i]);
	return (NULL);
}
```
{% endcode %}

</details>

<details>

<summary>get_next_line_utils_bonus.c</summary>

{% code title="get_next_line_utils_bonus.c" overflow="wrap" lineNumbers="true" %}
```c
#include "get_next_line.h"

char	*ft_strdup(char *s1)
{
	char			*dest;
	unsigned int	i;

	dest = (char *) malloc(ft_strlen(s1) + 1);
	if (!dest)
		return (NULL);
	i = 0;
	while (s1[i])
	{
		dest[i] = s1[i];
		i++;
	}
	dest[i] = 0;
	return (dest);
}

size_t	ft_strlen(char *s)
{
	int	i;

	i = 0;
	while (s[i])
		i++;
	return (i);
}

char	*ft_substr(char *s, unsigned int start, size_t len)
{
	size_t	i;
	char	*str;

	if (!s)
		return (NULL);
	if (start > ft_strlen(s))
		return (malloc(1));
	if (len > ft_strlen(s + start))
		len = ft_strlen(s + start);
	str = malloc((len + 1) * sizeof(char));
	if (!str)
		return (NULL);
	i = 0;
	while (i < len)
	{
		str[i] = s[start + i];
		i++;
	}
	str[i] = 0;
	return (str);
}

char	*ft_strjoin(char *s1, char *s2)
{
	char			*res;

	res = (char *) malloc((ft_strlen(s1) + ft_strlen(s2) + 1) * sizeof(char));
	if (!res)
		return (NULL);
	fill_str(res, s1, s2);
	return (res);
}

void	fill_str(char *res, char *s1, char *s2)
{
	unsigned int	i;
	unsigned int	j;

	i = 0;
	j = 0;
	while (s1[j])
		res[i++] = s1[j++];
	j = 0;
	while (s2[j])
		res[i++] = s2[j++];
	res[i] = '\0';
}

```
{% endcode %}

</details>

<details>

<summary>get_next_line_bonus.h</summary>

{% code title="get_next_line_bonus.h" overflow="wrap" lineNumbers="true" %}
```c
/*
 * The MAX_FD macro is defined based on the max number of file descriptors
 * based on my current OS and what I found online (MacOS Ventura 13.0)
 * (this information is particularly hard to find, or I just don't know 
 * what to search for on Google)
 */
#ifndef GET_NEXT_LINE_BONUS_H
# define GET_NEXT_LINE_BONUS_H
# ifndef BUFFER_SIZE
#  define BUFFER_SIZE 15
# endif
# define MAX_FD 10240
# include <stdlib.h>
# include <unistd.h>
# include <fcntl.h>

char	*get_next_line(int fd);

char	*ft_strdup(char *s);
size_t	ft_strlen(char *s);
char	*ft_substr(char *s, unsigned int start, size_t len);
char	*ft_strjoin(char *s1, char *s2);
void	fill_str(char *res, char *s1, char *s2);

#endif
```
{% endcode %}

</details>
