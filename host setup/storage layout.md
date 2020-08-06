* - mount points,create on new install


/ (root)                    /dev/nvme0n1p1
  +-- mnt  
  |  *+-- DC 
  |   |  *+-- cratedisk01   /dev/sdb
  |   |  *+-- cratedisk02   /dev/sdd
  |   |  *+-- cratedisk03   /dev/sde
  |   |  *+-- crateparity01 /dev/sdc
  |   |  *+-- vmrepo        /dev/sda 
  |   |  *\-- vmdisk        /dev/nvmexxxxx
  |  *+-- nas   (mergerfs volume mount point)
  |   |   +-- appstore 
  |   |   +-- arcade   
  |   |   +-- archive 
  |   |   +-- hlos_storage
  |   |   +-- junkdrawer
  |   |   +-- library
  |   |   +-- loading_dock
  |   |   +-- media_center
  |   |   +-- outer_realm
  |   |   \-- tardis 
