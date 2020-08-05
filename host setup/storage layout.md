/mnt  
  +-- DC 
  |   \-- cratedisk01   /dev/sdb
  |   \-- cratedisk02   /dev/sdd
  |   \-- cratedisk03   /dev/sde
  |   \-- crateparity01 /dev/sdc
  |   \-- vmworld       /dev/sda
  +-- nas   (mergerfs volume mount point)
  
  
  +-- var        (directory)
  |   \-- www    (subvolume root directory, to be mounted at /var/www)
  \-- postgres   (subvolume root directory, to be mounted at /var/lib/postgresql)
