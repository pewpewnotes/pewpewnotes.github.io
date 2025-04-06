Using an HDMI output
Most drivers these days, including the nVidia proprietary driver and the new Intel recommended "modesetting" driver do not support virtual outputs. In this case it is normally possible to use a free HDMI output (i.e. HDMI-1 or HDMI-2). This will mostly work, you will be able to move windows to the virtual screen and export it with VNC.

Some userspace programs (notably KDE, LibreOffice Impress, Zoom) do not recognize the screen properly and will not work in "dual screen mode" or may cause some glitches. You can work around this problem by forcing the HDMI output to be enabled, via the /sys/debug interface by running:

# echo on > /sys/kernel/debug/dri/0/OUTPUT/force
where OUTPUT can be HDMI-A-1, or HDMI-A-2, or other, depending on which output you are using. Note that the name is different from that used by xrandr. This may also enable the audio output of the HDMI port, redirecting your system audio to the fake output. In this case, you may want to revert to the previous audio output.
