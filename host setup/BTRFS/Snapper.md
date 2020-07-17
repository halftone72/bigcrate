# Setup and configuration

### Create a new configuration

Create a new snapper configuration named config for the btrfs subvolume at /path/to/subvolume

`snapper -c config_name create-config /path/to/subvolume`

Example:
`snapper -c root create-config / `

This will:
- create a configuration file at /etc/snapper/configs/config based on the default template from /etc/snapper/config-templates.
- create a subvolume at /path/to/subvolume/.snapshots where future snapshots of for this configuration will be stored. A snapshot's path is /path/to/subvolume/.snapshots/#/snapshot, where # is the snapshot number.
- add config to SNAPPER_CONFIGS in /etc/conf.d/snapper.

At this point, the configuration is active. If your cron daemon is running, snapper will take Automatic timeline snapshots

List configurations
`sudo snapper list-configs`

List snapshots for configuration
`sudo snapper config_name list`

Create simple snapshot
`snapper -c config_name create --description desc`

Create pre/post snapshots
`snapper -c config_name create --command cmd`
cmd = command to be wrapped by snapshots

Delete snapshot
`snapper -c config_name delete N`
N = snapshot number

### Automatic timeline snapshots

Enable/disable

If you have a cron daemon, this feature should start automatically. To disable it, edit the configuration file corresponding with the subvolume you do not want to have this feature and set:

`TIMELINE_CREATE="no"`

Config file
`/etc/snapper/configs/config_name`

```
TIMELINE_MIN_AGE="1800"
TIMELINE_LIMIT_HOURLY="5"
TIMELINE_LIMIT_DAILY="7"
TIMELINE_LIMIT_WEEKLY="0"
TIMELINE_LIMIT_MONTHLY="0"
TIMELINE_LIMIT_YEARLY="0"
```
Defines snapshot retention. Default is 10 hourly, 10 daily, 10 monthly and 10 yearly snapshots. Example above is 5 hourly snapshots, 7 daily ones, no monthly and no yearly.

# Reference

Snapper
http://snapper.io/

Arch Snapper reference 
https://wiki.archlinux.org/index.php/Snapper
