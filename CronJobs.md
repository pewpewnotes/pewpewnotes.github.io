```
  ____                  _       _     
 / ___|_ __ ___  _ __  (_) ___ | |__  
| |   | '__/ _ \| '_ \ | |/ _ \| '_ \ 
| |___| | | (_) | | | || | (_) | |_) |
 \____|_|  \___/|_| |_|/ |\___/|_.__/ 
                     |__/             
```

This is basically the header format for cron jobs, this will come in handy later on. 

```
#
# Crontab file
# Field 1   2    3            4              5             6
#      Min Hour Day of month Month of year  Day of week
#     0-59 0-23 1-31         1-12           0-6   0=Sun /path/command
#
# Days of the week: 0=Sun 1=Mon 2=Tues 3=Wed 4=Thu 5=Fri 6=Sat
```

```
Shortcuts for command |   Command     |   Output
----------------------|---------------|----------------------
@reboot               |               | Run once after reboot
@yearly or @annually  | 0  0  1  1  * | 1st day of the month on the, 1st day of the year
@monthly              | 0  0  1  *  * | 1st day of the month
@weekly               | 0  0  *  *  0 | Run on Sunday at 12:00 am
@daily                | 0  0  *  *  * | Run every day at 12:00 am
@hourly               | 0  *  *  *  * | Run every hour on the hour

```

You can also monitor the /var/log/cron file to see what cron is doing on the system 
throughout the day. This is very helpful when first creating a crontab file and trying
