## marialDb初始化

### 创建用户
 1.前提是你有root权限
 命令：
 ```msyql
 use mysql;
 create user life identified by 'life';
 ```
 ### 为用户授权
 为用户指定制定的权限
 
 ```mysql
 grant insert,update,delete,select,create on *.* to 'life'@'%';
 flush privileges;
 ```
 
