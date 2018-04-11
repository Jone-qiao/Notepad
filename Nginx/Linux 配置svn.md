# Linux 配置svn

## 创建项目的操作

​	进到项目的svn库路径

​	假设创建项目 project

​	svnadmin create project

## 修改项目配置文件

#### cd project/conf

​	修改三个文件 authz ,passwd ,svnserve.conf，该三项针对不同的项目内容不一样

#### vi authz

​	文件原有的内容全都注释掉，添加组成员并设置权限

​	project = admin1,admin2,admin3

​	\* = rw

**	************************************************

#### vi passwd

​	在[users]下面的位置添加成员的信息,对应格式：账号 = 密码

​	admin1 = 1234

​	admin2 = 1234

​	admin3 = 1234

**	**********************************************

#### vi svnserve.conf

​	去掉三个注释及当前行前面所有的空格 即可

​	anon-access = read

​	auth-access = write

​	password-db = passwd