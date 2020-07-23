# Pop!_OS 20.04 v2.0

### Install

Install with defaults. Do not encrypt system disk (unable to reconnect remotely to unlock on reboot.) Use system_drive.md for post-installation setup.

### apt-btrfs-snapper and snapper
Install Snapper and apt-btrfs-snapper

### Updates
`sudo apt update && sudo apt upgrade`

### Install some stuff

`sudo apt install btrfs-progs clinfo openssh-server glances lynx gnome-tweaks`

*NOTE* Samba removed, try manual install from scratch

### Install AMD drivers

Download drivers at https://www.amd.com/en/support/graphics/radeon-500-series/radeon-rx-500-series/radeon-rx-570

Extract archive
`unxz amdgpu-pro-20.20-1098277-ubuntu-20.04.xz`
`tar xvf amdgpu-pro-20.20-1098277-ubuntu-20.04.tar`

Edit `amdgpu-install`
`nano amdgpu-install`

In editor,  use ^w to search for `ubuntu`
Modify to read:

```
				case "$ID" in
                ubuntu|linuxmint|debian|pop)
```

Install driver
`./amdgpu-install --opencl=legacy,pal --no-dkms --headless`

Test OpenCL
`clinfo`

Will return GPU details if working

---

# Reference

Install AMD Proprietary OpenCL on Pop!OS and some Ubuntu Derivates
https://devtalk.blender.org/t/install-amd-proprietary-opencl-on-pop-os-and-some-ubuntu-derivates/13458

