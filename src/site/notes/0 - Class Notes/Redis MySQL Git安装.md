---
{"dg-publish":true,"permalink":"/0-class-notes/redis-my-sql-git/","dgPassFrontmatter":true,"created":"2023-10-03T22:20:19.488+08:00"}
---

### 网络工具和wget安装

```bash
yum -y install net-tools
yum -y install wget
```

### Redis安装

```bash
yum -y install redis
启动：systemctl start redis
设置开机自启动：systemctl enable redis
远程访问及密码：
		/etc/redis.conf
				sed -i 's/^bind 127/#bind 127/g' /etc/redis.conf
				sed -i '/^#requirepass/crequirepass qwe123!@#' /etc/redis.conf
防火墙：
		firewall-cmd --zone=public --add-port=6379/tcp --permanent
		firewall-cmd --reload
```
显示所有进程信息，并在输出中筛选包含 "redis" 字符串的行

```bash
ps -aux | grep redis
```

列出所有已安装的软件包

```bash
yum list installed | grep redis
```

### mysql安装

```bash
wget https://cdn.mysql.com/archives/mysql-8.0/mysql-8.0.19-1.el8.x86_64.rpm-bundle.tar
```

解压缩

```bash
tar -xvf mysql-8.0.19-1.el8.x86_64.rpm-bundle.tar
```

```bash
yum install mysql-community-common-8.0.19-1.el8.x86_64.rpm
```

```bash
yum install mysql-community-libs-8.0.19-1.el8.x86_64.rpm
```

```bash
yum install mysql-community-client-8.0.19-1.el8.x86_64.rpm
```

```bash
yum install mysql-community-server-8.0.19-1.el8.x86_64.rpm
```

启动mysql

```bash
systemctl restart mysqld
```

设置开机自启动

```bash
systemctl enable mysqld
```

获取mysql初始密码执行：

```bash
cat /var/log/mysqld.log | grep password
```

A temporary password is generated for root@localhost: **_uIlf,AHC7wG**

登录mysql

```bash
mysql -uroot -p
```

Enter password： **_uIlf,AHC7wG**

```sql
alter user 'root'@'localhost' IDENTIFIED BY 'Qwe123!@#';
```

开发远程访问

```sql
use mysql;
```

```sql
update user set Host='%'where user='root';
```

开放端口3306：

```bash
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```

```bash
firewall-cmd --reload
```

### 安装git
[[0 - Class Notes/Git常用命令\|Git常用命令]]

```bash
yum -y install git
```

在`/home`目录下创建`repo`文件夹，进入`repo`目录下

创建仓库

```bash
git init --bare book-ms-ui.git
```

```bash
git init --bare book-ms-interface.git
```
