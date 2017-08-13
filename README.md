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
	[root@localhost usr]# yum install mariadb mariadb-server         #这是安装nariadb和mariadb服务
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
	1安装mini版centos7系统默认关闭防火墙和selinux
	2安装wget    yum install -y wget
	3安装EPEL源
	wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm   #下载epel源rpm包

	rpm -ivh epel-release-latest-7.noarch.rpm        #安装rpm包
	4安装Aria2

	yum install aria2

	5生成配置文件并编辑
	mkdir /etc/aria2/   #创建目录
	vi /etc/aria2/aria2.conf   #创建配置文件
	配置文件内容
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

	6安装Git  yum install -y git

	安装前端控制UI：
	git clone https://github.com/ziahamza/webui-aria2 #从git上下载webui-aria2 UI端


	7安装httpd    yum  -y  install  httpd



	8把克隆下载的webui-aria2 复制到/var/www/html/下  我就不讲命令了，自己百度linux复制或移动目录命令

	9安装完成后，“aria2c  --enable-rpc  --rpc-listen-all”启用监听RP
	我是这个鬼样子
	解决办法，我是重启系统也就是centos7，原因应该是开头时候我们测试aria2时候端口占用。
	然后我们就开始测试连通性了
	10浏览器访问推荐使用谷歌浏览器或火狐浏览器

		http://IP地址/webui，就可访问成功；如果报错，在“设置”--> “服务器设置”中“主机：”后后面填写自己的IP地址就可；

		如果Aria2.conf配置文件中启用了RPC安全认证，需要在WEB客户端设置中填入RPC用户名和密码，否则客户端报错！如果是自己用，
			个人觉得没必要用RPC认证，打开/etc/aria2.conf删除里面的RPC用户名和密码

	11其他开机启动就自己百度呗
	无错误后台启动：
	aria2c --conf-path=/etc/aria2/aria2.conf -D
	下载目录看见web界面快速访问设置dir吗
	参考http://www.2kil.com/9472.html    http://painting.blog.51cto.com/10476797/1730074