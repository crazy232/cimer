### CentOS 常用命令

##### RPM

```shell
rpm -ivh package.rpm 安装一个rpm包

rpm -i --force --nodeps 可以忽略所有依赖关系和文件问题，什么包 都能安装上，但这种强制安装的软件包不能保证完全发挥功能

rpm -ivh --nodeeps package.rpm 安装一个rpm包而忽略依赖关系警告

rpm -U package.rpm 更新一个rpm包但不改变其配置文件

rpm -F package.rpm 更新一个确定已经安装的rpm包

rpm -e package_name.rpm 删除一个rpm包

rpm -qa 显示系统中所有已经安装的rpm包

rpm -qa | grep httpd 显示所有名称中包含 "httpd" 字样的rpm包

rpm -qi package_name 获取一个已安装包的特殊信息

rpm -ql package_name 显示一个已经安装的rpm包提供的文件列表

rpm -qc package_name 显示一个已经安装的rpm包提供的配置文件列表

rpm -q package_name --whatrequires 显示与一个rpm包存在依赖关系的列表

rpm -q package_name --whatprovides 显示一个rpm包所占的体积

rpm -q package_name --scripts 显示在安装/删除期间所执行的脚本l

rpm -q package_name --changelog 显示一个rpm包的修改历史

rpm -qf /etc/httpd/conf/httpd.conf 确认所给的文件由哪个rpm包所提供

rpm -qp package.rpm -l 显示由一个尚未安装的rpm包提供的文件列表

rpm --import /media/cdrom/RPM-GPG-KEY 导入公钥数字证书

rpm --checksig package.rpm 确认一个rpm包的完整性

rpm -qa gpg-pubkey 确认已安装的所有rpm包的完整性

rpm -V package_name 检查文件尺寸、 许可、类型、所有者、群组、MD5检查以及最后修改时间

rpm -Va 检查系统中所有已安装的rpm包- 小心使用

rpm -Vp package.rpm 确认一个rpm包还未安装

rpm2cpio package.rpm | cpio --extract --make-directories *bin* 从一个rpm包运行可执行文件

rpm -ivh /usr/src/redhat/RPMS/`arch`/package.rpm 从一个rpm源码安装一个构建好的包

rpmbuild --rebuild package_name.src.rpm 从一个rpm源码构建一个 rpm 包
```

##### yum

```shell
yum install package_name 下载并安装一个rpm包

yum localinstall package_name.rpm 将安装一个rpm包，使用你自己的软件仓库为你解决所有依赖关系

yum update package_name.rpm 更新当前系统中所有安装的rpm包

yum update package_name 更新一个rpm包

yum remove package_name 删除一个rpm包

yum list 列出当前系统中安装的所有包

yum search package_name 在rpm仓库中搜寻软件包

yum clean packages 清理rpm缓存删除下载的包

yum clean headers 删除所有头文件

yum clean all 删除所有缓存的包和头文件
```

##### CentOS下更改yum源和更新系统

```shell
# [1] 首先备份/etc/yum.repos.d/CentOS-Base.repo
$ cp /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup

# [2] 进入yum源配置文件所在文件夹
$ cd /etc/yum.repos.d/

# [3] 下载163的yum源配置文件，放入/etc/yum.repos.d/(操作前请做好相应备份)
$ wget http://mirrors.163.com/.help/CentOS6-Base-163.repo

# [4] 运行yum makecache生成缓存
$ yum makecache

# [5] 更新系统(时间比较久,主要看个人网速)
$ yum -y update

# [6] 安装vim编辑器
$ yum -y install vim*
```

