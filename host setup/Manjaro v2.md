Manjaro notes

Install on nvme drive using defaults

Update after reboot
`sudo pacman -Syu`

Reboot

Turn off sleep
Right-click on desktop>Settings>Power>Automatic Suspend

Enable sshd
`sudo systemctl enable sshd.service`
`sudo systemctl start sshd.service`

Enable access to AUR
`sudo pacman -Syu yay`

Install build utilities
`sudo pacman -Syu base-devel`

Install Samba
`sudo pamac install nautilus-share manjaro-settings-samba`

Enable service
`sudo systemctl enable smb nmb

Setup mount points for storage
`sudo mkdir /mnt/storage /mnt/appstore /mnt/arcade /mnt/archive /mnt/junkdrawer /mnt/loading_dock /mnt/media_center /mnt/outer_realm /mnt/library /mnt/tardis`

Install dnsutils (for dig)
`sudo pamac install dnsutils`

---

# Reference

https://tutorialforlinux.com/2020/02/06/how-to-install-radeon-rx-570-driver-on-manjaro-linux-18-x/2/


[outer_realm]
    comment = outer_realm
    path = /mnt/outer_realm
    browseable = yes
    writeable = yes
    create mask = 0777
    directory mask = 0777
    valid users = halftone72


