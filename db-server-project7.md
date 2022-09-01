# Working on MYSQL Server instance

### Provisioned an Ubuntu EC2 instance ###

### Installed mysql-server, created database named `webaccess` and DB `tooling`.

```
root@ip-172-31-95-153:/home/ubuntu/my-db-dir# mysql -u webaccess -p 
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 13
Server version: 8.0.30-0ubuntu0.20.04.2 (Ubuntu)

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| tooling            |
+--------------------+
5 rows in set (0.02 sec)

mysql> SELECT USER, HOST from mysql.user;
+------------------+-----------+
| USER             | HOST      |
+------------------+-----------+
| webaccess        | %         |
| debian-sys-maint | localhost |
| mysql.infoschema | localhost |
| mysql.session    | localhost |
| mysql.sys        | localhost |
| root             | localhost |
+------------------+-----------+
6 rows in set (0.00 sec)

mysql> exit
```

