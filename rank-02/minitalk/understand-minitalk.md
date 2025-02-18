---
description: >-
  You will have to realize a communication program in the form of a client and a
  server.
---

# ▪️ Understand minitalk

### Goal

<details>

<summary>Project-specific guidelines (2023)</summary>

You must create a communication program in the form of a client and a server.

* The server must be started first. After its launch, it has to print its PID.
* The client takes two parameters: 1) The server PID 2) The string to send.
* The client must send the string passed as a parameter to the server. Once the string has been received, the server must print it.
* The server has to display the string pretty quickly. Quickly means that if you think it takes too long, then it is probably too long.
* Your server should be able to receive strings from several clients in a row without needing to restart.
* The communication between your client and your server has to be done only using UNIX signals.
* You can only use these two signals: SIGUSR1 and SIGUSR2.

</details>

The goal of the Minitalk project is to develop a simple program that allows processes (= programs running on a computer) to communicate with each other using a communication protocol called "minitalk". It corresponds to the protocol that you need to code.

The minitalk communication protocol involves sending messages between two processes using a series of signals over a single wire.&#x20;

* One process, called the "speaker/client" sends the message by transmitting a series of signals over the wire.&#x20;
* The other process, called the "listener/server" receives the message by interpreting the series of signals as a message.

{% hint style="info" %}
**Signals are a form of communication between processes** used by Unix-like systems (e.g. MacOS or Linux) and those respecting the POSIX standards. **Signals can be defined as a message**, an event or an interrupt. When a process receives a signal, the process will stop what its doing and **take some action**.\
\
In the context of the Minitalk project, signals are used to transmit messages between processes using the minitalk communication protocol.
{% endhint %}

I am a visual person, so I tried to make this diagram for you to understand better:

<figure><img src="../../.gitbook/assets/minitalk_scheme.png" alt=""><figcaption><p>minitalk explanatory scheme</p></figcaption></figure>

As we can see, we have a client that wants to send a message to the server. The "Hello" (message) cannot be sent directly to the server. The client has to encrypt the message and the server has to decrypt/interpret it before it can be displayed.

I'll keep it general here and go into more detail in the "[Building the thing](building-the-thing.md)" section.



### Processes & signals

{% hint style="info" %}
We are going to go a little further than what is asked in the subject, but it is to better understand later what you do.
{% endhint %}

**Processes and signals are the most important terms to know in this project.** I've already explained a bit about them above, but you may not have fully understood them yet - let's take another simple example to understand these new concepts.

As i said before, in computer science, a signal is a message that is sent to a process to indicate a particular event has occurred or to request a particular action to be taken. A process is a program that is being executed by the computer.

Let's take a simple example:

Imagine you have a program that is running on your computer. This program is Google Chrome running in the background on your computer. When you have multiple windows open on your browser, you have multiple programs running. These programs are called processes.

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Now, suppose that you want to stop these program. You can do this by simply closing the browser window in question. Easy. Or by sending a signal to the process. **Remember: a signal is just telling a process to do a certain thing!**

Here, we want to close the windows. That will be the signal that we want to send to the processes.

For this, you might use the "kill" command in a terminal window to send a signal to the processes. This signal tells the process to terminate itself. So in this example, the signal (the "kill" command) is used to request a particular action (termination of the process) to be taken.

To send a signal to a certain process **you need the PID** of it. They will be useful, because that's how you will know which signal to send to which process. It's like a computerized version of our passports. Example on how to dit it:

`kill <PID>`

If you use the above command you will have to kill one process after the other. As they are all part of Chrome, you could also use a single command instead, which will close all running programs (processes) related to chrome.

`killall chrome`

<details>

<summary>To go a bit bit further</summary>

If you are curious, you can find all the "Google Chrome" programs currently running on your computer by typing this command:&#x20;

`ps -Af | grep chrome`

It will pull up a list of all Chrome processes. A bit like that:

```
1000      2706     1  2 23:01 ?        00:00:52 /usr/bin/google-chrome-stable
1000      2713  2706  0 23:01 ?        00:00:00 /usr/bin/google-chrome-stable
1000      2714  2706  0 23:01 ?        00:00:00 /opt/google/chrome/chrome-sandbox /opt/google/chrome/chrome --type=zygote
1000      2715  2714  0 23:01 ?        00:00:00 /opt/google/chrome/chrome --type=zygote
1000      2719  2715  0 23:01 ?        00:00:00 /opt/google/chrome/nacl_helper
1000      2720  2715  0 23:01 ?        00:00:00 /opt/google/chrome/chrome --type=zygote
1000      2839  2706  0 23:01 ?        00:00:08 /opt/google/chrome/chrome --type=gpu-process --channel=2706.3.250838429 --supports-dual-gpus=false --gpu-driver-bug-workarounds=0,1,27 --disable-accelerated-video-decode --gpu-vendor-id=0x1002 --gpu-device-id=0x6760 --gpu-driver-vendor=ATI / AMD --gpu-driver-version=13.30
1000      2843  2839  0 23:01 ?        00:00:00 /opt/google/chrome/chrome --type=gpu-process --channel=2706.3.250838429 --supports-dual-gpus=false --gpu-driver-bug-workarounds=0,1,27 --disable-accelerated-video-decode --gpu-vendor-id=0x1002 --gpu-device-id=0x6760 --gpu-driver-vendor=ATI / AMD --gpu-driver-version=13.30
1000      3038  2720  1 23:08 ?        00:00:28 /opt/google/chrome/chrome --type=renderer --lang=en-US --force-[...very long options list]
1000      4505  4441  0 23:40 pts/0    00:00:00 grep --color=auto chromebash
```

_Note: if you did not open google chrome but you still see a line appearing, it is by the simple fact of having called it with the command above (grep chrome)_

The second column will contain the process identifier (PID) of the processes. So 2706, 2713 or 2720, all correspond to the PID of a certain process.

</details>

Well, I hope you now have a better understanding of the basic concept! Now let's move on to the last theoretical part. To achieve this project, you will have to understand and use [new functions](functions-used.md) that allow to manage these computer signals: signal(), sigemptyset(), sigaddset(), sigaction(), kill(), pause() and sleep().&#x20;

