# NFS

### Set up NFS packages
`sudo apt install nfs-kernel-server`

manjaro - nfs-utils

Edit `sudo nano /etc/exports` and add the following line

`/mnt/storage *(ro,async,no_wdelay,all_squash,insecure,anonuid=0,anongid=0,fsid=0)`

This will allow access to all mounts to any device on the home network. Replace wildcard with octet detail for specific device access (be sure to reserve IPs on the home network as they will change on reboot.) 

### Restart the service to reread exports

`sudo exportfs -ra`

Manjaro - enable and start nfs-server.service
on client, make sure server name can be resolved as using IP instead of servername may cause a hang.

mount -t nfs -o vers=4 servername:/srv/nfs/music /mountpoint/on/client

fstab
servername:/music   /mountpoint/on/client   nfs   defaults,timeo=900,retrans=5,_netdev	0 0

---

# Reference and Notes

https://www.linuxbabe.com/ubuntu/nfs-share

https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-16-04

https://computingforgeeks.com/how-to-configure-nfs-client-on-ubuntu-debian-linux/
