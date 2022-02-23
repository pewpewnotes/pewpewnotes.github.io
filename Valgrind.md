```


__     __    _            _           _ 
\ \   / /_ _| | __ _ _ __(_)_ __   __| |
 \ \ / / _` | |/ _` | '__| | '_ \ / _` |
  \ V / (_| | | (_| | |  | | | | | (_| |
   \_/ \__,_|_|\__, |_|  |_|_| |_|\__,_|
               |___/                    
```


Valgrind Home	Information Source Code Documentation Contact How to Help Gallery
| Table of Contents | Quick Start | FAQ | User Manual | Download Manual | Research Papers | Books |
Prev	Up	Up	The Valgrind Quick Start Guide	Next
The Valgrind Quick Start Guide
1. Introduction
The Valgrind tool suite provides a number of debugging and profiling tools that help you make your programs faster and more correct. The most popular of these tools is called Memcheck. It can detect many memory-related errors that are common in C and C++ programs and that can lead to crashes and unpredictable behaviour.

The rest of this guide gives the minimum information you need to start detecting memory errors in your program with Memcheck. For full documentation of Memcheck and the other tools, please read the User Manual.

2. Preparing your program
Compile your program with -g to include debugging information so that Memcheck's error messages include exact line numbers. Using -O0 is also a good idea, if you can tolerate the slowdown. With -O1 line numbers in error messages can be inaccurate, although generally speaking running Memcheck on code compiled at -O1 works fairly well, and the speed improvement compared to running -O0 is quite significant. Use of -O2 and above is not recommended as Memcheck occasionally reports uninitialised-value errors which don't really exist.

3. Running your program under Memcheck
If you normally run your program like this:

  myprog arg1 arg2
Use this command line:

  valgrind --leak-check=yes myprog arg1 arg2
Memcheck is the default tool. The --leak-check option turns on the detailed memory leak detector.

Your program will run much slower (eg. 20 to 30 times) than normal, and use a lot more memory. Memcheck will issue messages about memory errors and leaks that it detects.

4. Interpreting Memcheck's output
Here's an example C program, in a file called a.c, with a memory error and a memory leak.

  #include <stdlib.h>

  void f(void)
  {
     int* x = malloc(10 * sizeof(int));
     x[10] = 0;        // problem 1: heap block overrun
  }                    // problem 2: memory leak -- x not freed

  int main(void)
  {
     f();
     return 0;
  }
Most error messages look like the following, which describes problem 1, the heap block overrun:

  ==19182== Invalid write of size 4
  ==19182==    at 0x804838F: f (example.c:6)
  ==19182==    by 0x80483AB: main (example.c:11)
  ==19182==  Address 0x1BA45050 is 0 bytes after a block of size 40 alloc'd
  ==19182==    at 0x1B8FF5CD: malloc (vg_replace_malloc.c:130)
  ==19182==    by 0x8048385: f (example.c:5)
  ==19182==    by 0x80483AB: main (example.c:11)
Things to notice:

There is a lot of information in each error message; read it carefully.

The 19182 is the process ID; it's usually unimportant.

The first line ("Invalid write...") tells you what kind of error it is. Here, the program wrote to some memory it should not have due to a heap block overrun.

Below the first line is a stack trace telling you where the problem occurred. Stack traces can get quite large, and be confusing, especially if you are using the C++ STL. Reading them from the bottom up can help. If the stack trace is not big enough, use the --num-callers option to make it bigger.

The code addresses (eg. 0x804838F) are usually unimportant, but occasionally crucial for tracking down weirder bugs.

Some error messages have a second component which describes the memory address involved. This one shows that the written memory is just past the end of a block allocated with malloc() on line 5 of example.c.

It's worth fixing errors in the order they are reported, as later errors can be caused by earlier errors. Failing to do this is a common cause of difficulty with Memcheck.

Memory leak messages look like this:

  ==19182== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
  ==19182==    at 0x1B8FF5CD: malloc (vg_replace_malloc.c:130)
  ==19182==    by 0x8048385: f (a.c:5)
  ==19182==    by 0x80483AB: main (a.c:11)
The stack trace tells you where the leaked memory was allocated. Memcheck cannot tell you why the memory leaked, unfortunately. (Ignore the "vg_replace_malloc.c", that's an implementation detail.)

There are several kinds of leaks; the two most important categories are:

"definitely lost": your program is leaking memory -- fix it!

"probably lost": your program is leaking memory, unless you're doing funny things with pointers (such as moving them to point to the middle of a heap block).

Memcheck also reports uses of uninitialised values, most commonly with the message "Conditional jump or move depends on uninitialised value(s)". It can be difficult to determine the root cause of these errors. Try using the --track-origins=yes to get extra information. This makes Memcheck run slower, but the extra information you get often saves a lot of time figuring out where the uninitialised values are coming from.

If you don't understand an error message, please consult Explanation of error messages from Memcheck in the Valgrind User Manual which has examples of all the error messages Memcheck produces.

5. Caveats
Memcheck is not perfect; it occasionally produces false positives, and there are mechanisms for suppressing these (see Suppressing errors in the Valgrind User Manual). However, it is typically right 99% of the time, so you should be wary of ignoring its error messages. After all, you wouldn't ignore warning messages produced by a compiler, right? The suppression mechanism is also useful if Memcheck is reporting errors in library code that you cannot change. The default suppression set hides a lot of these, but you may come across more.

Memcheck cannot detect every memory error your program has. For example, it can't detect out-of-range reads or writes to arrays that are allocated statically or on the stack. But it should detect many errors that could crash your program (eg. cause a segmentation fault).

Try to make your program so clean that Memcheck reports no errors. Once you achieve this state, it is much easier to see when changes to the program cause Memcheck to report new errors. Experience from several years of Memcheck use shows that it is possible to make even huge programs run Memcheck-clean. For example, large parts of KDE, OpenOffice.org and Firefox are Memcheck-clean, or very close to it.

6. More information
Please consult the Valgrind FAQ and the Valgrind User Manual, which have much more information. Note that the other tools in the Valgrind distribution can be invoked with the --tool option.


<< The Valgrind Quick Start Guide 	Up	 Valgrind User Manual >>
Home

Bad, Bad Bug!
Copyright © 2000-2021 Valgrind™ Developers

Hosting kindly provided by sourceware.org
Best Viewed With A(ny) Browser


