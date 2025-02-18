# Level 1 & 2

Let's go level by level and try to ask ourselves the right questions to solve each exercise.

PS: Don't check the answers immediately. Otherwise you will not learn anything and you'll have a hard time during your evaluation



## 0.1 How to find the IP _(from one mask & one IP)_&#x20;

Find the IP of one machine (Interface 2) using its mask and the IP of the other machine (Interface 1).

* Convert the IP address and subnet mask to binary.

Interface 1 IP address:   192.168.25.222 -> 11000000.10101000.00011001.11011110 \
Interface 2 subnet mask:    255.255.255.224 -> 11111111.11111111.11111111.11100000

* Perform the bitwise "AND" operation between each corresponding bit of the IP address and the subnet mask.&#x20;

11000000.10101000.00011001.11011110 \
11111111.11111111.11111111.11100000 \
\
\= 11000000.10101000.00011001.11000000

* Convert the binary result back to decimal notation.

\--> Thus, the IP address of interface 2 could be 192.168.25.192, assuming the provided subnet mask is applicable to the network configuration in this specific context.



Now, regarding the address range, with a subnet mask of 255.255.255.224 (or /27), [**the available address range is 30 addresses**](https://42-cursus.gitbook.io/guide/rank-04/netpractice/tcp-ic-and-masks#masks-subnet-masks). In this case, the address range would be 192.168.25.192 to 192.168.25.223.

It's important to note that every IP address in this range is considered valid for interface 2, as long as it's not already in use by another interface or device on the network.

So, if you mark the response 192.168.25.194, this would also be a valid IP address for interface 2, as it's within the range of addresses available with the given subnet mask.





## 0.2 How to find a subnet mask (from one IP and one mask)

To find the subnet mask of interface 2 from the IP address of interface 1 and the IP address of interface 2, you can follow these steps:

* Convert both IP addresses to binary.

Interface 1 IP address: 192.168.25.222 -> 11000000.10101000.00011001.11011110 \
Interface 2 IP address: 192.168.25.192 -> 11000000.10101000.00011001.11000000

* Compare the bits of the IP address of interface 1 and the IP address of interface 2

IF1: 11000000.10101000.00011001.11011110 \
IF2: 11000000.10101000.00011001.11000000&#x20;

Start with the most significant bit (from left to right) and compare each corresponding bit of the two IP addresses. Find the first instance where the bits differ between the two IP addresses.

From this point onwards, all subsequent bits must be set to 0 in the subnet mask.

\= 11111111.11111111.11111111.00000000

In this case, the longest sequence of consecutive 1 bits is "24 bits".&#x20;

* Convert this sequence of bits to decimal notation.

Interface 2 subnet mask: 255.255.255.0

Thus, the subnet mask of interface 2 would be 255.255.255.0, assuming the provided IP addresses correspond to a valid network configuration in this specific context.





Let's put what we've just learned into practice :)



## Level 1 : Simple case

The aim is to connect one computer with another, twice.

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption><p>NetPractice : Level 1</p></figcaption></figure>

Here we have two separate networks, each consisting of two computers. Try to find their IP using the first method that I told you.&#x20;

To find the IP address of interface A1, you need to use the mask of A1 and the IP address of B1.



## Level 2 : Masks are a bit modified

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption><p>Level 1 Example</p></figcaption></figure>

Here we have two separate networks, each consisting of two computers.

