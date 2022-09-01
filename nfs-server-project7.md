# Added 3 new volumes and attached them to the nfs storage instance
# Viewing the newly added LVM partitions 

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
