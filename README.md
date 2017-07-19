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
  
  
# 9：centos7根目录扩容
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