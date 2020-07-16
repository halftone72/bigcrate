# Layout

toplevel         (volume root directory, not to be mounted by default)
  +-- root       (subvolume root directory, to be mounted at /)
  +-- home       (subvolume root directory, to be mounted at /home)
  +-- var        (directory)
  |   \-- www    (subvolume root directory, to be mounted at /var/www)
  \-- postgres   (subvolume root directory, to be mounted at /var/lib/postgresql)

# /etc/fstab

LABEL=the-btrfs-fs-device   /                    btrfs subvol=/root,defaults,noatime  0  0
LABEL=the-btrfs-fs-device   /home                btrfs subvol=/home,defaults,noatime  0  0
LABEL=the-btrfs-fs-device   /var/www             btrfs subvol=/var/www,noatime        0  0
LABEL=the-btrfs-fs-device   /var/lib/postgresql  btrfs subvol=/postgres,noatime       0  0
