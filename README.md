# stu
linux学习 

# 1:[centos7查看版本信息](http://jingyan.baidu.com/article/e6c8503c062dcee54f1a18d0.html)
		登陆root帐户，输入 cat  /etc/redhat-release，即可显示系统版本
		
		输入 uname  -r ，可以查询内核版本
		
		输入 df  -h，可以查看各分区的使用情况。其中，从左到右各列的内容依次是：
           文件系统、总大小、已使用大小、剩余大小、使用率、挂载点。
		   
		输入du  -sh，则可以查看当前文件夹所占空间。它的功能等同于 du . -sh。而输入 du 目录名 -sh，则可以查看指定目录的大小。

# 2:[ntp安装](http://jingyan.baidu.com/article/22fe7cedd62b153002617ff2.html)

# 3:[centos7查看已启动的服务列表](http://man.linuxde.net/systemctl)

# 4:[centos7仓库导入公钥](https://github.com/vekrio/stu/blob/master/20170718/%E5%AF%BC%E5%85%A5%E5%85%AC%E9%92%A5)

# 5:[centos系统添加/删除用户和用户组的例子](http://www.111cn.net/sys/CentOS/63650.htm)

# 6:[centos7退出登录](http://blog.csdn.net/huangxiang360729/article/details/52650107)

# 7:[centos7忘记root密码](https://jingyan.baidu.com/article/cbf0e5009d61322eab28935f.html)

## 方法一

	1.重启开机按e

	2.编辑修改两处：ro改为rw,必须在LANG=en_US.UFT-8后面添加init=/bin/sh

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
  
  
# 9：[centos7根目录扩容及增加swap](http://www.centoscn.com/CentOS/config/2016/0530/7306.html)
	
	Last login: Fri Aug 18 15:12:01 2017 from 61.155.49.162
###	[root@localhost ~]# ll
	total 4
	-rw-------. 1 root root 1248 Jul 11 22:00 anaconda-ks.cfg
###	[root@localhost ~]# df -lhT
	Filesystem          Type      Size  Used Avail Use% Mounted on
	/dev/mapper/cl-root xfs       6.2G  1.4G  4.9G  22% /
	devtmpfs            devtmpfs  909M     0  909M   0% /dev
	tmpfs               tmpfs     920M     0  920M   0% /dev/shm
	tmpfs               tmpfs     920M   17M  904M   2% /run
	tmpfs               tmpfs     920M     0  920M   0% /sys/fs/cgroup
	/dev/sda1           xfs      1014M  166M  849M  17% /boot
	tmpfs               tmpfs     184M     0  184M   0% /run/user/0
	Last login: Fri Aug 18 15:42:03 2017 from 61.155.49.162
###	[root@localhost ~]# fdisk -l

	Disk /dev/sdb: 34.4 GB, 34359738368 bytes, 67108864 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes


	Disk /dev/sda: 8589 MB, 8589934592 bytes, 16777216 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk label type: dos
	Disk identifier: 0x000031df

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sda1   *        2048     2099199     1048576   83  Linux
	/dev/sda2         2099200    16777215     7339008   8e  Linux LVM

	Disk /dev/mapper/cl-root: 6652 MB, 6652166144 bytes, 12992512 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes


	Disk /dev/mapper/cl-swap: 859 MB, 859832320 bytes, 1679360 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes

###	[root@localhost ~]# parted /dev/sdb
	GNU Parted 3.1
	Using /dev/sdb
	Welcome to GNU Parted! Type 'help' to view a list of commands.
	(parted) mklabel  
	align-check  disk_toggle  mklabel      mktable      print        rescue       select       toggle       version      
	disk_set     help         mkpart       name         quit         rm           set          unit         
	(parted) mklabel  msdos
	(parted) mkpart p1
	parted: invalid token: p1
	Partition type?  primary/extended? p                                      
	File system type?  [ext2]?                                                
	Start?                                                                    
	Start? 0                                                                  
	End? 100%
	Warning: The resulting partition is not properly aligned for best performance.
	Ignore/Cancel? i                                                          
	(parted) p                                                                
	Model: VMware Virtual disk (scsi)
	Disk /dev/sdb: 34.4GB
	Sector size (logical/physical): 512B/512B
	Partition Table: msdos
	Disk Flags: 

	Number  Start  End     Size    Type     File system  Flags
	 1      512B   34.4GB  34.4GB  primary

	(parted) quit                                                             
	Information: You may need to update /etc/fstab.

###	[root@localhost ~]# fdisk -l                                              

	Disk /dev/sdb: 34.4 GB, 34359738368 bytes, 67108864 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk label type: dos
	Disk identifier: 0x0006e17c

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sdb1               1    67108863    33554431+  83  Linux

	Disk /dev/sda: 8589 MB, 8589934592 bytes, 16777216 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk label type: dos
	Disk identifier: 0x000031df

	   Device Boot      Start         End      Blocks   Id  System
	/dev/sda1   *        2048     2099199     1048576   83  Linux
	/dev/sda2         2099200    16777215     7339008   8e  Linux LVM

	Disk /dev/mapper/cl-root: 6652 MB, 6652166144 bytes, 12992512 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes


	Disk /dev/mapper/cl-swap: 859 MB, 859832320 bytes, 1679360 sectors
	Units = sectors of 1 * 512 = 512 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes

###	[root@localhost ~]# pvcreate /dev/sdb1
	  Physical volume "/dev/sdb1" successfully created.
	[root@localhost ~]# vgs
	  VG #PV #LV #SN Attr   VSize VFree
	  cl   1   2   0 wz--n- 7.00g    0 
###	[root@localhost ~]# pvs
	  PV         VG Fmt  Attr PSize  PFree 
	  /dev/sda2  cl lvm2 a--   7.00g     0 
	  /dev/sdb1     lvm2 ---  32.00g 32.00g
###	[root@localhost ~]# vgex
	vgexport  vgextend  
###	[root@localhost ~]# vgextend cl /dev/sdb1
	  Volume group "cl" successfully extended
	[root@localhost ~]# vgs
	  VG #PV #LV #SN Attr   VSize  VFree 
	  cl   2   2   0 wz--n- 38.99g 32.00g
###	[root@localhost ~]# lvextend -L +32GB /dev/cl/root 
	  Insufficient free space: 8192 extents needed, but only 8191 available
###	[root@localhost ~]# lvextend -L +31.95GB /dev/cl/root  
	  Rounding size to boundary between physical extents: 31.95 GiB.
	  Size of logical volume cl/root changed from 6.20 GiB (1586 extents) to 38.15 GiB (9766 extents).
	  Logical volume cl/root successfully resized.
###	[root@localhost ~]# df -lhT
	Filesystem          Type      Size  Used Avail Use% Mounted on
	/dev/mapper/cl-root xfs       6.2G  1.4G  4.9G  22% /
	devtmpfs            devtmpfs  3.9G     0  3.9G   0% /dev
	tmpfs               tmpfs     3.9G     0  3.9G   0% /dev/shm
	tmpfs               tmpfs     3.9G  8.5M  3.9G   1% /run
	tmpfs               tmpfs     3.9G     0  3.9G   0% /sys/fs/cgroup
	/dev/sda1           xfs      1014M  183M  832M  19% /boot
	tmpfs               tmpfs     783M     0  783M   0% /run/user/0
###	[root@localhost ~]# xfs_growfs /dev/cl/
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
	data blocks changed from 1624064 to 10000384
###	[root@localhost ~]# lvs
	  LV   VG Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
	  root cl -wi-ao----  38.15g                                                    
	  swap cl -wi-ao---- 820.00m                                                    
###	[root@localhost ~]# vgdisplay 
	  --- Volume group ---
	  VG Name               cl
	  System ID             
	  Format                lvm2
	  Metadata Areas        2
	  Metadata Sequence No  5
	  VG Access             read/write
	  VG Status             resizable
	  MAX LV                0
	  Cur LV                2
	  Open LV               2
	  Max PV                0
	  Cur PV                2
	  Act PV                2
	  VG Size               38.99 GiB
	  PE Size               4.00 MiB
	  Total PE              9982
	  Alloc PE / Size       9971 / 38.95 GiB
	  Free  PE / Size       11 / 44.00 MiB
	  VG UUID               Qgvl8Y-8uoN-05rT-D5oj-6jOA-pB0t-xpbPqR
	   
###	[root@localhost ~]# vgre
	vgreduce  vgremove  vgrename  
###	[root@localhost ~]# lvresize -L -8GB /dev/cl/root
	  WARNING: Reducing active and open logical volume to 30.15 GiB.
	  THIS MAY DESTROY YOUR DATA (filesystem etc.)
	Do you really want to reduce cl/root? [y/n]: y
	  Size of logical volume cl/root changed from 38.15 GiB (9766 extents) to 30.15 GiB (7718 extents).
	  Logical volume cl/root successfully resized.
###	[root@localhost ~]# vgdisplay 
	  --- Volume group ---
	  VG Name               cl
	  System ID             
	  Format                lvm2
	  Metadata Areas        2
	  Metadata Sequence No  6
	  VG Access             read/write
	  VG Status             resizable
	  MAX LV                0
	  Cur LV                2
	  Open LV               2
	  Max PV                0
	  Cur PV                2
	  Act PV                2
	  VG Size               38.99 GiB
	  PE Size               4.00 MiB
	  Total PE              9982
	  Alloc PE / Size       7923 / 30.95 GiB
	  Free  PE / Size       2059 / 8.04 GiB
	  VG UUID               Qgvl8Y-8uoN-05rT-D5oj-6jOA-pB0t-xpbPqR
	   
###	[root@localhost ~]# vgextend -L +8GB /dev/cl/
	root  swap  
###	[root@localhost ~]# vgextend -L +8GB /dev/cl/swap 
	vgextend: invalid option -- 'L'
	  Error during parsing of command line.
###	[root@localhost ~]# vgextend -l +8GB /dev/cl/swap  
	vgextend: invalid option -- 'l'
	  Error during parsing of command line.
###	[root@localhost ~]# lvextend -L +8GB /dev/cl/swap 
	  Size of logical volume cl/swap changed from 820.00 MiB (205 extents) to 8.80 GiB (2253 extents).
	  Logical volume cl/swap successfully resized.
###	[root@localhost ~]# lvdisplay 
	  --- Logical volume ---
	  LV Path                /dev/cl/swap
	  LV Name                swap
	  VG Name                cl
	  LV UUID                C7O7Xc-S60j-OHix-38Ko-BbfD-ZILN-rSMKXr
	  LV Write Access        read/write
	  LV Creation host, time localhost.localdomain, 2017-07-11 21:55:40 +0800
	  LV Status              available
	  # open                 2
	  LV Size                8.80 GiB
	  Current LE             2253
	  Segments               2
	  Allocation             inherit
	  Read ahead sectors     auto
	  - currently set to     8192
	  Block device           253:1
	   
	  --- Logical volume ---
	  LV Path                /dev/cl/root
	  LV Name                root
	  VG Name                cl
	  LV UUID                fh27Ps-QqJv-7CEe-Gt4n-aC2E-jP2j-TKlyCx
	  LV Write Access        read/write
	  LV Creation host, time localhost.localdomain, 2017-07-11 21:55:40 +0800
	  LV Status              available
	  # open                 1
	  LV Size                30.15 GiB
	  Current LE             7718
	  Segments               2
	  Allocation             inherit
	  Read ahead sectors     auto
	  - currently set to     8192
	  Block device           253:0
	   
###	[root@localhost ~]# df -lhT
	Filesystem          Type      Size  Used Avail Use% Mounted on
	/dev/mapper/cl-root xfs        39G  1.4G   37G   4% /
	devtmpfs            devtmpfs  3.9G     0  3.9G   0% /dev
	tmpfs               tmpfs     3.9G     0  3.9G   0% /dev/shm
	tmpfs               tmpfs     3.9G  8.5M  3.9G   1% /run
	tmpfs               tmpfs     3.9G     0  3.9G   0% /sys/fs/cgroup
	/dev/sda1           xfs      1014M  183M  832M  19% /boot
	tmpfs               tmpfs     783M     0  783M   0% /run/user/0
###	[root@localhost ~]# free -m
				  total        used        free      shared  buff/cache   available
	Mem:           7822         167        7380           8         275        7381
	Swap:           819           0         819
###	[root@localhost ~]# vi /etc/fstab 

	#
	# /etc/fstab
	# Created by anaconda on Tue Jul 11 21:55:42 2017
	#
	# Accessible filesystems, by reference, are maintained under '/dev/disk'
	# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
	#
	/dev/mapper/cl-root     /                       xfs     defaults        0 0
	UUID=4475fa42-8f2f-4371-ada0-95d370318466 /boot                   xfs     defaults        0 0
	/dev/mapper/cl-swap     swap                    swap    defaults        0 0
                                                                                                                
	~                                                                                                                                            
                                                                                                           
	~                                                                                                                                            
	"/etc/fstab" 11L, 465C

	[1]+  Stopped                 vi /etc/fstab
###	[root@localhost ~]# free –h
				  total        used        free      shared  buff/cache   available
	Mem:        8010268      171068     7557208        8680      281992     7558364
	Swap:        839676           0      839676

###	[root@localhost ~]# xfs_growfs /dev/cl/swap 
	xfs_growfs: /dev/cl/swap is not a mounted XFS filesystem
###	[root@localhost ~]# df -lhT
	Filesystem          Type      Size  Used Avail Use% Mounted on
	/dev/mapper/cl-root xfs        39G  1.4G   37G   4% /
	devtmpfs            devtmpfs  3.9G     0  3.9G   0% /dev
	tmpfs               tmpfs     3.9G     0  3.9G   0% /dev/shm
	tmpfs               tmpfs     3.9G  8.5M  3.9G   1% /run
	tmpfs               tmpfs     3.9G     0  3.9G   0% /sys/fs/cgroup
	/dev/sda1           xfs      1014M  183M  832M  19% /boot
	tmpfs               tmpfs     783M     0  783M   0% /run/user/0
###	[root@localhost ~]# lvdisplay 
	  --- Logical volume ---
	  LV Path                /dev/cl/swap
	  LV Name                swap
	  VG Name                cl
	  LV UUID                C7O7Xc-S60j-OHix-38Ko-BbfD-ZILN-rSMKXr
	  LV Write Access        read/write
	  LV Creation host, time localhost.localdomain, 2017-07-11 21:55:40 +0800
	  LV Status              available
	  # open                 2
	  LV Size                8.80 GiB
	  Current LE             2253
	  Segments               2
	  Allocation             inherit
	  Read ahead sectors     auto
	  - currently set to     8192
	  Block device           253:1
	   
	  --- Logical volume ---
	  LV Path                /dev/cl/root
	  LV Name                root
	  VG Name                cl
	  LV UUID                fh27Ps-QqJv-7CEe-Gt4n-aC2E-jP2j-TKlyCx
	  LV Write Access        read/write
	  LV Creation host, time localhost.localdomain, 2017-07-11 21:55:40 +0800
	  LV Status              available
	  # open                 1
	  LV Size                30.15 GiB
	  Current LE             7718
	  Segments               2
	  Allocation             inherit
	  Read ahead sectors     auto
	  - currently set to     8192
	  Block device           253:0
	   
###	[root@localhost ~]# swapoff -v /dev/cl/swap 
	swapoff /dev/cl/swap
###	[root@localhost ~]# mkswap /dev/cl/swap 
	mkswap: /dev/cl/swap: warning: wiping old swap signature.
	Setting up swapspace version 1, size = 9228284 KiB
	no label, UUID=a6ae2aa2-cf8e-4f33-8c74-943ae38846e9
	[root@localhost ~]# swapon -va 
	swapon /dev/mapper/cl-swap
	swapon: /dev/mapper/cl-swap: found swap signature: version 1, page-size 4, same byte order
	swapon: /dev/mapper/cl-swap: pagesize=4096, swapsize=9449766912, devsize=9449766912
###	[root@localhost ~]# free
				  total        used        free      shared  buff/cache   available
	Mem:        8010268      179852     7534032        8680      296384     7546784
	Swap:       9228284           0     9228284
###	[root@localhost ~]# free -m
				  total        used        free      shared  buff/cache   available
	Mem:           7822         175        7357           8         289        7370
	Swap:          9011           0        9011
###	[root@localhost ~]# free -g
				  total        used        free      shared  buff/cache   available
	Mem:              7           0           7           0           0           7
	Swap:             8           0           8
###	[root@localhost ~]# free -G
	free: invalid option -- 'G'

	Usage:
	 free [options]

	Options:
	 -b, --bytes         show output in bytes
	 -k, --kilo          show output in kilobytes
	 -m, --mega          show output in megabytes
	 -g, --giga          show output in gigabytes
		 --tera          show output in terabytes
	 -h, --human         show human-readable output
		 --si            use powers of 1000 not 1024
	 -l, --lohi          show detailed low and high memory statistics
	 -t, --total         show total for RAM + swap
	 -s N, --seconds N   repeat printing every N seconds
	 -c N, --count N     repeat printing N times, then exit
	 -w, --wide          wide output

		 --help     display this help and exit
	 -V, --version  output version information and exit

	For more details see free(1).
###	[root@localhost ~]# free -g
				  total        used        free      shared  buff/cache   available
	Mem:              7           0           7           0           0           7
	Swap:             8           0           8
	[root@localhost ~]# 


# 10.[CentOS下测试硬盘坏道](http://www.centoscn.com/CentOS/Intermediate/2014/1219/4344.html)

	硬盘状态测试工具：smartctl、Badblocks、hdparm 
	感觉用smartctl挺快的，也能快速看到硬盘是否健康，命令如下:
	[root@qy ~]#yum install smartmontools -y
	启动SMART
	# smartctl --smart=on --offlineauto=on --saveauto=on /dev/sda
	[root@qy ~]# smartctl -a /dev/sda
	smartctl 5.42 2011-10-20 r3458[i686-linux-2.6.18-194.el5PAE] (local build)
	Copyright (C) 2002-11 by Bruce Allen,http://smartmontools.sourceforge.net
	 
	Vendor:               SEAGATE
	Product:              ST3146356SS    
	Revision:             HS09
	User Capacity:        146,815,733,760 bytes [146 GB]
	Logical block size:   512 bytes
	Logical Unit id:      0x5000c50004fa837f
	Serial number:        3QN0EL91
	Device type:          disk
	Transport protocol:   SAS
	Local Time is:        Fri Oct 31 10:45:58 2014 CST
	Device supports SMART and is Enabled
	Temperature Warning Disabled or NotSupported
	SMART Health Status: OK   #版本的不通这里显示的也不一样。
	 
	Current Drive Temperature:     30 C
	Drive Trip Temperature:        68 C
	Elements in grown defect list: 0  #才是出坏道，俗称成长坏道。
	Vendor (Seagate) cache information
	 Blocks sent to initiator = 3752023409
	 Blocks received from initiator = 3916316860
	 Blocks read from cache and sent to initiator = 4025399956
	 Number of read and write commands whose size <= segment size =3339079605
	 Number of read and write commands whose size > segment size = 2746
	Vendor (Seagate/Hitachi) factoryinformation
	 number of hours powered up = 34120.02
	 number of minutes until next internal SMART test = 1
	 
	Error counter log:
			  Errors Corrected by          Total   Correction     Gigabytes    Total
				   ECC          rereads/    errors  algorithm      processed    uncorrected
			  fast | delayed   rewrites  corrected invocations   [10^9 bytes]  errors
	read:  248894024        0         0 248894024   248894024      85241.186           0
	write:         0        0         0         0          0     30998.996           0
	verify:  340001        0        0    340001     340001        141.757           0
	 
	Non-medium errorcount:       51  #非介质错误。意思是说不是盘的问题，一般是电缆、传输、校验问题，可以忽略的。
	No self-tests have been logged
	Long (extended) Self Test duration: 1740seconds [29.0 minutes]
	 
	可以用命令直接查看硬盘的好坏:
	[root@qy ~]# smartctl -H /dev/sda
	smartctl 5.42 2011-10-20 r3458[i686-linux-2.6.18-194.el5PAE] (local build)
	Copyright (C) 2002-11 by Bruce Allen,http://smartmontools.sourceforge.net
	 
	SMART Health Status: OK
	 
	[root@localhost ~]# smartctl -H /dev/sda
	smartctl 5.43 2012-06-30 r3573 [x86_64-linux-2.6.32-358.el6.x86_64] (local build)
	Copyright (C) 2002-12 by Bruce Allen, http://smartmontools.sourceforge.net
	 
	=== START OF READ SMART DATA SECTION ===
	SMART STATUS RETURN: incomplete response, ATA output registers missing
	SMART overall-health self-assessment test result: PASSED
	Warning: This result is based on an Attribute check.
	 
	OK和PASSED都属于磁盘是正常的。
	 
	Badblocks工具测试正常，无坏道信息：
	 
	badblocks命令可以检查磁盘装置中损坏的区块。执行该指令时须指定所要检查的磁盘装置，及此装置的磁盘区块数。
	 
	badblocks -s//显示进度  -v//显示执行详细情况   /dev/sda1
	badblocks -s//显示进度 -w//以写去检测 -v//显示执行详细情况 /dev/sda2
	注意，不能以写的方式检测已经挂载的硬盘
	 
	[root@qy ~]# badblocks -s -v /dev/sda
	Checking blocks 0 to 143374740
	Checking for bad blocks (read-only test):done                               
	Passcompleted, 0 bad blocks found.
	此磁盘通过测试，没有坏道（坏块）。您可以放心使用。
	磁盘有坏道了……
	但是，如果您检测过程中再某一个区块停滞不前，而后报告中提示有坏块，那么杯具了……您的磁盘有坏道了。
	不论是什么类型的坏道，均建议您首先进行数据备份！把重要数据进行备份然后再尝试修复。如果您有重要数据却无法读取（磁盘出现异常），那么请立即停止使用此磁盘并找专业人员进行修复。
	 
	使用hdparm测试   
	测试硬盘读写速度
	# hdparm -Tt /dev/sda
	/dev/sda:
	Timing cached reads:   
	1918 MB in  2.00 seconds = 959.62 MB/sec
	Timing buffered disk reads:  184 MB in  3.00 seconds =  61.26 MB/sec
	hdparm可检测，显示与设定IDE或SCSI硬盘的参数。
	语法：
	hdparm [-CfghiIqtTvyYZ][-a <快取分区>][-A <0或1>][-c <I/O模式>][-d <0或1>][-k <0或1>][-K <0或1>][-m <分区数>][-n <0或1>][-p <PIO模式>][-P <分区数>][-r <0或1>][-S <时间>][-u <0或1>][-W <0或1>][-X <传输模式>] [设备]
	-a<快取分区> 设定读取文件时，预先存入块区的分区数，若不加上<快取分区>选项，则显示目前的设定。 -A<0或1> 启动或关闭读取文件时的快取功能。-c<I/O模式> 设定IDE32位I/O模式。 -C 检测IDE硬盘的电源管理模式。-d<0或1> 设定磁盘的DMA模式。-f 将内存缓冲区的数据写入硬盘，并清楚缓冲区。 -g 显示硬盘的磁轨，磁头，磁区等参数。-h 显示帮助。-i 显示硬盘的硬件规格信息，这些信息是在开机时由硬盘本身所提供。 -I 直接读取硬盘所提供的硬件规格信息。-k<0或1> 重设硬盘时，保留-dmu参数的设定。 -K<0或1> 重设硬盘时，保留-APSWXZ参数的设定。-m<磁区数> 设定硬盘多重分区存取的分区数。 -n<0或1> 忽略硬盘写入时所发生的错误。-p<PIO模式> 设定硬盘的PIO模式。 -P<磁区数> 设定硬盘内部快取的分区数。-q 在执行后续的参数时，不在屏幕上显示任何信息。 -r<0或1> 设定硬盘的读写模式。-S<时间> 设定硬盘进入省电模式前的等待时间。-t 评估硬盘的读取效率。 -T 平谷硬盘快取的读取效率。-u<0或1> 在硬盘存取时，允许其他中断要求同时执行。-v 显示硬盘的相关设定。 -W<0或1> 设定硬盘的写入快取。-X<传输模式>  设定硬盘的传输模式。-y 使IDE硬盘进入省电模式。 -Y 使IDE硬盘进入睡眠模式。-Z 关闭某些Seagate硬盘的自动省电功能。
	 
	 
	可以使用sg_vpd命令查看硬盘转速，sg_vpd命令是sg3_utils其中一个工具.

	下载地址：http://sg.danny.cz/sg/sg3_utils.html

	VPD:Vital Product Data

	[root@qy sg3_utils-1.39]# sg_vpd /dev/sda

	 

	关于smart检测硬盘命令补充:
	smartctl -a <device> 检查该设备是否已经打开SMART技术。 smartctl -s on <device> 如果没有打开SMART技术，使用该命令打开SMART技术。 smartctl -t short <device> 后台检测硬盘，消耗时间短； smartctl -t long <device> 后台检测硬盘，消耗时间长； smartctl -C -t short <device> 前台检测硬盘，消耗时间短； smartctl -C -t long <device> 前台检测硬盘，消耗时间长。其实就是利用硬盘SMART的自检程序。 smartctl -X <device> 中断后台检测硬盘。 smartctl -l selftest <device> 显示硬盘检测日志。 smartctl -l error <device> 显示硬盘错误汇总。
	 
	首先通过dmesg工具，确认一下硬盘的设备符号。例如一个IDE硬盘连接到Primary IDE 总线上的Slave位置，硬盘设备符号是/dev/hdb，hdb中的h代表IDE，如果显示为sdb，则代表SATA和SCSI，最后一个字幕b代表Primary总线，第二块硬盘即Slave位置，确认硬盘是否打开了SMART支持：
	# smartctl -i /dev/sda
	smartctl 5.40 2010-10-16 r3189 [i386-redhat-linux-gnu] (local build)
	Copyright (C) 2002-10 by Bruce Allen, http://smartmontools.sourceforge.net
	=== START OF INFORMATION SECTION ===
	Device Model:     HITACHI HTS543225L9SA00
	Serial Number:    090131FB2F32YLG28JEA
	Firmware Version: FBEZC48C
	User Capacity:    250,059,350,016 bytes
	Device is:        Not in smartctl database [for details use: -P showall]
	ATA Version is:   8
	ATA Standard is:  ATA-8-ACS revision 3f
	Local Time is:    Wed May 25 10:10:39 2011 CST
	SMART support is: Available - device has SMART capability.
	SMART support is: Enabled                          //表示启用了smart支持
	如果看到SMART support is: Disabled表示SMART未启用，执行如下命令，启动SMART
	# smartctl --smart=on --offlineauto=on --saveauto=on /dev/sda
	smartctl 5.40 2010-10-16 r3189 [i386-redhat-linux-gnu] (local build)
	Copyright (C) 2002-10 by Bruce Allen, http://smartmontools.sourceforge.net
	=== START OF ENABLE/DISABLE COMMANDS SECTION ===
	SMART Enabled.
	SMART Attribute Autosave Enabled.
	SMART Automatic Offline Testing Enabled every four hours.
	现在硬盘的SMART功能已经被打开，执行如下命令查看硬盘的健康状况
	# smartctl -H /dev/sda
	smartctl 5.40 2010-10-16 r3189 [i386-redhat-linux-gnu] (local build)
	Copyright (C) 2002-10 by Bruce Allen, http://smartmontools.sourceforge.net
	=== START OF READ SMART DATA SECTION ===
	SMART overall-health self-assessment test result: PASSED
	请注意result后边的结果：PASSED，这表示硬盘健康状态良好；如果这里显示Failure，那么最好立刻给服务器更换硬盘。SMART只能报告磁盘已经不再健康，但是报警后还能继续运行多久是不确定的。通常，SMART报警参数是有预留的，磁盘报警后，不会当场坏掉，一般能坚持一段时间，有的硬盘SMART报警后还继续跑了好几年，有的硬盘SMART报错后几天就坏了。但是一旦出现报警，侥幸心里是万万不能的……
	#smartctl -A   /dev/sda  查看硬盘的详细信息
	#smartctl -s on  /dev/sda  如果没有打开SMART技术，使用该命令打开SMART技术。
	#smartctl -t short  /dev/sda  后台检测硬盘，消耗时间短；
	#smartctl -t long  /dev/sda   后台检测硬盘，消耗时间长；
	#smartctl -C -t  /dev/sda   short前台检测硬盘，消耗时间短；
	#smartctl -C -t  /dev/sda   long前台检测硬盘，消耗时间长。其实就是利用硬盘SMART的自检程序。
	#smartctl -X   /dev/sda      中断后台检测硬盘。
	#smartctl -l selftest  /dev/sda  显示硬盘检测日志。
	#smartctl -l error   /dev/sda    显示硬盘错误汇总。
	如果需要定期登录到服务器上运行smartctl比较麻烦时，linux还提供了系统进程smartd，编辑配置文件：1    vi  /etc/smartd.conf
	这个配置文件中大部分可能是注释掉的说明，只需要写入和当前硬盘相关的配置即可：
	/dev/sda -H  -m  test@test123123.com  //监控磁盘的健康状态,当SMART中报告PASSED的时候不理睬。一旦出现Failure，立刻用邮件通知用户指定的邮箱
	 /dev/sda -a -m  admin@example.com,root@localhost  //监控磁盘的所有属性,当SMART中报告PASSED的时候不理睬。一旦出现Failure，立刻用邮件通知用户指定的邮箱 
	 /dev/twa0 -d 3ware,0 -a -s L/../../7/00 //监控3ware 9000控制器上的第一个ATA磁盘的所有属性,在每个礼拜天的00:00--01:00进行长格式的自我检测
	 /dev/sg2 -d areca,1 -a  -s L/../(01|15)/./22 //监控Areca Raid控制器上的第一个SATA磁盘的所有属性,在每个礼拜月的第1天和第15天的22:00--23:00进行长格式的自我检测
	 -s (O/../.././(00|06|12|18)|S/../.././01|L/../../6/03) //在每天的00:00,06:00,12:00,18:00进行离线的自检，并在每天的01:00-02:00进行短格式的自检，并在每个礼拜6的03:00-04:00进行长格式的自检 
	配置好smartd.conf后需执行
	/etc/init.d/smartd restart 即可生效
	其他和smartd.conf相关的配置可参见:
	http://smartmontools.sourceforge.net/man/smartd.conf.5.html

# 11.[Linux source命令](http://www.cnblogs.com/pkufork/p/linux_source.html)

	Linux source命令：

	通常用法：source filepath 或 . filepath

	功能：使当前shell读入路径为filepath的shell文件并依次执行文件中的所有语句，通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录。例如，当我们修改了/etc/profile文件，并想让它立刻生效，而不用重新登录，就可以使用source命令，如source /etc/profile。

	source命令(从 C Shell 而来)是bash shell的内置命令；点命令(.)，就是个点符号(从Bourne Shell而来)是source的另一名称。这从用法中也能看出来。

	 

	source filepath 与 sh filepath 、./filepath的区别：

	当shell脚本具有可执行权限时，用sh filepath与./filepath是没有区别的。./filepath是因为当前目录没有在PATH中，所有"."是用来表示当前目录的。

	sh filepath 会重新建立一个子shell，在子shell中执行脚本里面的语句，该子shell继承父shell的环境变量，但子shell是新建的，其改变的变量不会被带回父shell，除非使用export。

	source filename其实只是简单地读取脚本里面的语句依次在当前shell里面执行，没有建立新的子shell。那么脚本里面所有新建、改变变量的语句都会保存在当前shell里面。

	 

	举例说明：

	新建一个test.sh脚本，内容为:A=1；

	修改其可执行权限：chmod +x test.sh；

	运行sh test.sh后，echo $A，显示为空，因为A=1并未传回给当前shell；

	运行./test.sh后，也是一样的效果；

	运行source test.sh 或者 . test.sh，然后echo $A，则会显示1，说明A=1的变量在当前shell中；

# 12.[windows server 2008解决无法PING通问题](https://jingyan.baidu.com/article/a24b33cd6926be19fe002b2c.html)

	windows server 2008解决无法PING通问题

	今天安装服务器（ｓｅｒｖｅｒ　２００８），配置完IP地址后，发现局域网其它电脑无法PING通服务器，测线仪测试链路都正常，网线接别的电脑也正常，以为是网卡问题，于是ping了自己的IP，发现能PING通，怀疑应该是２００８策略问题，果然找到解决方法。

	方法/步骤
	
	右键电脑，找到【管理】

	在服务器管理里找到【配置】项

	在高级安全windows防火墙里，找到【入站规则】，找到【文件和打印机共享（回显请求-ICMPv4-in）】双击。此时图片状态默认是没选中的


	找到【文件和打印机共享（回显请求-ICMPv4-in）】右击……选择【启用规则】就OK了！为避免以后不方便查找网络问题，此项尽量开启比较好。
![图片](https://github.com/vekrio/stu/blob/master/20170718/photo/1b4c510fd9f9d72a52d03f23d72a2834349bbb53.jpg?raw=true)




# 13.[虚拟机centos7安装 mariadb并修改默认密码设置远程访问](http://blog.csdn.net/u010757785/article/details/52152854)
   ## centos7默认MySQL是maridb

	注意：mariadb与mysql root权限不同




	本机连接虚拟机mariadb(本机连接虚拟机mysql,远程连接设置)
	centos查看ip


	这里为了防止失败，我首先检查mysql和mariadb没有安装

	 

	[root@localhost usr]# ps aux|grep mysql     #检测mysql服务
	root       2180  0.0  0.0 112664   972 pts/0    S+   17:46   0:00 grep --color=auto mysql
	[root@localhost usr]# whereis mysql     #是否有mysql残留文件
	[root@localhost usr]#
	mysql:[root@localhost usr]# whereis mariadb             #查找是否有mariadb如果有就会显示文件夹先卸掉
	mysql:[root@localhost usr]#
	[root@localhost usr]# ps aux|grep mariadb               #是否有安装mariadb服务出现下面一行就是没有安装
	root       2201  0.0  0.0 112664   980 pts/0    S+   17:48   0:00 grep --color=auto mariadb
	[root@localhost usr]# yum install mariadb mariadb-server         #这是安装mariadb和mariadb服务
	已加载插件：fastestmirror
	Loading mirror speeds from cached hostfile
	 * base: mirrors.tuna.tsinghua.edu.cn
	 * extras: mirrors.yun-idc.com
	 * updates: mirrors.sina.cn
	正在解决依赖关系
	--> 正在检查事务
	---> 软件包 mariadb.x86_64.1.5.5.47-1.el7_2 将被 安装
	--> 正在处理依赖关系 mariadb-libs(x86-64) = 1:5.5.47-1.el7_2，它被软件包 1:mariadb-5.5.47-1.el7_2.x86_64 需要
	---> 软件包 mariadb-server.x86_64.1.5.5.47-1.el7_2 将被 安装
	--> 正在检查事务
	---> 软件包 mariadb-libs.x86_64.1.5.5.47-1.el7_2 将被 安装
	--> 解决依赖关系完成

	依赖关系解决

	=======================================================================================================================================
	 Package                            架构                       版本                                  源                           大小
	=======================================================================================================================================
	正在安装:
	 mariadb                            x86_64                     1:5.5.47-1.el7_2                      updates                     8.9 M
	 mariadb-server                     x86_64                     1:5.5.47-1.el7_2                      updates                      11 M
	为依赖而安装:
	 mariadb-libs                       x86_64                     1:5.5.47-1.el7_2                      updates                     755 k

	事务概要
	=======================================================================================================================================
	安装  2 软件包 (+1 依赖软件包)

	总下载量：20 M
	安装大小：108 M
	Is this ok [y/d/N]: y
	Downloading packages:
	(1/3): mariadb-libs-5.5.47-1.el7_2.x86_64.rpm                                                                   | 755 kB  00:00:02     
	(2/3): mariadb-5.5.47-1.el7_2.x86_64.rpm                                                                        | 8.9 MB  00:00:08     
	(3/3): mariadb-server-5.5.47-1.el7_2.x86_64.rpm                                                                 |  11 MB  00:00:11     
	---------------------------------------------------------------------------------------------------------------------------------------
	总计                                                                                                   1.7 MB/s |  20 MB  00:00:11     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  正在安装    : 1:mariadb-libs-5.5.47-1.el7_2.x86_64                                                                               1/3
	  正在安装    : 1:mariadb-5.5.47-1.el7_2.x86_64                                                                                    2/3
	  正在安装    : 1:mariadb-server-5.5.47-1.el7_2.x86_64                                                                             3/3
	warning: /var/log/mariadb/mariadb.log created as /var/log/mariadb/mariadb.log.rpmnew
	  验证中      : 1:mariadb-server-5.5.47-1.el7_2.x86_64                                                                             1/3
	  验证中      : 1:mariadb-libs-5.5.47-1.el7_2.x86_64                                                                               2/3
	  验证中      : 1:mariadb-5.5.47-1.el7_2.x86_64                                                                                    3/3

	已安装:
	  mariadb.x86_64 1:5.5.47-1.el7_2                                mariadb-server.x86_64 1:5.5.47-1.el7_2                               

	作为依赖被安装:
	  mariadb-libs.x86_64 1:5.5.47-1.el7_2                                                                                                 

	完毕！
	[root@localhost usr]# systemctl start mariadb.server
	Failed to start mariadb.server.service: Unit mariadb.server.service failed to load: No such file or directory.
	[root@localhost usr]# systemctl start mariadb.service
	[root@localhost usr]# ps aux|grep mariadb
	mysql      2487  0.6  8.4 904952 84404 ?        Sl   17:53   0:00 /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysql --plugin-dir=/usr/lib64/mysql/plugin --log-error=/var/log/mariadb/mariadb.log --pid-file=/var/run/mariadb/mariadb.pid --socket=/var/lib/mysql/mysql.sock
	root       2521  0.0  0.0 112664   980 pts/0    S+   17:54   0:00 grep --color=auto mariadb

###	[root@localhost ~]# mysql -u root                        /*mariadb直接回车，密码为空*/

### [root@localhost ~]# mysqladmin -u root -p password ******     /*mariadb修改密码：-u root，是指定用户，指定修改root用户的密码。
	-p password 是密码选项，其后面的newpasswd即为新的密码*/
	
	[root@localhost usr]# mysql_secure_installation
	/usr/bin/mysql_secure_installation:行379: find_mysql_client: 未找到命令

	NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
		  SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

	In order to log into MariaDB to secure it, we'll need the current
	password for the root user.  If you've just installed MariaDB, and
	you haven't set the root password yet, the password will be blank,
	so you should just press enter here.

	Enter current password for root (enter for none): 
	OK, successfully used password, moving on...

	Setting the root password ensures that nobody can log into the MariaDB
	root user without the proper authorisation.

	Set root password? [Y/n] y     #这里选择Y是否重新设置密码
	New password:                  #新密码
	Re-enter new password:         #重复新密码
	Password updated successfully!
	Reloading privilege tables..
	 ... Success!


	By default, a MariaDB installation has an anonymous user, allowing anyone
	to log into MariaDB without having to have a user account created for
	them.  This is intended only for testing, and to make the installation
	go a bit smoother.  You should remove them before moving into a
	production environment.

	Remove anonymous users? [Y/n] n        #是否清楚其他用户的意思吧
	 ... skipping.

	Normally, root should only be allowed to connect from 'localhost'.  This
	ensures that someone cannot guess at the root password from the network.

	Disallow root login remotely? [Y/n] n         #是否禁止远程访问
	 ... skipping.

	By default, MariaDB comes with a database named 'test' that anyone can
	access.  This is also intended only for testing, and should be removed
	before moving into a production environment.

	Remove test database and access to it? [Y/n] y   #是否删除测试数据
	 - Dropping test database...
	 ... Success!
	 - Removing privileges on test database...
	 ... Success!

	Reloading the privilege tables will ensure that all changes made so far
	will take effect immediately.

	Reload privilege tables now? [Y/n] y          #是否重置权限
	 ... Success!

	Cleaning up...

	All done!  If you've completed all of the above steps, your MariaDB
	installation should now be secure.

	Thanks for using MariaDB!
	#这里就完成了
	#下面重启一下mariadb服务和apache服务
	[root@localhost usr]# systemctl restart mariadb.service
	[root@localhost usr]# systemctl restart httpd.service
	[root@localhost usr]# mysql -u root -p    #登录看一下是否成功
	Enter password: 
	Welcome to the MariaDB monitor.  Commands end with ; or \g.
	Your MariaDB connection id is 3
	Server version: 5.5.47-MariaDB MariaDB Server

	Copyright (c) 2000, 2015, Oracle, MariaDB Corporation Ab and others.

	Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

	MariaDB [(none)]> 

	之前看了一篇文章觉得太扯了，本来之前是看别人写的，后来自己研究一下，发现完全是两回事


	下面发现本地无法访问虚拟机可是ip都能ping通呀！我以为是防火墙，但是我发现我虚拟机防火墙是默认关闭的

	那就只有一个就是权限问题

	这里可以接着上面直接往下走

	[plain] view plain copy print?
	MariaDB [(none)]> use mysql   #<span style="font-family:Arial;">进入mysql库</span>  
	Reading table information for completion of table and column names  
	You can turn off this feature to get a quicker startup with -A  
	  
	Database changed  
	MariaDB [mysql]> select user,password,host from user;     #查询所有用户权限反正不管了  
	<span style="font-family:Arial;">#</span>我这里是之前<span style="font-family:Arial;">没整干净所以这样的</span>  
	+------+-------------------------------------------+-----------------------+  
	| user | password                                  | host                  |  
	+------+-------------------------------------------+-----------------------+  
	| root | *DB469070DB0AD0CA0B93040D166D7FC4713D6961 | localhost             |  
	| root | *DB469070DB0AD0CA0B93040D166D7FC4713D6961 | localhost.localdomain |  
	| root | *DB469070DB0AD0CA0B93040D166D7FC4713D6961 | 127.0.0.1             |  
	| root | *DB469070DB0AD0CA0B93040D166D7FC4713D6961 | ::1                   |  
	|      |                                           | localhost             |  
	|      |                                           | localhost.localdomain |  
	+------+-------------------------------------------+-----------------------+  
	6 rows in set (0.00 sec)  
	<span style="color:#362e2b;"><span style="font-size:14px;"><span style="font-family:Arial;"></span></span></span><pre name="code" class="plain"><span style="font-family:Arial;">#‘%’意思给用户设置所有ip都可以访问</span>  
	MariaDB [mysql]> grant all privileges on *.* to root@"%" identified by "1q2w3e4r";
	Query OK, 0 rows affected (0.00 sec)MariaDB [mysql]> flush privileges; #提交Query OK, 0 rows affected (0.00 sec)MariaDB [mysql]> quit 退出Bye[root@localhost usr]# systemctl stop mariadb.service #停止服务[root@localhost usr]# ps aux|grep mariadb #看一下mariadb服务是否停止如下已停止root 2899 0.0 0.0 112664 980 pts/0 S+ 19:01 0:00 grep --color=auto mariadb[root@localhost usr]# systemctl start mariadb #启动赶快本地用navcat连接试一下
	[root@localhost usr]# ip addr #不知道ip centos7用ip addr查看 建议最好用静态ip不然每次secure充连多麻烦
	1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN 
		link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
		inet 127.0.0.1/8 scope host lo
		   valid_lft forever preferred_lft forever
		inet6 ::1/128 scope host 
		   valid_lft forever preferred_lft forever
	2: eno16777736: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
		link/ether 00:0c:29:4f:a3:ab brd ff:ff:ff:ff:ff:ff
		inet 192.168.0.173/24 brd 192.168.0.255 scope global dynamic eno16777736
		   valid_lft 7166sec preferred_lft 7166sec
		inet6 fe80::20c:29ff:fe4f:a3ab/64 scope link 
		   valid_lft forever preferred_lft forever
   
   
   
   
			
			
#  14.查询某个工具包是哪个包装出来的（这里比如netstat）
	which netstat    /*看看有没装netstat*/
	如没装，在一个已经装好的服务器上查询which netstat
	/usr/bin/netstat
	rpm -qf  /usr/bin/netstat    /*查询netstat是哪个包装出来的*/
	
	
#	15  [CentOS 7 上安装 Docker详解](http://www.linuxidc.com/Linux/2014-12/110034.htm)
		Docker 是一个开源工具，它可以让创建和管理 Linux 容器变得简单。容器就像是轻量级的虚拟机，并且可以以毫秒级的速度来启动或停止。Docker 帮助系统管理员和程序员在容器中开发应用程序，并且可以扩展到成千上万的节点。

	容器和 VM（虚拟机）的主要区别是，容器提供了基于进程的隔离，而虚拟机提供了资源的完全隔离。虚拟机可能需要一分钟来启动，而容器只需要一秒钟或更短。容器使用宿主操作系统的内核，而虚拟机使用独立的内核。

	Docker 的局限性之一是，它只能用在 64 位的操作系统上。



	在这篇文章中我们将讨论如何在 CentOS 7.x 中安装 docker。

	CentOS 6/7系列安装Docker http://www.linuxidc.com/Linux/2014-07/104768.htm

	Docker的搭建Gitlab CI 全过程详解 http://www.linuxidc.com/Linux/2013-12/93537.htm

	Docker安装应用(CentOS 6.5_x64) http://www.linuxidc.com/Linux/2014-07/104595.htm

	在 Docker 中使用 MySQL http://www.linuxidc.com/Linux/2014-01/95354.htm

	在Ubuntu Trusty 14.04 (LTS) (64-bit)安装Docker http://www.linuxidc.com/Linux/2014-10/108184.htm

	Docker安装应用(CentOS 6.5_x64) http://www.linuxidc.com/Linux/2014-07/104595.htm

	Ubuntu 14.04安装Docker  http://www.linuxidc.com/linux/2014-08/105656.htm

	阿里云CentOS 6.5 模板上安装 Docker http://www.linuxidc.com/Linux/2014-11/109107.htm

	CentOS 7 中 Docker 的安装

	Docker 软件包已经包括在默认的 CentOS-Extras 软件源里。因此想要安装 docker，只需要运行下面的 yum 命令：

	[root@localhost ~]# yum install docker
	启动 Docker 服务

	安装完成后，使用下面的命令来启动 docker 服务，并将其设置为开机启动：

	[root@localhost ~]# service docker start
	[root@localhost ~]# chkconfig docker on
	（LCTT 译注：此处采用了旧式的 sysv 语法，如采用CentOS 7中支持的新式 systemd 语法，如下：

	[root@localhost ~]# systemctl start docker.service
	[root@localhost ~]# systemctl enable docker.service
	）

	下载官方的 CentOS 镜像到本地 （LCTT 译注：由于 Docker 被墙 :-< ，所以请使用 http://docker.cn  的镜像，感谢 @马全一 的镜像。 ）

	[root@localhost ~]# docker pull centos
	Pulling repository centos
	192178b11d36:Download complete
	70441cac1ed5:Download complete
	ae0c2d0bdc10:Download complete
	511136ea3c5a:Download complete
	5b12ef8fd570:Download complete
	确认 CentOS 镜像已经被获取：

	[root@localhost ~]# docker images centos
	REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE
	centos centos5 192178b11d362 weeks ago 466.9 MB
	centos centos6 70441cac1ed52 weeks ago 215.8 MB
	centos centos7 ae0c2d0bdc10 2 weeks ago 224 MB
	centos latest ae0c2d0bdc10 2 weeks ago 224 MB
	运行一个 Docker 容器：

	[root@localhost ~]# docker run -i -t centos /bin/bash
	[root@dbf66395436d /]#
	我们可以看到，CentOS 容器已经被启动，并且我们得到了 bash 提示符。在 docker 命令中我们使用了 “-i 捕获标准输入输出”和 “-t 分配一个终端或控制台”选项。若要断开与容器的连接，输入 exit。

	[root@cd05639b3f5c /]# cat /etc/RedHat-release
	CentOSLinux release 7.0.1406(Core)
	[root@cd05639b3f5c /]#exit
	exit
	[root@localhost ~]#
	我们还可以搜索基于 Fedora 和 Ubuntu 操作系统的容器。

	[root@localhost ~]# docker search ubuntu
	[root@localhost ~]# docker search fedora
	显示当前正在运行容器的列表

	
#	16.centos7安装云监工

	
	yum -y install net-tools

	yum install setuptool（使用setup配置工具很方便地配置防火墙、网络、系统服务等配置项）

	上传crysadm到/root

	yum -y install wget

	cd /etc/yum.repos.d/
	mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
	wget -O CentOS-Base.repo http://mirrors.163.com/.help/CentOS7-Base-163.repo

	wget http://mirrors.fuzhihui.cn/linux/centos/7/crysadm/nginx.repo

	yum clean all

	yum makecache
	
	python -V    /*查看python版本*/

	cd 
	yum -y install openssl-devel bzip2-devel gdbm-devem-devel readline-devel sqlite-devel gcc make gcc++

	ls
	cd crysadm
	wget http://img.fuzhihui.cn/Python-3.4.4.tgz

	tar -zxvf Python-3.4.4.tgz 

	mv Python-3.4.4 /usr/bin
	ll /usr/bin | grep python
	cd /usr/bin/Python-3.4.4/

	./configure

	make && make install

	python3.4 -V

	yum -y install epel-release
	cd /root/crysadm/
	ls
	yum -y install redis

	rm -rf get-pip.py
	wget http://mirrors.fuzhihui.cn/linux/centos/7/crysadm/get-pip.py

	python3.4 get-pip.py 

	pip3.4 install --upgrade pip

	pip3.4 install --upgrade redis

	pip3.4 install --upgrade requests

	pip3.4 install --upgrade flask

	pip3.4 install --upgrade flask-mail

	rm -rf run.sh 
	wget http://mirrors.fuzhihui.cn/linux/centos/7/crysadm/run.sh

	chmod +x run.sh 
	./run.sh 


	systemctl stop firewalld.service

	systemctl disable firewalld.service




	yum -y install nginx



	cd /etc/nginx/

	rm -rf nginx.conf

	wget http://mirrors.fuzhihui.cn/linux/centos/7/crysadm/nginx.conf



	cd conf.d

	rm -rf default.conf

	wget http://mirrors.fuzhihui.cn/linux/centos/7/crysadm/default.conf


	wget http://mirrors.fuzhihui.cn/linux/centos/7/crysadm/crysadm.conf



	cd

	setsebool -P httpd_can_network_connect 1

	systemctl restart nginx.service
	
	
<<<<<<< HEAD
#  17.[思科CISCO4900M交换机CONSOLE密码破解](http://jingyan.baidu.com/article/d621e8da2d8a622865913f2a.html)

#  18.[cisco3560交换机密码破解](http://jingyan.baidu.com/article/0964eca270688a8285f536eb.html)
=======
# 17.[分区工具parted的详解及常用分区使用方法](http://zhangmingqian.blog.51cto.com/1497276/1068779)
	
	一、         parted的用途及说明
	概括使用说明：
	
	parted用于对磁盘（或RAID磁盘）进行分区及管理，与fdisk分区工具相比，支持2TB以上的磁盘分区，并且允许调整分区的大小。
	
	GNU手册说明：
	
	parted是一个用于硬盘分区或调整分区大小的工具。使用它你可以创建、清除、调整、移动和复制ext2、ext3、linux-swap、FAT、FAT32和
	
	reiserfs分区；也能创建、调整和移动苹果系统的HFS分区；还能检测jfs、ntfs、ufs和xfs分区。该工具常用于为新安装的操作系统创建空
	ygfv bcv b nm  b
	间，重新分配硬盘使用情况，在将数据拷贝到新硬盘的时候也常常使用。

	二、         parted的使用方法及步骤
	
	1、对磁盘进行分区
![图片1](https://github.com/vekrio/stu/blob/master/20170718/photo/%E5%88%86%E5%8C%BA%E5%B7%A5%E5%85%B7parted%E7%9A%84%E8%AF%A6%E8%A7%A3%E5%8F%8A%E5%B8%B8%E7%94%A8%E5%88%86%E5%8C%BA%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%951.png?raw=true)
![图片2](https://github.com/vekrio/stu/blob/master/20170718/photo/%E5%88%86%E5%8C%BA%E5%B7%A5%E5%85%B7parted%E7%9A%84%E8%AF%A6%E8%A7%A3%E5%8F%8A%E5%B8%B8%E7%94%A8%E5%88%86%E5%8C%BA%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%952.png?raw=true)
![图片3](https://github.com/vekrio/stu/blob/master/20170718/photo/%E5%88%86%E5%8C%BA%E5%B7%A5%E5%85%B7parted%E7%9A%84%E8%AF%A6%E8%A7%A3%E5%8F%8A%E5%B8%B8%E7%94%A8%E5%88%86%E5%8C%BA%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%953.png?raw=true)
![图片4](https://github.com/vekrio/stu/blob/master/20170718/photo/%E5%88%86%E5%8C%BA%E5%B7%A5%E5%85%B7parted%E7%9A%84%E8%AF%A6%E8%A7%A3%E5%8F%8A%E5%B8%B8%E7%94%A8%E5%88%86%E5%8C%BA%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%954.png?raw=true)

	  [root@CentOS7 ~]# parted /dev/sdb
	GNU Parted 3.1
	Using /dev/sdb
	Welcome to GNU Parted! Type 'help' to view a list of commands.
	(parted) p                                                                
	Model: ATA ST4000NM0035-1V4 (scsi)
	Disk /dev/sdb: 4001GB
	Sector size (logical/physical): 512B/512B
	Partition Table: gpt
	Disk Flags: 

	Number  Start   End     Size    File system  Name  Flags
	 1      17.4kB  4001GB  4001GB               p1

	(parted) q                                                                
	[root@CentOS7 ~]# mkfs.ext4 /dev/sdb1
	mke2fs 1.42.9 (28-Dec-2013)
	Filesystem label=
	OS type: Linux
	Block size=4096 (log=2)
	Fragment size=4096 (log=2)
	Stride=0 blocks, Stripe width=0 blocks
	244195328 inodes, 976754637 blocks
	48837731 blocks (5.00%) reserved for the super user
	First data block=0
	Maximum filesystem blocks=3124756480
	29809 block groups
	32768 blocks per group, 32768 fragments per group
	8192 inodes per group
	Superblock backups stored on blocks: 
			32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
			4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968, 
			102400000, 214990848, 512000000, 550731776, 644972544

	Allocating group tables: done                            
	Writing inode tables: done                            
	Creating journal (32768 blocks): done
	Writing superblocks and filesystem accounting information: done       

	[root@CentOS7 ~]# pvs
	  PV         VG             Fmt  Attr PSize  PFree 
	  /dev/sda2  centos_centos7 lvm2 a--  74.04g 64.00m
	[root@CentOS7 ~]# df -h
	Filesystem                       Size  Used Avail Use% Mounted on
	/dev/mapper/centos_centos7-root   48G  5.7G   42G  12% /
	devtmpfs                         1.7G     0  1.7G   0% /dev
	tmpfs                            1.8G  140K  1.8G   1% /dev/shm
	tmpfs                            1.8G  8.9M  1.7G   1% /run
	tmpfs                            1.8G     0  1.8G   0% /sys/fs/cgroup
	/dev/mapper/centos_centos7-home   24G  3.7G   20G  16% /home
	/dev/sda1                        497M  125M  373M  26% /boot
	[root@CentOS7 ~]# mount /dev/sdb1 /home/u
	[root@CentOS7 ~]# df -h
	Filesystem                       Size  Used Avail Use% Mounted on
	/dev/mapper/centos_centos7-root   48G  5.7G   42G  12% /
	devtmpfs                         1.7G     0  1.7G   0% /dev
	tmpfs                            1.8G  140K  1.8G   1% /dev/shm
	tmpfs                            1.8G  8.9M  1.7G   1% /run
	tmpfs                            1.8G     0  1.8G   0% /sys/fs/cgroup
	/dev/mapper/centos_centos7-home   24G  3.7G   20G  16% /home
	/dev/sda1                        497M  125M  373M  26% /boot
	/dev/sdb1                        3.6T   89M  3.4T   1% /home/u
	[root@CentOS7 ~]# 
	
	
#  18.[centos7安装aria2及web端](http://blog.csdn.net/yangfanv/article/details/69952065)
	1.安装mini版centos7系统默认关闭防火墙和selinux
	2.安装wget    yum install -y wget
	3.安装EPEL源
	wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm   #下载epel源rpm包

	rpm -ivh epel-release-latest-7.noarch.rpm        #安装rpm包
	4.安装Aria2

	yum install aria2

	5.生成配置文件并编辑
	mkdir /etc/aria2/   #创建目录
	vi /etc/aria2/aria2.conf   #创建配置文件
	
	
	配置文件内容:
	
	#用户名
	#rpc-user=user
	#密码
	#rpc-passwd=passwd
	#上面的认证方式不建议使用,建议使用下面的token方式
	#设置加密的密钥
	#rpc-secret=token
	#允许rpc
	enable-rpc=true
	#允许所有来源, web界面跨域权限需要
	rpc-allow-origin-all=true
	#允许外部访问，false的话只监听本地端口
	rpc-listen-all=true
	#RPC端口, 仅当默认端口被占用时修改
	rpc-listen-port=6800
	#最大同时下载数(任务数), 路由建议值: 3
	max-concurrent-downloads=5
	#断点续传
	continue=true
	#同服务器连接数
	max-connection-per-server=5
	#最小文件分片大小, 下载线程数上限取决于能分出多少片, 对于小文件重要
	min-split-size=10M
	#单文件最大线程数, 路由建议值: 5
	split=10
	#下载速度限制
	max-overall-download-limit=0
	#单文件速度限制
	max-download-limit=0
	#上传速度限制
	max-overall-upload-limit=0
	#单文件速度限制
	max-upload-limit=0
	#断开速度过慢的连接
	#lowest-speed-limit=0
	#验证用，需要1.16.1之后的release版本
	#referer=*
	#文件保存路径, 默认为当前启动位置
	dir=/root/downloads
	#文件缓存, 使用内置的文件缓存, 如果你不相信Linux内核文件缓存和磁盘内置缓存时使用
	#disk-cache=0
	#另一种Linux文件缓存方式
	#enable-mmap=true
	#文件预分配, 能有效降低文件碎片, 提高磁盘性能. 缺点是预分配时间较长
	file-allocation=prealloc
	
	
	启动测试：
	aria2c --conf-path=/etc/aria2/aria2.conf

	6.安装Git  yum install -y git

	安装前端控制UI：
	git clone https://github.com/ziahamza/webui-aria2 #从git上下载webui-aria2 UI端
![photo](https://github.com/vekrio/stu/blob/master/20170718/photo/20170410173751749_1.png?raw=true)


	7.安装httpd    yum  -y  install  httpd
![photo](https://github.com/vekrio/stu/blob/master/20170718/photo/20170410174022231_2.png?raw=true)



	8.把克隆下载的webui-aria2 复制到/var/www/html/下  我就不讲命令了，自己百度linux复制或移动目录命令
![photo](https://github.com/vekrio/stu/blob/master/20170718/photo/20170410174533858_3.png?raw=true)

	9.安装完成后，“aria2c  --enable-rpc  --rpc-listen-all”启用监听RP
	我是这个鬼样子
![photo](https://github.com/vekrio/stu/blob/master/20170718/photo/20170410174852531_3.png?raw=true)
	解决办法，我是重启系统也就是centos7，原因应该是开头时候我们测试aria2时候端口占用。
	然后我们就开始测试连通性了
	10.浏览器访问推荐使用谷歌浏览器或火狐浏览器

		http://IP地址/webui，就可访问成功；如果报错，在“设置”--> “服务器设置”中“主机：”后后面填写自己的IP地址就可；

		如果Aria2.conf配置文件中启用了RPC安全认证，需要在WEB客户端设置中填入RPC用户名和密码，否则客户端报错！如果是自己用，
			个人觉得没必要用RPC认证，打开/etc/aria2.conf删除里面的RPC用户名和密码
![photo](https://github.com/vekrio/stu/blob/master/20170718/photo/20170410175602774_5.png?raw=true)

	11.其他开机启动就自己百度呗
	无错误后台启动：
	aria2c --conf-path=/etc/aria2/aria2.conf -D
	下载目录看见web界面快速访问设置dir吗
	参考http://www.2kil.com/9472.html    http://painting.blog.51cto.com/10476797/1730074



# 	19.[cisco3560交换机密码破解:新IOS](http://jingyan.baidu.com/article/0964eca270688a8285f536eb.html)

#	20.[思科CISCO4900M交换机CONSOLE密码破解:旧IOS](http://jingyan.baidu.com/article/d621e8da2d8a622865913f2a.html)

#	21.[yum -y upgrade 和 yum -y update 区别](http://www.linuxidc.com/Linux/2013-08/88808.htm)
	分别测试yum -y upgrade和yum -y update

	升级前

	系统版本：  CentOS5.5

	内核版本：  2.6.18-194.el5

	升级前做过简单配置文件修改

	yum -y upgrade    升级后

	系统版本：    centos5.7

	内核版本：  2.6.18-194.el5

	系统和软件配置不做修改

	yum -y update    升级后

	系统版本：    centos5.7

	内核版本：    2.6.18-238.el5

	系统和软件配置文件更新

	结论：

	yum -y update

	升级所有包，改变软件设置和系统设置,系统版本内核都升级

	yum -y upgrade

	升级所有包，不改变软件设置和系统设置，系统版本升级，内核不改变
	
# 	22.	[Centos 7中安装Python包管理工具——Pip](http://blog.lxx1.com/1420)

	pip 是一个常用的Python包管理工具，主要是用于安装 PyPI 上的软件包，可以替代 easy_install 工具。
	这里解决的是无法安装pip 时问题，或者说是如何在Centos 7中安装Python包管理工具Pip 。

	一、脚本安装pip
	首先下载get-pip.py脚本，然后运行即可安装：

	$  curl -O https://bootstrap.pypa.io/get-pip.py
	$  python get-pip.py
	二、使用包管理软件安装
	1、首先安装epel扩展源：

	$ sudo yum -y install epel-release
	
	2、然后安装python-pip

	$ sudo yum -y install python-pip

	 
	三、其他linux中安装 Pip
	1、Debian/Ubuntu

	sudo apt-get install python-pip
	2、Fedora

	Fedora 21:

	   Python 2:

			sudo yum upgrade python-setuptools
			sudo yum install python-pip python-wheel
	   Python 3:

			sudo yum install python3 python3-wheel
	Fedora 22:

	   Python 2:

			sudo dnf upgrade python-setuptools
			sudo dnf install python-pip python-wheel
	   Python 3:

			sudo dnf install python3 python3-wheel
	3、openSUSE

	   Python 2:

			sudo zypper install python-pip python-setuptools python-wheel
	   Python 3:

			sudo zypper install python3-pip python3-setuptools python3-wheel
	4、Arch Linux

	   Python 2:

			sudo pacman -S python2-pip
	   Python 3:

			sudo pacman -S python-pip
	 

		
#	23。centos7.2测速

    首先安装epel扩展源：

　　yum -y install epel-release

　　更新完成之后，就可安装pip：

　　yum -y install python-pip

　　安装完成之后清除cache：

　　yum clean all

	Last login: Tue Aug 15 22:17:50 2017 from 180.117.106.199
###	[root@localhost ~]# yum -y install epel-release
	已加载插件：fastestmirror, langpacks
	Loading mirror speeds from cached hostfile
	 * base: mirrors.btte.net
	 * extras: mirrors.163.com
	 * updates: mirrors.163.com
	正在解决依赖关系
	--> 正在检查事务
	---> 软件包 epel-release.noarch.0.7-9 将被 安装
	--> 解决依赖关系完成

	依赖关系解决

	============================================================================================================================================================
	 Package                                   架构                                版本                               源                                   大小
	============================================================================================================================================================
	正在安装:
	 epel-release                              noarch                              7-9                                extras                               14 k

	事务概要
	============================================================================================================================================================
	安装  1 软件包

	总下载量：14 k
	安装大小：24 k
	Downloading packages:
	epel-release-7-9.noarch.rpm                                                                                                          |  14 kB  00:00:00     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  正在安装    : epel-release-7-9.noarch                                                                                                                 1/1 
	  验证中      : epel-release-7-9.noarch                                                                                                                 1/1 

	已安装:
	  epel-release.noarch 0:7-9                                                                                                                                 

	完毕！
###	[root@localhost ~]# yum clean all
	已加载插件：fastestmirror, langpacks
	正在清理软件源： base epel extras updates
	Cleaning up everything
	Cleaning up list of fastest mirrors
###	[root@localhost ~]# yum makecache
	已加载插件：fastestmirror, langpacks
	base                                                                                                                                 | 3.6 kB  00:00:00     
	epel/x86_64/metalink                                                                                                                 | 6.5 kB  00:00:00     
	epel                                                                                                                                 | 4.3 kB  00:00:00     
	extras                                                                                                                               | 3.4 kB  00:00:00     
	updates                                                                                                                              | 3.4 kB  00:00:00     
	(1/17): base/7/x86_64/group_gz                                                                                                       | 155 kB  00:00:00     
	(2/17): epel/x86_64/group_gz                                                                                                         | 170 kB  00:00:00     
	(3/17): epel/x86_64/updateinfo                                                                                                       | 807 kB  00:00:00     
	(4/17): epel/x86_64/primary_db                                                                                                       | 4.7 MB  00:00:02     
	(5/17): epel/x86_64/other_db                                                                                                         | 2.2 MB  00:00:04     
	(6/17): extras/7/x86_64/filelists_db                                                                                                 | 1.1 MB  00:00:00     
	(7/17): extras/7/x86_64/prestodelta                                                                                                  | 149 kB  00:00:00     
	(8/17): extras/7/x86_64/primary_db                                                                                                   | 191 kB  00:00:00     
	(9/17): extras/7/x86_64/other_db                                                                                                     | 903 kB  00:00:00     
	(10/17): updates/7/x86_64/filelists_db                                                                                               | 4.4 MB  00:00:00     
	(11/17): updates/7/x86_64/prestodelta                                                                                                | 954 kB  00:00:00     
	(12/17): updates/7/x86_64/primary_db                                                                                                 | 7.8 MB  00:00:01     
	(13/17): base/7/x86_64/primary_db                                                                                                    | 5.6 MB  00:00:18     
	(14/17): updates/7/x86_64/other_db                                                                                                   |  93 MB  00:00:10     
	(15/17): base/7/x86_64/other_db                                                                                                      | 2.4 MB  00:01:19     
	base/7/x86_64/filelists_db     FAILED                                          ======================================-    ] 118 kB/s | 127 MB  00:01:36 ETA 
	http://mirrors.nju.edu.cn/centos/7.3.1611/os/x86_64/repodata/3a1b41925bb25892c1003b22979ea0705aa815fed57f992cf0229b76539a9ac4-filelists.sqlite.bz2: [Errno 12] Timeout on http://mirrors.nju.edu.cn/centos/7.3.1611/os/x86_64/repodata/3a1b41925bb25892c1003b22979ea0705aa815fed57f992cf0229b76539a9ac4-filelists.sqlite.bz2: (28, 'Operation too slow. Less than 1000 bytes/sec transferred the last 30 seconds')
	正在尝试其它镜像。
	(16/17): base/7/x86_64/filelists_db                                                                                                  | 6.6 MB  00:00:03     
	(17/17): epel/x86_64/filelists_db                                                                                                    | 7.9 MB  00:02:20     
	Determining fastest mirrors
	 * base: mirrors.cn99.com
	 * epel: mirrors.ustc.edu.cn
	 * extras: mirrors.163.com
	 * updates: mirrors.163.com
	元数据缓存已建立
###	[root@localhost ~]# yum -y install pip
	已加载插件：fastestmirror, langpacks
	Loading mirror speeds from cached hostfile
	 * base: mirrors.cn99.com
	 * epel: mirrors.ustc.edu.cn
	 * extras: mirrors.163.com
	 * updates: mirrors.163.com
	没有可用软件包 pip。
	错误：无须任何处理
###	[root@localhost ~]# yum -y install python-pip
	已加载插件：fastestmirror, langpacks
	Loading mirror speeds from cached hostfile
	 * base: mirrors.cn99.com
	 * epel: mirrors.ustc.edu.cn
	 * extras: mirrors.163.com
	 * updates: mirrors.163.com
	正在解决依赖关系
	--> 正在检查事务
	---> 软件包 python2-pip.noarch.0.8.1.2-5.el7 将被 安装
	--> 解决依赖关系完成

	依赖关系解决

	============================================================================================================================================================
	 Package                                 架构                               版本                                     源                                大小
	============================================================================================================================================================
	正在安装:
	 python2-pip                             noarch                             8.1.2-5.el7                              epel                             1.7 M

	事务概要
	============================================================================================================================================================
	安装  1 软件包

	总下载量：1.7 M
	安装大小：7.2 M
	Downloading packages:
	警告：/var/cache/yum/x86_64/7/epel/packages/python2-pip-8.1.2-5.el7.noarch.rpm: 头V3 RSA/SHA256 Signature, 密钥 ID 352c64e5: NOKEY/s | 864 kB  --:--:-- ETA 
	python2-pip-8.1.2-5.el7.noarch.rpm 的公钥尚未安装
	python2-pip-8.1.2-5.el7.noarch.rpm                                                                                                   | 1.7 MB  00:00:02     
	从 file:///etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7 检索密钥
	导入 GPG key 0x352C64E5:
	 用户ID     : "Fedora EPEL (7) <epel@fedoraproject.org>"
	 指纹       : 91e9 7d7c 4a5e 96f1 7f3e 888f 6a2f aea2 352c 64e5
	 软件包     : epel-release-7-9.noarch (@extras)
	 来自       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  正在安装    : python2-pip-8.1.2-5.el7.noarch                                                                                                          1/1 
	  验证中      : python2-pip-8.1.2-5.el7.noarch                                                                                                          1/1 

	已安装:
	  python2-pip.noarch 0:8.1.2-5.el7                                                                                                                          

	完毕！
###	[root@localhost ~]# easy_install speedtest-cli
	Searching for speedtest-cli
	Reading https://pypi.python.org/simple/speedtest-cli/
	Best match: speedtest-cli 1.0.6
	Downloading https://pypi.python.org/packages/12/3e/e6d34ed8ce9f2d111480fd585e5404a00d74cfd3d076c538f31538195ec8/speedtest-cli-1.0.6.tar.gz#md5=594bc47b1bc11fcc4861eedb976feecb
	Processing speedtest-cli-1.0.6.tar.gz
	Writing /tmp/easy_install-yoD4Ga/speedtest-cli-1.0.6/setup.cfg
	Running speedtest-cli-1.0.6/setup.py -q bdist_egg --dist-dir /tmp/easy_install-yoD4Ga/speedtest-cli-1.0.6/egg-dist-tmp-XHjtOC
	zip_safe flag not set; analyzing archive contents...
	Adding speedtest-cli 1.0.6 to easy-install.pth file
	Installing speedtest script to /usr/bin
	Installing speedtest-cli script to /usr/bin

	Installed /usr/lib/python2.7/site-packages/speedtest_cli-1.0.6-py2.7.egg
	Processing dependencies for speedtest-cli
	Finished processing dependencies for speedtest-cli
###	[root@localhost ~]# ls 
	anaconda-ks.cfg
###	[root@localhost ~]# pip install --upgrade pip
	Collecting pip
	  Downloading pip-9.0.1-py2.py3-none-any.whl (1.3MB)
		100% |████████████████████████████████| 1.3MB 35kB/s 
	Installing collected packages: pip
	  Found existing installation: pip 8.1.2
		Uninstalling pip-8.1.2:
		  Successfully uninstalled pip-8.1.2
	Successfully installed pip-9.0.1
###	[root@localhost ~]# git clone https://github.com/sivel/speedtest-cli.git
	bash: git: 未找到命令...
###	[root@localhost ~]# yum -y install git
	已加载插件：fastestmirror, langpacks
	Loading mirror speeds from cached hostfile
	 * base: mirrors.cn99.com
	 * epel: mirrors.ustc.edu.cn
	 * extras: mirrors.163.com
	 * updates: mirrors.163.com
	正在解决依赖关系
	--> 正在检查事务
	---> 软件包 git.x86_64.0.1.8.3.1-6.el7_2.1 将被 安装
	--> 正在处理依赖关系 perl-Git = 1.8.3.1-6.el7_2.1，它被软件包 git-1.8.3.1-6.el7_2.1.x86_64 需要
	--> 正在处理依赖关系 perl(Term::ReadKey)，它被软件包 git-1.8.3.1-6.el7_2.1.x86_64 需要
	--> 正在处理依赖关系 perl(Git)，它被软件包 git-1.8.3.1-6.el7_2.1.x86_64 需要
	--> 正在处理依赖关系 perl(Error)，它被软件包 git-1.8.3.1-6.el7_2.1.x86_64 需要
	--> 正在检查事务
	---> 软件包 perl-Error.noarch.1.0.17020-2.el7 将被 安装
	---> 软件包 perl-Git.noarch.0.1.8.3.1-6.el7_2.1 将被 安装
	---> 软件包 perl-TermReadKey.x86_64.0.2.30-20.el7 将被 安装
	--> 解决依赖关系完成

	依赖关系解决

	============================================================================================================================================================
	 Package                                   架构                            版本                                         源                             大小
	============================================================================================================================================================
	正在安装:
	 git                                       x86_64                          1.8.3.1-6.el7_2.1                            base                          4.4 M
	为依赖而安装:
	 perl-Error                                noarch                          1:0.17020-2.el7                              base                           32 k
	 perl-Git                                  noarch                          1.8.3.1-6.el7_2.1                            base                           53 k
	 perl-TermReadKey                          x86_64                          2.30-20.el7                                  base                           31 k

	事务概要
	============================================================================================================================================================
	安装  1 软件包 (+3 依赖软件包)

	总下载量：4.5 M
	安装大小：22 M
	Downloading packages:
	(1/4): perl-Git-1.8.3.1-6.el7_2.1.noarch.rpm                                                                                         |  53 kB  00:00:00     
	(2/4): perl-TermReadKey-2.30-20.el7.x86_64.rpm                                                                                       |  31 kB  00:00:00     
	(3/4): perl-Error-0.17020-2.el7.noarch.rpm                                                                                           |  32 kB  00:00:00     
	(4/4): git-1.8.3.1-6.el7_2.1.x86_64.rpm                                                                                              | 4.4 MB  00:00:02     
	------------------------------------------------------------------------------------------------------------------------------------------------------------
	总计                                                                                                                        1.8 MB/s | 4.5 MB  00:00:02     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  正在安装    : 1:perl-Error-0.17020-2.el7.noarch                                                                                                       1/4 
	  正在安装    : perl-TermReadKey-2.30-20.el7.x86_64                                                                                                     2/4 
	  正在安装    : git-1.8.3.1-6.el7_2.1.x86_64                                                                                                            3/4 
	  正在安装    : perl-Git-1.8.3.1-6.el7_2.1.noarch                                                                                                       4/4 
	  验证中      : perl-Git-1.8.3.1-6.el7_2.1.noarch                                                                                                       1/4 
	  验证中      : perl-TermReadKey-2.30-20.el7.x86_64                                                                                                     2/4 
	  验证中      : 1:perl-Error-0.17020-2.el7.noarch                                                                                                       3/4 
	  验证中      : git-1.8.3.1-6.el7_2.1.x86_64                                                                                                            4/4 

	已安装:
	  git.x86_64 0:1.8.3.1-6.el7_2.1                                                                                                                            

	作为依赖被安装:
	  perl-Error.noarch 1:0.17020-2.el7                perl-Git.noarch 0:1.8.3.1-6.el7_2.1                perl-TermReadKey.x86_64 0:2.30-20.el7               

	完毕！
###	[root@localhost ~]# git clone https://github.com/sivel/speedtest-cli.git
	正克隆到 'speedtest-cli'...
	remote: Counting objects: 913, done.
	remote: Total 913 (delta 0), reused 0 (delta 0), pack-reused 913
	接收对象中: 100% (913/913), 264.34 KiB | 148.00 KiB/s, done.
	处理 delta 中: 100% (515/515), done.
###	[root@localhost ~]# ls 
	anaconda-ks.cfg  speedtest-cli
###	[root@localhost ~]# cd speedtest-cli/
###	[root@localhost speedtest-cli]# ll
	总用量 96
	-rw-r--r--. 1 root root  1671 8月  15 23:04 CONTRIBUTING.md
	-rw-r--r--. 1 root root 11358 8月  15 23:04 LICENSE
	-rw-r--r--. 1 root root    35 8月  15 23:04 MANIFEST.in
	-rw-r--r--. 1 root root  5215 8月  15 23:04 README.rst
	-rw-r--r--. 1 root root    20 8月  15 23:04 setup.cfg
	-rw-r--r--. 1 root root  3196 8月  15 23:04 setup.py
	-rw-r--r--. 1 root root  2385 8月  15 23:04 speedtest-cli.1
	-rw-r--r--. 1 root root  1200 8月  15 23:04 speedtest_cli.py
	-rwxr-xr-x. 1 root root 47228 8月  15 23:04 speedtest.py
	-rw-r--r--. 1 root root   333 8月  15 23:04 tox.ini
###	[root@localhost speedtest-cli]# ./speedtest.py
	Retrieving speedtest.net configuration...
	Testing from China Telecom (61.155.49.166)...
	Retrieving speedtest.net server list...
	Selecting best server based on ping...
	Hosted by China Mobile Group Jiangsu Co.,Ltd. (Wuxi) [154.00 km]: 19.032 ms
	Testing download speed................................................................................
	Download: 23.56 Mbit/s
	Testing upload speed................................................................................................
	Upload: 11.36 Mbit/s
###	[root@localhost speedtest-cli]# ./speedtest.py
	Retrieving speedtest.net configuration...
	Testing from China Telecom (61.155.49.166)...
	Retrieving speedtest.net server list...
	Selecting best server based on ping...
	Hosted by China Mobile Group Jiangsu Co.,Ltd. (Wuxi) [154.00 km]: 29.803 ms
	Testing download speed................................................................................
	Download: 47.78 Mbit/s
	Testing upload speed................................................................................................
	Upload: 13.57 Mbit/s
###	[root@localhost speedtest-cli]# speedtest-cli --list | grep China
	 5446) CHINA UNICOM JIANGSU COMPANY (Nanjing, China) [1.67 km]
	13704) China Unicom (Nanjing, China) [1.80 km]
	 5724) ChinaUnicom (Hefei, China) [142.64 km]
	 4377) China Mobile Group Anhui Co.,Ltd (Hefei, China) [142.64 km]
	 5122) China Mobile Group Jiangsu Co.,Ltd. (Wuxi, China) [154.00 km]
	 3927) China Mobile Jiangsu Co., Ltd. (Suzhou, China) [191.28 km]
	 4647) China Mobile Group Zhejiang Co.,Ltd (Hangzhou, China) [240.93 km]
	12278) China Mobile Group Zhejiang Branch (Hangzhou, China) [240.93 km]
	 5300) Hangzhou , Zhejiang Unicom (Hangzhou, China) [240.93 km]
	 7509) China Telecom ZheJiang Branch (Hangzhou, China) [240.93 km]
	 3633) China Telecom (Shanghai, China) [274.95 km]
	 4665) China Mobile Group Shanghai Co.,LTD (Shanghai, China) [274.95 km]
	 5083) Shanghai Branch, China Unicom (Shanghai, China) [274.95 km]
	 6715) China Mobile Group Zhejiang Co., Ltd. (Ningbo, China) [359.75 km]
	 5097) Chinaunicom.jx (Nanchang, China) [467.10 km]
	 7230) China Unicom.JiangXi Co.,Ltd (Nanchang, China) [467.10 km]
	 5563) JINAN Wo China company (Jinan, China) [537.86 km]
	12538) SHANDONG UNICOM (Jinan, China) [537.86 km]
	 6810) HENAN UNICOM (Zhengzhou, China) [562.89 km]
	 5131) China unicom henan branch (Zhengzhou, China) [562.89 km]
	 4595) China Telecom HeNan Branch (Zhengzhou, China) [562.89 km]
	 6435) china Telecom hubei branch (Xiangyang, China) [626.25 km]
	12637) China Telecom Xiangyang Branch (XiangYang, China) [626.25 km]
	 4884) China Unicom FuJian (Fuzhou, China) [667.54 km]
	 4870) Changsha, Hunan Unicom (Changsha, China) [704.41 km]
	 6132) ChinaTelecom.Hunan (Changsha, China) [704.41 km]
	 5475) China Unicom (Tianjin, China) [799.39 km]
	 5506) china unicom (Xiamen, China) [848.03 km]
	12868) China unicom shanxi branch (Taiyuan, China) [858.63 km]
	 5505) Beijing Broadband Network (Beijing, China) [899.03 km]
	 4751) Beijing Telecom (Beijing, China) [899.03 km]
	 6302) Beijing Fiber City (Beijing, China) [899.03 km]
	 5145) Beijing Unicom (Beijing, China) [899.03 km]
	 4863) Xi'an branch,Chinaunicom (Xi'an, China) [951.12 km]
	11605) HHB SOLUTIONS (Guangzhou, China) [1131.65 km]
	 5081) ShenZhen Telecom (Shenzhen, China) [1154.24 km]
	10201) China Network Unicom Shenzhen Branch (Shenzhen, China) [1154.24 km]
	12512) nmzl (Huhehaote, China) [1160.25 km]
	 5017) China Unicom,Liaoning Branch (Shenyang, China) [1166.75 km]
	 6852) FPT Telecom (Chai Wan, China) [1177.32 km]
	 2993) Website Solution Limited (Hong Kong, China) [1182.16 km]
	10267) Interoute VDC (Hong Kong, China) [1182.16 km]
	12990) QTS Data Centers (Hong Kong, China) [1182.16 km]
	 1536) STC (Hong Kong, China) [1182.16 km]
	 8170) Atombase Global Datamation (Hong Kong, China) [1182.16 km]
	 5726) China Unicom Chong Qing Branch (Chongqing, China) [1198.20 km]
	 6592) China Telecom Chongqing (Chongqing, China) [1198.20 km]
	 5509) Chinaunicom Ningxia branch (Ningxia, China) [1333.26 km]
	11444) University of Electronic Science and Technology of China (Chengdu, China) [1404.59 km]
	 4624) ChinaTelecom (Chengdu, China) [1404.59 km]
	 2461) China Unicom (Chengdu, China) [1404.59 km]
	10742) Changchun Unicom (Changchun, China) [1432.71 km]
	 9484) China Unicom (Changchun, China) [1432.71 km]
	 4690) China Unicom Lanzhou Branch Co.Ltd (Lanzhou, China) [1447.09 km]
	10305) GX-Telecom (Nanning, China) [1455.24 km]
	 5674) GX-Unicom (Nanning, China) [1455.24 km]
	 5992) Qinghai China Unicom (Xining, China) [1639.68 km]
	 5460) China Unicom Heilongjiang Branch (Harbin, China) [1664.91 km]
	 5103) Yunnan Chinaunicom (Kunming, China) [1751.00 km]
	 6168) China Telecom (Kunming, China) [1751.00 km]
	 5750) Lhasaunicom (Lhasa, China) [2648.36 km]
	 6144) xjunicom (Urumqi, China) [3005.19 km]
###	[root@localhost speedtest-cli]# speedtest-cli --server=3633 --share
	Retrieving speedtest.net configuration...
	Cannot retrieve speedtest configuration
	ERROR: <urlopen error timed out>
###	[root@localhost speedtest-cli]# 

 #另注释：speedtest-cli  用法
![1](https://github.com/vekrio/stu/blob/master/20170718/photo/speedtest-cli%E5%91%BD%E4%BB%A4_Linux%20speedtest-cli%20%E5%91%BD%E4%BB%A4%E7%94%A8%E6%B3%95%E8%AF%A6%E8%A7%A3%EF%BC%9A%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%B8%8B%E6%B5%8B%E8%AF%95%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%A4%96%E7%BD%91%E9%80%9F%E5%BA%A61.png?raw=true)
![2](https://github.com/vekrio/stu/blob/master/20170718/photo/speedtest-cli%E5%91%BD%E4%BB%A4_Linux%20speedtest-cli%20%E5%91%BD%E4%BB%A4%E7%94%A8%E6%B3%95%E8%AF%A6%E8%A7%A3%EF%BC%9A%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%B8%8B%E6%B5%8B%E8%AF%95%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%A4%96%E7%BD%91%E9%80%9F%E5%BA%A62.png?raw=true)
![3](https://github.com/vekrio/stu/blob/master/20170718/photo/speedtest-cli%E5%91%BD%E4%BB%A4_Linux%20speedtest-cli%20%E5%91%BD%E4%BB%A4%E7%94%A8%E6%B3%95%E8%AF%A6%E8%A7%A3%EF%BC%9A%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%B8%8B%E6%B5%8B%E8%AF%95%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%A4%96%E7%BD%91%E9%80%9F%E5%BA%A63.png?raw=true)
	-h, --help show this help message and exit
	--share 分享你的网速，该命令会在speedtest网站上生成网速测试结果的图片。
	--simple Suppress verbose output, only show basic information 
	--list 根据距离显示speedtest.net的测试服务器列表。
	--server=SERVER 指定列表中id的服务器来做测试。 
	--mini=MINI URL of the Speedtest Mini server 
	--source=SOURCE Source ip address to bind to 
	--version Show the version number and exit
	
#  24.[各种端口以及相应的服务](http://www.cnblogs.com/chenbuer/p/3842281.html)

	1 tcpmux TCP 端口服务多路复用 
	5 rje 远程作业入口 
	7 echo Echo 服务 
	9 discard 用于连接测试的空服务 
	11 systat 用于列举连接了的端口的系统状态 
	13 daytime 给请求主机发送日期和时间 
	17 qotd 给连接了的主机发送每日格言 
	18 msp 消息发送协议 
	19 chargen 字符生成服务；发送无止境的字符流 
	20 ftp-data FTP 数据端口 
	21 ftp 文件传输协议（FTP）端口；有时被文件服务协议（FSP）使用 
	22 ssh 安全 Shell（SSH）服务 
	23 telnet Telnet 服务 
	25 smtp 简单邮件传输协议（SMTP） 
	37 time 时间协议 
	39 rlp 资源定位协议 
	42 nameserver 互联网名称服务 
	43 nicname WHOIS 目录服务 
	49 tacacs 用于基于 TCP/IP 验证和访问的终端访问控制器访问控制系统 
	50 re-mail-ck 远程邮件检查协议 
	53 domain 域名服务（如 BIND） NOTE：其实就是DNS域名解析服务
	63 whois++ WHOIS++，被扩展了的 WHOIS 服务 
	67 bootps 引导协议（BOOTP）服务；还被动态主机配置协议（DHCP）服务使用 
	68 bootpc Bootstrap（BOOTP）客户；还被动态主机配置协议（DHCP）客户使用 
	69 tftp 小文件传输协议（TFTP） 
	70 gopher Gopher 互联网文档搜寻和检索 
	71 netrjs-1 远程作业服务 
	72 netrjs-2 远程作业服务 
	73 netrjs-3 远程作业服务 
	73 netrjs-4 远程作业服务 
	79 finger 用于用户联系信息的 Finger 服务 
	80 http 用于万维网（WWW）服务的超文本传输协议（HTTP） 
	88 kerberos Kerberos 网络验证系统 
	95 supdup Telnet 协议扩展 
	101 hostname SRI-NIC 机器上的主机名服务 
	102 iso-tsap ISO 开发环境（ISODE）网络应用 
	105 csnet-ns 邮箱名称服务器；也被 CSO 名称服务器使用 
	107 rtelnet 远程 Telnet 
	109 pop2 邮局协议版本2 
	110 pop3 邮局协议版本3 
	111 sunrpc 用于远程命令执行的远程过程调用（RPC）协议，被网络文件系统（NFS）使用 
	113 auth 验证和身份识别协议 
	115 sftp 安全文件传输协议（SFTP）服务 
	117 uucp-path Unix 到 Unix 复制协议（UUCP）路径服务 
	119 nntp 用于 USENET 讨论系统的网络新闻传输协议（NNTP） 
	123 ntp 网络时间协议（NTP） 
	137 netbios-ns 在红帽企业 Linux 中被 Samba 使用的 NETBIOS 名称服务 
	138 netbios-dgm 在红帽企业 Linux 中被 Samba 使用的 NETBIOS 数据报服务 
	139 netbios-ssn 在红帽企业 Linux 中被 Samba 使用的NET BIOS 会话服务 
	143 imap 互联网消息存取协议（IMAP） 
	161 snmp 简单网络管理协议（SNMP） 
	162 snmptrap SNMP 的陷阱 
	163 cmip-man 通用管理信息协议（CMIP） 
	164 cmip-agent 通用管理信息协议（CMIP） 
	174 mailq MAILQ 
	177 xdmcp X 显示管理器控制协议 
	178 nextstep NeXTStep 窗口服务器 
	179 bgp 边界网络协议 
	191 prospero Cliffod Neuman 的 Prospero 服务 
	194 irc 互联网中继聊天（IRC） 
	199 smux SNMP UNIX 多路复用 
	201 at-rtmp AppleTalk 选路 
	202 at-nbp AppleTalk 名称绑定 
	204 at-echo AppleTalk echo 服务 
	206 at-zis AppleTalk 区块信息 
	209 qmtp 快速邮件传输协议（QMTP） 
	210 z39.50 NISO Z39.50 数据库 
	213 ipx 互联网络分组交换协议（IPX），被 Novell Netware 环境常用的数据报协议 
	220 imap3 互联网消息存取协议版本3 
	245 link LINK 
	347 fatserv Fatmen 服务器 
	363 rsvp_tunnel RSVP 隧道 
	369 rpc2portmap Coda 文件系统端口映射器 
	370 codaauth2 Coda 文件系统验证服务 
	372 ulistproc UNIX Listserv 
	389 ldap 轻型目录存取协议（LDAP） 
	427 svrloc 服务位置协议（SLP） 
	434 mobileip-agent 可移互联网协议（IP）代理 
	435 mobilip-mn 可移互联网协议（IP）管理器 
	443 https 安全超文本传输协议（HTTP） 加密的超文本协议https
	444 snpp 小型网络分页协议 
	445 microsoft-ds 通过 TCP/IP 的服务器消息块（SMB） 
	464 kpasswd Kerberos 口令和钥匙改换服务 
	468 photuris Photuris 会话钥匙管理协议 
	487 saft 简单不对称文件传输（SAFT）协议 
	488 gss-http 用于 HTTP 的通用安全服务（GSS） 
	496 pim-rp-disc 用于协议独立的多址传播（PIM）服务的会合点发现（RP-DISC） 
	500 isakmp 互联网安全关联和钥匙管理协议（ISAKMP） 
	535 iiop 互联网内部对象请求代理协议（IIOP） 
	538 gdomap GNUstep 分布式对象映射器（GDOMAP） 
	546 dhcpv6-client 动态主机配置协议（DHCP）版本6客户 
	547 dhcpv6-server 动态主机配置协议（DHCP）版本6服务 
	554 rtsp 实时流播协议（RTSP） 
	563 nntps 通过安全套接字层的网络新闻传输协议（NNTPS） 
	565 whoami whoami 
	587 submission 邮件消息提交代理（MSA） 
	610 npmp-local 网络外设管理协议（NPMP）本地 / 分布式排队系统（DQS） 
	611 npmp-gui 网络外设管理协议（NPMP）GUI / 分布式排队系统（DQS） 
	612 hmmp-ind HMMP 指示 / DQS 
	631 ipp 互联网打印协议（IPP） 
	636 ldaps 通过安全套接字层的轻型目录访问协议（LDAPS） 
	674 acap 应用程序配置存取协议（ACAP） 
	694 ha-cluster 用于带有高可用性的群集的心跳服务 
	749 kerberos-adm Kerberos 版本5（v5）的“kadmin”数据库管理 
	750 kerberos-iv Kerberos 版本4（v4）服务 
	765 webster 网络词典 
	767 phonebook 网络电话簿 
	873 rsync rsync 文件传输服务 
	992 telnets 通过安全套接字层的 Telnet（TelnetS） 
	993 imaps 通过安全套接字层的互联网消息存取协议（IMAPS） 
	994 ircs 通过安全套接字层的互联网中继聊天（IRCS） 
	995 pop3s 通过安全套接字层的邮局协议版本3（POPS3） 
	表 C-1. 著名端口 
	以下端口是 UNIX 特有的，涉及了从电子邮件到验证不等的服务。在方括号内的名称（如 [service]）是服务的守护进程名称或它的常用别名。 
	端口号码 / 层 名称 注释 
	512/tcp exec 用于对远程执行的进程进行验证 
	512/udp biff [comsat] 异步邮件客户（biff）和服务（comsat） 
	513/tcp login 远程登录（rlogin） 
	513/udp who [whod] 登录的用户列表 
	514/tcp shell [cmd] 不必登录的远程 shell（rshell）和远程复制（rcp） 
	514/udp syslog UNIX 系统日志服务 
	515 printer [spooler] 打印机（lpr）假脱机 
	517/udp talk 远程对话服务和客户 
	518/udp ntalk 网络交谈（ntalk），远程对话服务和客户 
	519 utime [unixtime] UNIX 时间协议（utime） 
	520/tcp efs 扩展文件名服务器（EFS） 
	520/udp router [route, routed] 选路信息协议（RIP） 
	521 ripng 用于互联网协议版本6（IPv6）的选路信息协议 
	525 timed [timeserver] 时间守护进程（timed） 
	526/tcp tempo [newdate] Tempo 
	530/tcp courier [rpc] Courier 远程过程调用（RPC）协议 
	531/tcp conference [chat] 互联网中继聊天 
	532 netnews Netnews 
	533/udp netwall 用于紧急广播的 Netwall 
	540/tcp uucp [uucpd] Unix 到 Unix 复制服务 
	543/tcp klogin Kerberos 版本5（v5）远程登录 
	544/tcp kshell Kerberos 版本5（v5）远程 shell 
	548 afpovertcp 通过传输控制协议（TCP）的 Appletalk 文件编制协议（AFP） 
	556 remotefs [rfs_server, rfs] Brunhoff 的远程文件系统（RFS） 
	表 C-2. UNIX 特有的端口 
	表 C-3列举了由网络和软件社区向 IANA 提交的要在端口号码列表中正式注册的端口。 
	端口号码 / 层 名称 注释 
	1080 socks SOCKS 网络应用程序代理服务 
	1236 bvcontrol [rmtcfg] Garcilis Packeten 远程配置服务器[a] 
	1300 h323hostcallsc H.323 电话会议主机电话安全 
	1433 ms-sql-s Microsoft SQL 服务器 
	1434 ms-sql-m Microsoft SQL 监视器 
	1494 ica Citrix ICA 客户 
	1512 wins Microsoft Windows 互联网名称服务器 
	1524 ingreslock Ingres 数据库管理系统（DBMS）锁定服务 
	1525 prospero-np 无特权的 Prospero 
	1645 datametrics [old-radius] Datametrics / 从前的 radius 项目 
	1646 sa-msg-port [oldradacct] sa-msg-port / 从前的 radacct 项目 
	1649 kermit Kermit 文件传输和管理服务 
	1701 l2tp [l2f] 第2层隧道服务（LT2P） / 第2层转发（L2F） 
	1718 h323gatedisc H.323 电讯守门装置发现机制 
	1719 h323gatestat H.323 电讯守门装置状态 
	1720 h323hostcall H.323 电讯主持电话设置 
	1758 tftp-mcast 小文件 FTP 组播 
	1759 mtftp 组播小文件 FTP（MTFTP） 
	1789 hello Hello 路由器通信端口 
	1812 radius Radius 拨号验证和记帐服务 
	1813 radius-acct Radius 记帐 
	1911 mtp Starlight 网络多媒体传输协议（MTP） 
	1985 hsrp Cisco 热备用路由器协议 
	1986 licensedaemon Cisco 许可管理守护进程 
	1997 gdp-port Cisco 网关发现协议（GDP） 
	2049 nfs [nfsd] 网络文件系统（NFS） 
	2102 zephyr-srv Zephyr 通知传输和发送服务器 
	2103 zephyr-clt Zephyr serv-hm 连接 
	2104 zephyr-hm Zephyr 主机管理器 
	2401 cvspserver 并行版本系统（CVS）客户 / 服务器操作 
	2430/tcp venus 用于 Coda 文件系统（codacon 端口）的 Venus 缓存管理器 
	2430/udp venus 用于 Coda 文件系统（callback/wbc interface 界面）的 Venus 缓存管理器 
	2431/tcp venus-se Venus 传输控制协议（TCP）的副作用 
	2431/udp venus-se Venus 用户数据报协议（UDP）的副作用 
	2432/udp codasrv Coda 文件系统服务器端口 
	2433/tcp codasrv-se Coda 文件系统 TCP 副作用 
	2433/udp codasrv-se Coda 文件系统 UDP SFTP 副作用 
	2600 hpstgmgr [zebrasrv] HPSTGMGR；Zebra 选路 

	2601 discp-client [zebra] discp 客户；Zebra 集成的 shell 
	2602 discp-server [ripd] discp 服务器；选路信息协议守护进程（ripd） 
	2603 servicemeter [ripngd] 服务计量；用于 IPv6 的 RIP 守护进程 
	2604 nsc-ccs [ospfd] NSC CCS；开放式短路径优先守护进程（ospfd） 
	2605 nsc-posa NSC POSA；边界网络协议守护进程（bgpd） 
	2606 netmon [ospf6d] Dell Netmon；用于 IPv6 的 OSPF 守护进程（ospf6d） 
	2809 corbaloc 公共对象请求代理体系（CORBA）命名服务定位器 
	3130 icpv2 互联网缓存协议版本2（v2）；被 Squid 代理缓存服务器使用 
	3306 mysql MySQL 数据库服务 
	3346 trnsprntproxy Trnsprnt 代理 
	4011 pxe 执行前环境（PXE）服务 
	4321 rwhois 远程 Whois（rwhois）服务 
	4444 krb524 Kerberos 版本5（v5）到版本4（v4）门票转换器 
	5002 rfe 无射频以太网（RFE）音频广播系统 
	5308 cfengine 配置引擎（Cfengine） 
	5999 cvsup [CVSup] CVSup 文件传输和更新工具 
	6000 x11 [X] X 窗口系统服务 
	7000 afs3-fileserver Andrew 文件系统（AFS）文件服务器 
	7001 afs3-callback 用于给缓存管理器回电的 AFS 端口 
	7002 afs3-prserver AFS 用户和组群数据库 
	7003 afs3-vlserver AFS 文件卷位置数据库 
	7004 afs3-kaserver AFS Kerberos 验证服务 
	7005 afs3-volser AFS 文件卷管理服务器 
	7006 afs3-errors AFS 错误解释服务 
	7007 afs3-bos AFS 基本监查进程 
	7008 afs3-update AFS 服务器到服务器更新器 
	7009 afs3-rmtsys AFS 远程缓存管理器服务 
	9876 sd 会话指引器 
	10080 amanda 高级 Maryland 自动网络磁盘归档器（Amanda）备份服务 
	11371 pgpkeyserver 良好隐私（PGP） / GNU 隐私卫士（GPG）公钥服务器 
	11720 h323callsigalt H.323 调用信号交替 
	13720 bprd Veritas NetBackup 请求守护进程（bprd） 
	13721 bpdbm Veritas NetBackup 数据库管理器（bpdbm） 
	13722 bpjava-msvc Veritas NetBackup Java / Microsoft Visual C++ (MSVC) 协议 
	13724 vnetd Veritas 网络工具 
	13782 bpcd Vertias NetBackup 
	13783 vopied Veritas VOPIED 协议 
	22273 wnn6 [wnn4] 假名/汉字转换系统[c] 
	26000 quake Quake（以及相关的）多人游戏服务器 
	26208 wnn6-ds 
	33434 traceroute Traceroute 网络跟踪工具 
	注: 
	a. /etc/services 中的注释如下：端口1236被注册为“bvcontrol”，但是它也被 Gracilis Packeten 远程配置服务器使用。正式名称被列为主要名称，未注册的名称被列为别名。 
	b. 在 /etc/services 中的注释：端口 2600 到 2606 被 zebra 软件包未经注册而使用。主要名称是被注册的名称，被 zebra 使用的未注册名称被列为别名。 
	c. /etc/services 文件中的注释：该端口被注册为 wnn6，但是还在 FreeWnn 软件包中使用了未注册的“wnn4”。 

	表 C-3. 注册的端口 
	表 C-4显示了一个和数据报传递协议（DDP）有关的端口列表。DDP 在 AppleTalk 网络上被使用。 
	端口号码 / 层 名称 注释 
	1/ddp rtmp 路由表管理协议 
	2/ddp nbp 名称绑定协议 
	4/ddp echo AppleTalk Echo 协议 
	6/ddp zip 区块信息协议 
	表 C-4. 数据报传递协议端口 
	表 C-5是和 Kerberos 网络验证协议相关的端口列表。在标记的地方，v5 代表 Kerberos 版本5协议。注意，这些端口没有在 IANA 注册。 
	端口号码 / 层 名称 注释 
	751 kerberos_master Kerberos 验证 
	752 passwd_server Kerberos 口令（kpasswd）服务器 
	754 krb5_prop Kerberos v5 从属传播 
	760 krbupdate [kreg] Kerberos 注册 
	1109 kpop Kerberos 邮局协议（KPOP） 
	2053 knetd Kerberos 多路分用器 
	2105 eklogin Kerberos v5 加密的远程登录（rlogin） 
	表 C-5. Kerberos（工程 Athena/MIT）端口 
	表 C-6是一个未注册的端口列表。这些端口可能被安装在你的红帽企业 Linux 系统上的服务或协议使用，或者它们是在红帽企业 Linux 和运行其它操作系统的机器通信所必需的端口。 
	端口号码 / 层 名称 注释 
	15/tcp netstat 网络状态（netstat） 
	98/tcp linuxconf Linuxconf Linux 管理工具 
	106 poppassd 邮局协议口令改变守护进程（POPPASSD） 
	465/tcp smtps 通过安全套接字层的简单邮件传输协议（SMTPS） 
	616/tcp gii 使用网关的（选路守护进程）互动界面 
	808 omirr [omirrd] 联机镜像（Omirr）文件镜像服务 
	871/tcp supfileserv 软件升级协议（SUP）服务器 
	901/tcp swat Samba 万维网管理工具（SWAT） 
	953 rndc Berkeley 互联网名称域版本9（BIND 9）远程名称守护进程配置工具 
	1127 sufiledbg 软件升级协议（SUP）调试 
	1178/tcp skkserv 简单假名到汉字（SKK）日文输入服务器 
	1313/tcp xtel 法国 Minitel 文本信息系统 
	1529/tcp support [prmsd, gnatsd] GNATS 错误跟踪系统 
	2003/tcp cfinger GNU Finger 服务 
	2150 ninstall 网络安装服务 
	2988 afbackup afbackup 客户-服务器备份系统 
	3128/tcp squid Squid 万维网代理缓存 
	3455 prsvp RSVP 端口 
	5432 postgres PostgreSQL 数据库 
	4557/tcp fax FAX 传输服务（旧服务） 
	4559/tcp hylafax HylaFAX 客户-服务器协议（新服务） 
	5232 sgi-dgl SGI 分布式图形库 
	5354 noclog NOCOL 网络操作中心记录守护进程（noclogd） 
	5355 hostmon NOCOL 网络操作中心主机监视 
	5680/tcp canna Canna 日文字符输入界面 
	6010/tcp x11-ssh-offset 安全 Shell（SSH）X11 转发偏移 
	6667 ircd 互联网中继聊天守护进程（ircd） 
	7100/tcp xfs X 字体服务器（XFS） 
	7666/tcp tircproxy Tircproxy IRC 代理服务 
	8008 http-alt 超文本传输协议（HTTP）的另一选择 
	8080 webcache 万维网（WWW）缓存服务 
	8081 tproxy 透明代理 
	9100/tcp jetdirect [laserjet, hplj] Hewlett-Packard (HP) JetDirect 网络打印服务 
	9359 mandelspawn [mandelbrot] 用于 X 窗口系统的并行 Mandelbrot 生成程序 
	10081 kamanda 使用 Kerberos 的 Amanda 备份服务 
	10082/tcp amandaidx Amanda 备份服务 
	10083/tcp amidxtape Amanda 备份服务 
	20011 isdnlog 综合业务数字网（ISDN）登录系统 
	20012 vboxd ISDN 音箱守护进程（vboxd） 
	22305/tcp wnn4_Kr kWnn 韩文输入系统 
	22289/tcp wnn4_Cn cWnn 中文输入系统 
	22321/tcp wnn4_Tw tWnn 中文输入系统（台湾） 
	24554 binkp Binkley TCP/IP Fidonet 邮寄程序守护进程 
	27374 asp 地址搜索协议 
	60177 tfido Ifmail FidoNet 兼容邮寄服务 
	60179 fido FidoNet 电子邮件和新闻网络
	
#	25. [RHEL 7 & CentOS 7禁用IPV6](http://blog.csdn.net/bluishglc/article/details/41390785)
	RHEL 7 & CentOS 7下禁用IPV6的方法和之前的版本不太一样了，本文整理了一下处理方法：本文原文出处: http://blog.csdn.net/bluishglc/article/details/41390785 严禁任何形式的转载，否则将委托CSDN官方维护权益！

	首先，我们必须给出最根本的解决方法：修改grub，在引导时就不加载IPV6模块

![1](https://github.com/vekrio/stu/blob/master/20170718/photo/20141122232658847.png?raw=true)

	这样修改之后，使用

	# lsmod | grep ipv6

	进行验证！

	下面我们再看一种处理方式，它不如上面提到的方式彻底，但也是有效的！
	验证IPV6是否关闭

	1. 通过命令：

	Check to see if you’re installation is currently set up for IPv6:

	# cat /proc/sys/net/ipv6/conf/all/disable_ipv6

	If the output is 0, IPv6 is enabled.
	If the output is 1, IPv6 is already disabled.

	需要特别说明的是：在这种方法下，使用# lsmod | grep ipv6依然会有一些相关模块列出。

	2. 通过ifconfig查看网卡信息，以下打开和关闭ipv6的差别：
![2](https://github.com/vekrio/stu/blob/master/20170718/photo/221212121212121.png?raw=true)

	禁用IPV6的操作步骤
	Step 1: add this rule in /etc/sysctl.conf : net.ipv6.conf.all.disable_ipv6=1

	Step 2: add this rule in /etc/sysconfig/network: NETWORKING_IPV6=no

	Step 3: add this setting for each nic X (X is the corresponding number for each nic) in /etc/sysconfig/network-scripts/ifcfg-ethX: IPV6INIT=no

	Step 4: disable the ip6tables service : chkconfig ip6tables off

	Step 5: Reload the sysctl configuration:

	# sysctl -p
	or
	# reboot

	注意：禁用IPV6后，可能会导致某些服务无法启动,比如VSFTP，对于VSFTP，需要修改/etc/vsftpd/vsftpd.conf文件中的listen和listen_ipv6两个选项：
	listen=YES
	listen_ipv6=NO

#	25.[Centos7下的systemctl命令与service和chkconfig](http://blog.csdn.net/cds86333774/article/details/51165361)

#    26.centos7最小化安装支持tab补全
	yum -y install bash-completion

#	27.yum -y install vim*

#	28. tar -zvxf 文件解压缩 tar -zcvf 新压缩文件名.tar.gz  需要压缩的文件

#	29.hwclock 
###	-r  读取硬件时钟
###	-s  硬件时钟->系统时钟
###	-w  系统时钟->硬件时钟

# 	30.更改主机名：nmtui

#	31.[CentOS7使用firewalld打开关闭防火墙与端口](http://www.cnblogs.com/moxiaoan/p/5683743.html)
###		1、firewalld的基本使用
		启动： systemctl start firewalld
		查看状态： systemctl status firewalld 
		停止： systemctl disable firewalld
		禁用： systemctl stop firewalld
		 
###		2.systemctl是CentOS7的服务管理工具中主要的工具，它融合之前service和chkconfig的功能于一体。
		启动一个服务：systemctl start firewalld.service
		关闭一个服务：systemctl stop firewalld.service
		重启一个服务：systemctl restart firewalld.service
		显示一个服务的状态：systemctl status firewalld.service
		在开机时启用一个服务：systemctl enable firewalld.service
		在开机时禁用一个服务：systemctl disable firewalld.service
		查看服务是否开机启动：systemctl is-enabled firewalld.service
		查看已启动的服务列表：systemctl list-unit-files|grep enabled
		查看启动失败的服务列表：systemctl --failed

###		3.配置firewalld-cmd

		查看版本： firewall-cmd --version
		查看帮助： firewall-cmd --help
		显示状态： firewall-cmd --state
		查看所有打开的端口： firewall-cmd --zone=public --list-ports
		更新防火墙规则： firewall-cmd --reload
		查看区域信息:  firewall-cmd --get-active-zones
		查看指定接口所属区域： firewall-cmd --get-zone-of-interface=eth0
		拒绝所有包：firewall-cmd --panic-on
		取消拒绝状态： firewall-cmd --panic-off
		查看是否拒绝： firewall-cmd --query-panic
		 
		那怎么开启一个端口呢
		添加
		firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）
		重新载入
		firewall-cmd --reload
		查看
		firewall-cmd --zone= public --query-port=80/tcp
		删除
		firewall-cmd --zone= public --remove-port=80/tcp --permanent
		
		
		
#	32.[宝塔Linux面板](https://www.bt.cn/)

#	33.[【Linux下如何创建 阵列 Raid 1】](http://m.toutiaocdn.cn/group/6454709155730031118/?iid=13449879950&app=news_article&tt_from=android_share&utm_medium=toutiao_android&utm_campaign=client_share)

#	34.[Linux有问必答：如何扩展XFS文件系统](https://linux.cn/article-3997-1.html)

#	35.[解决SSH连接超时的2个配置方法](http://sooxin.iteye.com/blog/2314305)
	连自己的VPS经常会断开，时间久了感觉挺讨厌，以下是两种解决方法。
	方法一：
	1、设置服务器向SSH客户端连接会话发送频率和时间
	.代码如下:
	#vi /etc/ssh/sshd_config，添加如下两行
	ClientAliveInterval 60
	ClientAliveCountMax 86400

	注：
	ClientAliveInterval选项定义了每隔多少秒给SSH客户端发送一次信号；
	ClientAliveCountMax选项定义了超过多少秒后断开与ssh客户端连接
	2、重新启动系统SSH服务
	.代码如下:
	#service sshd restart 
	 
	方法二：
	使用命令直接用户修改配置文件，设置“TMOUT=180”，即超时时间为3分钟
	.代码如下:
	#vim /etc/profile 添加下面两行
	#设置为3分钟
	TMOUT=180
	
	
#	36.[Centos7开机启动自己的脚本](http://blog.csdn.net/qq_32783353/article/details/72866915)	
###	1. 自己新建一个脚本,如centnet-service.sh

	经过后面的几个步骤后,这个脚本在开机的时候会执行,在这个脚本里面可以写你开机的时候想执行的命令,如启动python等服务

###	2. 在脚本中输入启动服务的命令,如(开机启动python 服务端):

	#!/bin/bash
	python /home/usr/bin/server.py 

	or

	#!/bin/bash
	export JDK_HOME=/home/java/jdk1.8.0_91
	export JAVA_HOME=/home/java/jdk1.8.0_91
	/home/tomcat/apache-tomcat-8.0.36/bin/startup.sh
	
###	3. 执行如下命令,将该脚本标记为可执行文件(添加可执行的权限)

	chmod +x /home/centnet/centnet-service.sh
	
###	4. 执行如下命令将/etc/rc.d/rc.local文标记为可执行文件

	在centos7中,/etc/rc.d/rc.local文件的权限被降低了,开机的时候执行在自己的脚本是不能起动一些服务的,执行下面的命令可以文件标记为可执行的文件

	chmod +x /etc/rc.d/rc.local
	
###	5. 打开/etc/rc.d/rc.local文件,在最后面添加如下脚本

	/home/centnet/centnet-service.sh
	
	这样,centnet-service.sh这个脚本在开机的时候就会被执行了,以后再这里面写启动服务的命令就可以了.

# 37.[Linux扩展Swap分区的三种方法](http://blog.sina.com.cn/s/blog_7c80356b0102wgro.html)

		What's Swap?

	当物理内存占用完了后，当系统还需要更多的物理内存时，物理内存中Inactive Pages 就转移到了到Swap空间。Swap 空间是在位于硬盘上的一个逻辑分区，因此访问速度较物理内存慢。

	当机器的物理内存发生变化时，Swap 分区也要根据需要作相应的扩展。

	有三种方法可以对Swap 分区进行扩展：

	一、扩展正在使用的Swap 分区的逻辑卷（Recommended）；

	二、新建Swap 分区；

	三、新建swap file。

	具体步骤如下：

	一、扩展正在使用的Swap 分区的逻辑卷

	设定用作Swap 分区的逻辑卷为：/dev/VolGroup00/LogVol01

	#swapoff -v /dev/VolGroup00/LogVol01    //关闭该卷的Swap分区

	# lvm lvresize /dev/VolGroup00/LogVol01 -L +1024M    //为该卷的容量增加1024M

	# mkswap /dev/VolGroup00/LogVol01    //格式化Swap分区

	# swapon -va    //启用Swap分区

	# free    //验证结果

	二、新建Swap 分区

	设定新建的Swap 分区的逻辑卷为：/dev/VolGroup00/LogVol02

	# lvm lvcreate VolGroup00 -n LogVol02 -L 1024M    //新建一个1024M大小的逻辑卷

	# mkswap /dev/VolGroup00/LogVol02    //格式化成Swap分区

	#/dev/VolGroup00/LogVol02 swap swap defaults 0 0    //将这个分区信息写进fstab文件（相当于分区表）

	# swapon -va    //启动Swap分区

	# free    //验证结果

	三、新建swapfile

	通过此种方式进行Swap 的扩展，首先要计算出block的数目。具体为根据需要扩展的swapfile的大小，以M为单位。block=swap分区大小*1024, 例如，需要扩展1024M的swapfile，则：block=1024*1024=1048576。

	然后做如下步骤：

	#dd if=/dev/zero of=/swapfile bs=1024 count=1048576

	#mkswap /swapfile   //使该文件成为Swap配置文件

	#swapon /swapfile   //启用swapfile

	#/swapfile swap swap defaults 0 0   //使该文件加入开机启动项并写入fstab文件

	#free   //验证结果 

	总结：三种方法都能对Swap分区进行扩展，但是推荐使用第一种方法。

	注：以上方法仅在基于RedHat制作的发行版本（如CentOS、OracleLinux、NeoKylin等），其他诸如Fedora、Debian等系统未做测试。​
# 38.私有云搭建
	
###	[root@localhost ~]# cd /home/
###	[root@localhost home]# mkdir mycloud
###	[root@localhost home]# cd mycloud/
###	[root@localhost mycloud]# wget http://seafile-downloads.oss-cn-shanghai.aliyuncs.com/seafile-server_6.1.2_x86-64.tar.gz
	--2017-08-19 08:50:45--  http://seafile-downloads.oss-cn-shanghai.aliyuncs.com/seafile-server_6.1.2_x86-64.tar.gz
	正在解析主机 seafile-downloads.oss-cn-shanghai.aliyuncs.com (seafile-downloads.oss-cn-shanghai.aliyuncs.com)... 106.14.229.115
	正在连接 seafile-downloads.oss-cn-shanghai.aliyuncs.com (seafile-downloads.oss-cn-shanghai.aliyuncs.com)|106.14.229.115|:80... 已连接。
	已发出 HTTP 请求，正在等待回应... 200 OK
	长度：23948057 (23M) [application/x-tar]
	正在保存至: “seafile-server_6.1.2_x86-64.tar.gz”

	100%[===================================================================================================>] 23,948,057  2.20MB/s 用时 11s    

	2017-08-19 08:50:56 (2.17 MB/s) - 已保存 “seafile-server_6.1.2_x86-64.tar.gz” [23948057/23948057])

###	[root@localhost mycloud]# tar -xzf seafile-server_*
###	[root@localhost mycloud]# ll
	总用量 23392
	drwxrwxr-x. 6  500  500     4096 8月  14 16:45 seafile-server-6.1.2
	-rw-r--r--. 1 root root 23948057 8月  15 10:19 seafile-server_6.1.2_x86-64.tar.gz
###	[root@localhost mycloud]# cd seafile-server-6.1.2/
###	[root@localhost seafile-server-6.1.2]# ll
	总用量 132
	-rw-rw-r--.  1 500 500 11322 8月  14 16:45 check_init_admin.py
	-rwxrwxr-x.  1 500 500  1821 8月  14 16:45 reset-admin.sh
	drwxrwxr-x.  2 500 500    25 8月  14 16:45 runtime
	-rwxrwxr-x.  1 500 500  1937 8月  14 16:45 seaf-fsck.sh
	-rwxrwxr-x.  1 500 500  3325 8月  14 16:45 seaf-fuse.sh
	-rwxrwxr-x.  1 500 500  2832 8月  14 16:45 seaf-gc.sh
	drwxrwxr-x.  6 500 500    53 8月  14 16:45 seafile
	-rwxrwxr-x.  1 500 500  5176 8月  14 16:45 seafile.sh
	drwxrwxr-x. 12 500 500  4096 8月  14 16:42 seahub
	-rwxrwxr-x.  1 500 500  7737 8月  14 16:45 seahub.sh
	-rw-rw-r--.  1 500 500 52792 8月  14 16:45 setup-seafile-mysql.py
	-rwxrwxr-x.  1 500 500  2604 8月  14 16:45 setup-seafile-mysql.sh
	-rwxrwxr-x.  1 500 500 22058 8月  14 16:45 setup-seafile.sh
	drwxrwxr-x.  4 500 500  4096 8月  14 16:41 upgrade
###	[root@localhost seafile-server-6.1.2]# cd ..
###	[root@localhost mycloud]# mkdir installed
###	[root@localhost mycloud]# mv seafile-server_* installed
###	[root@localhost mycloud]# ll
	总用量 4
	drwxr-xr-x. 2 root root   48 8月  19 08:52 installed
	drwxrwxr-x. 6  500  500 4096 8月  14 16:45 seafile-server-6.1.2
###	[root@localhost mycloud]# cd seafile-server-6.1.2/
###	[root@localhost seafile-server-6.1.2]# yum install mariadb-server
	已加载插件：fastestmirror
	base                                                                                                                  | 3.6 kB  00:00:00     
	extras                                                                                                                | 3.4 kB  00:00:00     
	updates                                                                                                               | 3.4 kB  00:00:00     
	Loading mirror speeds from cached hostfile
	 * base: mirrors.zju.edu.cn
	 * extras: mirrors.cn99.com
	 * updates: mirrors.zju.edu.cn
	正在解决依赖关系
	--> 正在检查事务
	---> 软件包 mariadb-server.x86_64.1.5.5.52-1.el7 将被 安装
	--> 正在处理依赖关系 mariadb(x86-64) = 1:5.5.52-1.el7，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl-DBI，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl-DBD-MySQL，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(vars)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(strict)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Sys::Hostname)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(POSIX)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Getopt::Long)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(File::Temp)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(File::Path)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(File::Copy)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(File::Basename)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Data::Dumper)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 perl(DBI)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 libaio.so.1(LIBAIO_0.4)(64bit)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 libaio.so.1(LIBAIO_0.1)(64bit)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 /usr/bin/perl，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在处理依赖关系 libaio.so.1()(64bit)，它被软件包 1:mariadb-server-5.5.52-1.el7.x86_64 需要
	--> 正在检查事务
	---> 软件包 libaio.x86_64.0.0.3.109-13.el7 将被 安装
	---> 软件包 mariadb.x86_64.1.5.5.52-1.el7 将被 安装
	--> 正在处理依赖关系 perl(Exporter)，它被软件包 1:mariadb-5.5.52-1.el7.x86_64 需要
	---> 软件包 perl.x86_64.4.5.16.3-291.el7 将被 安装
	--> 正在处理依赖关系 perl-libs = 4:5.16.3-291.el7，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Socket) >= 1.3，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Scalar::Util) >= 1.10，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl-macros，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl-libs，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(threads::shared)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(threads)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(constant)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Time::Local)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Time::HiRes)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Storable)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Socket)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Scalar::Util)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Pod::Simple::XHTML)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Pod::Simple::Search)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Filter::Util::Call)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(File::Spec::Unix)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(File::Spec::Functions)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(File::Spec)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Cwd)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 perl(Carp)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	--> 正在处理依赖关系 libperl.so()(64bit)，它被软件包 4:perl-5.16.3-291.el7.x86_64 需要
	---> 软件包 perl-DBD-MySQL.x86_64.0.4.023-5.el7 将被 安装
	---> 软件包 perl-DBI.x86_64.0.1.627-4.el7 将被 安装
	--> 正在处理依赖关系 perl(RPC::PlServer) >= 0.2001，它被软件包 perl-DBI-1.627-4.el7.x86_64 需要
	--> 正在处理依赖关系 perl(RPC::PlClient) >= 0.2000，它被软件包 perl-DBI-1.627-4.el7.x86_64 需要
	---> 软件包 perl-Data-Dumper.x86_64.0.2.145-3.el7 将被 安装
	---> 软件包 perl-File-Path.noarch.0.2.09-2.el7 将被 安装
	---> 软件包 perl-File-Temp.noarch.0.0.23.01-3.el7 将被 安装
	---> 软件包 perl-Getopt-Long.noarch.0.2.40-2.el7 将被 安装
	--> 正在处理依赖关系 perl(Pod::Usage) >= 1.14，它被软件包 perl-Getopt-Long-2.40-2.el7.noarch 需要
	--> 正在处理依赖关系 perl(Text::ParseWords)，它被软件包 perl-Getopt-Long-2.40-2.el7.noarch 需要
	--> 正在检查事务
	---> 软件包 perl-Carp.noarch.0.1.26-244.el7 将被 安装
	---> 软件包 perl-Exporter.noarch.0.5.68-3.el7 将被 安装
	---> 软件包 perl-Filter.x86_64.0.1.49-3.el7 将被 安装
	---> 软件包 perl-PathTools.x86_64.0.3.40-5.el7 将被 安装
	---> 软件包 perl-PlRPC.noarch.0.0.2020-14.el7 将被 安装
	--> 正在处理依赖关系 perl(Net::Daemon) >= 0.13，它被软件包 perl-PlRPC-0.2020-14.el7.noarch 需要
	--> 正在处理依赖关系 perl(Net::Daemon::Test)，它被软件包 perl-PlRPC-0.2020-14.el7.noarch 需要
	--> 正在处理依赖关系 perl(Net::Daemon::Log)，它被软件包 perl-PlRPC-0.2020-14.el7.noarch 需要
	--> 正在处理依赖关系 perl(Compress::Zlib)，它被软件包 perl-PlRPC-0.2020-14.el7.noarch 需要
	---> 软件包 perl-Pod-Simple.noarch.1.3.28-4.el7 将被 安装
	--> 正在处理依赖关系 perl(Pod::Escapes) >= 1.04，它被软件包 1:perl-Pod-Simple-3.28-4.el7.noarch 需要
	--> 正在处理依赖关系 perl(Encode)，它被软件包 1:perl-Pod-Simple-3.28-4.el7.noarch 需要
	---> 软件包 perl-Pod-Usage.noarch.0.1.63-3.el7 将被 安装
	--> 正在处理依赖关系 perl(Pod::Text) >= 3.15，它被软件包 perl-Pod-Usage-1.63-3.el7.noarch 需要
	--> 正在处理依赖关系 perl-Pod-Perldoc，它被软件包 perl-Pod-Usage-1.63-3.el7.noarch 需要
	---> 软件包 perl-Scalar-List-Utils.x86_64.0.1.27-248.el7 将被 安装
	---> 软件包 perl-Socket.x86_64.0.2.010-4.el7 将被 安装
	---> 软件包 perl-Storable.x86_64.0.2.45-3.el7 将被 安装
	---> 软件包 perl-Text-ParseWords.noarch.0.3.29-4.el7 将被 安装
	---> 软件包 perl-Time-HiRes.x86_64.4.1.9725-3.el7 将被 安装
	---> 软件包 perl-Time-Local.noarch.0.1.2300-2.el7 将被 安装
	---> 软件包 perl-constant.noarch.0.1.27-2.el7 将被 安装
	---> 软件包 perl-libs.x86_64.4.5.16.3-291.el7 将被 安装
	---> 软件包 perl-macros.x86_64.4.5.16.3-291.el7 将被 安装
	---> 软件包 perl-threads.x86_64.0.1.87-4.el7 将被 安装
	---> 软件包 perl-threads-shared.x86_64.0.1.43-6.el7 将被 安装
	--> 正在检查事务
	---> 软件包 perl-Encode.x86_64.0.2.51-7.el7 将被 安装
	---> 软件包 perl-IO-Compress.noarch.0.2.061-2.el7 将被 安装
	--> 正在处理依赖关系 perl(Compress::Raw::Zlib) >= 2.061，它被软件包 perl-IO-Compress-2.061-2.el7.noarch 需要
	--> 正在处理依赖关系 perl(Compress::Raw::Bzip2) >= 2.061，它被软件包 perl-IO-Compress-2.061-2.el7.noarch 需要
	---> 软件包 perl-Net-Daemon.noarch.0.0.48-5.el7 将被 安装
	---> 软件包 perl-Pod-Escapes.noarch.1.1.04-291.el7 将被 安装
	---> 软件包 perl-Pod-Perldoc.noarch.0.3.20-4.el7 将被 安装
	--> 正在处理依赖关系 perl(parent)，它被软件包 perl-Pod-Perldoc-3.20-4.el7.noarch 需要
	--> 正在处理依赖关系 perl(HTTP::Tiny)，它被软件包 perl-Pod-Perldoc-3.20-4.el7.noarch 需要
	---> 软件包 perl-podlators.noarch.0.2.5.1-3.el7 将被 安装
	--> 正在检查事务
	---> 软件包 perl-Compress-Raw-Bzip2.x86_64.0.2.061-3.el7 将被 安装
	---> 软件包 perl-Compress-Raw-Zlib.x86_64.1.2.061-4.el7 将被 安装
	---> 软件包 perl-HTTP-Tiny.noarch.0.0.033-3.el7 将被 安装
	---> 软件包 perl-parent.noarch.1.0.225-244.el7 将被 安装
	--> 解决依赖关系完成

	依赖关系解决

	=============================================================================================================================================
	 Package                                     架构                       版本                                  源                        大小
	=============================================================================================================================================
	正在安装:
	 mariadb-server                              x86_64                     1:5.5.52-1.el7                        base                      11 M
	为依赖而安装:
	 libaio                                      x86_64                     0.3.109-13.el7                        base                      24 k
	 mariadb                                     x86_64                     1:5.5.52-1.el7                        base                     8.7 M
	 perl                                        x86_64                     4:5.16.3-291.el7                      base                     8.0 M
	 perl-Carp                                   noarch                     1.26-244.el7                          base                      19 k
	 perl-Compress-Raw-Bzip2                     x86_64                     2.061-3.el7                           base                      32 k
	 perl-Compress-Raw-Zlib                      x86_64                     1:2.061-4.el7                         base                      57 k
	 perl-DBD-MySQL                              x86_64                     4.023-5.el7                           base                     140 k
	 perl-DBI                                    x86_64                     1.627-4.el7                           base                     802 k
	 perl-Data-Dumper                            x86_64                     2.145-3.el7                           base                      47 k
	 perl-Encode                                 x86_64                     2.51-7.el7                            base                     1.5 M
	 perl-Exporter                               noarch                     5.68-3.el7                            base                      28 k
	 perl-File-Path                              noarch                     2.09-2.el7                            base                      26 k
	 perl-File-Temp                              noarch                     0.23.01-3.el7                         base                      56 k
	 perl-Filter                                 x86_64                     1.49-3.el7                            base                      76 k
	 perl-Getopt-Long                            noarch                     2.40-2.el7                            base                      56 k
	 perl-HTTP-Tiny                              noarch                     0.033-3.el7                           base                      38 k
	 perl-IO-Compress                            noarch                     2.061-2.el7                           base                     260 k
	 perl-Net-Daemon                             noarch                     0.48-5.el7                            base                      51 k
	 perl-PathTools                              x86_64                     3.40-5.el7                            base                      82 k
	 perl-PlRPC                                  noarch                     0.2020-14.el7                         base                      36 k
	 perl-Pod-Escapes                            noarch                     1:1.04-291.el7                        base                      51 k
	 perl-Pod-Perldoc                            noarch                     3.20-4.el7                            base                      87 k
	 perl-Pod-Simple                             noarch                     1:3.28-4.el7                          base                     216 k
	 perl-Pod-Usage                              noarch                     1.63-3.el7                            base                      27 k
	 perl-Scalar-List-Utils                      x86_64                     1.27-248.el7                          base                      36 k
	 perl-Socket                                 x86_64                     2.010-4.el7                           base                      49 k
	 perl-Storable                               x86_64                     2.45-3.el7                            base                      77 k
	 perl-Text-ParseWords                        noarch                     3.29-4.el7                            base                      14 k
	 perl-Time-HiRes                             x86_64                     4:1.9725-3.el7                        base                      45 k
	 perl-Time-Local                             noarch                     1.2300-2.el7                          base                      24 k
	 perl-constant                               noarch                     1.27-2.el7                            base                      19 k
	 perl-libs                                   x86_64                     4:5.16.3-291.el7                      base                     688 k
	 perl-macros                                 x86_64                     4:5.16.3-291.el7                      base                      43 k
	 perl-parent                                 noarch                     1:0.225-244.el7                       base                      12 k
	 perl-podlators                              noarch                     2.5.1-3.el7                           base                     112 k
	 perl-threads                                x86_64                     1.87-4.el7                            base                      49 k
	 perl-threads-shared                         x86_64                     1.43-6.el7                            base                      39 k

	事务概要
	=============================================================================================================================================
	安装  1 软件包 (+37 依赖软件包)

	总下载量：32 M
	安装大小：144 M
	Is this ok [y/d/N]: y
	Downloading packages:
	(1/38): libaio-0.3.109-13.el7.x86_64.rpm                                                                              |  24 kB  00:00:00     
	(2/38): mariadb-5.5.52-1.el7.x86_64.rpm                                                                               | 8.7 MB  00:00:01     
	(3/38): mariadb-server-5.5.52-1.el7.x86_64.rpm                                                                        |  11 MB  00:00:02     
	(4/38): perl-Carp-1.26-244.el7.noarch.rpm                                                                             |  19 kB  00:00:00     
	(5/38): perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64.rpm                                                                |  32 kB  00:00:00     
	(6/38): perl-Compress-Raw-Zlib-2.061-4.el7.x86_64.rpm                                                                 |  57 kB  00:00:00     
	(7/38): perl-DBD-MySQL-4.023-5.el7.x86_64.rpm                                                                         | 140 kB  00:00:00     
	(8/38): perl-5.16.3-291.el7.x86_64.rpm                                                                                | 8.0 MB  00:00:01     
	(9/38): perl-DBI-1.627-4.el7.x86_64.rpm                                                                               | 802 kB  00:00:00     
	(10/38): perl-Data-Dumper-2.145-3.el7.x86_64.rpm                                                                      |  47 kB  00:00:00     
	(11/38): perl-Exporter-5.68-3.el7.noarch.rpm                                                                          |  28 kB  00:00:00     
	(12/38): perl-File-Path-2.09-2.el7.noarch.rpm                                                                         |  26 kB  00:00:00     
	(13/38): perl-File-Temp-0.23.01-3.el7.noarch.rpm                                                                      |  56 kB  00:00:00     
	(14/38): perl-Filter-1.49-3.el7.x86_64.rpm                                                                            |  76 kB  00:00:00     
	(15/38): perl-Getopt-Long-2.40-2.el7.noarch.rpm                                                                       |  56 kB  00:00:00     
	(16/38): perl-Encode-2.51-7.el7.x86_64.rpm                                                                            | 1.5 MB  00:00:00     
	(17/38): perl-HTTP-Tiny-0.033-3.el7.noarch.rpm                                                                        |  38 kB  00:00:00     
	(18/38): perl-IO-Compress-2.061-2.el7.noarch.rpm                                                                      | 260 kB  00:00:00     
	(19/38): perl-Net-Daemon-0.48-5.el7.noarch.rpm                                                                        |  51 kB  00:00:00     
	(20/38): perl-PlRPC-0.2020-14.el7.noarch.rpm                                                                          |  36 kB  00:00:00     
	(21/38): perl-PathTools-3.40-5.el7.x86_64.rpm                                                                         |  82 kB  00:00:00     
	(22/38): perl-Pod-Escapes-1.04-291.el7.noarch.rpm                                                                     |  51 kB  00:00:00     
	(23/38): perl-Pod-Perldoc-3.20-4.el7.noarch.rpm                                                                       |  87 kB  00:00:00     
	(24/38): perl-Pod-Usage-1.63-3.el7.noarch.rpm                                                                         |  27 kB  00:00:00     
	(25/38): perl-Scalar-List-Utils-1.27-248.el7.x86_64.rpm                                                               |  36 kB  00:00:00     
	(26/38): perl-Socket-2.010-4.el7.x86_64.rpm                                                                           |  49 kB  00:00:00     
	(27/38): perl-Pod-Simple-3.28-4.el7.noarch.rpm                                                                        | 216 kB  00:00:00     
	(28/38): perl-Text-ParseWords-3.29-4.el7.noarch.rpm                                                                   |  14 kB  00:00:00     
	(29/38): perl-Storable-2.45-3.el7.x86_64.rpm                                                                          |  77 kB  00:00:00     
	(30/38): perl-Time-HiRes-1.9725-3.el7.x86_64.rpm                                                                      |  45 kB  00:00:00     
	(31/38): perl-Time-Local-1.2300-2.el7.noarch.rpm                                                                      |  24 kB  00:00:00     
	(32/38): perl-constant-1.27-2.el7.noarch.rpm                                                                          |  19 kB  00:00:00     
	(33/38): perl-macros-5.16.3-291.el7.x86_64.rpm                                                                        |  43 kB  00:00:00     
	(34/38): perl-parent-0.225-244.el7.noarch.rpm                                                                         |  12 kB  00:00:00     
	(35/38): perl-podlators-2.5.1-3.el7.noarch.rpm                                                                        | 112 kB  00:00:00     
	(36/38): perl-threads-1.87-4.el7.x86_64.rpm                                                                           |  49 kB  00:00:00     
	(37/38): perl-threads-shared-1.43-6.el7.x86_64.rpm                                                                    |  39 kB  00:00:00     
	(38/38): perl-libs-5.16.3-291.el7.x86_64.rpm                                                                          | 688 kB  00:00:00     
	---------------------------------------------------------------------------------------------------------------------------------------------
	总计                                                                                                         7.8 MB/s |  32 MB  00:00:04     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  正在安装    : 1:perl-parent-0.225-244.el7.noarch                                                                                      1/38 
	  正在安装    : perl-HTTP-Tiny-0.033-3.el7.noarch                                                                                       2/38 
	  正在安装    : perl-podlators-2.5.1-3.el7.noarch                                                                                       3/38 
	  正在安装    : perl-Pod-Perldoc-3.20-4.el7.noarch                                                                                      4/38 
	  正在安装    : 1:perl-Pod-Escapes-1.04-291.el7.noarch                                                                                  5/38 
	  正在安装    : perl-Encode-2.51-7.el7.x86_64                                                                                           6/38 
	  正在安装    : perl-Text-ParseWords-3.29-4.el7.noarch                                                                                  7/38 
	  正在安装    : perl-Pod-Usage-1.63-3.el7.noarch                                                                                        8/38 
	  正在安装    : perl-Storable-2.45-3.el7.x86_64                                                                                         9/38 
	  正在安装    : perl-Exporter-5.68-3.el7.noarch                                                                                        10/38 
	  正在安装    : perl-constant-1.27-2.el7.noarch                                                                                        11/38 
	  正在安装    : perl-Carp-1.26-244.el7.noarch                                                                                          12/38 
	  正在安装    : perl-Time-Local-1.2300-2.el7.noarch                                                                                    13/38 
	  正在安装    : perl-Socket-2.010-4.el7.x86_64                                                                                         14/38 
	  正在安装    : 4:perl-Time-HiRes-1.9725-3.el7.x86_64                                                                                  15/38 
	  正在安装    : perl-PathTools-3.40-5.el7.x86_64                                                                                       16/38 
	  正在安装    : perl-Scalar-List-Utils-1.27-248.el7.x86_64                                                                             17/38 
	  正在安装    : 4:perl-libs-5.16.3-291.el7.x86_64                                                                                      18/38 
	  正在安装    : 4:perl-macros-5.16.3-291.el7.x86_64                                                                                    19/38 
	  正在安装    : 1:perl-Pod-Simple-3.28-4.el7.noarch                                                                                    20/38 
	  正在安装    : perl-File-Temp-0.23.01-3.el7.noarch                                                                                    21/38 
	  正在安装    : perl-File-Path-2.09-2.el7.noarch                                                                                       22/38 
	  正在安装    : perl-threads-shared-1.43-6.el7.x86_64                                                                                  23/38 
	  正在安装    : perl-threads-1.87-4.el7.x86_64                                                                                         24/38 
	  正在安装    : perl-Filter-1.49-3.el7.x86_64                                                                                          25/38 
	  正在安装    : perl-Getopt-Long-2.40-2.el7.noarch                                                                                     26/38 
	  正在安装    : 4:perl-5.16.3-291.el7.x86_64                                                                                           27/38 
	  正在安装    : perl-Data-Dumper-2.145-3.el7.x86_64                                                                                    28/38 
	  正在安装    : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                                                                             29/38 
	  正在安装    : perl-Net-Daemon-0.48-5.el7.noarch                                                                                      30/38 
	  正在安装    : 1:mariadb-5.5.52-1.el7.x86_64                                                                                          31/38 
	  正在安装    : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                                                                            32/38 
	  正在安装    : perl-IO-Compress-2.061-2.el7.noarch                                                                                    33/38 
	  正在安装    : perl-PlRPC-0.2020-14.el7.noarch                                                                                        34/38 
	  正在安装    : perl-DBI-1.627-4.el7.x86_64                                                                                            35/38 
	  正在安装    : perl-DBD-MySQL-4.023-5.el7.x86_64                                                                                      36/38 
	  正在安装    : libaio-0.3.109-13.el7.x86_64                                                                                           37/38 
	  正在安装    : 1:mariadb-server-5.5.52-1.el7.x86_64                                                                                   38/38 
	  验证中      : perl-HTTP-Tiny-0.033-3.el7.noarch                                                                                       1/38 
	  验证中      : perl-threads-shared-1.43-6.el7.x86_64                                                                                   2/38 
	  验证中      : perl-Storable-2.45-3.el7.x86_64                                                                                         3/38 
	  验证中      : perl-IO-Compress-2.061-2.el7.noarch                                                                                     4/38 
	  验证中      : perl-Exporter-5.68-3.el7.noarch                                                                                         5/38 
	  验证中      : perl-constant-1.27-2.el7.noarch                                                                                         6/38 
	  验证中      : perl-PathTools-3.40-5.el7.x86_64                                                                                        7/38 
	  验证中      : perl-Carp-1.26-244.el7.noarch                                                                                           8/38 
	  验证中      : 1:perl-Pod-Escapes-1.04-291.el7.noarch                                                                                  9/38 
	  验证中      : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                                                                             10/38 
	  验证中      : 1:perl-parent-0.225-244.el7.noarch                                                                                     11/38 
	  验证中      : perl-Net-Daemon-0.48-5.el7.noarch                                                                                      12/38 
	  验证中      : 1:mariadb-server-5.5.52-1.el7.x86_64                                                                                   13/38 
	  验证中      : perl-File-Temp-0.23.01-3.el7.noarch                                                                                    14/38 
	  验证中      : 1:perl-Pod-Simple-3.28-4.el7.noarch                                                                                    15/38 
	  验证中      : perl-Time-Local-1.2300-2.el7.noarch                                                                                    16/38 
	  验证中      : perl-Pod-Perldoc-3.20-4.el7.noarch                                                                                     17/38 
	  验证中      : perl-DBI-1.627-4.el7.x86_64                                                                                            18/38 
	  验证中      : libaio-0.3.109-13.el7.x86_64                                                                                           19/38 
	  验证中      : perl-Socket-2.010-4.el7.x86_64                                                                                         20/38 
	  验证中      : 1:mariadb-5.5.52-1.el7.x86_64                                                                                          21/38 
	  验证中      : perl-Data-Dumper-2.145-3.el7.x86_64                                                                                    22/38 
	  验证中      : 4:perl-Time-HiRes-1.9725-3.el7.x86_64                                                                                  23/38 
	  验证中      : perl-Scalar-List-Utils-1.27-248.el7.x86_64                                                                             24/38 
	  验证中      : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                                                                            25/38 
	  验证中      : perl-PlRPC-0.2020-14.el7.noarch                                                                                        26/38 
	  验证中      : 4:perl-libs-5.16.3-291.el7.x86_64                                                                                      27/38 
	  验证中      : 4:perl-macros-5.16.3-291.el7.x86_64                                                                                    28/38 
	  验证中      : perl-Pod-Usage-1.63-3.el7.noarch                                                                                       29/38 
	  验证中      : perl-DBD-MySQL-4.023-5.el7.x86_64                                                                                      30/38 
	  验证中      : perl-Encode-2.51-7.el7.x86_64                                                                                          31/38 
	  验证中      : perl-podlators-2.5.1-3.el7.noarch                                                                                      32/38 
	  验证中      : perl-Getopt-Long-2.40-2.el7.noarch                                                                                     33/38 
	  验证中      : perl-File-Path-2.09-2.el7.noarch                                                                                       34/38 
	  验证中      : 4:perl-5.16.3-291.el7.x86_64                                                                                           35/38 
	  验证中      : perl-threads-1.87-4.el7.x86_64                                                                                         36/38 
	  验证中      : perl-Filter-1.49-3.el7.x86_64                                                                                          37/38 
	  验证中      : perl-Text-ParseWords-3.29-4.el7.noarch                                                                                 38/38 

	已安装:
	  mariadb-server.x86_64 1:5.5.52-1.el7                                                                                                       

	作为依赖被安装:
	  libaio.x86_64 0:0.3.109-13.el7                 mariadb.x86_64 1:5.5.52-1.el7                  perl.x86_64 4:5.16.3-291.el7                 
	  perl-Carp.noarch 0:1.26-244.el7                perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7   perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7  
	  perl-DBD-MySQL.x86_64 0:4.023-5.el7            perl-DBI.x86_64 0:1.627-4.el7                  perl-Data-Dumper.x86_64 0:2.145-3.el7        
	  perl-Encode.x86_64 0:2.51-7.el7                perl-Exporter.noarch 0:5.68-3.el7              perl-File-Path.noarch 0:2.09-2.el7           
	  perl-File-Temp.noarch 0:0.23.01-3.el7          perl-Filter.x86_64 0:1.49-3.el7                perl-Getopt-Long.noarch 0:2.40-2.el7         
	  perl-HTTP-Tiny.noarch 0:0.033-3.el7            perl-IO-Compress.noarch 0:2.061-2.el7          perl-Net-Daemon.noarch 0:0.48-5.el7          
	  perl-PathTools.x86_64 0:3.40-5.el7             perl-PlRPC.noarch 0:0.2020-14.el7              perl-Pod-Escapes.noarch 1:1.04-291.el7       
	  perl-Pod-Perldoc.noarch 0:3.20-4.el7           perl-Pod-Simple.noarch 1:3.28-4.el7            perl-Pod-Usage.noarch 0:1.63-3.el7           
	  perl-Scalar-List-Utils.x86_64 0:1.27-248.el7   perl-Socket.x86_64 0:2.010-4.el7               perl-Storable.x86_64 0:2.45-3.el7            
	  perl-Text-ParseWords.noarch 0:3.29-4.el7       perl-Time-HiRes.x86_64 4:1.9725-3.el7          perl-Time-Local.noarch 0:1.2300-2.el7        
	  perl-constant.noarch 0:1.27-2.el7              perl-libs.x86_64 4:5.16.3-291.el7              perl-macros.x86_64 4:5.16.3-291.el7          
	  perl-parent.noarch 1:0.225-244.el7             perl-podlators.noarch 0:2.5.1-3.el7            perl-threads.x86_64 0:1.87-4.el7             
	  perl-threads-shared.x86_64 0:1.43-6.el7       

	完毕！
###	[root@localhost seafile-server-6.1.2]# yum install python-setuptools python-imaging python-ldap MySQL-python python-memcached python-urllib3
	已加载插件：fastestmirror
	Loading mirror speeds from cached hostfile
	 * base: mirrors.zju.edu.cn
	 * extras: mirrors.cn99.com
	 * updates: mirrors.zju.edu.cn
	正在解决依赖关系
	--> 正在检查事务
	---> 软件包 MySQL-python.x86_64.0.1.2.5-1.el7 将被 安装
	---> 软件包 python-ldap.x86_64.0.2.4.15-2.el7 将被 安装
	---> 软件包 python-memcached.noarch.0.1.48-4.el7 将被 安装
	---> 软件包 python-pillow.x86_64.0.2.0.0-19.gitd1c6db8.el7 将被 安装
	--> 正在处理依赖关系 libwebp.so.4()(64bit)，它被软件包 python-pillow-2.0.0-19.gitd1c6db8.el7.x86_64 需要
	---> 软件包 python-setuptools.noarch.0.0.9.8-4.el7 将被 安装
	--> 正在处理依赖关系 python-backports-ssl_match_hostname，它被软件包 python-setuptools-0.9.8-4.el7.noarch 需要
	---> 软件包 python-urllib3.noarch.0.1.10.2-2.el7_1 将被 安装
	--> 正在处理依赖关系 python-six，它被软件包 python-urllib3-1.10.2-2.el7_1.noarch 需要
	--> 正在检查事务
	---> 软件包 libwebp.x86_64.0.0.3.0-3.el7 将被 安装
	---> 软件包 python-backports-ssl_match_hostname.noarch.0.3.4.0.2-4.el7 将被 安装
	--> 正在处理依赖关系 python-backports，它被软件包 python-backports-ssl_match_hostname-3.4.0.2-4.el7.noarch 需要
	---> 软件包 python-six.noarch.0.1.9.0-2.el7 将被 安装
	--> 正在检查事务
	---> 软件包 python-backports.x86_64.0.1.0-8.el7 将被 安装
	--> 解决依赖关系完成

	依赖关系解决

	=============================================================================================================================================
	 Package                                            架构                  版本                                     源                   大小
	=============================================================================================================================================
	正在安装:
	 MySQL-python                                       x86_64                1.2.5-1.el7                              base                 90 k
	 python-ldap                                        x86_64                2.4.15-2.el7                             base                159 k
	 python-memcached                                   noarch                1.48-4.el7                               base                 33 k
	 python-pillow                                      x86_64                2.0.0-19.gitd1c6db8.el7                  base                438 k
	 python-setuptools                                  noarch                0.9.8-4.el7                              base                396 k
	 python-urllib3                                     noarch                1.10.2-2.el7_1                           base                100 k
	为依赖而安装:
	 libwebp                                            x86_64                0.3.0-3.el7                              base                170 k
	 python-backports                                   x86_64                1.0-8.el7                                base                5.8 k
	 python-backports-ssl_match_hostname                noarch                3.4.0.2-4.el7                            base                 12 k
	 python-six                                         noarch                1.9.0-2.el7                              base                 29 k

	事务概要
	=============================================================================================================================================
	安装  6 软件包 (+4 依赖软件包)

	总下载量：1.4 M
	安装大小：5.3 M
	Is this ok [y/d/N]: y
	Downloading packages:
	(1/10): MySQL-python-1.2.5-1.el7.x86_64.rpm                                                                           |  90 kB  00:00:00     
	(2/10): libwebp-0.3.0-3.el7.x86_64.rpm                                                                                | 170 kB  00:00:00     
	(3/10): python-backports-1.0-8.el7.x86_64.rpm                                                                         | 5.8 kB  00:00:00     
	(4/10): python-backports-ssl_match_hostname-3.4.0.2-4.el7.noarch.rpm                                                  |  12 kB  00:00:00     
	(5/10): python-ldap-2.4.15-2.el7.x86_64.rpm                                                                           | 159 kB  00:00:00     
	(6/10): python-pillow-2.0.0-19.gitd1c6db8.el7.x86_64.rpm                                                              | 438 kB  00:00:00     
	(7/10): python-setuptools-0.9.8-4.el7.noarch.rpm                                                                      | 396 kB  00:00:00     
	(8/10): python-six-1.9.0-2.el7.noarch.rpm                                                                             |  29 kB  00:00:00     
	(9/10): python-urllib3-1.10.2-2.el7_1.noarch.rpm                                                                      | 100 kB  00:00:00     
	(10/10): python-memcached-1.48-4.el7.noarch.rpm                                                                       |  33 kB  00:00:00     
	---------------------------------------------------------------------------------------------------------------------------------------------
	总计                                                                                                         2.8 MB/s | 1.4 MB  00:00:00     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  正在安装    : libwebp-0.3.0-3.el7.x86_64                                                                                              1/10 
	  正在安装    : python-backports-1.0-8.el7.x86_64                                                                                       2/10 
	  正在安装    : python-backports-ssl_match_hostname-3.4.0.2-4.el7.noarch                                                                3/10 
	  正在安装    : python-six-1.9.0-2.el7.noarch                                                                                           4/10 
	  正在安装    : python-urllib3-1.10.2-2.el7_1.noarch                                                                                    5/10 
	  正在安装    : python-setuptools-0.9.8-4.el7.noarch                                                                                    6/10 
	  正在安装    : python-pillow-2.0.0-19.gitd1c6db8.el7.x86_64                                                                            7/10 
	  正在安装    : python-ldap-2.4.15-2.el7.x86_64                                                                                         8/10 
	  正在安装    : python-memcached-1.48-4.el7.noarch                                                                                      9/10 
	  正在安装    : MySQL-python-1.2.5-1.el7.x86_64                                                                                        10/10 
	  验证中      : python-six-1.9.0-2.el7.noarch                                                                                           1/10 
	  验证中      : python-setuptools-0.9.8-4.el7.noarch                                                                                    2/10 
	  验证中      : python-backports-ssl_match_hostname-3.4.0.2-4.el7.noarch                                                                3/10 
	  验证中      : python-backports-1.0-8.el7.x86_64                                                                                       4/10 
	  验证中      : MySQL-python-1.2.5-1.el7.x86_64                                                                                         5/10 
	  验证中      : python-memcached-1.48-4.el7.noarch                                                                                      6/10 
	  验证中      : python-pillow-2.0.0-19.gitd1c6db8.el7.x86_64                                                                            7/10 
	  验证中      : python-ldap-2.4.15-2.el7.x86_64                                                                                         8/10 
	  验证中      : python-urllib3-1.10.2-2.el7_1.noarch                                                                                    9/10 
	  验证中      : libwebp-0.3.0-3.el7.x86_64                                                                                             10/10 

	已安装:
	  MySQL-python.x86_64 0:1.2.5-1.el7                   python-ldap.x86_64 0:2.4.15-2.el7           python-memcached.noarch 0:1.48-4.el7       
	  python-pillow.x86_64 0:2.0.0-19.gitd1c6db8.el7      python-setuptools.noarch 0:0.9.8-4.el7      python-urllib3.noarch 0:1.10.2-2.el7_1     

	作为依赖被安装:
	  libwebp.x86_64 0:0.3.0-3.el7        python-backports.x86_64 0:1.0-8.el7     python-backports-ssl_match_hostname.noarch 0:3.4.0.2-4.el7    
	  python-six.noarch 0:1.9.0-2.el7    

	完毕！
###	[root@localhost seafile-server-6.1.2]# mysql -u root
	ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2)
###	[root@localhost seafile-server-6.1.2]# netstat -luntp
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
	tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      920/sshd            
	tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1790/master         
	tcp6       0      0 :::22                   :::*                    LISTEN      920/sshd            
	tcp6       0      0 ::1:25                  :::*                    LISTEN      1790/master         
	udp        0      0 0.0.0.0:68              0.0.0.0:*                           9651/dhclient       
	udp        0      0 127.0.0.1:323           0.0.0.0:*                           594/chronyd         
	udp        0      0 0.0.0.0:39441           0.0.0.0:*                           9651/dhclient       
	udp6       0      0 :::20670                :::*                                9651/dhclient       
	udp6       0      0 ::1:323                 :::*                                594/chronyd         
###	[root@localhost seafile-server-6.1.2]# yum intsall tree
	已加载插件：fastestmirror
	没有该命令：intsall。请使用 /usr/bin/yum --help
###	[root@localhost seafile-server-6.1.2]# yum install tree   
	已加载插件：fastestmirror
	Loading mirror speeds from cached hostfile
	 * base: mirrors.zju.edu.cn
	 * extras: mirrors.cn99.com
	 * updates: mirrors.zju.edu.cn
	正在解决依赖关系
	--> 正在检查事务
	---> 软件包 tree.x86_64.0.1.6.0-10.el7 将被 安装
	--> 解决依赖关系完成

	依赖关系解决

	=============================================================================================================================================
	 Package                        架构                             版本                                   源                              大小
	=============================================================================================================================================
	正在安装:
	 tree                           x86_64                           1.6.0-10.el7                           base                            46 k

	事务概要
	=============================================================================================================================================
	安装  1 软件包

	总下载量：46 k
	安装大小：87 k
	Is this ok [y/d/N]: y
	Downloading packages:
	tree-1.6.0-10.el7.x86_64.rpm                                                                                          |  46 kB  00:00:00     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  正在安装    : tree-1.6.0-10.el7.x86_64                                                                                                 1/1 
	  验证中      : tree-1.6.0-10.el7.x86_64                                                                                                 1/1 

	已安装:
	  tree.x86_64 0:1.6.0-10.el7                                                                                                                 

	完毕！
###	[root@localhost seafile-server-6.1.2]# cd ..
###	[root@localhost mycloud]# tree -LC 2
	.
	├── installed
	│   └── seafile-server_6.1.2_x86-64.tar.gz
	└── seafile-server-6.1.2
		├── check_init_admin.py
		├── reset-admin.sh
		├── runtime
		├── seaf-fsck.sh
		├── seaf-fuse.sh
		├── seaf-gc.sh
		├── seafile
		├── seafile.sh
		├── seahub
		├── seahub.sh
		├── setup-seafile-mysql.py
		├── setup-seafile-mysql.sh
		├── setup-seafile.sh
		└── upgrade

	6 directories, 11 files
###	[root@localhost mycloud]# yum -y install bash-com*
	已加载插件：fastestmirror
	Loading mirror speeds from cached hostfile
	 * base: mirrors.zju.edu.cn
	 * extras: mirrors.cn99.com
	 * updates: mirrors.zju.edu.cn
	正在解决依赖关系
	--> 正在检查事务
	---> 软件包 bash-completion.noarch.1.2.1-6.el7 将被 安装
	--> 解决依赖关系完成

	依赖关系解决

	=============================================================================================================================================
	 Package                                架构                          版本                                 源                           大小
	=============================================================================================================================================
	正在安装:
	 bash-completion                        noarch                        1:2.1-6.el7                          base                         85 k

	事务概要
	=============================================================================================================================================
	安装  1 软件包

	总下载量：85 k
	安装大小：259 k
	Downloading packages:
	bash-completion-2.1-6.el7.noarch.rpm                                                                                  |  85 kB  00:00:00     
	Running transaction check
	Running transaction test
	Transaction test succeeded
	Running transaction
	  正在安装    : 1:bash-completion-2.1-6.el7.noarch                                                                                       1/1 
	  验证中      : 1:bash-completion-2.1-6.el7.noarch                                                                                       1/1 

	已安装:
	  bash-completion.noarch 1:2.1-6.el7                                                                                                         

	完毕！
###	[root@localhost mycloud]# systemctl start mariadb
###	[root@localhost seafile-server-6.1.2]# systemctl enable mariadb
###	[root@localhost mycloud]# netstat -luntp          
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
	tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN      16962/mysqld        
	tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      920/sshd            
	tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1790/master         
	tcp6       0      0 :::22                   :::*                    LISTEN      920/sshd            
	tcp6       0      0 ::1:25                  :::*                    LISTEN      1790/master         
	udp        0      0 0.0.0.0:68              0.0.0.0:*                           9651/dhclient       
	udp        0      0 127.0.0.1:323           0.0.0.0:*                           594/chronyd         
	udp        0      0 0.0.0.0:39441           0.0.0.0:*                           9651/dhclient       
	udp6       0      0 :::20670                :::*                                9651/dhclient       
	udp6       0      0 ::1:323                 :::*                                594/chronyd         
###	[root@localhost mycloud]# mysqladmin -u root -p password ******
	Enter password: 
###	[root@localhost mycloud]# cd seafile-server-*
###	[root@localhost seafile-server-6.1.2]# ./setup-seafile-mysql.sh
	Checking python on this machine ...
	  Checking python module: setuptools ... Done.
	  Checking python module: python-imaging ... Done.
	  Checking python module: python-mysqldb ... Done.

	-----------------------------------------------------------------
	This script will guide you to setup your seafile server using MySQL.
	Make sure you have read seafile server manual at

			https://github.com/haiwen/seafile/wiki

	Press ENTER to continue
	-----------------------------------------------------------------


	What is the name of the server? It will be displayed on the client.
	3 - 15 letters or digits
	[ server name ] my_cloud

	What is the ip or domain of the server?
	For example: www.mycompany.com, 192.168.1.101
	[ This server's ip or domain ] 192.168.1.115

	Where do you want to put your seafile data?
	Please use a volume with enough free space
	[ default "/home/mycloud/seafile-data" ] 

	Which port do you want to use for the seafile fileserver?
	[ default "8082" ] 

	-------------------------------------------------------
	Please choose a way to initialize seafile databases:
	-------------------------------------------------------

	[1] Create new ccnet/seafile/seahub databases
	[2] Use existing ccnet/seafile/seahub databases

	[ 1 or 2 ] 
	-------------------------------------------------------
	Please choose a way to initialize seafile databases:
	-------------------------------------------------------

	[1] Create new ccnet/seafile/seahub databases
	[2] Use existing ccnet/seafile/seahub databases

	[ 1 or 2 ] 1

	What is the host of mysql server?
	[ default "localhost" ] 

	What is the port of mysql server?
	[ default "3306" ] 

	What is the password of the mysql root user?
	[ root password ] 

	verifying password of user root ...  done

	Enter the name for mysql user of seafile. It would be created if not exists.
	[ default "seafile" ] 

	Enter the password for mysql user "seafile":
	[ password for seafile ] 
	Enter the password for mysql user "seafile":
	[ password for seafile ] 

	Enter the database name for ccnet-server:
	[ default "ccnet-db" ] 

	Enter the database name for seafile-server:
	[ default "seafile-db" ] 

	Enter the database name for seahub:
	[ default "seahub-db" ] 

	---------------------------------
	This is your configuration
	---------------------------------

		server name:            my_cloud
		server ip/domain:       192.168.1.115

		seafile data dir:       /home/mycloud/seafile-data
		fileserver port:        8082

		database:               create new
		ccnet database:         ccnet-db
		seafile database:       seafile-db
		seahub database:        seahub-db
		database user:          seafile



	---------------------------------
	Press ENTER to continue, or Ctrl-C to abort
	---------------------------------

	Generating ccnet configuration ...

	done
	Successly create configuration dir /home/mycloud/ccnet.
	Generating seafile configuration ...

	Done.
	done
	Generating seahub configuration ...

	----------------------------------------
	Now creating seahub database tables ...

	----------------------------------------

	creating seafile-server-latest symbolic link ...  done




	-----------------------------------------------------------------
	Your seafile server configuration has been finished successfully.
	-----------------------------------------------------------------

	run seafile server:     ./seafile.sh { start | stop | restart }
	run seahub  server:     ./seahub.sh  { start <port> | stop | restart <port> }

	-----------------------------------------------------------------
	If you are behind a firewall, remember to allow input/output of these tcp ports:
	-----------------------------------------------------------------

	port of seafile fileserver:   8082
	port of seahub:               8000

	When problems occur, Refer to

			https://github.com/haiwen/seafile/wiki

	for information.


###	[root@localhost seafile-server-6.1.2]# ./seafile.sh start

	[08/19/17 09:03:25] ../common/session.c(132): using config file /home/mycloud/conf/ccnet.conf
	Starting seafile server, please wait ...
	Seafile server started

	Done.
###	[root@localhost seafile-server-6.1.2]# seahub.sh
	-bash: seahub.sh: 未找到命令
###	[root@localhost seafile-server-6.1.2]# ./seahub.sh start 

	LC_ALL is not set in ENV, set to en_US.UTF-8
	Starting seahub at port 8000 ...

	----------------------------------------
	It's the first time you start the seafile server. Now let's create the admin account
	----------------------------------------

	What is the email for the admin account?
	[ admin email ] 894893421@qq.com

	What is the password for the admin account?
	[ admin password ] 

	Enter the password again:
	[ admin password again ] 



	----------------------------------------
	Successfully created seafile admin
	----------------------------------------




	Seahub is started

	Done.

###	[root@localhost seafile-server-6.1.2]# netstat -luntp
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
	tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN      16962/mysqld        
	tcp        0      0 0.0.0.0:8082            0.0.0.0:*               LISTEN      17062/seaf-server   
	tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      920/sshd            
	tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      1790/master         
	tcp        0      0 0.0.0.0:8000            0.0.0.0:*               LISTEN      17138/python2.7     
	tcp6       0      0 :::22                   :::*                    LISTEN      920/sshd            
	tcp6       0      0 ::1:25                  :::*                    LISTEN      1790/master         
	udp        0      0 0.0.0.0:68              0.0.0.0:*                           9651/dhclient       
	udp        0      0 127.0.0.1:323           0.0.0.0:*                           594/chronyd         
	udp        0      0 0.0.0.0:39441           0.0.0.0:*                           9651/dhclient       
	udp6       0      0 :::20670                :::*                                9651/dhclient       
	udp6       0      0 ::1:323                 :::*                                594/chronyd         
###	[root@localhost seafile-server-6.1.2]# ip add
	1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
		link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
		inet 127.0.0.1/8 scope host lo
		   valid_lft forever preferred_lft forever
		inet6 ::1/128 scope host 
		   valid_lft forever preferred_lft forever
	2: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP qlen 1000
		link/ether 00:0c:29:59:d6:58 brd ff:ff:ff:ff:ff:ff
		inet 192.168.1.115/24 brd 192.168.1.255 scope global dynamic ens160
		   valid_lft 4507sec preferred_lft 4507sec
		inet6 fe80::6c48:97c4:d17a:c34f/64 scope link 
		   valid_lft forever preferred_lft forever
###	[root@localhost seafile-server-6.1.2]# firewall-cmd --zone=public --add-port=8000/tcp --permanent
	success
###	[root@localhost seafile-server-6.1.2]# firewall-cmd --zone=public --add-port=8082/tcp --permanent  
	success
###	[root@localhost seafile-server-6.1.2]# firewall-cmd --list
	usage: see firewall-cmd man page
	firewall-cmd: error: ambiguous option: --list could match --list-lockdown-whitelist-contexts, --list-all, --list-lockdown-whitelist-uids, --list-ports, --list-source-ports, --list-lockdown-whitelist-users, --list-forward-ports, --list-icmp-blocks, --list-interfaces, --list-rich-rules, --list-services, --list-lockdown-whitelist-commands, --list-all-zones, --list-sources, --list-protocols
###	[root@localhost seafile-server-6.1.2]# firewall-cmd --list-all
	public (active)
	  target: default
	  icmp-block-inversion: no
	  interfaces: ens160
	  sources: 
	  services: dhcpv6-client ssh
	  ports: 
	  protocols: 
	  masquerade: no
	  forward-ports: 
	  sourceports: 
	  icmp-blocks: 
	  rich rules: 

###	[root@localhost seafile-server-6.1.2]# firewall-cmd -reload
	usage: see firewall-cmd man page
	firewall-cmd: error: unrecognized arguments: -reload
###	[root@localhost seafile-server-6.1.2]# firewall-cmd --reload
	success
###	[root@localhost seafile-server-6.1.2]# firewall-cmd --list-all
	public (active)
	  target: default
	  icmp-block-inversion: no
	  interfaces: ens160
	  sources: 
	  services: dhcpv6-client ssh
	  ports: 8000/tcp 8082/tcp
	  protocols: 
	  masquerade: no
	  forward-ports: 
	  sourceports: 
	  icmp-blocks: 
	  rich rules: 


# 39.
# 40.