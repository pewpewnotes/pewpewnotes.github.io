```text
 ____                 _                            ____  _ 
|  _ \ __ _ ___ _ __ | |__   ___ _ __ _ __ _   _  |  _ \(_)
| |_) / _` / __| '_ \| '_ \ / _ \ '__| '__| | | | | |_) | |
|  _ < (_| \__ \ |_) | |_) |  __/ |  | |  | |_| | |  __/| |
|_| \_\__,_|___/ .__/|_.__/ \___|_|  |_|   \__, | |_|   |_|
               |_|                         |___/           
```

## Stuffs regarding RPI 3b+
***

### Enabling UART
```bash
[Inside config.txt]
enable_uart=1
```
### == Wifi Interference with HDMI ==
* A simple solution to that is to make sure that TV is at 720p and frequency of wifi to 5ghz, or 6+ channel.
* [https://www.raspberrypi.org/documentation/configuration/config-txt/video.md](Config.txt) Refer to this for configuration option.
```
disable_overscan=0
overscan_left=-8
overscan_right=-8
overscan_top=-13
overscan_bottom=-10
framebuffer_width=1280
framebuffer_height=720
hdmi_force_hotplug=1
hdmi_group=1
hdmi_mode=4
hdmi_drive=2
dtparam=audio=on
[pi4]
dtoverlay=vc4-fkms-v3d
max_framebuffers=2
[all]
```


### == Android ==

* TBI
