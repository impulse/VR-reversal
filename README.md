# VR-reversal

Uses mpv and a plugin to display a 3D side-by-side video as a 2D video, allows you to look around and zoom within the video, logs the head motions to a file for later rendering out to a 2D video with ffmpeg.

![Example output](https://github.com/dfaker/VR-reversal/blob/master/example.gif?raw=true)

# Steps:

- Download the lastest mpv https://mpv.io/
- Download the 360plugin.lua from this repo.
- Play a video using the plugin with the command: `mpv --script=360plugin.lua videoFile.mp4`

Alternatively rather than typing the command `mpv --script=360plugin.lua videoFile.mp4` on the command line, you may choose to:
- Place mpv.exe and 360plugin.lua in the same folder.
- Make a shortcut to mpv.exe in that same folder by right clicking and seelcting `Create Shortcut`
- Right click on the shortcut and select `Properties`
- In the field 'Target:' in the properties popup add ` --script=360plugin.lua` after mpv.exe (not forgetting the space between mpv.exe and the dashes.)
- You may themn drag and drop videos directly onto your newly created shortcurt to play them.

# Controls
- `y` Increase resolution
- `h` decrease resolution
- `i`,`j`,`k`,`l` look around 
- `u`,`o` roll head
- `=`,`-` zoom
- `q` quit
- MouseLook: to look around with the mouse: one click to start, move the mouse to look around and then click again to stop
- MouseScroll: Zoom in and out

The video will start at a low resolution, press `y` increase the initial preview quality.

# 'Head' Motion Logging
Your 'head' movements in the video will be logged to a file named `3dViewHistory.txt` this is in the format of ffmpeg commands and looks like:

```
188.792256-188.807622 [expr] v360 pitch -0.100000, [expr] v360 yaw 0.400000, [expr] v360 roll 0.000000, [expr] v360 d_fov 90.000000;
188.807622-188.824578 [expr] v360 pitch -0.300000, [expr] v360 yaw 1.000000, [expr] v360 roll 0.000000, [expr] v360 d_fov 90.000000;
...
224.595089-224.611200 [expr] v360 pitch -3.500000, [expr] v360 yaw 7.100000, [expr] v360 roll 0.000000, [expr] v360 d_fov 95.000000;
224.611200-224.627511 [expr] v360 pitch -3.200000, [expr] v360 yaw 7.100000, [expr] v360 roll 0.000000, [expr] v360 d_fov 95.000000;
# ffmpeg -ss 188 -i videoFile.mp4 -to 224 -copyts -vf "v360=hequirect:flat:in_stereo=sbs:out_stereo=2d:id_fov=180.0:d_fov=90:yaw=0:pitch=0:roll=0:w=1920.0:h=1080.0:interp=cubic,sendcmd=filename=3dViewHistory.txt" outputVideo.webm
```
The comment at the end of the file is the suggested ffmpeg command to convert your video tracking data into an output video, it has the start and stop times set to the times when you intitially starting changing the view of the vr 'head'.
