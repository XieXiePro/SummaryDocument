���Բ������룺
![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-beeb44ca5a61a702.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**ԭ�����ַ�������**

1 �鿴�ַ���
```
show variables like 'character%'; 
show variables like '%char%';
```
�������ֵĽ����

 ![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-be9cdbef634cc3ef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


Ĭ�ϵķ���������latin1�����Ի����롣
 
 
 2 �޸�my-huge.cnf

��/usr/share/mysql/ ���ҵ�my-huge.cnf�������ļ���
�������е�my-huge.cnf �� /etc/  ������Ϊmy.cnf 

Ȼ���޸�my.cnf:
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

 ![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-425c356082d7759c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![ͼƬ.png](https://upload-images.jianshu.io/upload_images/2783386-1ac015de15b3b9b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 3����������mysql

 �鿴ԭ����ַ�����
```
show create database mydb
```

 ����ԭ����趨���ᷢ���仯�������޸�֮���½������ݿ���Ч
 
4�������ɵĿ���ַ�����α��
�޸����ݿ���ַ���
```
mysql> alter database mydb character set 'utf8';
```
�޸����ݱ���ַ���
```
mysql> alter table mytbl convert to  character set 'utf8';
 ```
 ����ԭ�е�����������÷�'utf8'����Ļ������ݱ����ᷢ���ı䡣
 
 MySQL�����������⣺
[mysql�ַ�����������Լ�mysql��������Ľ������](https://blog.csdn.net/mynamepg/article/details/81044957)
