Get device detail information

`sudo hdparm -I /dev/sda`

Get device UUID

`sudo blkid`

Show device list and mountpoints

`sudo lsblk`

Show mounted devices with space information

`sudo df -h`

Show space used by a directory

`sudo du -sh /directory`

To debug your system, run these commands:

1. systemctl --failed
2. Run systemctl status with the names that was in the result of the previous command.
3. sudo journalctl -xb


## RSYNC
`sudo rsync -avh --progress /media/4tb/the_outer_realm /media/outer_realm/legacy`
`sudo rsync -avh --progress /media/4tb2 /media/outer_realm/sorted`

## Samba
Save and restart samba
`sudo service smbd restart`
Create samba account for Linux user
`sudo smbpasswd -a username`