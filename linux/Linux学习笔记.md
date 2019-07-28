# Linux学习笔记

## Linux文件权限与目录配置

### Linux用户用户组

​	1、添加账号

~~~ linux
useradd 选项 用户名
参数说明
	-c 注释
	-d 目录
	-g 用户组
	-G 用户组
	-s shell文件
	-u 用户号
~~~

2、删除账号

~~~ linux
useradd 选项 用户名
~~~

3、修改账号

~~~ linux
usermod 选项 用户名
~~~

相关概念：文件所有者、用户组

### Linux权限概念

![linux1](D:\myLearningMaterials\learning-notes\linux\linux1.png)

改变文件的属性与权限

- chgrp:改变文件所属用户组 

- chown：改变文件所有者

- chmod：改变文件权限

  权限的数字类型

  | r    | 4    |
  | ---- | ---- |
  | w    | 2    |
  | x    | 1    |

  权限的符号类型

  | u    | user  |
  | ---- | ----- |
  | g    | group |
  | o    | other |
  | a    | all   |

  实例：

  ``` shell
  chomd u=rwx,go=rx filename
  ```

   linux 文件种类

  - 普通文件
  - 纯文本文件
  - 二进制文件
  - 数据格式文件
  - 目录
  - 连接文件
  - 设备与设备文件
    - 块设备文件
    - 字符设备文件
    - 套接字
    - 管道

  linux文件扩展名

  ​	linux文件能不能被执行跟文件扩展名没有关系，与他第一列的10个属性有关。

### linux目录配置

1. FHS目录定义说明

   |          | 可分享的           | 不可分享的            |
   | -------- | ------------------ | --------------------- |
   | 不变的   | /usr(软件放置处)   | /etc（配置文件）      |
   | 不变的   | /opt（第三方软件） | /boot(开机与内核文件) |
   | 可变动的 | /var/mail          | /var/run(程序相关)    |
   | 可变动的 | /var/spool/news    | /var/lock             |

2. 目录定义

   1. / ：与开机系统有关

      根目录所在的分区越小越好，应用程序最好不要和根目录一个分区

      lunux根目录下目录

      ![linux2](D:\myLearningMaterials\learning-notes\linux\linux2.jpg)

      | 目录   | 放置文件内容                           |
      | ------ | -------------------------------------- |
      | /bin   | 系统大部分执行文件内容                 |
      | /boot  | 开机核心文件                           |
      | /dev   | linux外部设备                          |
      | /etc   | 系统主要配置文件                       |
      | /home  | 系统默认用户主文件夹                   |
      | /lib   | 开机会用到的函数库                     |
      | /media | 可删除设备                             |
      | /mnt   | 挂载设备存放目录                       |
      | /opt   | 第三方软件放值目录                     |
      | /root  | 系统管理员主文件夹                     |
      | /sbin  | 存放的是系统管理员使用的系统管理程序。 |
      | /srv   | 网络服务所需取用数据的目录             |
      | ./tmp  | 临时文件存放目录                       |
      |        |                                        |

   2. /usr:与软件安装/执行有关

   3. /var ：与系统运行有关

      ![](D:\myLearningMaterials\learning-notes\linux\roottree.jpg)

3. 绝对路径和相对路径

   ~~~ linux
   cd /home/xxx			绝对路径
   cd  home/xxx or cd ../home/test		 相对路径					
   
   ~~~

### 总结

- FHS四种目录特色：可分享、不可分享、静态的、可变的

- FHS的三层主目录： /、/var、/usr

- /etc、/bin、/lib、/dev、/sbin不可 与根目录放在不同的分区

  

