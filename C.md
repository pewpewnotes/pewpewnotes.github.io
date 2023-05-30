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
***
### == Example of Strsep and Token pointers ==

```
Something that I really use a lot is .split in python, and found a very nice equivalent in C
```

```C
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int compare(const void * elem1, const void * elem2) {
    int f = *((int *) elem1);
    int s = *((int *) elem2);
    if (f >= s) {
        return 1;
    } else {
        return -1;
    }
    return 0;
}

int main() {
    char s[100];
    int a[100];
    scanf("%s",s);
    int i, j = 1;
    a[0] = s[0];
    char *token;
    char *r = strdup(s);
    for (i = 1; ; i++){
        token = strsep(&r, "+");
            if (token == NULL){
                break;
            }
        printf("%d: %s\n",i, token);
        a[j] = (int) (*token) - '0';
        printf("> %d\n", a[j]);
        j++;
    }
    // Onwards from here is not working. Please ignore
    a[(strlen(s)+1)/2];
    qsort (a, sizeof(a)/sizeof(*a), sizeof(*a), compare);
    for (i = 0; i < ((strlen(s)+1)/2); i++) {
        printf("%d ",a[i]);
    }
    return 0;
}
```
***
### == Take space Separated input in C ==
```C
 cat problem.c                                                                                                              
───────┬─────────────────────────────────────────────────────────────────┬
       │ File: problem.c                                                 │
───────┼─────────────────────────────────────────────────────────────────┼
   1   │ #include <stdio.h>                                              │
   2   │ int main() {                                                    │
   3   │     int n,k,i=0, count = 0;                                     │
   4   │     int scores[100];                                            │
   5   │     scanf("%d %d", &n, &k);                                     │
   6   │     do {                                                        │
   7   │         scanf("%d", &scores[i++]);                              │
   8   │     } while (getchar() != '\n' && i < n);                       │
   9   │     scores[n];                                                  │
  10   │     for (i=0;i < n;i++) {                                       │
  11   │         if (scores[i] >= scores[k-1] && scores[i] > 0) {        │
  12   │             count += 1;                                         │
  13   │         }                                                       │
  14   │     }                                                           │
  15   │     printf("%d", count);                                        │
  16   │     return 0;                                                   │
  17   │ }                                                               │
  18   │                                                                 │
───────┴─────────────────────────────────────────────────────────────────┴

```

***
### === Minimum of Three Numbers in C ===
```
int max = n1 > n2 ? (n1 > n3 ? n1 : n3) : (n2 >n3 ? n2 : n3)
```
### === GCD ===
```C
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
     
}
```
### === Reduce Fractions === 
```C
void reduceFraction(int x, int y)
{
    int d;
    d = __gcd(x, y);
 
    x = x / d;
    y = y / d;
 
    cout << "x = " << x << ", y = " << y << endl;
}

```
