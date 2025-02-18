# ▪️ Building the thing

### Main checklist

This is a checklist containing the main steps you have to do, I don't want to give you too much information, you still have to search things by yourself.

* [ ] Create a data structure to store all required information about a philosopher
* [ ] Create the correct number of philosopher
* [ ] Create the correct number of threads
* [ ] Create a routine
  * [ ] What each philosopher has to do ? In which order ?
* [ ] Initiate the threads with said routine

{% hint style="info" %}
Some variables have to be shared between all philosophers so take this into account when creating your data structures.
{% endhint %}

### Routine checklist

* [ ] Create a loop that runs until any of your philosophers die

{% hint style="info" %}
If you have to loop until any of your philosphers die, it might be a good idea to check in the routine if any of your philosopher has died.
{% endhint %}

That's basically it. Your philosophers have to do the following things (in order) in the routine.

1. Eat
2. Sleep
3. Think
4. Repeat

The most complex thing in this project is to understand how threads work and how you can use mutexes to lock / unlock some values. Once you understood that, you "just" have to make each philosopher eat, sleep and think in a loop. Don't forget to print the logs when the state of your philosophers change.

### Final word

That's basically it, the things you have to do are not the most complicated, the most important part of this exercise is to understand everything about threads and mutexes and all. Also, if you do the bonuses, you'll have to understand semaphores and processes. We already used processes, in a way or another by doing [Minitalk](../../rank-02/minitalk/) or [pipex](../../rank-02/pipex/), but semaphores are an all new subject.

I don't want to add more details for this exercise, I want you to search information and really understand how everything works, this is the best I can do for you.

But don't hesitate to [contact](../../team.md) us if you have any question, I'll be happy to help you with your project.
