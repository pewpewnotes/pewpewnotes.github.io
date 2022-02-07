```
 _     _                    ____        _                  _       
| |   (_)_ __  _   ___  __ / ___| _ __ (_)_ __  _ __   ___| |_ ___ 
| |   | | '_ \| | | \ \/ / \___ \| '_ \| | '_ \| '_ \ / _ \ __/ __|
| |___| | | | | |_| |>  <   ___) | | | | | |_) | |_) |  __/ |_\__ \
|_____|_|_| |_|\__,_/_/\_\ |____/|_| |_|_| .__/| .__/ \___|\__|___/
                                         |_|   |_|                 
```

### Process Management
* VSZ (virtual set size) shows the size of the image process (in kilobytes), and RSS (resident 
set size) shows the size of the program in memory. The VSZ and RSS sizes may be differ-
ent because VSZ is the amount of memory allocated for the process, whereas RSS is the 
amount that is actually being used. RSS memory represents physical memory that cannot 
be swapped.
* START shows the time the process began running, and TIME shows the cumulative 
system time used. (Many commands consume very little CPU time, as reflected by 0:00 for 
processes that haven’t even used a whole second of CPU time.)
Many processes running on a computer are not associated with a terminal. A normal Linux 
system has many processes running in the background. Background system processes per-
form such tasks as logging system activity or listening for data coming in from the net-
work. They are often started when Linux boots up and run continuously until the system 
shuts down. Likewise, logging into a Linux desktop causes many background processes to 
kick off, such as processes for managing audio, desktop panels, authentication, and other 
desktop features.

```Source: Linux Bible Christopher Negus 10th Ed.```
