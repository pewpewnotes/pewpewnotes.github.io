```



```


### C++ studies
***

* {} Method of initialization allows to zero initialize the variables in C++
* std::endl flushes all of the content of buffer to stdout before returning to the new line.
* learncpp suggests to use '\n'
* Notice, single quotes.

### Summaries
***
* Chapter 1: [Summary](Summary_chapter1.md)
* Chapter 2:


```
# Chapter 1.5 Summary

std::cin and std::cout always go on the left-hand side of the statement.
std::cout is used to output a value (cout = character output)
std::cin is used to get an input value (cin = character input)
<< is used with std::cout, and shows the direction that data is moving (if std::cout represents the console, the output data is moving from the variable to the console). std::cout << 4 moves the value of 4 to the console
>> is used with std::cin, and shows the direction that data is moving (if std::cin represents the keyboard, the input data is moving from the keyboard to the variable). std::cin >> x moves the value the user entered from the keyboard into x

```

Example Code:

```
#include <iostream>

int main() {
    std::cout << "Enter two numbers separated by space: ";

    int x{};
    int y{}; 
    // remember {} -> zero initialize a variable.

    std::cin >> x >> y;
    std::cout << "Entered: " << x << y << '\n';
    return 0;
}
```
