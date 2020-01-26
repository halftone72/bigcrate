# Pop!_OS 19.10


### Settings

Appearance - set a wallpaper!
Sharing - set host name to bigcrate
Devices>Display - set refresh rate much higher (can go to 144)

### Enable rapid release

Open the Pop!_Shop, then click on the gear for settings
Expand developer options, then select Pre-released updates. 
Click on X and enter password
Open Terminal and run`sudo apt update && sudo apt upgrade`

### Sign into Firefox

Log into Bitwarden and close other extension info windows after sync

### Install some stuff

`sudo apt install samba openssh-server mergerfs glances lynx`

___Set up mergerFS and Snapraid now. See 2 Storage Install___

Install Dash to Dock, OpenWeather Gnome, and Gnome Tweaks extensions from the Gnome add-in in Firefox. **Configure extensions within Firefox**

### Web installations

<https://www.nomachine.com/>
<https://code.visualstudio.com/Download>

___Setup Samba shares. See 3 TARDIS___


---

# Reference and Notes

<https://system76.com/pop>

Install similar to Ubuntu. Items of note:

- For home server, do not select encrypt disk - requires password with each restart.
- DO NOT install the AMD GPU drivers, just use what comes with the OS - GPU drivers don't work. 
- Samba sharing through GUI doesn't work. Requires installing nautilus-share but still is ineffective because nothing is written to /etc/samba/smb.conf. Best to set up shares manually.
- ~~Don't connect to WiFi unless necessary. There seems to be an issue with the driver where it randomly failed under vanilla Ubuntu and prevented booting under Pop!_OS after many restarts (unexpected!!!)~~ Jan 2020: WiFi is enabled and connected to guest network, appears to be stable.
- Minimize window isn’t enabled by default. Use Gnome Tweaks.
