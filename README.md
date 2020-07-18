## Best pulseaudio mic settings 
Install pulseaudio
```
sudo apt install pulseaudio pavucontrol
```
Copy the pulse audio folder into config and open using nano
```
sudo cp -r /etc/pulse ~/.config/
sudo nano ~/.config/pulse/daemon.conf
```
Find a line that says
```
;avoid-resampling = false
```
Remove semi-colon and set to true	
```	
avoid-resampling = true
```
Now do **Ctrl+X**,**Y** to accept and Enter to save.

Find out which resample methods your PulseAudio setup supports. In terminal, type
```
pulseaudio --dump-resample-methods
```
and take a look at the output. You should see some speex-float-#, etc. I read that "float" is best for most computers, and 0-10 is the "quality". We want the highest quality possible... 10. Make note of that, for example speex-float-10. We'll put that in our config file next.

Go back into the config file like before, using
```
sudo nano ~/.config/pulse/daemon.conf
```

Change
```
resample-method = speex-float-#
```
to the new method that we just found. Delete the semi-colon.
Ctrl-X, Y, and Enter to save.

Open the **/etc/pulse/default.pa** file and go to the end of the file and add
```
load-module module-udev-detect
```

Restart PulseAudio. To do this, type
```
pulseaudio --kill
pulseaudio --start
```
Wait a moment, and it will restart itself with the new settings.

You are done!
