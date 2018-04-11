# Centos7下使用yum安装mysql

CentOS7的yum源中默认好像是没有mysql的。为了解决这个问题，我们要先下载mysql的repo源。

## 下载mysql的repo源

```
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
```
## 安装mysql-community-release-el7-5.noarch.rpm包

```
rpm -ivh mysql-community-release-el7-5.noarch.rpm
```

安装这个包后，会获得两个mysql的yum repo源：

/etc/yum.repos.d/mysql-community.repo；

/etc/yum.repos.d/mysql-community-source.repo；

## 安装mysql

```
yum install mysql-server
```

根据步骤安装就可以了，不过安装完成后，没有密码，需要重置密码。

## 重置密码（重置密码前，首先要登录）

```
mysql -u root
```

```
mysql > use mysql;
mysql > update user set password=password('你的密码') where user='root';
mysql > exit;
```
## 开放远程访问

```
mysql -u root -p你的密码
```

```
mysql>use mysql;
mysql>update user set host = '%' where user = 'root';
mysql>flush privileges;
mysql>exit;
```