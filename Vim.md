### How to add permanent line numbers to a file?

#### In pure Vim fashion:

```
:%s/^/\=line('.').". "
```

Explanation:
```
:%s/^/            " the substitution will be applied to the beginning of every line
\=                " the rest of the replacement part is an expression
line('.').". "    " the expression returns the current line n
```


I think the chosen answer is the best, but in the sprit of variety, I'll offer an alternative using an external program:

```
:%!cat -n
```

This will filter your entire buffer (as denoted by %) through the external program, cat, where the -n flag prepends each line of input with a line number.

This, of course, requires that you have cat installed, which is true for (probably) all Unix-like systems.

Check out :help :range! for more details on filtering through external programs.

### Inserting current date and time

`:pu=strftime('%c')`

Vim's internal strftime() function (:help strftime()) returns a date/time string formatted in a way you specify with a format string. Most systems support strftime(), but some don't.

or using external program 
`:r !date` 

### Switch Case

```
You can change the case of text:

Toggle case "HellO" to "hELLo" with g~ then a movement.
Uppercase "HellO" to "HELLO" with gU then a movement.
Lowercase "HellO" to "hello" with gu then a movement.
Alternatively, you can visually select text then press ~ to toggle case, or U to convert to uppercase, or u to convert to lowercase.
```

### Join a vertical line

```
An easy one. Use a range from first line until last one and join them with an space between them:

:0,$join

answered Feb 18 2015 at 12:38

Birei
Or even shorter :%j
```
