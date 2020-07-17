# Install

Install dependencies
`sudo apt install snapper python`

Clone repository
`git clone https://github.com/agronick/apt-btrfs-snapper.git`

Build and install

```
cd apt-btrfs-snapper
sudo ./setup.py build
sudo ./setup.py install
```

Run `apt-btrfs-snapper` and confirm install was successful

Test further by installing or removing a package via `apt install`. Once complete, confirm a pre and post snap were taken with Snapper (apt-btrfs-snapper does not appear to return a list of snapshots):
`sudo snapper list`

Rollback snapshot
`sudo apt-btrfs-snapper rollback N`
N = snapshot number

# Reference

apt-btrfs-snapshot pages
https://github.com/agronick/apt-btrfs-snapper
https://poisonpacket.wordpress.com/2015/06/06/apt-btrfs-snapper-apt-get-snapper-snapshots/
