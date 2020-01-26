# Oracle VirtualBox v6.1

Download and install VirtualBox, then install the extension pack

### Disable IPv6 NOT REQUIRED - REFERENCE ONLY

```
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
```

### Install Guest Additions:

1. Start VirtualBox.
2. Start the host in question.
3. Once the host has booted, click Devices | Insert Guest Additions CD Image.
4. Log in to your guest server.
5. Mount the CD-ROM with the command sudo mount /dev/cdrom /media/cdrom.
6. Change into the mounted directory with the command cd /media/cdrom.
7. Install the necessary dependencies with the command sudo apt-get install -y dkms build-essential linux-headers-generic linux-headers-$(uname -r).
8. Change to the root user with the command sudo su.
9. Install the Guest Additions package with the command ./VBoxLinuxAdditions.run.
10. Allow the installation to complete.

---

# Reference

https://www.virtualbox.org/wiki/Downloads