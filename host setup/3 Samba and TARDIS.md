# TARDISL13 (latest stable)

Make sure that prerequisites of filesystem and samba are complete first.
_mount drives, including mergerfs, sudo apt install samba_

Add connecting user

`sudo adduser thedoctor`

Add user and password for Samba

`sudo smbpasswd -a thedoctor`
`sudo smbpasswd -a halftone72`

Deploy updated smb.conf

```
sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.bak
sudo cp /mnt/cratedisk01/bigcrate/host\ setup/config/smb.conf /etc/samba/smb.conf
```

Restart samba

`sudo service smbd restart`

---

# Reference and Notes

_Based on instructions for original TARDIS (Time Machine share via SMB) image. Lucky 13_

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

