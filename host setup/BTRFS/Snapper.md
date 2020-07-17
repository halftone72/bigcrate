# Setup and configuration

### Create a new configuration

Create a new snapper configuration named config for the btrfs subvolume at /path/to/subvolume

`snapper -c config create-config /path/to/subvolume`
This will:
- create a configuration file at /etc/snapper/configs/config based on the default template from /etc/snapper/config-templates.
- create a subvolume at /path/to/subvolume/.snapshots where future snapshots of for this configuration will be stored. A snapshot's path is /path/to/subvolume/.snapshots/#/snapshot, where # is the snapshot number.
- add config to SNAPPER_CONFIGS in /etc/conf.d/snapper.

At this point, the configuration is active. If your cron daemon is running, snapper will take #Automatic timeline snapshots. If you do not use a cron daemon, you will need to use the systemd service and timer. See #Enable/disable.

See man page for snapper-configs.

# Reference

Snapper
http://snapper.io/

Arch a Snapper reference 
https://wiki.archlinux.org/index.php/Snapper
