```

  ____                 _        ____        _                  _       
 / ___|   ___ ___   __| | ___  / ___| _ __ (_)_ __  _ __   ___| |_ ___ 
| |      / __/ _ \ / _` |/ _ \ \___ \| '_ \| | '_ \| '_ \ / _ \ __/ __|
| |___  | (_| (_) | (_| |  __/  ___) | | | | | |_) | |_) |  __/ |_\__ \
 \____|  \___\___/ \__,_|\___| |____/|_| |_|_| .__/| .__/ \___|\__|___/
                                             |_|   |_|                 

```
***
### == Function to count Set bits in an Integer ==
```c
unsigned int countSetBits(int n) 
{ 
    unsigned int count = 0; 
    while (n) { 
        n &= (n - 1); 
        count++; 
    } 
    return count; 
} 
```
***
### == Function to find even or odd ==
```c
bool isEven(int n)  
{  
    // n&1 is 1, then odd, else even  
    return (!(n & 1));  
}
```
***
### == Abrupt behaviour of Scanf ==
```text
The %c conversion specifier won't automatically skip any leading whitespace,
so if there's a stray newline in the input stream (from a previous entry,
for example) the scanf call will consume it immediately.

One way around the problem is to put a blank space before the conversion specifier in the format string:

scanf(" %c", &c);
The blank in the format string tells scanf to skip leading whitespace,
and the first non-whitespace character will be read with the %c conversion specifier.
```
