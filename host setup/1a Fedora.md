# Fedora 31

### Installation

Install from USB like other distros. Create user after reboot

### Add RPM Fusion repository

```
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

### Add RPM Sphere repository

Web based - https://rpmsphere.github.io/

### Install some stuff

`sudo apt install samba openssh-server mergerfs glances lynx nano`

### mergerfs install

https://github.com/trapexit/mergerfs/releases