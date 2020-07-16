# Notes

# Todo
- [ ]

# Commands
---
# BTRFS system drive setup

1. Boot into the Pop OS live image and open your terminal **NOTE:** Choose EFI option from flash drive
2. Create your partitions. I used:
	* 512MiB fat32 for the boot partition
	* 64GiB swap partition
	* the rest of the disk was a btrfs partition
3. Install Pop!_OS using the graphical installer
4. At the install type step, choose Custom (Advanced)
	* Click on the first partition (set up as boot in your partition manager) and select Use Partition, select Format, select fat32, and the filesystem will be /boot/efi **NOTE:** If you see /boot or will only allow ext4 format, you need to boot using EFI option in step 1.
	* Click on the second partition (set up as swap in your partition manager), select Use Partition, use as Swap
	* Click on your btrfs partition, select Use Partition, select Format, select btrfs, and / as the filesystem. Make sure all of your partitions have a black checkmark icon on them
5. Click Erase and Install
6. When install finishes, DO NOT click Restart Device. Instead go to your trusty terminal to continue post-install steps
7. make sure you are **root**
8. Mount the newly-created btrfs filesystem to /mnt using the below command
`mount -t btrfs -o subvolid=5,ssd,noatime,space_cache /dev/nvme0n1p3 /mnt`
9. Create the "@" and "@home" subvolumes
`btrfs subvol create /mnt/@`
`btrfs subvol create /mnt/@home`
10. Now, we need to move the folders in /mnt into the /mnt/@ subvolume
`cd /mnt`
`ls | grep -v @ | xargs mv -t @`
11. Now, we have to edit the fstab to account for the changes made
`cat /mnt/@/etc/fstab` #it should look something like the below

```
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
```

12. You will need to change it to add the subvols you created and add another entry for u/home. Like so:

```
# /etc/fstab: static file system information.
Use 'blkid' to print the universally unique identifier for a device; this may be used with UUID= as a more robust way to name devices that works even if disks are added and removed. See fstab(5).
#
# <file system>  <mount point>  <type>  <options>  <dump>  <pass>
  PARTUUID=8d5407ee-527a-4e67-af2a-a0ca648c5726  /boot/efi  vfat  umask=0077  0  0
/dev/mapper/cryptswap  none  swap  defaults  0  0
UUID=458aebbe-2761-4b15-9737-cb26f7e72c48  /  btrfs defaults,subvol=@,ssd,noatime,space_cache  0  0 UUID=458aebbe-2761-4b15-9737-cb26f7e72c48  /home btrfs defaults,subvol=@home,ssd,noatime,space_cache  0  0
```

13. Once your fstab is saved, mount your efi partition
`mount /dev/nvme0n1p1 /mnt/@/boot/efi`
14.  Add `rootflags=subvol=@` to the options line of Pop_OS_current.conf
`nano /mnt/@/boot/efi/loader/entries/Pop_OS-current.conf`
Options line will look like:

```
options root=UUID=0b3e7957-8861-439f-a02d-4be9db8e07cf ro quiet loglevel=0 systemd.show_status=false splash rootflags=subvol=@ 
```

15. Now, add support for booting to the @ subvol to the kernelstub configuration file
`nano /mnt/@/etc/kernelstub/configuration`
In that config file, add the `rootflags=subvol=@` under the default and user sections, like so:

```
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
```

16. Now, you can go back to the install window and click *Restart Device*


# Reference
PopOS and BTRFS
https://www.reddit.com/r/pop_os/comments/g6c9l2/pop_os_2004_and_btrfs/

BTRFS wiki
https://btrfs.wiki.kernel.org/index.php/Main_Page
