# Ubuntu 20.04

### Clone repository

`sudo git clone https://github.com/halftone72/bigcrate.git`

Alternative: Use /mnt/cratedisk01/bigcrate

### Install VS Code

```
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install code # or code-insiders
```

Restart

Alternative: Install from Ubuntu Store. Search for `Visual Studio Code`

### Sign into Firefox

Log into Bitwarden and close other extension info windows after sync

### Install some stuff

`sudo apt install samba openssh-server mergerfs glances lynx make gcc git`

___Set up mergerFS and Snapraid now. See 2 Storage Install___ 