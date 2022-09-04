# Working on the 2 web servers

### Installed nfs clients on the web instances ###

### Created directory `/var/www/` and `/var/log/`, then mounted NFS `/mnt/apps` and `/mnt/logs` on them ###

```
mount -t nfs -o rw,nosuid 172.31.30.203:/mnt/apps /var/www
mount -t nfs -o rw,nosuid 172.31.30.203:/mnt/logs /var/log
on `etc/fstab` 172.31.30.203:/mnt/apps /var/www nfs defaults 0 0 172.31.30.203:/mnt/logss /var/log nfs defaults 0 0
```

df -h:

```
Filesystem               Size  Used Avail Use% Mounted on
devtmpfs                 368M     0  368M   0% /dev
tmpfs                    401M     0  401M   0% /dev/shm
tmpfs                    401M   21M  381M   6% /run
tmpfs                    401M     0  401M   0% /sys/fs/cgroup
/dev/xvda2                10G  2.9G  7.2G  29% /
tmpfs                     81M     0   81M   0% /run/user/1000
172.31.30.203:/mnt/apps   10G  104M  9.9G   2% /var/www
172.31.30.203:/mnt/logs  9.0G   97M  8.9G   2% /var/log
```

### Updating the website’s configuration to connect to the database ###

In /var/www/html/functions.php (replacing the password with xxxxxx)

```
// connect to database
$db = mysqli_connect('172.31.95.153', 'webaccess', 'xxxxxxxx', 'tooling');
```

### Inserting new user into table `users` in database `tooling` ###

```

INSERT INTO users (id, username, password, email, user_type, status) VALUES
-> (1, 'myuser', 'xxxxxxx', 'xxxxx@gmail.com', 'admin', '2');
```

# ALL DONE

<img src="final.png" alt="final look" title="My website" style="display: inline-block; margin: 0 auto; max-width: 300px"/>
