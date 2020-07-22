# Pop!_OS 20.04 v2.0

### Install

Install with defaults. Do not encrypt system disk (unable to reconnect remotely to unlock on reboot.) Follow drive setup instructions under BTRFS.md if using BTRFS for the system drive.

### Mount storage

Get disk info
`blkid`
Note UUID

Create mount point
`sudo mkdir /mnt/storage`

Edit /etc/fstab
`sudo nano /etc/fstab/`

add entries

```
dev/disk/by-id/wwn-0x5000c500b5162876 /mnt/storage auto nosuid,nodev,nofail,autodefrag,compress=zstd,noatime 0 0
```

```
/dev/disk/by-id/wwn-0x5000c500b5162876 /home/halftone72/@appstore auto nosuid,nodev,nofail,autodefrag,compress=zstd,noatime,subvol=@appstore 0 0
/dev/disk/by-id/wwn-0x5000c500b5162876 /home/halftone72/@junkdrawer auto nosuid,nodev,nofail,autodefrag,compress=zstd,noatime,subvol=@junkdrawer 0 0
/dev/disk/by-id/wwn-0x5000c500b5162876 /home/halftone72/@outer_realm auto nosuid,nodev,nofail,autodefrag,compress=zstd,noatime,subvol=@outer_realm 0 0
```

Mount storage pool
`sudo mount -a`

### Updates
`sudo apt update && sudo apt upgrade`

### Install some stuff

`sudo apt install btrfs-progs clinfo samba openssh-server glances lynx gnome-tweaks`

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

PopOS and BTRFS
https://www.reddit.com/r/pop_os/comments/g6c9l2/pop_os_2004_and_btrfs/

Install AMD Proprietary OpenCL on Pop!OS and some Ubuntu Derivates
https://devtalk.blender.org/t/install-amd-proprietary-opencl-on-pop-os-and-some-ubuntu-derivates/13458

