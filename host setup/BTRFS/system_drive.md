1. Boot into the Pop OS live image using EFI option from flash drive
2. Install Pop!_OS using the graphical installer
3. At the install type step, choose Custom (Advanced)
	* Click on the first partition (set up as boot in your partition manager) and select Use Partition, select Format, select fat32, and the filesystem will be /boot/efi **NOTE:** If you see /boot or will only allow ext4 format, you need to boot using EFI option in step 1.
	* Click on the second partition (set up as swap in your partition manager), select Use Partition, use as Swap
	* Click on your btrfs partition, select Use Partition, select Format, select btrfs, and / as the filesystem. 
	Make sure all of your partitions have a black checkmark icon on them
4. Click Erase and Install
5. When install finishes, DO NOT click Restart Device. Open terminal to continue post-install steps
6. Make sure you are **root** `sudo su`
7. Mount the newly-created btrfs filesystem to /mnt using the below command
`mount -t btrfs -o subvolid=5,ssd,noatime,space_cache /dev/nvme0n1p3 /mnt`
8. Create the subvolumes
`btrfs subvol create /mnt/@`
`btrfs subvol create /mnt/@home`
`btrfs subvol create /mnt/@var`
9. Move the folders in /mnt into the /mnt/@ subvolume
`cd /mnt`
`ls | grep -v @ | xargs mv -t @`
10. Create mount points
`sudo mkdir /mnt/storage /mnt/appstore /mnt/arcade /mnt/archive /mnt/junkdrawer /mnt/loading_dock /mnt/media_center /mnt/outer_realm /mnt/library`
11. Edit fstab
`sudo nano /mnt/@/etc/fstab`
12. Replace contents with fstab from github source and save
13. Mount your efi partition
`mount /dev/nvme0n1p1 /mnt/@/boot/efi`
14. Add `rootflags=subvol=@` to the options line of Pop_OS_current.conf
`nano /mnt/@/boot/efi/loader/entries/Pop_OS-current.conf`
Options line will look like:

```
options root=UUID=0b3e7957-8861-439f-a02d-4be9db8e07cf ro quiet loglevel=0 systemd.show_status=false splash rootflags=subvol=@ 
```

15. Add support for booting to the @ subvol to the kernelstub configuration file
`nano /mnt/@/etc/kernelstub/configuration`
Add the `rootflags=subvol=@` under the default and user sections

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

16. Go back to the install window and click *Restart Device*

---

# Reference

PopOS and BTRFS
https://www.reddit.com/r/pop_os/comments/g6c9l2/pop_os_2004_and_btrfs/
