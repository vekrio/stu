# stu
linux学习 

# 1:[centos7查看版本信息](https://github.com/vekrio/stu/blob/master/20170718/Redhat-release)

# 2:[ntp安装](https://github.com/vekrio/stu/blob/master/20170718/ntp)

# 3:[centos7查看已启动的服务列表](https://github.com/vekrio/stu/blob/master/20170718/list-unit-files)

# 4:[centos7仓库导入公钥](https://github.com/vekrio/stu/blob/master/20170718/%E5%AF%BC%E5%85%A5%E5%85%AC%E9%92%A5)

# 5:[centos系统添加/删除用户和用户组的例子](http://www.111cn.net/sys/CentOS/63650.htm)

# 6:[centos7退出登录](http://blog.csdn.net/huangxiang360729/article/details/52650107)

# 7:[centos7忘记root密码](https://jingyan.baidu.com/article/cbf0e5009d61322eab28935f.html)

   开机启动centos 7.0,看到如下画面，选择下图选单，按"e"键
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
