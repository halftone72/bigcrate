# Pop!_OS 20.04 v2.0

###BTRFS drive setup
1. Boot into the Pop OS live image and open your terminal
2. Create your partitions. I used:
	- 512MiB fat32 for the boot partition
	- 8GiB swap partition
	- the rest of the disk was a btrfs partition
3. Install Pop!_OS using the graphical installer
4. At the install type step, choose Custom (Advanced)
	a. Click on the first partition (set up as boot in your partition manager) and select Use Partition, select Format, select fat32, and the filesystem will be /boot/efi
	b. Click on the second partition (set up as swap in your partition manager), select Use Partition, use as Swap
	c. Click on your btrfs partition, select Use Partition, select Format, select btrfs, and / as the filesystem
	d. Make sure all of your partitions have a black checkmark icon on them
5. Click Erase and Install
6. When install finishes, DO NOT click Restart Device. Instead go to your trusty terminal to continue post-install steps
7. make sure you are root
8. Mount the newly-created btrfs filesystem to /mnt using the below command
`mount -t btrfs -o subvolid=5,ssd,noatime,space_cache /dev/<yourrootpartition> /mnt`
9. Create the "@" and "@home" subvolumes
`btrfs subvol create /mnt/@`
`btrfs subvol create /mnt/@home`
10. Now, we need to move the folders in /mnt into the /mnt/@ subvolume
`cd /mnt`
` ls | grep -v @ | xargs mv -t @``
11. Now, we have to edit the fstab to account for the changes made
`cat /mnt/@/etc/fstab` #it should look something like the below

````
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system>  <mount point>  <type>  <options>  <dump>  <pass>
PARTUUID=8d5407ee-527a-4e67-af2a-a0ca648c5726  /boot/efi  vfat  umask=0077  0  0
/dev/mapper/cryptswap  none  swap  defaults  0  0
UUID=0b3e7957-8861-439f-a02d-4be9db8e07cf  /  btrfs defaults,ssd,noatime,space_cache  0  0
````
12. You will need to change it to add the subvols you created and add another entry for u/home. Like so:

````
# /etc/fstab: static file system information.
Use 'blkid' to print the universally unique identifier for a device; this may be used with UUID= as a more robust way to name devices that works even if disks are added and removed. See fstab(5).
#
# <file system>  <mount point>  <type>  <options>  <dump>  <pass>
  PARTUUID=8d5407ee-527a-4e67-af2a-a0ca648c5726  /boot/efi  vfat  umask=0077  0  0
          /dev/mapper/cryptswap  none  swap  defaults  0  0
          UUID=0b3e7957-8861-439f-a02d-4be9db8e07cf  /  btrfs  defaults,subvol=@,ssd,noatime,space_cache  0  0
          UUID=0b3e7957-8861-439f-a02d-4be9db8e07cf  /home btrfs defaults,subvol=@home,ssd,noatime,space_cache  0  0
````
13. Once your fstab is saved, mount your efi partition
`mount /dev/<yourEFIpartition> /mnt/@/boot/efi`
14.  Add `rootflags=subvol=@` to the options line of Pop_OS_current.conf
`nano /mnt/@/boot/efi/loader/entries/Pop_OS-current.conf`
Options line will look like:
````
options root=UUID=0b3e7957-8861-439f-a02d-4be9db8e07cf ro quiet loglevel=0 systemd.show_status=false splash rootflags=subvol=@ 
````
15. Now, add support for booting to the @ subvol to the kernelstub configuration file
`nano /mnt/@/etc/kernelstub/configuration`
In that config file, add the `rootflags=subvol=@` under the default and user sections, like so:

````
{
  "default": {
    "kernel_options": [
      "quiet",
      "splash",
      "rootflags=subvol=@"
    ],
    "esp_path": "/boot/efi",
    "setup_loader": false,
    "manage_mode": false,
    "force_update": false,
    "live_mode": false,
    "config_rev": 3
  },
  "user": {
    "kernel_options": [
      "quiet",
      "loglevel=0",
      "systemd.show_status=false",
      "splash",
      "rootflags=subvol=@"
````
16. Now, you can go back to the install window and click *Restart Device*

###Mount storage

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

````
/dev/disk/by-id/wwn-0x5000c500b5162876 /home/halftone72/@appstore auto nosuid,nodev,nofail,autodefrag,compress=zstd,noatime,subvol=@appstore 0 0
/dev/disk/by-id/wwn-0x5000c500b5162876 /home/halftone72/@junkdrawer auto nosuid,nodev,nofail,autodefrag,compress=zstd,noatime,subvol=@junkdrawer 0 0
/dev/disk/by-id/wwn-0x5000c500b5162876 /home/halftone72/@outer_realm auto nosuid,nodev,nofail,autodefrag,compress=zstd,noatime,subvol=@outer_realm 0 0
````

Mount storage pool
`sudo mount -a`

###Updates
`sudo apt update && sudo apt upgrade`

###Install some stuff

`sudo apt install samba openssh-server glances lynx`

###Install AMD drivers

Download drivers at https://www.amd.com/en/support/graphics/radeon-500-series/radeon-rx-500-series/radeon-rx-570

Extract archive
`unxz amdgpu-pro-20.20-1098277-ubuntu-20.04.xz`
`tar xvf amdgpu-pro-20.20-1098277-ubuntu-20.04.tar`

Edit `amdgpu-install`
`nano amdgpu-install`

In editor,  use ^w to search for `ubuntu`
Modify to read:

````
				case "$ID" in
                ubuntu|linuxmint|debian|pop)
````

Install driver
`./amdgpu-pro-install --opencl=legacy,pal --no-dkms --headless`
Or if install errors,
`./amdgpu-install --opencl=legacy,pal --no-dkms --headless`

Test OpenCL
`clinfo`

Will return GPU details if working

###FoldingAtHome

Install client
`wget https://download.foldingathome.org/releases/public/release/fahclient/debian-testing-64bit/v7.4/fahclient_7.4.4_amd64.deb`
`sudo dpkg -i --force-depends fahclient_7.4.4_amd64.deb`

Edit confit file
`sudo nano /etc/fahclient/config.xml`

```
<config>
  <!-- Client Control -->
  <fold-anon v='true'/>

  <!-- User Information -->
  <user v='halftone72'/>

  <!-- Folding Slots -->
  <slot id='0' type='CPU'>
    <paused v='true'/> 
  </slot>              
  <slot id='1' type='GPU'>
    <paused v='true'/> 
  </slot>                      
</config> 
```

Restart the service and run as root
`sudo /etc/init.d/FAHClient stop`
`sudo /etc/init.d/FAHClient -u root start`

Use the web client to configure name and confirm GPU is picking up jobs
http://client.foldingathome.org

---

# Reference and Notes
PopOS and BTRFS
https://www.reddit.com/r/pop_os/comments/g6c9l2/pop_os_2004_and_btrfs/

Install AMD Proprietary OpenCL on Pop!OS and some Ubuntu Derivates
https://devtalk.blender.org/t/install-amd-proprietary-opencl-on-pop-os-and-some-ubuntu-derivates/13458

FAH command line options
https://foldingathome.org/support/faq/installation-guides/linux/command-line-options/

