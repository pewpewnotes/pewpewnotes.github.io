### == Tricks ==

* Changing deafult applications in ubuntu
 For torrent :  gio mime x-scheme-handler/magnet qbittorrent.desktop
* For always playing amv in small window mpv --geometry=422x240 Amv &
* So as to find all the open ports just run `netstat -lntup` ofcourse, 
  you can grep it
* `tree -f | grep "file_name_pewpew"` is a really fast way to search for a file,
with some tests I have found that this is actually faster than 
`find -type f -name ""`
* To use certain commands without sudo and password
```
Cmnd_Alias PASSWORDLESS = /usr/bin/systemctl restart network manager
yourusername ALL=(ALL) ALL
yourusername ALL=(ALL) NOPASSWD: PASSWORDLESS

```
* gopherpedia is wikipedia using gopher protocol, which is very cool! gopher://gopherpedia.com/
* To make get post put requests like inside a shell, you can use http-prompt which is Truly excellent.
* cat pew | (exec 3<>/dev/tcp/termbin.com/9999;cat >&3;cat <&3;exec 3<&-)
This basically allows us to post snippets on bash. Without using any other program, ideal for netcat less devices.
* date -d @timestamp allows converting timestamps to UTC time
* date --date = "DATE" "+%s" converts normal date to timestamp
* Press a at android's boot in qemu and then after ram0 add androidboot.hardware=x86 if its not booting in gui
