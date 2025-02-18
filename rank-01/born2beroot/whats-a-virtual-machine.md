---
description: Some definitions to understand what you're doing
---

# 📠 What's a virtual machine ?

Very briefly, a **virtual machine** (VM) is a machine in your machine.&#x20;

**Virtualization** is the art of running on the same physical machine, several systems as if they were running on separate physical machines.&#x20;

To better understand what I'm saying and for you to better visualize what it is for, let's go back to the basics. We will take the example of a computer server, as a machine since that's what we have to create in this project.



## Components of a computer server

A physical server has a number of hardware elements such as a motherboard, a CPU (processor), some RAM to store information temporarily, a hard disk to store information for a longer period of time, a network card and many other components. An operating system is installed on top and it can contain several applications.

A virtual machine will use the hardware of the machine it is running on (CPU & memory i.e.), but everything inside will be different. The virtual machine can have a different operating system and many different applications.&#x20;

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

You can see in the diagram that I added a "virtualization layer". This step is performed by a hypervisor.&#x20;



## Hypervisor

A **hypervisor** is a piece of software that enables a user to create and run one or more virtual machines simultaneously. A hypervisor is also known as the virtual machine monitor (VMM) and controls the resources of the host machine and allocates to each VM the resources it needs (memory, CPU...), making sure that these VM's do not interfere with each other.

### VirtualBox

In 42, it is recommended to work with **"VirtualBox"** (or UTM if VB doesn't work). It's an open-source software that you will find on your Mac, if you are using one at a 42 school. Otherwise you can [install it](https://www.virtualbox.org/manual/ch02.html). It acts as a hypervisor, creating a VM (virtual machine) where the user can run another OS (operating system).&#x20;

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>



## Operating System

Every machine runs on an **operating system (OS)**, which is a set of programs that allows to run and control a machine. In other words, it's the interface between the user, the programs and the computer components. For example, Apple machines run mainly on macOS. Other machines can run on Windows or Linux, which are other two known operating system.

Your virtual machine will also have to use an operating system. You will have the choice between Debian and CentOS. Let's see the difference between these two

{% hint style="danger" %}
The subject changed since we wrote this so make sure to read your subject correctly before validating your project.\
We'll update this guide when we have checked what the differences are exactly.
{% endhint %}

### Debian VS CentOS

`Debian` was one of the first Linux distributions and has been available since 1993. Debian offers a higher degree of control and customization of its configuration.&#x20;

Released in 2004, `CentOS` is commonly used in the IT world on a large scale. CentOS ensures enterprise-level security, thus making it safe for users.&#x20;

* Debian is a lot easier to update then CentOS when a new version is released.&#x20;
* Debian is more user-friendly and supports many libraries, filesystems and architecture. It also has more options for customisation.&#x20;
* If you are a larger business CentOS offers more Enterprise features and excellent support for the Enterprise software.

If you are a beginner, 42 recommends you to use Debian.

{% hint style="info" %}
I will continue this GitBook with Debian.
{% endhint %}

##

## What is the purpose of virtual machines?

The very first point, which is obvious, is that it is **more convenient and cheaper** to install a virtual machine than to buy another computer. Moreover, **the maintenance of VMs is very low** compared to the maintenance of a server (or other physical machine). And on top of all that, **you save a lot of space**. Instead of storing X number of machines at home, they are all on the same machine.

When a physical server crashes, it can be complex to recover the data it contained. **The software aspect of VMs simplifies data backup**. While your VM is running, it is possible to obtain a backup thanks to a snapshot of the VM and its data. In case of an incident, this snapshot allows you to restore the VM to its previous state.&#x20;

Virtualization allows you to **increase the security of your data** by partitioning them and isolating services on different servers. Each VM is isolated from the others, including the host system. This limits the risks of propagation in case of malware intrusion. Moreover, **if a virtual machine crashes, the other VMs are not affected**.

But it can also simply allow you to **test operating systems** or **be used as a test environment** for other things.



{% hint style="success" %}
**To summarize...**\
\
A virtual machine is a machine that is inside a host machine. It will behave exactly the same way as any other machine; it has an operating system and some apps.

There are several advantages to having a virtual machine:

* Inexpensive
* Save physical space (stock)
* Less maintenance than a physical machine
* Data backup simplified
* Increased security
{% endhint %}



Now that you have some theory, we can start the practice by installing our first virtual machine ! See you in the next section

