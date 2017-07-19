# stu
linux学习 

# 1:[centos7查看版本信息](https://github.com/vekrio/stu/blob/master/20170718/Redhat-release)

# 2:[ntp安装](https://github.com/vekrio/stu/blob/master/20170718/ntp)

# 3:[centos7查看已启动的服务列表](https://github.com/vekrio/stu/blob/master/20170718/list-unit-files)

# 4:[centos7仓库导入公钥](https://github.com/vekrio/stu/blob/master/20170718/%E5%AF%BC%E5%85%A5%E5%85%AC%E9%92%A5)

# 5:[centos系统添加/删除用户和用户组的例子](http://www.111cn.net/sys/CentOS/63650.htm)

# 6:[centos7退出登录](http://blog.csdn.net/huangxiang360729/article/details/52650107)

# 7:[centos7忘记root密码](https://jingyan.baidu.com/article/cbf0e5009d61322eab28935f.html)

 ## 方法一

1.重启开机按e

2.编辑修改两处：ro改为rw,在LANG=en_US.UFT-8后面添加init=/bin/sh

3.按Ctrl+X重启，并修改密码

4.由于selinux开启着的需要执行以下命令更新系统信息,否则重启之后密码未生效

touch /.autorelabel

5.重启系统

## 方法二

1.重启开机按e

2.编辑修改LANG=en_US.UFT-8后面添加rd.break

3.按Ctrl+X重启

4.mount -o remount，rw /sysroot

5.chroot  /sysroot

6.修改密码

7.由于selinux开启着的需要执行以下命令更新系统信息,否则重启之后密码未生效

touch /.autorelabel

8.重启系统


# 8:  [ 中文man ](https://jingyan.baidu.com/article/f25ef25466bffc482c1b82b6.html)

虽然在CentOS操作系统中具有多语言包，但其man手册是英文的，对于新手来说能够使用中文man手册将加快学习速度。

工具/原料

>Linux操作系统：CentOS 6.6

>软件：manpages-zh-1.5.1.tar.gz

>方法/步骤

1:将安装包下载到本地

wget http://pkgs.fedoraproject.org/repo/pkgs/man-pages-zh-CN/manpages-zh-1.5.1.tar.gz/13275fd039de8788b15151c896150bc4/manpages-zh-1.5.1.tar.gz


2:打开系统终端,输入：tar xf manpages-zh-1.5.1.tar.gz进行解压缩

3: cd manpages-zh-1.5.1             #进入安装目录

4: ./configure --disable-zhtw      #安装配置

5:  make && make install            #安装

6:设置环境变量：vim /etc/profile.d/cman.sh

  输入内容：alias cman='man -M /usr/local/share/man/zh_CN'
  
  保存退出

7:source /etc/profile.d/cman.sh      #重新执行别名文件

CentOS系统安装中文man手册

8:测试，输入命令：cman ls

  #注意事项:
  
  #中文帮助手册的使用命令是cman,目前只翻译部分不是所有的帮助都是中文
  
  #如果想使用英文帮助，可以使用命令man
  
  
# 9：[centos7根目录扩容](http://www.centoscn.com/CentOS/config/2016/0530/7306.html)
[root@localhost ~]# fdisk -l

Disk /dev/sda: 8589 MB, 8589934592 bytes, 16777216 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk label type: dos

Disk identifier: 0x00024b27


   Device Boot      Start         End      Blocks   Id  System
   
/dev/sda1   *        2048     2099199     1048576   83  Linux

/dev/sda2         2099200    16777215     7339008   8e  Linux LVM

Disk /dev/sdb: 8589 MB, 8589934592 bytes, 16777216 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk /dev/mapper/cl-root: 6652 MB, 6652166144 bytes, 12992512 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/cl-swap: 859 MB, 859832320 bytes, 1679360 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes


[root@localhost ~]# fdisk /dev/sdb

Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.

Be careful before using the write command.

Device does not contain a recognized partition table

Building a new DOS disklabel with disk identifier 0x8393e904.

Command (m for help): n

Partition type:

   p   primary (0 primary, 0 extended, 4 free)
   
   e   extended
   
Select (default p): p

Partition number (1-4, default 1): 

First sector (2048-16777215, default 2048): 

Using default value 2048

Last sector, +sectors or +size{K,M,G} (2048-16777215, default 16777215): 

Using default value 16777215

Partition 1 of type Linux and of size 8 GiB is set

Command (m for help): t

Selected partition 1

Hex code (type L to list all codes): 8e

Changed type of partition 'Linux' to 'Linux LVM'

Command (m for help): p

Disk /dev/sdb: 8589 MB, 8589934592 bytes, 16777216 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk label type: dos

Disk identifier: 0x8393e904

   Device Boot      Start         End      Blocks   Id  System
   
/dev/sdb1            2048    16777215     8387584   8e  Linux LVM

Command (m for help): w

The partition table has been altered!

Calling ioctl() to re-read partition table.

Syncing disks.

[root@localhost ~]# pvs

  PV         VG Fmt  Attr PSize PFree
  
  /dev/sda2  cl lvm2 a--  7.00g    0 
  
[root@localhost ~]# pvcreate /dev/sdb1
 
  Physical volume "/dev/sdb1" successfully created.
  
[root@localhost ~]# pvs

  PV         VG Fmt  Attr PSize PFree
  
  /dev/sda2  cl lvm2 a--  7.00g    0 
  
  /dev/sdb1     lvm2 ---  8.00g 8.00g
  
[root@localhost ~]# vgex

vgexport  vgextend  

[root@localhost ~]# vgs

  VG #PV #LV #SN Attr   VSize VFree
  
  cl   1   2   0 wz--n- 7.00g    0 
  
[root@localhost ~]# vgex

vgexport  vgextend  

[root@localhost ~]# vgextend cl /dev/sdb1

  Volume group "cl" successfully extended
  
[root@localhost ~]# vgs

  VG #PV #LV #SN Attr   VSize  VFree
  
  cl   2   2   0 wz--n- 14.99g 8.00g
  
[root@localhost ~]# lgs

bash: lgs: command not found...

[root@localhost ~]# lvs

  LV   VG Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  
  root cl -wi-ao----   6.20g    
  
  swap cl -wi-ao---- 820.00m  
  
[root@localhost ~]# lvextend /dev/cl/

/dev/cl/root  /dev/cl/swap  

[root@localhost ~]# lvextend /dev/cl/

/dev/cl/root  /dev/cl/swap 
 
[root@localhost ~]# lvextend -L +8G /dev/cl/root  

  Insufficient free space: 2048 extents needed, but only 2047 available
  
[root@localhost ~]# lvextend -L +7.95G /dev/cl/root  

  Rounding size to boundary between physical extents: 7.95 GiB.
  
  Size of logical volume cl/root changed from 6.20 GiB (1586 extents) to 14.15 GiB (3622 extents).
  
  Logical volume cl/root successfully resized.
  
[root@localhost ~]# xfs

xfs_admin      xfs_db         xfs_freeze     xfs_info       xfs_logprint   xfs_mkfile     xfs_repair   
  
xfs_bmap       xfsdump        xfs_fsr        xfsinvutil     xfs_mdrestore  xfs_ncheck     xfsrestore 
    
xfs_copy       xfs_estimate   xfs_growfs     xfs_io         xfs_metadump   xfs_quota      xfs_rtcp 
      
[root@localhost ~]# xfs_growfs /dev/

Display all 162 possibilities? (y or n)

[root@localhost ~]# xfs_growfs /dev/cl/

root  swap  

[root@localhost ~]# xfs_growfs /dev/cl/

root  swap 
 
[root@localhost ~]# xfs_growfs /dev/cl/root 

meta-data=/dev/mapper/cl-root    isize=512    agcount=4, agsize=406016 blks

         =                       sectsz=512   attr=2, projid32bit=1
		 
         =                       crc=1        finobt=0 spinodes=0
		 
data     =                       bsize=4096   blocks=1624064, imaxpct=25

         =                       sunit=0      swidth=0 blks
		 
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1

log      =internal               bsize=4096   blocks=2560, version=2

         =                       sectsz=512   sunit=0 blks, lazy-count=1
		 
realtime =none                   extsz=4096   blocks=0, rtextents=0

data blocks changed from 1624064 to 3708928

[root@localhost ~]# df -h

Filesystem           Size  Used Avail Use% Mounted on

/dev/mapper/cl-root   15G  4.5G  9.8G  32% /

devtmpfs             905M     0  905M   0% /dev

tmpfs                920M     0  920M   0% /dev/shm

tmpfs                920M  8.9M  911M   1% /run

tmpfs                920M     0  920M   0% /sys/fs/cgroup

/dev/sda1           1014M  227M  788M  23% /boot

tmpfs                184M     0  184M   0% /run/user/0

[root@localhost ~]# 


# [Markdown 常用技巧](http://blog.csdn.net/u010177286/article/details/50358720)

2015/12/19 16:05:18

换行：

<br>方法1: 连续两个以上空格+回车
<br>方法2：使用html语言换行标签： <br>
<br>首行缩进两个字符：(每个表示一个空格，连续使用两个即可）

<br>&ensp; 半角的空格
<br>&emsp; 全角的空格
<br>字体、字号与颜色: 

<br>  Markdown是一种可以使用普通文本编辑器编写的标记语言，通过类似HTML的标记语法，它可以使普通文本内容具有一定的格式。但是它本身是不支持修改字体、字号与颜色等功能的！ 
  CSDN-markdown编辑器是其衍生版本，扩展了Markdown的功能（如表格、脚注、内嵌HTML等等）！对，就是内嵌HTML，接下来要讲的功能就需要使用内嵌HTML的方法来实现。 
字体，字号和颜色编辑如下代码

<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=#0099ff size=7 face="黑体">color=#0099ff size=72 face="黑体"</font>
<font color=#00ffff size=72>color=#00ffff</font>
<font color=gray size=72>color=gray</font>

Size：规定文本的尺寸大小。可能的值：从 1 到 7 的数字。浏览器默认值是 3
具体颜色分类及标记请参照：各种颜色

背景色: 
Markdown本身不支持背景色设置，需要采用内置html的方式实现：借助 table, tr, td 等表格标签的 bgcolor 属性来实现背景色的功能。举例如下：

<table><tr><td bgcolor=orange>背景色是：orange</td></tr></table>
效果如下： 
背景色是：orange
2015/12/19 16:04:07
分割线：你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线

链接：链接文字都是用 [方括号] 来标记,在方块括号后面紧接着圆括号并插入网址链接即可:可参照 
[This link](http://example.NET/) has no title attribute.

代码块：

代码块：用2个以上TAB键起始的段落，会被认为是代码块（效果如下）：

struct {
  int year;
  int month;
  int day;
 }bdate;
如果在一个行内需要引用代码，只要用反引号`引起来就好(Esc健）

代码块与语法高亮：在需要高亮的代码块的前一行及后一行使用三个反引号“`”，同时第一行反引号后面表面代码块所使用的语言
插入互联网上图片： 

![这里写图片描述](http://img3.douban.com/mpic/s1108264.jpg) 

使用LaTex数学公式: 
行内公式：使用两个”$”符号引用公式: $公式$
行间公式：使用两对“$$”符号引用公式： $$公式$$ 

