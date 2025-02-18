# 📠 Install your virtual machine

I'm not going to lie to you, I don't know how to install a virtual machine by myself. I had to follow some guides. Here is the one that i used:&#x20;

{% embed url="https://github.com/pasqualerossi/Born2BeRoot-Guide/blob/main/README.md" %}

Other guides can be found on the internet. I used this one and it worked great! Feel free to use another one if it doesn't seem clear to you. From now, I will use this guide above and try to explain some theoretical things that are not explained there.



{% hint style="info" %}
I put my virtual machine & the image of debian on my sgoinfre directory.

_sgoinfre_ is a server accessible from the 42 School network and available from each computer. It is a document server where you have a directory with your login name that only you can access.

On each computer, there's also a folder called _goinfre,_ this folder let's you store some documents. This folder is different on each computer and larger than your session storage.

If you put your virtual machine on the _sgoinfre_ server, you can change computer during your project, if you put it in the _goinfre_ folder, you have to stay on the same computer all along.
{% endhint %}

## Part 1, 2 - Downloading & installing your Virtual Machine

This part is quite simple to do.&#x20;

You are creating an empty virtual machine. It is as if you were setting up a computer from scratch.&#x20;





## Part 3 - Accessing  your Virtual Machine

In this part you will configure the first elements of your machine. You will...

* &#x20;select the language, time zone & country on which your machine will run&#x20;
* create a hostname (your\_42\_login42) and a password for your machine&#x20;
* create a first simple user (your\_42\_login) and a password for it&#x20;
* configure the partitions of your machine

### What is disk <mark style="color:blue;">partitioning</mark> with LVM ?

Disk _partitioning_ is the creation of one or more storage regions (called _partitions_), so that each region can be managed separately.

Each OS has a different way to designate partitions. On Linux (and thus Debian or CentOS) they are designated like that: sdXN, with X a letter representing the medium and N the number of the partition on the medium (for example sdb3 for the third partition of disk b).

Partitioning offers many advantages in terms of security.

It is common practice to reserve partitions for services that can generate a lot of volume in order to avoid saturating the system partitions.

Here is a short list of partitions that may exist (and that we use in this project):

| Name  |                                                                                  |
| ----- | -------------------------------------------------------------------------------- |
| /     | Contains the rest of the tree.                                                   |
| /boot | Contains data that is used before the kernel begins executing user-mode programs |
| /var  | Contains variable files                                                          |
| /tmp  | Contains temporary files                                                         |
| /home | Contains HOME users                                                              |

And what's LVM ? You can think of LVM as "dynamic partitions", meaning that you can create/resize/delete LVM "partitions" (they're called "Logical Volumes" in LVM-speak) from the command line while your Linux system is running: no need to reboot the system to make the kernel aware of the newly-created or resized partitions.





{% hint style="info" %}
The next steps are the most important parts of the project - if you understand what you are doing here, you will be fine with the evaluation.&#x20;
{% endhint %}

## Part 4, 5, 6 - Configurating your Virtual Machine

Now that you have installed your virtual machine, you have to fill it. Imagine that at this stage you just have an empty machine and you can't do anything. You have to add the tools you want to use.



### `apt` vs `aptitude`

You probably noticed that you used the command `apt` a lot during the configuration of your VM. Actually `aptitude` and `apt` are two of the popular tools which handle package management. In this project we used `apt` instead of `aptitude`. Even if they both offer the same basic functionality, installing and removing packages from the command-line, they have a little difference:

* `aptitude` remembers which packages were explicitly requested and which were only installed due to dependencies. It will automatically uninstall packages which were not explicitly requested when they are no longer needed.
* `apt` will only do explicitly what it is told to do in the command line



### APPArmor

Linux security system that provides Mandatory Access Control (MAC) security. Allows the system admin to restrict the actions that processes can perform. It is included by default with Debian.&#x20;

Run `aa-status` to check if it is running.



### Git & Vim

If you are doing this project, you already used git and vim in the past. You will install these tools on your VM to be able to use them.



### SSH (Secure Shell)

SSH stands for "Secure Shell", it is therefore a "shell" (or terminal) which is secure. A shell will allow you to administer your Linux servers, locally, that is to say when you are physically in front of your server, but also remotely! In particular thanks to Secure Shell (SSH).&#x20;

The use of the SSH protocol will allow you to connect remotely to your servers to manage them. For example, you can be in New York and manage your computer in Paris in a few clicks.



### UFW (Uncomplicated Firewall)

A firewall is an element of the computer network. Its role is to secure a network by defining the allowed or forbidden communications via rules. In other words it monitors incoming and outgoing network traffic and decides whether to block or allow traffic.&#x20;

In this project you will be asked to configure your operating system with the UFW firewall and leave only port 4242 open. You will need to set up a rule for this.



### Password Policy

A password policy is a set of rules designed to improve security by encouraging users to use relatively strong passwords and to use them correctly. For example, in this project, it is asked to implement a strong password policy (which expires every 30 days, must be longer than 10 words and not contain a logical sequence, must contain capital letters, special characters and numbers).

If your password can be guessed or easily hacked, it is likely to be vulnerable to hacking attempts and allows access to sensitive information.

{% hint style="danger" %}
Each user of your virtual machine will have to follow the following password rules:



* PASS\_MAX\_DAYS 30
* PASS\_MIN\_DAYS 2
* PASS\_WARN\_AGE 7



It is possible that your default user does not have these modifications, you will have to do it manually.

To see which password parameter is associated with a user, you can type this command:

`sudo chage -l username`\
\
if c does not correspond to the above figures, they must be changed manually as follows:

`sudo chage -M 30 <user>`\
`sudo chage -m 2 <user>`\
`sudo chage -W 7 <user>`
{% endhint %}



### Groups and users

Linux uses groups as a way to organize users. They exist to make permissioning of files and folders simpler. Linux was designed to allow more than one user to have access to the system at the same time but with different permissions.

#### Root

`root` is the super user and has the ability to do anything on a system. Therefore, in order to have an additional layer of security, a `sudo` user is generally used in place of root.&#x20;

#### Sudo

You will need to install sudo. Sudo stands for "superuser do". In a few words `sudo` gives the designated user a super power. A power to act as an administrator temporarily. `sudo` is used to give another user limited access to another user’s account for the purpose of performing tasks. `sudo` enables a user to have administration privileges without logging in directly as root.

This management of the rights given to users is contained in the file `/etc/sudoers`



### Crontab

Cron is a program that allows users of Unix systems to automatically execute scripts, commands or software at a pre-specified date and time, or on a pre-defined cycle.

In this project you will have to post a message every 10 minutes. You will need cron in order to do it. Here is how it works:

1. You create a script (in our case it will be the monitoring script containing all the information) that you want to run using cron.
2. you type then `sudo crontab -u root -e` to open crontab and add a rule
3. The rule should be written like that:&#x20;

`* * * * * <path>/<name_of_the_program_to_be_executed>`

Where `* * * * *` means every minute of every hour of every day of every month and every day of the week. Let's take some examples:

`0 * * * *` -this means the cron will run always when the minutes are `0` (so hourly)\
`0 1 * * *` - this means the cron will run always at 1 o'clock.\
`* 1 * * *` - this means the cron will run each minute when the hour is 1. So `1:00`, `1:01`, ...`1:59`\
`*/10 * * * *` - means the cron will run each ten minutes.&#x20;



## Part 7 - Signature.txt&#x20;

A signature is a unique, identifying number for a hard disk drive or other data storage device. An operating system uses it to differentiate among storage devices on your computer.

