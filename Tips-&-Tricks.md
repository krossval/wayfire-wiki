## Run xwayland apps as root

This is a small wrapper script that uses `xhost` and `sudo` to launch x11 clients as root under xwayland. Save to a file, make executable and use in place of sudo to run an x11 client with privileges in wayfire.

```
#!/bin/bash
# small script to enable root access to x-windows system

# enable root access
xhost +SI:localuser:root

sudo -E $@

# disable root access after application terminates
xhost -SI:localuser:root
```

## Native webcam with gst-launch-1.0 (gstreamer)
Use the following command to show /dev/video0 in a native window. Note that glimagesink must be available.
```
gst-launch-1.0 -v v4l2src device=/dev/video0 ! glimagesink
```

## Wine
If you are having trouble with wine applications, such as input not responding, tearing windows, or buggy mouse behavior in some fullscreen games check the following:
- Make sure xwayland is enabled in wayfire meson configure output and in wayfire.ini [core] xwayland = 1
- In winecfg in the Graphics tab, enable 'Automatically capture mouse in full screen mode', disable 'Allow the window manager to decorate the windows', disable 'Allow the window manager to control the windows' and enable 'Emulate a virtual desktop'