# ▪️ Building the thing

{% hint style="warning" %}
Draw the pipes on paper, this helps, a lot. Before writing to the outfile, make sure you read from the correct end of the correct pipe.
{% endhint %}

Here I'll give you some checklist on what you have to do to achieve this project. All the code for my pipex is available on my [Github](https://github.com/Laendrun/42-pipex), if you have any question, don't hesitate to [contact](../../team.md) me (Simon), it'll be a pleasure to help you.

### Main checklist

* [ ] Check the existence of `infile` and `outfile`
  * [ ] be sure to understand what `>` does when the file does not exist
* [ ] Create the necessary pipe (or pipes)
* [ ] Create a child process for each command
* [ ] Wait for all the processes to end before writing to the outfile

{% hint style="warning" %}
When using `here_doc`, the second argument is not a command ;)
{% endhint %}

### Execute checklist

Remember that the `execve()` function needs the path to a binary file as parameter, so you'll have to find where the commands binaries are stored on your computer. Before going further, you have to know how to find any command binary.

* [ ] Check in all possible locations if the binary (command) requested by the user exists.
* [ ] "Build" the arguments array for the command.
* [ ] Execute the command using `execve()`

{% hint style="info" %}
I know this is pretty small, but you have the information you need, you have to search and try things by yourself or else you won't learn anything.
{% endhint %}
