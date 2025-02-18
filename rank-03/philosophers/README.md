---
description: >-
  The purpose of this project is to introduce you to threading and processes,
  and how to work on shared memory space. You'll discover threads, mutex,
  semaphores and shared memory
---

# Philosophers

The "philosophers' dinner" problem is a classic thought experiment and a well-known problem in computer science and distributed systems.

The problem is typically presented in the context of five philosophers who are sitting around a circular table, with a plate of spaghetti in front of each of them, and a single fork between each pair of adjacent philosophers. The goal of each philosopher is to eat the spaghetti, but in order to do so, they must each use two forks.

I recommend you to watch this video to better understand the problem

{% embed url="https://youtu.be/VSkvwzqo-Pk" %}

{% hint style="danger" %}
the subject of 42 changes a bit from what is on the video - always read the subject carefully
{% endhint %}

The problem is to design a protocol that allows each philosopher to pick up the two forks to their sides without causing a deadlock, where every philosopher is waiting for a fork that is currently being held by their neighbor. The protocol must ensure that no philosopher goes hungry, and that no two adjacent philosophers hold the same fork at the same time.

The philosophers' dinner problem is an example of a concurrency problem in computer science and distributed systems, and it has been used as a case study in various fields, including operating systems, distributed algorithms, and concurrent programming. **It highlights the importance of designing protocols that can handle concurrent access to shared resources without causing deadlocks or other issues**.



Now that you know the general idea, let's try to see together how we can solve this problem
