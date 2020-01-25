# TARDISL13 (latest stable)
_Based on instructions for original TARDIS (Time Machine share via SMB) image. Lucky 13_

Make sure that prerequisites of filesystem and samba are complete first.
_mount drives, including mergerfs, sudo apt install samba_

Add connecting user

`sudo adduser thedoctor`

Add user and password for Samba

`sudo smbpasswd -a thedoctor`

Add Samba share entry with Time Machine specifics

**NOTE:** Replace /etc/samba/smb.conf with github copy. Below is for reference only.

`sudo nano /etc/samba/smb.conf`

Add at end of file:

```
[time machine]
    comment = Time Machine
    path = /mnt/storage/tardis
    browseable = yes
    writeable = yes
    create mask = 0777
    directory mask = 0777
    spotlight = yes
    vfs objects = catia fruit streams_xattr
    fruit:aapl = yes
    fruit:time machine = yes
```

Restart samba

`sudo service smbd restart`

