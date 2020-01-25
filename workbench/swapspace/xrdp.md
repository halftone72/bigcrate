# xrdp

**NOTE:** _The information here is known working,but needs review and better documentation_

 _These notes were written to run KDE Plasma on Ubuntu Server and confirmed working_
 
```
echo "startkde" > ~/.xsession
D=/usr/share/plasma:/usr/local/share:/usr/share:/var/lib/snapd/desktop
C=/etc/xdg/xdg-plasma:/etc/xdg
 C=${C}:/usr/share/kubuntu-default-settings/kf5-settings
cat <<EOF > ~/.xsessionrc
export XDG_SESSION_DESKTOP=KDE
export XDG_DATA_DIRS=${D}
export XDG_CONFIG_DIRS=${C}
EOF
```

```
cat <<EOF | \
  sudo tee /etc/polkit-1/localauthority/50-local.d/xrdp-NetworkManager.pkla
[Networkmanager]
Identity=unix-group:sudo
Action=org.freedesktop.NetworkManager.network-control
ResultAny=yes
ResultInactive=yes
ResultActive=yes
EOF
```

```
cat <<EOF | \
  sudo tee /etc/polkit-1/localauthority/50-local.d/xrdp-packagekit.pkla
[Networkmanager]
Identity=unix-group:sudo
Action=org.freedesktop.packagekit.system-sources-refresh
ResultAny=yes
ResultInactive=auth_admin
ResultActive=yes
EOF
```

---

# Reference

https://www.hiroom2.com/2018/05/07/ubuntu-1804-xrdp-kde-en/

https://www.hiroom2.com/2018/05/06/ubuntu-1804-kde-en/

https://www.hiroom2.com/2018/04/29/ubuntu-1804-xrdp-gnome-en/

