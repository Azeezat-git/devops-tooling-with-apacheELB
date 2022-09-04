# Configuring Apache As A Load Balancer


**Instance:** Launched an EC2 Ubuntu server and installed apache 2 on it

### apache service running ###

```
root@ip-172-31-25-157:/home/ubuntu# sudo systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor prese>
     Active: active (running) since Sun 2022-09-04 14:03:26 UTC; 31min ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 7277 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SU>
   Main PID: 7281 (apache2)
      Tasks: 55 (limit: 1145)
     Memory: 5.3M
     CGroup: /system.slice/apache2.service
             ├─7281 /usr/sbin/apache2 -k start
             ├─7282 /usr/sbin/apache2 -k start
             └─7283 /usr/sbin/apache2 -k start

Sep 04 14:03:26 ip-172-31-25-157 systemd[1]: Starting The Apache HTTP Server...
Sep 04 14:03:26 ip-172-31-25-157 systemd[1]: Started The Apache HTTP Server.
```

### Configuring load balancing by editing `/etc/apache2/sites-available/000-default.conf` ###

```
        <Proxy "balancer://mycluster">
               BalancerMember http://172.31.23.136:80 loadfactor=5 timeout=1
               BalancerMember http://172.31.22.152:80 loadfactor=5 timeout=1
               ProxySet lbmethod=bytraffic
               # ProxySet lbmethod=byrequests
        </Proxy>

        ProxyPreserveHost On
        ProxyPass / balancer://mycluster/
        ProxyPassReverse / balancer://mycluster/
```

**Tested connection successfully on http://<Load-Balancer-Public-IP-Address-or-Public-DNS-Name>/index.php**

### Configuring Local DNS Names Resolution ###

**Added the below in `/etc/hosts` file**

```
172.31.23.136 Web1
172.31.22.152 Web2
```

**Then updated `/etc/apache2/sites-available/000-default.conf`**

```
BalancerMember http://Web1:80 loadfactor=5 timeout=1
BalancerMember http://Web2:80 loadfactor=5 timeout=1
```

# Final 


<img src="finish.png" alt="final look" title="My site with apache LB" style="display: inline-block; margin: 0 auto; max-width: 300px"/>


