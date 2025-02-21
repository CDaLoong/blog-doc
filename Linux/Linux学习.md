# Linux

!>可以通过 tab 键补齐命令和目录文件名

## 常用初始配置

### SELINUX管理

```shell
# 1. 查看selinux状态
getenforce

# 2. 关闭当前selinux
setenforce 0

# 3. 修改配置文件 /etc/sysconfig/selinux，确保如下参数值
SELINUX=permissive
```

### 防火墙管理

```shell
# 1，查看防火墙状态
systemctl status firewalld.service

# 2，开启防火墙
systemctl start firewalld.service

# 3，关闭防火墙
systemctl stop firewalld.service

# 4，禁用防火墙（关闭随机启动）
systemctl disable firewalld.service
```

## 常用操作

### 系统开关

```shell
# 1. 关机命令  
# 0、1、2、3、4、5、6 linux里的级别划分，3级别为终端登录使用(多用户文本模式,文本界面 + 网络)，5级别是图形界面模式(与级别3相同，但额外启动图形界面)，4级别是保留级别(通常未定义，可由管理员自定义用途)，1级别是单用户模式(仅启动基本服务，无需密码即可获得 root 权限用于系统修复。)，6级别是重启模式(停止所有服务并重新启动系统)，0级别为关机(停止所有服务并关闭系统)，2级别为多用户模式（无网络）,启动基本服务，但通常不启用网络
# shutdown   now 立即马上执行
poweroff # 关闭系统并关闭电源，是 shutdown -h now 的简写，意味着立即关闭系统
init 0 # init 命令用于改变系统的运行级别，运行级别 0 表示关闭系统（即关机），运行 init 0 会让系统进入关机状态
halt # halt 命令会停止系统的所有进程，类似于关机操作，但不一定关闭电源。它是强制停止系统的一种方法，通常需要额外的步骤来关闭电源
shutdown -h now # shutdown 命令用于关闭系统。-h 选项意味着关闭系统（halt），now 表示立即执行关机操作
shutdown -h +20 # 这个命令会在 20 分钟后关机。+20 表示延迟 20 分钟后执行关机

# 2. 重启命令
reboot # 重启系统， shutdown -r now 的简写
init 6 # 运行级别 6 表示重启系统，init 6 会让系统重启
shutdown -r now # -r 表示重启，now 表示立即执行重启
shutdown -r +20 # 这个命令会在 20 分钟后重启系统，+20 表示延迟 20 分钟后执行重启
```

```shell
# 查看ip
hostname -1
ifconfig
ip addr
ip address
ip addr show
ip address show
```

### 更新系统

```shell
sudo dnf clean all
sudo dnf update
```

### 更新yum源

```shell
# 1、将源文件备份
cd /etc/yum.repos.d/ && mkdir backup && mv *repo backup/

# 2、下载阿里源文件
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-8.repo

#3、更新源里面的地址
sed -i -e "s|mirrors.cloud.aliyuncs.com|mirrors.aliyun.com|g " /etc/yum.repos.d/CentOS-*
sed -i -e "s|releasever|releasever-stream|g" /etc/yum.repos.d/CentOS-*

#4、生成缓存
yum clean all && yum makecache
```

### 安装vim

```shell
sudo dnf install vim
```
 - 将 VIM 编辑器设置为默认的系统范围编辑器
```shell
cat ～/etc/profile.d/vim.sh
export VISUAL="vim"
export EDITOR="vim"
```
- [vi操作](https://www.runoob.com/linux/linux-vim.html)

### 修改本地系统默认语言环境

- 查看本机语言包
```shell
locale -a
```
- 查看当前语言环境
```shell
localectl
```
- 修改语言环境
```shell
loclocalectl set-locale LANG=en_US.UTF-8alectl
```
- 下载语言包
```shell
# 下载单个语言包
dnf install glibc-langpack-en
# 下载全部语言包
dnf install glibc-all-langpacks -y
```

### [添加和删除用户](https://www.myfreax.com/how-to-add-and-delete-users-on-centos-8/)

```shell
# 添加用户
sudo useradd daloong

# 给用户设置密码
sudo passwd daloong

# 在CentOS中默认情况下，wheel组成员具有sudo访问权限。如果要赋予新创建的用户具有sudo权限，需要将用户添加到wheel组中
sudo usermod -aG wheel daloong

# 删除用户
sudo userdel daloong
sudo userdel -r daloong #包括用户邮件和home目录

# 切换用户，使用root切换到其它账号无需密码，其它账号切换到root需要输入root密码
su - daloong

# 注销当前用户的登录状态
exit

# 查看一个用户的ID信息
id daloong

# 查看某一时刻用户的行为
w

# 查看当前已经登录的账号
who

# 查看当前用户的登录历史
last

# 查看系统中所有用户的最后一次登录时间、登录端口和来源IP
lastlog

# 使用如下命令打开 CentOS8用户组的配置文件
vi /etc/group

# 建立一个CentOS8用户组
groupadd users

# 删除一个用户组，初始组（主组）是不能删除的，只能删除附加组
groupdel users

# 为用户组users添加用户daloong
gpasswd -a users daloong

# 为CentOS8用户组users删除用户daloong
gpasswd -d users daloong
```

### 新建、重命名、删除文件夹、文件

- 新建文件夹
  - 格式：mkdir [选项] DirName
  - 命令中的［选项］一般有以下两种：
    -m 用于对新建目录设置存取权限，也可以用 chmod 命令进行设置。
    -p 需要时创建上层文件夹(或目录)，如果文件夹(或目录)已经存在，则不视为错误。
```shell

```

### 查找
