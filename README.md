# VR-reversal

Uses mpv and a plugin to play a 3D side-by-side video as a 2D video, allows you to look around and zoom within the video, optionally logs the head motions to a file for later rendering out to a 2D video with ffmpeg.

![Example output](https://github.com/dfaker/VR-reversal/blob/master/example.gif?raw=true)

# Installation and Usage:

- Download the lastest mpv https://mpv.io/
- Download the 360plugin.lua from this repo.
- Play a video using the plugin with the command: `mpv --script=360plugin.lua videoFile.mp4`

If you want to save the 2D versions videos rather than just watch them you'll need a recent version of ffmpeg from https://ffmpeg.org/ but it's not needed just for viewing.

Alternatively rather than using the command line, windows users may choose to:

- Place mpv.exe, vr-reversal.bat and 360plugin.lua (vr-reversal.bat and 360plugin.lua are avalaible in a single zip file from the most recent release https://github.com/dfaker/VR-reversal/releases) in the same folder.
- Run vr-reversal.bat
- Drag and drop videos onto the mpv window that opens up.

# Controls

You can press `?` to show all of the keyboard controls on screen at any time.

When the player is started, you'll be looking straight forwards. 
The video will start at a low resolution, if you'd like more detail press `y` increase the initial preview quality `h` to reduce it again.

- `y` Increase resolution
- `h` decrease resolution

Control where you're looking with the mouse:

- MouseLook: click anywhere in the video and your mouse position will control the camera, click again to stop mouse control
- MouseScroll: Zoom in and out

or alternately look around with these keys:

- `i`,`j`,`k`,`l` look around 
- `u`,`o` roll head
- `=`,`-` zoom

Additional controls:

- `t` switch the eye you're looking through between left and right
- `e` switch the video scaler between nearest neighbour and bicubic
- `g` toggle mouse smothing
- `n` start or stop logging head motions to file for later rendering
- `?` show keybaord and mouse control reminder on screen

Advanced projection controls:

90% of modern vr releases work perfectly with the defauls of 180 degree 'hequirect' projection so you shound't need these unless playing older or unusually formatted content:

- `r` toggle stereo mode between top/bottom and side by-side
- `b` cycle input fov bounds between 180,360 and 90
- `1` cycle through input projections
- `2` cycle through output projections

Most of the standard mpv controls are maintained:

- `Arrow keys` seek through video
- `SPACE` pause
- `f` fullscreen toggle
- `9`,`0` volume up and down
- `m` mute

And finally when  you're done:

- `q` quit

# 'Head' Motion Logging and saving your clips
If you have pressed `n` during your session your 'head' movements in the video will be logged to a file named `{originalFilename}_3dViewHistory_{sectionNumber}.txt` this is in the format of motion commands to be processed by ffmpeg https://ffmpeg.org/

The script will create a batch file `convert_3dViewHistory.bat` after you exit the player, if you have ffmpeg installed you may simply run this file to perform the conversion to 2D .mp4 clips automatically.
