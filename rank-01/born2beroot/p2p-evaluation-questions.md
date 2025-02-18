# 📠 P2P Evaluation - Questions

{% hint style="danger" %}
Be careful, the first check that the student is going to do is checking that in your git repo there is only the signature of your virtual machine and NOTHING else. The signature must be identical as the one on your VM at the time of the evaluation (if you change something on your VM afterwards, the signature will be different).
{% endhint %}



## Theoretical questions

Here are the **theoretical questions** you will be asked during the evaluation:

* How does a virtual machine work ? And what its purpose ?
* Wh did you choose Debian or CentOS ?
* What's the difference between Debian and CentOS ?
  * If you chose Debian: what's the difference between aptitude, apt and what's APPArmor ?
  * If you chose CentOS: what's SELinux and DNF ?
* What the advantages/disadvantages of a strong password policy ? What can you say about its implementation ?
* What's a partition ? And more generally how does LVM (Logical Volume Management) work ?
* What's sudo ?&#x20;
* What's an UFW and what's the value of using it ?
* What's SSH (Secure Shell) and what's the value of using it ?
* What is cron ?

Everything (and even more than necessary) is explained here:

{% content-ref url="whats-a-virtual-machine.md" %}
[whats-a-virtual-machine.md](whats-a-virtual-machine.md)
{% endcontent-ref %}

{% content-ref url="install-your-virtual-machine.md" %}
[install-your-virtual-machine.md](install-your-virtual-machine.md)
{% endcontent-ref %}





## Practical questions

And here are the **practical questions** that you will be asked to demonstrate and the command that you need to write to get to the answer:

* Check that the signature contained is identical to that of the ".vdi" file of the virtual machine to be evaluated.&#x20;
  1. Open iTerm and type `cd`
  2. Then type `cd sgoinfre/students/<your_intra_username>/<file of your VM>`
  3. Then type `shasum VirtualBox.vdi` (or any other name that your VM has .vdi)
* During the evaluation a script must display information every 10 minutes

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption><p>Script that should appear every 10 minutes</p></figcaption></figure>

* The machine should not have a graphical environment at launch.
* A password is requested before attempting to connect to this machine.
* You need to connect with an user. The user must not be root.
* Check that the UFW service is started
  * `sudo ufw status`
* Check that the SSH service is started
  * `sudo systemctl status ssh`

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>you will find the status of the ssh service</p></figcaption></figure>

* Check that the operating system is Debian or CentOS (you can check it on the information script that is displayed every 10 minutes)
*   Check that a user with your login exists and is present on your VM. This user should belong to the groups "sudo" and "user42".

    * `getent group sudo`
    * `getent group user42`



    <figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
*   Make sure that the rules imposed in the subject concerning the password policy have been put in place by following these steps:

    * Create a new user for the evaluator: `sudo adduser <new_username>`
    * He/She chooses a password
    * Create a new group named "evaluating": `sudo groupadd <groupname>`
    * Assign it to your new user (the evaluator's user): `sudo usermod -aG <groupname> <username>`
    * Check the password expire rules: `sudo chage -l username`



    <figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption><p>your password rules should look like this</p></figcaption></figure>
* Check that this new user belongs to the "evaluating" group: `getent group evaluating`
* Check that the hostname of the machine is correctly formatted as follows: login42
  * `hostnamectl`
* Modify this hostname by replacing the login with yours, then restart the machine (the new host name should be updated)
  * `hostnamectl set-hostname <new_hostname>`
  * change the hostname in this file too: `sudo nano /etc/hosts`
  * Restart your virtual machine
* Restore the machine to the original name (just do the same thing as above)
* Check the partitions for your VM (compare the output with the example in the subject).
  * `lsblk`
* Check that the sudo program is properly installed on the virtual machine
  * `dpkg -l | grep sudo –`
* Assign the evaluator's username to the "sudo" group
  * `sudo usermod -aG <groupname> <username>`
* Verify that the " /var/log/sudo/" folder exists and hast at least one file.
  * `cd /var/log/sudo/`
* Check the contents of the files in this folder. You should see a history of the command used with sudo.
  * `ls` to check what contains this folder
  * `cat sudo.log` (this file is the file with the history of sudo commands)
* Try to run a command via sudo and see if the files above have been updated
  * write whatever you want (i.e. sudo ls) and check if the new log has been added to the history by reading the file again (`cat sudo.log`)
* Check that the UFW program is installed on your VM and that is working properly
  * `dpkg -l | grep ufw –`
*   List the active rule in UFW. A rule must exist for port 4242.&#x20;

    * `sudo ufw status numbered`

    <figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>
* Add a new rule to open port 8080
  * `sudo ufw allow 8080`
* Check that it has been added to the active rules
  * `sudo ufw status numbered`
* Delete this new added rule.
  * `sudo ufw delete <rule_number>` (mine is 2 and then i do it again with 3)
* Check that the SSH service is installed and working on your virtual machine
  * `dpkg -l | grep ssh –`
* Verify that the SSH service only uses port 4242
  * Open your iTerm
  * write: `ssh your_user_id@127.0.0.1 -p 4242`
  * You are now connected on your VM through your terminall
* Make sure that you cannot user SSH with the "root" user
* Open your information script (the one that appears every 10 minutes) and explain it
  * if you followed the same github guide as me just type: `cd /usr/local/bin/`
  * and then: `cat monitoring.sh`&#x20;

<details>

<summary>Explanation for monitoring.sh</summary>

<pre class="language-bash"><code class="lang-bash">#!/bin/bash #>> you are telling your environment/ os to use bash as a command interpreter
arc=$(uname -a) #uname displays information about the system and -a means all information


#grep or "global regular expression print” is a command used in searching 
#and matching text files contained in the regular expressions

#awk is a kind of super command with which you can do many things
<strong>#for example awk '{ print $2; }' prints the second field of each line
</strong>
#The /proc/cpuinfo command provides information about 
pcpu=$(grep "physical id" /proc/cpuinfo | sort | uniq | wc -l) 

vcpu=$(grep "^processor" /proc/cpuinfo | wc -l) #Provides each processor with an identifying number.
						#If you have one processor it will display a 0. 
						#If you have more than one processor it will display 
						#all processor information separately counting the processors
						#using zero notation.

#The free command provides information about the total amount of the physical and 
#swap memory, as well as the free and used memory
# -m displays the amount of memory in mebibytes
fram=$(free -m | awk '$1 == "Mem:" {print $2}') #Display the free/unused memory

uram=$(free -m | awk '$1 == "Mem:" {print $3}') #Diplay the used memory

pram=$(free | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}') #Display the usage rate as a percentage


#The df command (short for disk free), is used to display information related to
# file systems about total space and available space.
fdisk=$(df -BG | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $2} END {print ft}')

udisk=$(df -BM | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}')

pdisk=$(df -BM | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} {ft+= $2} END {printf("%d"), ut/ft*100}')


cpul=$(top -bn1 | grep '^%Cpu' | cut -c 9- | xargs | awk '{printf("%.1f%%"), $1 + $3}')


lb=$(who -b | awk '$1 == "system" {print $3 " " $4}')


#here the goal is to know if your VM has dynamic partitions.
#so if you have more than 0 partitions when you type the lsblk command
#then you can display "yes
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -eq 0 ]; then echo no; else echo yes; fi)

ctcp=$(ss -neopt state established | wc -l)

ulog=$(users | wc -w)

#hostname command displays the system hostname
ip=$(hostname -I) # -I is used to get all IP(network) addresses

mac=$(ip link show | grep "ether" | awk '{print $2}')

cmds=$(journalctl _COMM=sudo | grep COMMAND | wc -l)

#here you will call all the variables that you created above
#and display eveything in an aesthetic way
wall "	#Architecture: $arc
	#CPU physical: $pcpu
	#vCPU: $vcpu
	#Memory Usage: $uram/${fram}MB ($pram%)
	#Disk Usage: $udisk/${fdisk}Gb ($pdisk%)
	#CPU load: $cpul
	#Last boot: $lb
	#LVM use: $lvmu
	#Connections TCP: $ctcp ESTABLISHED
	#User log: $ulog
	#Network: IP $ip ($mac)
	#Sudo: $cmds cmd"
</code></pre>

</details>

* Change the cron and to make sure that your informative script appears now every minute
  * Type `sudo crontab -u root -e` to open the crontab and add the rule
  * New rule: `*/1 * * * *`
  * Restart the server one last time



Okay... now you're ready to present your project :-) Good luck !
