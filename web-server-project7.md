# Working on the web servers - Using 3 webservers

### Installed nfs clients on the web instances ###

### Created directory `/var/www/` and mounted NFS `/mnt/apps` on it ###

```
sudo mount -t nfs -o rw,nosuid 172.31.30.203:/mnt/apps /var/www
on `etc/fstab` 172.31.30.203:/mnt/apps /var/www nfs defaults 0 0
```

df -h:

```
[root@ip-172-31-27-47 ~]# df -h
Filesystem               Size  Used Avail Use% Mounted on
devtmpfs                 368M     0  368M   0% /dev
tmpfs                    401M     0  401M   0% /dev/shm
tmpfs                    401M   21M  381M   6% /run
tmpfs                    401M     0  401M   0% /sys/fs/cgroup
/dev/xvda2                10G  2.9G  7.2G  29% /
tmpfs                     81M     0   81M   0% /run/user/1000
172.31.30.203:/mnt/apps   10G  104M  9.9G   2% /var/www
```

