# Storage setup

Create mount points for the drives

`sudo mkdir /mnt/cratedisk01 /mnt/cratedisk02 /mnt/cratedisk03 /mnt/crateparity01 /mnt/storage /mnt/vmworld`

Edit /etc/fstab and add to end

```
/dev/disk/by-id/wwn-0x5000cca257ee36d7 /mnt/cratedisk01 auto nosuid,nodev,nofail 0 0
/dev/disk/by-id/wwn-0x5000cca257ee9baa /mnt/cratedisk02 auto nosuid,nodev,nofail 0 0
/dev/disk/by-id/wwn-0x5000cca257eb5e67 /mnt/cratedisk03 auto nosuid,nodev,nofail 0 0
/dev/disk/by-id/wwn-0x5000c500b5162876 /mnt/crateparity01 auto nosuid,nodev,nofail 0 0
/mnt/cratedisk* /mnt/storage fuse.mergerfs allow_other,direct_io,use_ino,category.create=lfs,moveonenospc=true,minfreespace=20G,fsname=mergerfsPool 0 0
/dev/disk/by-id/wwn-0x5f8db4c381801218-part1 /mnt/vmworld auto nosuid,nodev,nofail 0 0
```

Remount

`sudo mount -a`

Set permissions

```
sudo chmod 0777 /mnt/storage /mnt/vmworld
sudo chown -R halftone72:halftone72 /mnt/storage  /mnt/vmworld
```

---

# Reference and Notes

https://blog.linuxserver.io/2017/06/24/the-perfect-media-server-2017/
