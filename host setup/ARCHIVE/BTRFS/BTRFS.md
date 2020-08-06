# Commands

### Initial setup
Scan for BTRFS FS
`sudo btrfs scan`

Create BTRFS filesystem
`sudo mkfs.btrfs /dev/sdb /dev/sdc /dev/sdd`
Specify multiple devices like the example if creating a BTRFS pool. See https://btrfs.wiki.kernel.org/index.php/Mkfs.btrfs for more options.

Mount pool
`sudo mount -t btrfs /dev/sdc /mnt/storage`
Specify one device to mount, BTRFS will take care of the rest.

Create subvolume
`btrfs subvolume create /mnt/storage/new_subvol`

Mount subvolume
`sudo mount -t btrfs -o subvol=new_subvol /dev/sdc /mnt/new_subvol`

Remove subvolume
`btrfs subvolume delete /mnt/storage/new_subvol`

Create snapshot
`btrfs subvolume snapshot /mnt/new_subvol /mnt/storage/snapshot_of_subvol`

Mount snapshot
`sudo mount -t btrfs -o subvol=snapshot_of_subvol /dev/sdc /mnt/snap`

Mount options
https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs(5)#MOUNT_OPTIONS

---

# Reference

BTRFS wiki
https://btrfs.wiki.kernel.org/index.php/Main_Page
