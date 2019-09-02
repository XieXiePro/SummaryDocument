尝试插入输入：
![图片.png](https://upload-images.jianshu.io/upload_images/2783386-beeb44ca5a61a702.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**原因是字符集问题**

1 查看字符集
```
show variables like 'character%'; 
show variables like '%char%';
```
看看出现的结果：

 ![图片.png](https://upload-images.jianshu.io/upload_images/2783386-be9cdbef634cc3ef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


默认的服务器用了latin1，所以会乱码。
 
 
 2 修改my-huge.cnf

在/usr/share/mysql/ 中找到my-huge.cnf的配置文件，
拷贝其中的my-huge.cnf 到 /etc/  并命名为my.cnf 

然后修改my.cnf:
```
[client]
default-character-set=utf8
[mysqld]
character_set_server=utf8
character_set_client=utf8
collation-server=utf8_general_ci
[mysql]
default-character-set=utf8
```

 ![图片.png](https://upload-images.jianshu.io/upload_images/2783386-425c356082d7759c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![图片.png](https://upload-images.jianshu.io/upload_images/2783386-1ac015de15b3b9b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 3、重新启动mysql

 查看原库的字符集：
```
show create database mydb
```

 但是原库的设定不会发生变化，参数修改之对新建的数据库生效
 
4、已生成的库表字符集如何变更
修改数据库的字符集
```
mysql> alter database mydb character set 'utf8';
```
修改数据表的字符集
```
mysql> alter table mytbl convert to  character set 'utf8';
 ```
 但是原有的数据如果是用非'utf8'编码的话，数据本身不会发生改变。
 
 MySQL中文乱码问题：
[mysql字符编码的设置以及mysql中文乱码的解决方法](https://blog.csdn.net/mynamepg/article/details/81044957)
