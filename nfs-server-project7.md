# Working on the NFS storage  instance

### Added  new volumes and attached them to the nfs storage instance ###

**Description:** 3 new volumes (10GB each) were created in the same AZ as the storage instance. The volume were attached to the storage instance, then partitioned with gdisk utility

### Viewing the newly added LVM partitions ###

```
[root@ip-172-31-30-203 ec2-user]# lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0  10G  0 disk 
|-xvda1 202:1    0   1M  0 part 
`-xvda2 202:2    0  10G  0 part /
xvdf    202:80   0  10G  0 disk 
`-xvdf1 202:81   0  10G  0 part 
xvdg    202:96   0  10G  0 disk 
`-xvdg1 202:97   0  10G  0 part 
xvdh    202:112  0  10G  0 disk 
`-xvdh1 202:113  0  10G  0 part 
```

### Viewing the complete setup - After creating VG, PV and LV ###

```
[root@ip-172-31-30-203 ec2-user]# vgdisplay -v
  --- Volume group ---
  VG Name               nfs-vg
  System ID             
  Format                lvm2
  Metadata Areas        3
  Metadata Sequence No  4
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                3
  Open LV               0
  Max PV                0
  Cur PV                3
  Act PV                3
  VG Size               <29.99 GiB
  PE Size               4.00 MiB
  Total PE              7677
  Alloc PE / Size       7424 / 29.00 GiB
  Free  PE / Size       253 / 1012.00 MiB
  VG UUID               35T0w7-UCBF-TTTm-BkZ6-s0hS-VXKc-VP6dQE
   
  --- Logical volume ---
  LV Path                /dev/nfs-vg/lv-opt
  LV Name                lv-opt
  VG Name                nfs-vg
  LV UUID                0uqvuj-D0RS-dFRh-N9j1-D406-Ecrf-qM392c
  LV Write Access        read/write
  LV Creation host, time ip-172-31-30-203.ec2.internal, 2022-09-01 08:01:15 +0000
  LV Status              available
  # open                 0
  LV Size                10.00 GiB
  Current LE             2560
  Segments               2
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:0
   
  --- Logical volume ---
  LV Path                /dev/nfs-vg/lv-apps
  LV Name                lv-apps
  VG Name                nfs-vg
  LV UUID                uBH4Yl-ggKI-iAVU-ff47-3w3S-bmpj-IcCMRv
  LV Write Access        read/write
  LV Creation host, time ip-172-31-30-203.ec2.internal, 2022-09-01 08:01:29 +0000
  LV Status              available
  # open                 0
  LV Size                10.00 GiB
  Current LE             2560
  Segments               2
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:1
   
  --- Logical volume ---
  LV Path                /dev/nfs-vg/lv-logs
  LV Name                lv-logs
  VG Name                nfs-vg
  LV UUID                iANz5U-CwfR-nJe2-5gtk-vsfd-yDPu-vkxVK5
  LV Write Access        read/write
  LV Creation host, time ip-172-31-30-203.ec2.internal, 2022-09-01 08:01:45 +0000
  LV Status              available
  # open                 0
  LV Size                9.00 GiB
  Current LE             2304
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:2
   
  --- Physical volumes ---
  PV Name               /dev/xvdf1     
  PV UUID               x7fJky-VimS-Fdd3-Gy3B-CAOF-h9Ta-TeRDJ2
  PV Status             allocatable
  Total PE / Free PE    2559 / 0
   
  PV Name               /dev/xvdg1     
  PV UUID               IfdlvB-p73X-19T1-MqeC-UkoF-qcWJ-ZjoanJ
  PV Status             allocatable
  Total PE / Free PE    2559 / 253
   
  PV Name               /dev/xvdh1     
  PV UUID               bfdcEw-f9cX-AQcY-9PWY-DZIm-UiGP-05CeD1
  PV Status             allocatable
  Total PE / Free PE    2559 / 0
```

### After updating /etc/fstab ###

```
[root@ip-172-31-30-203 ec2-user]# df -h
Filesystem                    Size  Used Avail Use% Mounted on
devtmpfs                      368M     0  368M   0% /dev
tmpfs                         401M     0  401M   0% /dev/shm
tmpfs                         401M   11M  391M   3% /run
tmpfs                         401M     0  401M   0% /sys/fs/cgroup
/dev/xvda2                     10G  2.2G  7.9G  22% /
tmpfs                          81M     0   81M   0% /run/user/1000
/dev/mapper/nfs--vg-lv--opt    10G  104M  9.9G   2% /mnt/opt
/dev/mapper/nfs--vg-lv--apps   10G  104M  9.9G   2% /mnt/apps
/dev/mapper/nfs--vg-lv--logs  9.0G   97M  8.9G   2% /mnt/logs
```

   

