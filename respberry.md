#用树莓派搭建我自己的媒体中心#

---

##安装系统##
有很多文章讲到树莓派系统的安装，这里是下载的树莓派官方系统的镜像。
使用SD card Formater格式化SD卡，通过balenaEtcher把镜像文件烧到SD卡中。

把制作好的SD卡插入树莓派，启动后按向导配置好系统语言/用户密码，开启SSH登录。

##配置静态IP地址##

sudo nano /etc/dhcpcd.conf

~~~
interface eth0

static ip_address=192.168.0.8/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8.8

interface wlan0

static ip_address=192.168.0.18/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8.8
~~~

##更换阿里源

~~~
sudo nano /etc/apt/sources.list

deb http://mirrors.aliyun.com/raspbian/raspbian/ jessie main non-free contrib rpi
deb-src http://mirrors.aliyun.com/raspbian/raspbian/ jessie main non-free contrib rpi
~~~

##挂载NTFS磁盘##

~~~
apt-get install ntfs-3g

mkdir -p /mnt/disk

编辑/etc/fstab文件，就可以进行开机自动挂在配置

sudo nano /etc/fstab

#在最后一行添加如下内容

/dev/sda1 /mnt/disk ntfs-3g defaults,noexec,umask=0000 0 0
~~~

##
