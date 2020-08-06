Setup Snapd if not already installed
`sudo apt install snapd`

Install Multipass
`sudo snap install multipass`

Setup Multipass to use libvirt

```
# you'll need to stop all the instances first
$ multipass stop --all

# and tell Multipass to use libvirt
$ sudo multipass set local.driver=libvirt
```

If there is an error connecting to libvirt from Multipass:

`snap connect multipass:libvirt`

---

# Reference

Using livbirt with Multipass
https://discourse.ubuntu.com/t/using-libvirt-in-multipass/13732

Unhelpful error when `libvirt` interface is disconnected #1554
https://github.com/canonical/multipass/issues/1554