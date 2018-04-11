# CentOS 7  安装 openresty

你可以在你的 CentOS 系统中添加 openresty 资源库，这样就可以方便的安装我们的包，以后也可以更新（通过 yum update 命令）。

添加资源库，你只用创建一个名为 /etc/yum.repos.d/OpenResty.repo 的文件，内容如下:

```php
[openresty]
name=Official OpenResty Repository
baseurl=https://copr-be.cloud.fedoraproject.org/results/openresty/openresty/epel-$releasever-$basearch/
skip_if_unavailable=True
gpgcheck=1
gpgkey=https://copr-be.cloud.fedoraproject.org/results/openresty/openresty/pubkey.gpg
enabled=1
enabled_metadata=1
```

然后你可以安装一个包，比如安装  openresty , 像这样:

```linux
yum install openresty
```

你可以这样操作openresty：

```
service openresty start | stop | restart
```
