# ◾ Building the thing

Push\_swap is not a very difficult project in terms of code construction. You will see that it doesn't need many steps to finish it. The hardest part is to find a solution to the problem and to to construct its algorithm.&#x20;

As usual, in this page I will make checklists for you to succeed push swap at best

### Main Checklist

* [ ] Decide if you are going to do your project using chained lists or using tables
* [ ] Handle the arguments you are given in input
* [ ] (If you choose radix sort, normalize your data ! )

### Error Checklist

There are a lot of errors to handle in push\_swap. Don't forget any of them!

* [ ] **The program must work with several numerical arguments**
  * [ ] ./push\_swap 1 3 5 +9 20 -4 50 60 04 08
* [ ] **The program also works if you receive a single character list as a parameter**
  * [ ] ./push\_swap "3 4 6 8 9 74 -56 +495"
* [ ] **The program should NOT work if it encounters another character**
  * [ ] ./push\_swap 1 3 dog 35 80 -3
  * [ ] ./push\_swap a
  * [ ] ./push\_swap 1 2 3 5 67b778 947
  * [ ] .push\_swap " 12 4 6 8 54fhd 4354"
  * [ ] ./push\_swap 1 --    45 32
    * [ ] these examples should return "Error\n"
* [ ] **The program should NOT work if it encounters a double number**
  * [ ] ./push\_swap 1 3 58 9 3
  * [ ] ./push\_swap 3 03
  * [ ] ./push\_swap " 49 128     50 38   49"
    * [ ] these examples should return "Error\n"
  * [ ] ./push\_swap "95 99 -9 10 9"
    * [ ] this example should work because -9 & 9 are not equal
* [ ] **The program should work with INT MAX & INT MIN**
  * [ ] ./push\_swap 2147483647 2 4 7
  * [ ] ./push\_swap 99 -2147483648 23 545
  * [ ] ./push\_swap "2147483647 843 56544 24394"
    * [ ] these examples should work and sort your list
  * [ ] ./push\_swap 54867543867438 3
  * [ ] ./push\_swap -2147483647765 4 5
  * [ ] ./push\_swap "214748364748385 28 47 29"
    * [ ] these examples should return "Error\n"
* [ ] **Nothing has been specified when strings and int are mixed.** It's up to you what you want to do
  * [ ] ./push\_swap "1 2 4 3" 76 90 "348 05

### Instructions Checklist

This checklist will help you to verify that you have coded all the instructions (11) to use them in your algorithms (next step). If you don't understand what these functions do you can check the [main page of push\_swap](./) where you will be given a better explanation

* [ ] **sa (swap a)**: If there are 2 numbers, swap the first 2 elements at the top of the stack a.
* [ ] **sb (swap b )** :  If there are 2 numbers, swap the first 2 elements at the top of the stack b.
* [ ] **ss** : sa and sb at the same time.&#x20;
* [ ] **pa (push a)**: If b is not empty it takes the first element on top of b and puts it on a.
* [ ] **pb (push b)**: If a is not empty, it takes the first element on top of a and puts it on b.
* [ ] **ra (rotate a)**: Shifts all the elements of the stack a up by one position. The first element becomes the last.&#x20;
* [ ] **rb (rotate b)** : Shifts all the elements of the stack b one position upwards. The first element becomes the last one.&#x20;
* [ ] **rr** : ra and rb at the same time.&#x20;
* [ ] **rra (reverse rotate a)**: Shifts all elements of the stack down one position. the stack a. The last element becomes the first.&#x20;
* [ ] **rrb (reverse rotate b)**: Shifts all the elements of the stack b one position downwards. the stack b. The last element becomes the first.&#x20;
* [ ] **rrr** : rra and rrb at the same time

### Algorithm/Sort Checklist

* [ ] Check if the order of the list is correct or if it should be sorted
* [ ] Make a small algorithm for small numbers (5 and less)
  * [ ] Implement a condition for 2 numbers
  * [ ] Create an algorithm for 3 numbers
  * [ ] Create an algorithm for 4 numbers
  * [ ] Create an algorithm for 5 numbers
* [ ] Create another algorithm for all other numbers

And obviously at the end check if everything is correct ! **No leaks should be present**, remember to always free the allocated memory when you are not using it anymore.

And that's it... Good luck with the code! If you have any other questions don't hesitate to contact me (Laura), and I'll be happy to help you :)
