# Installation

`sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virt-manager`

# Setup network bridge

Modify interfaces 
`sudo nano /etc/network/interfaces`

Add

```
auto br0

iface enp5s0 inet manual

iface br0 inet dhcp
    bridge_ports enp5s0
    bridge-ifaces enp5s0
    up inconfig enp5s0 up
```

Add user to libvirt groups
`sudo adduser halftone72 libvirt`
`sudo adduser halftone72 libvirt-qemu`

restart

NOTE: bridged networking not working for Multipass VM. Manually created VMs work fine.

---

# Reference

Install And Set Up KVM On Ubuntu 20.04 Focal Fossa Linux
https://linuxconfig.org/install-and-set-up-kvm-on-ubuntu-20-04-focal-fossa-linux