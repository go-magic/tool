# 介绍
CentOS7.0安装mysql教程,执行 yum install mysql-server 的时候可能出错或变慢,可以尝试ctrl + c多试几次。

# 安装
- 下载yum repo配置文件(如果提示-bash: wget: command not found,请先安装wget)

```
//yum install wget
wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
```
- 安装repo

```
rpm -ivh mysql57-community-release-el7-9.noarch.rpm
cd /etc/yum.repos.d/
```

- 安装mysql

```
yum install mysql-server
如果出现：
    mysql-community-libs-5.7.30-1.el7.x86_64: [Errno 256] No more mirrors to try.
    mysql-community-common-5.7.30-1.el7.x86_64: [Errno 256] No more mirrors to try.
多试几次 yum install mysql-server
```

- 启动msyql

```
systemctl start mysqld
```

- 获取初始密码
```
grep 'temporary password' /var/log/mysqld.log
//root@localhost: xxxxxxxxx
//xxxxxxxxx为初始密码,后面修改密码要用
```

- 修改密码
```
mysql -u root -p 
回车输入 xxxxxxxxx
set password=password("yourpassword");
```

- 外部不允许连接mysql
```
use mysql;
update user set host = '%' where user ='root';
flush privileges;
```