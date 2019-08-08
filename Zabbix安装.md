# Zabbix安装

## 基本安装

### yum源配置

​		配置阿里云的Zabbix源

```sh
rpm -ivh https://mirrors.aliyun.com/zabbix/zabbix/3.0/rhel/7/x86_64/zabbix-release-3.0-1.el7.noarch.rpm
```

### 安装相关软件

```sh
yum install zabbix-server zabbix-web zabbix-server-mysql zabbix-web-mysql mariadb-server mariadb zabbix-agent -y
```

### 修改PHP时区配置

```sh
vim /etc/httpd/conf.d/zabbix.conf
```

![1564669394896](picture\1564669394896.png)

## 数据库配置

### 启动数据库

CentOS7中mysql变为mariadb

```sh
systemctl start mariadb
```

### 创建Zabbix所用的数据库

```mysql
[root@localhost ~]# mysql
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 8
Server version: 10.3.10-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> create database zabbix character set utf8 collate utf8_bin;
Query OK, 1 row affected (0.000 sec)

MariaDB [(none)]> grant all on zabbix.* to zabbix@'localhost' identified by '123456';
Query OK, 0 rows affected (0.001 sec)

MariaDB [(none)]> exit
Bye

```

```sh
cd /usr/share/doc/zabbix-server-mysql-3.0.28/

zcat create.sql.gz | mysql -uzabbix -p123456 zabbix
```



### 修改Zabbix配置

```sh
vim /etc/zabbix/zabbix_server.conf
DBHost=localhost         #数据库所在主机
DBName=zabbix            #数据库名
DBUser=zabbix            #数据库用户
DBPassword=123456        #数据库密码
```

### 启动Zabbix及http

```
systemctl start zabbix-server

systemctl start httpd
```

### 配置Zabbix_agentd.conf，修改server：IP地址

```sh
vim /etc/zabbix/zabbix_agentd.conf
```



### Zabbix登录

用户名：Admin

密码：zabbix

记得登录后先修改密码

