# Gaming Setup

### Lutris

```
sudo add-apt-repository ppa:lutris-team/lutris
sudo apt-get update
sudo apt-get install lutris
```
Install Epic Game Store through the launchers setup (click on gear)

### Steam

`sudo apt install steam-installer`

**Note: this only installs the installer. Installer must be run to download and install updates and dependencies, including WINE**


# Visual Studio Code

```
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install code
```

# VirtualBox

### Install
Download and install VirtualBox from https://www.virtualbox.org/wiki/Downloads
Extension pack is available from same link. Use if you need to use one of the extensions (https://www.virtualbox.org/manual/ch01.html#intro-installing)

### Install Guest Additions (CLI-based VM)

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
