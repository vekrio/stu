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


# 9.[CentOS下测试硬盘坏道](http://www.centoscn.com/CentOS/Intermediate/2014/1219/4344.html)

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

# 10.[Linux source命令](http://www.cnblogs.com/pkufork/p/linux_source.html)

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

# 11.[windows server 2008解决无法PING通问题](https://jingyan.baidu.com/article/a24b33cd6926be19fe002b2c.html)

	windows server 2008解决无法PING通问题

	今天安装服务器（ｓｅｒｖｅｒ　２００８），配置完IP地址后，发现局域网其它电脑无法PING通服务器，测线仪测试链路都正常，网线接别的电脑也正常，以为是网卡问题，于是ping了自己的IP，发现能PING通，怀疑应该是２００８策略问题，果然找到解决方法。

	方法/步骤
	
	右键电脑，找到【管理】

	在服务器管理里找到【配置】项

	在高级安全windows防火墙里，找到【入站规则】，找到【文件和打印机共享（回显请求-ICMPv4-in）】双击。此时图片状态默认是没选中的


	找到【文件和打印机共享（回显请求-ICMPv4-in）】右击……选择【启用规则】就OK了！为避免以后不方便查找网络问题，此项尽量开启比较好。


