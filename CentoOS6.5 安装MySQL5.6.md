一、安装CentoOS6.5

1、修改网络

输入命令如下：
```
vi /etc/sysconfig/network-scripts/ifcfg-eth0
```
![图片.png](https://upload-images.jianshu.io/upload_images/2783386-c178122a85aaaf5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

修改ONBOOT为yes:

![图片.png](https://upload-images.jianshu.io/upload_images/2783386-d57a4ef56fef32b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

执行网络重启命令，使配置生效：

```
service network restart
```

2、修改ssh远程连接

输入如下命令：

```
vi /etc/ssh/sshd_config
```
![图片.png](https://upload-images.jianshu.io/upload_images/2783386-bcd5dc967c6ea0fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

修改UseDNS为no:

![图片.png](https://upload-images.jianshu.io/upload_images/2783386-7dc764234c71829c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

执行ssh重启命令，使配置生效：

```
service ssh restart
```

3、使用SecureCRT ssh登录root账户

查看ip地址

![图片.png](https://upload-images.jianshu.io/upload_images/2783386-b021ec6343e7f511.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

远程登录root账户

![图片.png](https://upload-images.jianshu.io/upload_images/2783386-ea1b7d7b7a483962.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


4、上传安装文件到CentoOS上

```
yum install vim lrzsz -y
```

```
rz
```
选择要上传的文件，等待上传即可。

[lrzsz（Linux服务器和window互传文件工具）](https://blog.csdn.net/wuzhangweiss/article/details/79842283)

二、安装MySQL5.6

1、修改my.cnf->/etc/my.cnf

```
vim install_mysql-5.6.36_x86_64.sh
```

![图片.png](https://upload-images.jianshu.io/upload_images/2783386-9a5750d5c464ba49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2、执行脚本：

```
sh install_mysql-5.6.36_x86_64.sh
```

3、执行
```
service mysqlId status
```
运行结果如下，则MySQL安装成功。

![图片.png](https://upload-images.jianshu.io/upload_images/2783386-32d12bd38900c5eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4、登录到mysql。

![图片.png](https://upload-images.jianshu.io/upload_images/2783386-66f87e2108be07a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

附录mysql-5.6.36_x86_64.sh：

```
#!/bin/bash
rpm -qa|grep libaio
if [[ $? -gt 0 ]] 
then
yum install -y libaio
fi
cPWD=`pwd`
echo $PWD >> /tmp/mysql.log
groupadd -r mysql
useradd -r -g mysql -s /sbin/nologin mysql
mkdir -p /data/mysql
chown -R mysql:mysql /data/mysql
tar zxvf mysql-5.6.36-linux-glibc2.5-x86_64.tar.gz -C /usr/local
ln -s /usr/local/mysql-5.6.36-linux-glibc2.5-x86_64 /usr/local/mysql
chown -R mysql.mysql /usr/local/mysql
chown -R mysql.mysql /usr/local/mysql-5.6.36-linux-glibc2.5-x86_64
cd /usr/local/mysql
scripts/mysql_install_db --basedir=/usr/local/mysql --datadir=/data/mysql --user=mysql
#ln -s /usr/local/mysql/bin/mysql /usr/bin/
#ln -s /usr/local/mysql/bin/mysqldump /usr/bin/mysqldump
#ln -s /usr/local/mysql/bin/mysqld_safe /usr/bin/mysqld_safe
cp support-files/mysql.server /etc/init.d/mysqld
chkconfig --add mysqld
chkconfig mysqld on
#/etc/my.cnf
cd $cPWD
echo `pwd` >> /tmp/mysql.log
rm -f /etc/my.cnf
cp conf/my.cnf /etc/my.cnf
service mysqld start
#/usr/local/mysql/bin/mysqld_safe --user=mysql &
/usr/local/mysql/bin/mysqladmin -u root password 'root'
ln -s /usr/local/mysql/include /usr/include/mysql
echo "/usr/local/mysql/lib" > /etc/ld.so.conf.d/mysql.conf
ldconfig
ldconfig -v | grep mysql
#
#/usr/local/mysql/bin/mysql_secure_installation
{
mysql -uroot -proot -e "delete from mysql.user where user='';FLUSH PRIVILEGES;"
mysql -uroot -proot -e "DELETE FROM mysql.user WHERE User='root' AND Host NOT IN ('localhost', '127.0.0.1', '::1');"
mysql -uroot -proot -e "DROP DATABASE test;DELETE FROM mysql.db WHERE Db='test' OR Db='test\\_%';"
mysql -uroot -proot -e "FLUSH PRIVILEGES;"
} > /dev/null 2>&1
echo "export PATH=/usr/local/mysql/bin:$PATH" >> /etc/profile
source /etc/profile
service mysqld restart

```

参考链接：
[centos 6.0安装图解教程](https://wenku.baidu.com/view/668f53e9e009581b6bd9ebc9.html)

安装包下载链接：https://pan.baidu.com/s/18URDzeQabQ5NmyrfpC9dCQ 
提取码：sb4o 