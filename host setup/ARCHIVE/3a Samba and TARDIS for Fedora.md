# Fedora details

### SELinux config

```
setsebool -P samba_export_all_ro=1 samba_export_all_rw=1
getsebool -a | grep samba_export
semanage fcontext –a -t samba_share_t "/mnt/storage(/.*)?"
restorecon /mnt/storage
```

### Firewall config

```
firewall-cmd --permanent --add-service=samba
firewall-cmd --reload
```

---

# Reference and Notes

https://www.tecmint.com/setup-samba-file-sharing-for-linux-windows-clients/