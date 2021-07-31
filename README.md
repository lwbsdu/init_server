# init_server
# 如何完整的搭建并初始化服务
参考文章 https://www.cnblogs.com/xrg-blog/p/12801196.html
## mysql
1. 前提：服务器 centos ，已经装好了yum
2. 备份原数据库
mysqldump -uroot -p --database database_name >name.dump
3. 停止服务运行
systemctl stop mariadb && systemctl status mariadb

4. 卸载mariadb
```bash
yum remove -y mariadb &&yum remove -y mariadb-*
```

5. 查找安装信息并删除
```bash
yun list installed |grep mariadb
rpm -qa |grep mariadb
find / -name mysql
find / -name mariadb
删除配置文件：rm -f /etc/my.cnf
删除数据目录：rm -rf /var/lib/mysql
```
6.添加国内yum源

vim /etc/yum.repos.d/Mariadb.repo
添加以下内容：
```bash
[mariadb]
name = MariaDB
baseurl=https://mirrors.ustc.edu.cn/mariadb/yum/10.2/centos7-amd64
gpgkey=https://mirrors.ustc.edu.cn/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

7. 清除yum源缓存数据，并生成新的yum源数据缓存

yum clean all && yum makecache all
查看下载缓存信息：ll /var/cache/yum/x86_64/7/mariadb
8. 安装mariadb

yum install MariaDB-server MariaDB-client -y

启动并添加开机自启：

systemctl start mariadb
systemctl enable mariadb
9. mariadb初始化

mysql_secure_installation
一般建议按以下进行配置：
```bash
Enter current password for root (enter for none): Just press the Enter button
Set root password? [Y/n]: Y
New password: your-MariaDB-root-password
Re-enter new password: your-MariaDB-root-password
Remove anonymous users? [Y/n]: Y
Disallow root login remotely? [Y/n]: n
Remove test database and access to it? [Y/n]: Y
Reload privilege tables now? [Y/n]: Y
```
