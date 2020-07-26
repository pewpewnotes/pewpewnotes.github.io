# Bit Arithmetic Programs 

This is basically a file made alongside programs_list.md to explain (or precisely make an attempt) the logic behind the programs.

1. Finding whether a number is power of two or not.

So, first of all lets observer few powers of two.

2 -> 10
4 -> 100
8 -> 1000
16 -> 10000
.
.
.

Basically we can see that the rightmost digit is always 0, meaning from a number, if the unit digit is removed and operation and is operated from same number we should get 0. 
For our example lets take 9
9 -> 1001
8 -> 1000

here, upon &ing the numbers, we will get 8. Now lets take 8 as an example

8 -> 1000
7 -> 0111

upon anding we will obtain 0
This is a common case with every number that is power of two. So to check whether a number is power of two or not,
all we need to do is evaluate x&(x-1)

Furthermore, x-1 basically sets the leftmost bit to 0, if its power of two and we know that the rest of the bits in x are already 0, meaning we will get 0 upon anding.

By a very similar logic, you can turn all one's by oring with x+1
x = 2 -> 10
x + 1 = 3 -> 11
x|(x+1) -> 11
which is setting up all the bits to be precise. 

