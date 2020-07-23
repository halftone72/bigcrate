_Last Updated 071620_

# Layout

Example:

```
toplevel         (volume root directory, not to be mounted by default)
  +-- root       (subvolume root directory, to be mounted at /)
  +-- home       (subvolume root directory, to be mounted at /home)
  +-- var        (directory)
  |   \-- www    (subvolume root directory, to be mounted at /var/www)
  \-- postgres   (subvolume root directory, to be mounted at /var/lib/postgresql)
```

## System

/dev/nvme0n1p1 - /boot/efi (FAT32)
/dev/nvme0n1p2 - swap
/dev/nvme0n1p3 - / (BTRFS)

512 MB NVME

sudo btrfs subvolume list /

```
ID 263 gen 14901 top level 5 path @
ID 264 gen 14900 top level 5 path @home
```
*NOTE* add VAR subvolume and update list
### Layout

```
toplevel          (volume root directory, not to be mounted by default)
  +-- @           (subvolume root directory, to be mounted at /)
  +-- @home       (subvolume root directory, to be mounted at /home)
  +-- @var        (subvolume root directory, to be mounted at /var)
```

## NAS

/dev/sdb
/dev/sdc
/dev/sdd
/dev/sde

RAID10 (mirrored and striped) - 32 TB physical, 16 TB actual

sudo btrfs subvolume list /mnt/storage

```
ID 9084 gen 44268 top level 5 path @appstore
ID 9085 gen 43374 top level 5 path @arcade
ID 9086 gen 43382 top level 5 path @archive
ID 9087 gen 44268 top level 5 path @junkdrawer
ID 9088 gen 44260 top level 5 path @loading_dock
ID 9089 gen 43384 top level 5 path @media_center
ID 9090 gen 43952 top level 5 path @outer_realm
ID 9098 gen 44266 top level 5 path @library
```

### Layout

```
toplevel            (volume root directory, not to be mounted by default)
  +-- @appstore     (subvolume root directory, to be mounted at /mnt/appstore)
  +-- @arcade       (subvolume root directory, to be mounted at /mnt/arcade)
  +-- @archive      (subvolume root directory, to be mounted at /mnt/archive)
  +-- @junkdrawer   (subvolume root directory, to be mounted at /mnt/junkdrawer)
  +-- @loading_dock (subvolume root directory, to be mounted at /mnt/loading_dock)
  +-- @media_center (subvolume root directory, to be mounted at /mnt/media_center)
  +-- @outer_realm  (subvolume root directory, to be mounted at /mnt/outer_realm)
  +-- @library      (subvolume root directory, to be mounted at /mnt/library)
```

### Usage

| Subvolume | Contents |
|-----------|----------|
| @appstore | Software and driver repository, ISOs |
| @arcade | Emulators and ROMs |
| @archive | Work archive, other long term storage |
| @junkdrawer | Misc files that don't fit elsewhere |
| @loading_dock | An open share for file transfer/sharing |
| @media_center | Movies, TV, Other video|
| @outer_realm | Out of bounds, Download folder for Transmission |
| @library | Ebooks, audiobooks, comics, games/RPG, magazines, audio drama |
