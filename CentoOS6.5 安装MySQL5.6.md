һ����װCentoOS6.5

1���޸�����

�����������£�
```
vi /etc/sysconfig/network-scripts/ifcfg-eth0
```
![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-c178122a85aaaf5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

�޸�ONBOOTΪyes:

![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-d57a4ef56fef32b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

ִ�������������ʹ������Ч��

```
service network restart
```

2���޸�sshԶ������

�����������

```
vi /etc/ssh/sshd_config
```
![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-bcd5dc967c6ea0fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

�޸�UseDNSΪno:

![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-7dc764234c71829c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

ִ��ssh�������ʹ������Ч��

```
service ssh restart
```

3��ʹ��SecureCRT ssh��¼root�˻�

�鿴ip��ַ

![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-b021ec6343e7f511.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Զ�̵�¼root�˻�

![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-ea1b7d7b7a483962.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


4���ϴ���װ�ļ���CentoOS��

```
yum install vim lrzsz -y
```

```
rz
```
ѡ��Ҫ�ϴ����ļ����ȴ��ϴ����ɡ�

[lrzsz��Linux��������window�����ļ����ߣ�](https://blog.csdn.net/wuzhangweiss/article/details/79842283)

������װMySQL5.6

1���޸�my.cnf->/etc/my.cnf

```
vim install_mysql-5.6.36_x86_64.sh
```

![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-9a5750d5c464ba49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2��ִ�нű���

```
sh install_mysql-5.6.36_x86_64.sh
```

3��ִ��
```
service mysqlId status
```
���н�����£���MySQL��װ�ɹ���

![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-32d12bd38900c5eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4����¼��mysql��

![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-66f87e2108be07a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

��¼mysql-5.6.36_x86_64.sh��

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

�ο����ӣ�
[centos 6.0��װͼ��̳�](https://wenku.baidu.com/view/668f53e9e009581b6bd9ebc9.html)

��װ���������ӣ�https://pan.baidu.com/s/18URDzeQabQ5NmyrfpC9dCQ 
��ȡ�룺sb4o 