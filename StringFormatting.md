```text 
 ____  _        _             
/ ___|| |_ _ __(_)_ __   __ _ 
\___ \| __| '__| | '_ \ / _` |
 ___) | |_| |  | | | | | (_| |
|____/ \__|_|  |_|_| |_|\__, |
                        |___/ 
  __                            _   _   _             
 / _| ___  _ __ _ __ ___   __ _| |_| |_(_)_ __   __ _ 
| |_ / _ \| '__| '_ ` _ \ / _` | __| __| | '_ \ / _` |
|  _| (_) | |  | | | | | | (_| | |_| |_| | | | | (_| |
|_|  \___/|_|  |_| |_| |_|\__,_|\__|\__|_|_| |_|\__, |
                                                |___/ 
```

How does this work? Well we need to discuss some of the basic text formatting 
control sequences. These control the style of the text, which includes properties such 
as emboldening text, underlining, and inverting the terminal printing. The control 
sequences are as follows:
`  \e[ABm --> A decides the pattern, B decides the color.`

* `\e[1m` BOLD`\e[0m`
* `\e[2m` DIM `\e[0m`
* `\e[3m` ITALICS `\e[0m`
* `\e[4m` UNDERLINE `\e[0m`
* `\e[5m` BLINK `\e[0m`
* `\e[6m` BLINK `\e[0m`
* `\e[7m` INVERT `\e[0m`
* `\e[8m` HIDES `\e[0m`
* `\e[21m` HIDES BOLD `\e[0m` `Simply prepend with 2 to escape the effect`
* `\e[1m` TEXT `\e[0m`
* `\e[1m` TEXT `\e[0m`
* `\e[1m` TEXT `\e[0m`
* `\e[1m` TEXT `\e[0m`
* `\e[1m` TEXT `\e[0m`

Colors: 
* 0 Black
* 1 Red
* 2 Green
* 3 Yellow
* 4 Blue
* 5 Magenta
* 6 Cyan
* 7 Light Gray

A quick code to demonstrate most of these things:
```
for i in {1..8}; do echo -ne "\e[${i}m >>TEXT<< \e[0m \n"; done

```

![Image File](https://i.imgur.com/p23MCZ3.png)


Important extracts: 

```text
yet, because for most cases you probably will never make use of this.
The \[\033[01;32m\] part,
as discussed in the previous section, causes the terminal 
to print bold green text.
The format here is slightly different from the examples 
discussed in the previous section, 
because escaped brackets are used to demarcate 
the beginning and end of the control sequences. 
As we've seen in previous examples, these are not a hard requirement for later bash shell versions.
The \u part is another one of those really useful escape characters. This one acts asa
shorthand for your username or the username of current user.
The \h part this escape character follows the @ sign in this example—the @ sign is just 
plain text, nothing special about it. The \h escape character will print your current 
hostname in its place when the prompt string is displayed.
The \[\033[00m\] part as discussed in the previous section. This will reset all the 
formatting rules so that everything following it is printed as normal text. After 
resetting the formatting, we see \[\033[01;34m\]. This will format all the text that 
precedes it so that it appears emboldened in blue.
The \w part is a shorthand for the current working directory. Directly after the 
working directory is a good old line feed that is printed by using the \n escape 
character shorthand. Following this is the\$ escape character, which is a shorthand 
that will print a $ sign if anything besides the root user is currently using the shell 
and a # when the root user is logged in.
The bash shell offers a few other useful shorthands to make use of in your prompt 
string, each causing a different piece of information to be printed directly into your
```
