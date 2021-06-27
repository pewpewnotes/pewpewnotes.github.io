## Icinga Installation

In order to prepare for the configuration we need to install some prerequisites like icinga and epel repositories

You should either "sudo su -" or append the "sudo" prefix to get these installed.
``` bash
yum install https://packages.icinga.com/epel/icinga-rpm-release-7-latest.noarch.rpm -y 
yum install epel-release -y
```

After this we are able to install, start and enable icinga.

``` bash
yum install icinga2 -y 
systemctl enable icinga2
systemctl start icinga2
```
Q: How about non systemd systems? Is that possible to install and configure on non systemd? 
Q: Why is icinga only on centos/redhat like os? 
Q: what is icinga? XD

``` bash
yum install nagios-plugins-all -y 
```
Had issues, look below for common fixes.
1. https://bugzilla.redhat.com/show_bug.cgi?id=1837397
2. https://forums.centos.org/viewtopic.php?t=74458 
	

```
yum install icinga2-selinux -y
systemctl restart icinga2
```

Q: What is SElinux
Security-Enhanced Linux is a Linux kernel security module that provides a mechanism for supporting
access control security policies, including mandatory access controls. SELinux is a set of kernel
modifications and user-space tools that have been added to various Linux distributions. Its
architecture strives to separate enforcement of security decisions from the security policy, and
streamlines the amount of software involved with security policy enforcement.

Database is necessary for storing files and stuffs, and then we need the plugin. 
` yum install mariadb-server mariadb icinga2-ido-mysql -y
`
Now to start the mariadb

`systemctl enable mariadb
systemctl start mariadb`

mysql_secure_installation doesn't work, here we go. 

(not really, I am just an idiot arghs)

``
[root@localhost ~]# mysqladmin -u root password 123456
[root@localhost ~]# mysql -u root -p

After that we create icinga db, and grant access to icinga (like pewpew!)

MariaDB [(none)]> CREATE DATABASE icinga;
Query OK, 1 row affected (0.001 sec)

MariaDB [(none)]> GRANT SELECT, INSERT, UPDATE, DELETE, DROP, CREATE VIEW, INDEX, EXECUTE ON icinga.* TO 'icinga'@'localhost' IDENTIFIED BY 'icinga';
Query OK, 0 rows affected (0.001 sec)


Now we need to apply the schema to our icinga database.
``
``
┌──────────────────────────────────────────────────────────────────────────────┐
│mysql -u root -p                                                              │
│                                                                              │
│CREATE DATABASE icinga;                                                       │
│GRANT SELECT, INSERT, UPDATE, DELETE, DROP, CREATE VIEW, INDEX, EXECUTE ON    │
│icinga.* TO 'icinga'@'localhost' IDENTIFIED BY 'icinga';                      │
│quit                                                                          │
└──────────────────────────────────────────────────────────────────────────────┘
``
Now we apply the schema to our icinga database.                                 
``
┌──────────────────────────────────────────────────────────────────────────────┐
│mysql -u root -p icinga < /usr/share/icinga2-ido-mysql/schema/mysql.sql       │
└──────────────────────────────────────────────────────────────────────────────┘
``
NOW the best part, enable the features and pewpew!
[root@localhost ~]# icinga2 feature enable ido-mysql
Enabling feature ido-mysql. Make sure to restart Icinga 2 for these changes to take effect.
[root@localhost ~]# systemctl restart icinga2



Now we move on to configure web ui. 


q: what is the SCL package? 
Red Hat promises software compatibility for the life of any given RHEL release. It will not upgrade major applications mid-release. For example, if RHEL 6.0 contains PostgreSQL 8.4, RHEL 6.7 cannot move to PostgreSQL 9.4. Too many applications will break.

Yet some customers require the upgraded software. By way of an answer, Red Hat and the CentOS project have published what are called Software Collections (SCL). Packages provided in the SCL repositories typically provide newer versions of software that play a key role in the Linux world: Python, Apache, PostgreSQL, MySQL, gcc, etc.

Now for updated stuffs: 

``yum install centos-release-scl -y``


Now we need webserver and web/cli commands
```
[root@localhost ~]# yum install centos-release-scl -y  
Last metadata expiration check: 1:40:29 ago on Tue 21 Jul 2020 04:44:41 AM UTC.
No match for argument: centos-release-scl
Error: Unable to find a match
[root@localhost ~]# yum install centos-release-scl -y  
Last metadata expiration check: 1:45:20 ago on Tue 21 Jul 2020 04:44:41 AM UTC.
No match for argument: centos-release-scl
Error: Unable to find a match
```

Related link: https://forums.centos.org/viewtopic.php?f=13&t=59280

Now this was very irritating
Nevertheless, It seems that this is not really necessary, 
probably because scl is integrated in COS8

```
yum install icingaweb2 icingacli -y
```
Done!
```
┌──────────────────────────────────────────────────────────────────────────────┐
│yum install httpd -y                                                          │
│systemctl start httpd.service                                                 │
│systemctl enable httpd.service                                                │
└──────────────────────────────────────────────────────────────────────────────┘
```
```
We need to allow http service through the firewall permanently.

┌──────────────────────────────────────────────────────────────────────────────┐
│firewall-cmd –permanent –add-service=http                                     │
└──────────────────────────────────────────────────────────────────────────────┘
```

Well my fw is down and not that I am complaining :P 
[root@localhost ~]# firewall-cmd --permanent --add-service=http
FirewallD is not running

Inchinga needs latest version of php for processing needs

```
systemctl start rh-php71-php-fpm.service
systemctl enable rh-php71-php-fpm.service
```
Well service not found, (seriously?)

So I am trying yum install php-* :P
Well that kinda worked and then next step was: 
```
Complete!
[root@localhost ~]# systemctl start rh-php71-php-frm.service
Failed to start rh-php71-php-frm.service: Unit rh-php71-php-frm.service not found.
[root@localhost ~]# dnf module enable php:remi-7.4
Last metadata expiration check: 0:15:22 ago on Tue 21 Jul 2020 06:45:36 AM UTC.
Error: Problems in request:
missing groups or modules: php:remi-7.4
[root@localhost ~]# dnf install php php-opcache php-gd php-curl php-mysqlnd
Last metadata expiration check: 0:15:51 ago on Tue 21 Jul 2020 06:45:36 AM UTC.
Package php-7.2.24-1.module_el8.2.0+313+b04d0a66.x86_64 is already installed.
Package php-opcache-7.2.24-1.module_el8.2.0+313+b04d0a66.x86_64 is already installed.
Package php-gd-7.2.24-1.module_el8.2.0+313+b04d0a66.x86_64 is already installed.
Package php-common-7.2.24-1.module_el8.2.0+313+b04d0a66.x86_64 is already installed.
Package php-mysqlnd-7.2.24-1.module_el8.2.0+313+b04d0a66.x86_64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!
[root@localhost ~]# sudo systemctl enable --now php-fpm
Created symlink /etc/systemd/system/multi-user.target.wants/php-fpm.service → /usr/lib/systemd/system/php-fpm.service.
[root@localhost ~]#

```

Gotta change icinga2 root context prevent disabling of selinux

```
[root@localhost ~]# chcon -R -t httpd_sys_rw_content_t /etc/icingaweb2/
[root@localhost ~]# icingacli setup token create
The newly generated setup token is: 0e3218718d893388
[root@localhost ~]# icingacli setup token show
The current setup token is: 0e3218718d893388
[root@localhost ~]#
```
```
For this we need to issue the following commands.

┌──────────────────────────────────────────────────────────────────────────────┐
│icinga2 api setup                                                             │
└──────────────────────────────────────────────────────────────────────────────┘

Then add the following content to this file: vim
/etc/icinga2/conf.d/api-users.conf

┌──────────────────────────────────────────────────────────────────────────────┐
│object ApiUser "icingaweb2" {                                                 │
│  password = "Wijsn8Z9eRs5E25d"                                               │
│  permissions = [ "status/query", "actions/*", "objects/modify/*",            │
│"objects/query/*" ]                                                           │
│}                                                                             │
└──────────────────────────────────────────────────────────────────────────────┘

Then restart the icinga2.

```
```
Then restart the icinga2.

┌──────────────────────────────────────────────────────────────────────────────┐
│systemctl restart icinga2                                                     │
└──────────────────────────────────────────────────────────────────────────────┘

After this we can enter the necessary details and the validation will succeed.
```


