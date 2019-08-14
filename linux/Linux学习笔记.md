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
  chmod u=rwx,go=rx filename
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

## Linux文件与目录系统

### 目录与路径

``` linux
.	当前目录	
..	上一级目录
-	前一个工作目录
~	当前用户身份所在的主文件夹
~account	代表account账号的主文件夹	

cd	
pwd
mkdir	
	-m	设置权限
	-p	递归创建文件目录
rmdir
```

### 文件与目录管理

``` linux
ls	查看文件与目录
	-a	查看全部文件（包括隐藏文件）
	-A	列出全部的文件（不包含.和..这两个目录）
	-d	仅列出目录本身
	-f	直接列出结果
	-F	根据文件、目录等信息给与附加结构
	-h	将文件以容易读的方式展示
	-i	列出inode码
	-l	列出长数据串
	-n	列出UID和GID
	-r	将排序结果反向输出
	-R	连同子目录内容一起列出来
	-S	以文件大小容量排序
	-t	依时间排序
	--full-time	以完整的时间模式输出
cp	复制文件或者目录
	-a	相当于-pdr
	-d	若源文件时link file，则复制连接文件属性
	-f	强制,若目标文件存在且无法开启，则删除后再尝试一次
	-i	目标文件已经存在时，在覆盖时先询问
	-l	进行硬链接
	-p	连同文件的属性一起复制过去
	-r	递归持续复制
	-s	复制成快捷方式文件
rm	移动目录或者文件夹
	-f	忽略
	-i	提示
	-r	递归删除
mv	移动目录或者文件夹
	-f	直接复制或者覆盖
	-i	提示
	-u	比较后根据新旧决定是否覆盖
```

### 文件内容查看

``` linux
cat	由第一行开始显示内容
	-A	可列出特殊字符
	-b	显示行号，空白行不显示
	-E	将结尾断字符输出
	-n	打印行号
	-T	将tab以^I显示出来
	-v	列出看不见的特殊字符
	
tac	从最后一行开始显示内容
	与cat一致
	
nl	显示内容并输出行号
	
more	按页显示内容
	-空格键	翻页
	Enter	向下滚动一行
	/	向下查询
	:f	立刻显示文件名和当前行数
	q	退出
	b	往回翻页

less	more类似，可以向前翻页
	空格键	向下翻页
	PageDown	向下翻页
	PageUp	向下翻页
	/	向下查询
	？	向上查询
	n	重复前一个查询
	N	反向重复前一个查询
	q	退出命令

chattr	隐藏属性
lsattr	查看隐藏属性
```

### 数据选取

``` linux
head	只看头几行
	-n	后面接数字，显示几行
	
tail	只看结尾几行
	-n	显示最后几行
	-f	持续检测文件，Ctrl+c结束

od	二进制方式读取文件
```

### 修改文件时间或创建新文件

``` linux
touch	修改文件时间或者创建文件
	mtime	文件内容数据更改时间
	ctime	文件状态更新时间
	atime	读取时间
	-a	仅修改访问时间
	-c	仅修改文件的时间
	-d	后面接要修改的时间
	-m	仅修改，mtime
	-t	欲修改的时间
```

### 命令与文件查询<重要>

``` linux
which	脚本文件名查找

whereis	寻找特定文件
	-b	只找二进制文件
	-m	只找说明文件
	-s	只找source文件
	-u	非以上三种的文件

locate	寻找文件（依赖/var/lib/mlocate内的数据记载，可用updatedb更新）
	-i	忽略大小写差异
	-r	后面接正则表达式

find [PATH] [option] [action]
	（1）	与时间相关参数 atime	ctime	mtime
			n	n天之前的“一天内”被xxx的文件
			+n	n天前（不包括n天）被xx的文件名
			-n	列出n天之内(包含)的文件xx的文件名
			-newer file	file为一个存在的文件，列出比file还要新的文件
	（2）	与用户或者用户组名有关的参数
    		-uid n	n为数字，数字时用户的账号ID,UID记录在/etc/passwd里面
    		-gid n	n为数字，代表用户组的ID,GID保存在/etc/group中
			-user name name为用户账号名称
			-nouser	文件所有者不存在/etc/passwd的文件
			-nogroup 文件用户组不存在/etc/passwd的文件
	（3） 文件权限以及名称有关的参数
			-name filename	查找filename
			-size [+-]SIZE	查找比SIZE还要大或者还要小的文件
			-type TYPE	查找文件类型为TYPE的文件
			-perm -mode	查找权限必须包含"model权限的文件"
			-perm +model 查找文件权限包含“任意model”的文件
	（4）	其他操作
			-exec command	-exec后面可再接其他的命令来处理查找到的结果
			-print	将结果打印到屏幕上
```

## Linux磁盘与文件系统

