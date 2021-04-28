The gamepad might not support vibration. If you can edit your post to include the vendor and product IDs for the device it's much easier for other people to know which model you have and whether it should work. You can get this with lsusb (assuming it's connected with USB):

$ lsusb
```
Bus002 Device 056: ID 045e:02ea Microsoft Corp. 
```

In this case I have a connected gamepad with vendor ID 045e and product ID 02ea. Those are the IDs for an Xbox One controller.

A gamepad supports vibration if it supports the FF_RUMBLE event, which you can check with the evtest tool. Here's the output for my Xbox One controller, which does support vibration.

```
$ evtest
No device specified, trying to scan all of /dev/input/event*
Not running as root, no devices may be available.
Available devices:
/dev/input/event16: Microsoft X-Box One S pad
Select the device event number [0-16]: 16
Input driver version is 1.0.1
Input device ID: bus 0x3 vendor 0x45e product 0x2ea version 0x301
Input device name: "Microsoft X-Box One S pad"
Supported events:
  Event type 0 (EV_SYN)
  Event type 1 (EV_KEY)
    Event code 304 (BTN_SOUTH)
    Event code 305 (BTN_EAST)
    Event code 307 (BTN_NORTH)
    Event code 308 (BTN_WEST)
    Event code 310 (BTN_TL)
    Event code 311 (BTN_TR)
    Event code 314 (BTN_SELECT)
    Event code 315 (BTN_START)
    Event code 316 (BTN_MODE)
    Event code 317 (BTN_THUMBL)
    Event code 318 (BTN_THUMBR)
  Event type 3 (EV_ABS)
    Event code 0 (ABS_X)
      Value    738
      Min   -32768
      Max    32767
      Flat     128
    Event code 1 (ABS_Y)
      Value    705
      Min   -32768
      Max    32767
      Flat     128
    Event code 2 (ABS_Z)
      Value      0
      Min        0
      Max     1023
    Event code 3 (ABS_RX)
      Value    482
      Min   -32768
      Max    32767
      Fuzz      16
      Flat     128
    Event code 4 (ABS_RY)
      Value   -339
      Min   -32768
      Max    32767
      Fuzz      16
      Flat     128
    Event code 5 (ABS_RZ)
      Value      0
      Min        0
      Max     1023
    Event code 16 (ABS_HAT0X)
      Value      0
      Min       -1
      Max        1
    Event code 17 (ABS_HAT0Y)
      Value      0
      Min       -1
      Max        1
  Event type 21 (EV_FF)
    Event code 80 (FF_RUMBLE)
    Event code 81 (FF_PERIODIC)
    Event code 88 (FF_SQUARE)
    Event code 89 (FF_TRIANGLE)
    Event code 90 (FF_SINE)
    Event code 96 (FF_GAIN)
Properties:
Testing ... (interrupt to exit)
Event code 80 (FF_RUMBLE) means it should support vibration effects.
```
To test rumble, use fftest. You'll need to provide the path to the evdev node for the gamepad, which is included in the output from evtest. For my Xbox controller this was /dev/input/event16:
```
$ fftest /dev/input/event16
Force feedback test program.
HOLD FIRMLY YOUR WHEEL OR JOYSTICK TO PREVENT DAMAGES

Device /dev/input/event16 opened
Features:
  * Absolute axes: X, Y, Z, RX, RY, RZ, Hat 0 X, Hat 0 Y, 
    [3F 00 03 00 00 00 00 00 ]
  * Relative axes: 
    [00 00 ]
  * Force feedback effects types: Periodic, Rumble, Gain, 
    Force feedback periodic effects: Square, Triangle, Sine, 
    [00 00 00 00 00 00 00 00 00 00 03 07 01 00 00 00 ]
  * Number of simultaneous effects: 16

Setting master gain to 75% ... OK
Uploading effect #0 (Periodic sinusoidal) ... OK (id 0)
Uploading effect #1 (Constant) ... Error: Invalid argument
Uploading effect #2 (Spring) ... Error: Invalid argument
Uploading effect #3 (Damper) ... Error: Invalid argument
Uploading effect #4 (Strong rumble, with heavy motor) ... OK (id 1)
Uploading effect #5 (Weak rumble, with light motor) ... OK (id 2)
Enter effect number, -1 to exit
Use effects 4 and 5 to test rumble effects:

Enter effect number, -1 to exit
4
Now Playing: Strong Rumble
Enter effect number, -1 to exit
5
Now Playing: Weak Rumble
Enter effect number, -1 to exit
```
