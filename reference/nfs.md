# NFS

### Set up NFS packages
`sudo apt install nfs-kernel-server`

Edit `sudo nano /etc/exports` and add the following line

`/mnt/storage *(ro,async,no_wdelay,all_squash,insecure,anonuid=0,anongid=0,fsid=0)`

This will allow access to all mounts to any device on the home network. Replace wildcard with octet detail for specific device access (be sure to reserve IPs on the home network as they will change on reboot.) 

### Restart the service to reread exports

`sudo exportfs -ra`

---

# Reference

https://www.linuxbabe.com/ubuntu/nfs-share

https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-16-04

