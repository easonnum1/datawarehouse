<!-- TOC -->

* [1. 感觉好卡怎么办](#1-感觉好卡怎么办)
    * [1.1. 查看CPU是不是飙升了](#11-查看cpu是不是飙升了)
        * [1.1.1. 查看高CPU使用率的进程](#111-查看高cpu使用率的进程)
        * [1.1.2. 查看某个进程如python](#112-查看某个进程如python)
    * [1.2. 查看负载load average是不是满负荷](#12-查看负载load-average是不是满负荷)
    * [1.3. 查看IO情况](#13-查看io情况)
* [2. 磁盘满了怎么办](#2-磁盘满了怎么办)
    * [2.1. 查看磁盘情况](#21-查看磁盘情况)
    * [2.2. 显示每个顶级目录的总大小](#22-显示每个顶级目录的总大小)

<!-- TOC -->

## 1. 感觉好卡怎么办

### 1.1. 查看CPU是不是飙升了

#### 1.1.1. 查看高CPU使用率的进程

```text
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
```

#### 1.1.2. 查看某个进程如python

```text
ps -ef | grep python
```

### 1.2. 查看负载load average是不是满负荷

```text
top
```

top命令是Linux下常用的性能分析工具，能够实时显示系统中各个进程的资源占用状况，类似于Windows的任务管理器。

top是一个动态显示过程,即可以通过用户按键来不断刷新当前状态. 如果在前台执行该命令,它将独占前台,直到用户终止该程序为止.

比较准确的说,top命令提供了实时的对系统处理器的状态监视.

主要是看`load average`, 比如：

```
load average: 1.25, 1.32, 1.35
```

假设你的CPU是4C，那么这代表这最近是1分钟、5分钟、15分钟的负载情况, 1.25/4 ，其实还好。

### 1.3. 查看IO情况

先安装：

```text
sudo apt-get install sysstat  # Ubuntu/Debian
sudo yum install sysstat      # CentOS/RHEL
```

每十秒输出一次IO统计信息：

```text
iostat -x 1 10
```

## 2. 磁盘满了怎么办

### 2.1. 查看磁盘情况

```text
df -h
```

显示各个磁盘情况：

```text
Filesystem      Size  Used Avail Use% Mounted on
udev            435M     0  435M   0% /dev
tmpfs            96M  1.3M   95M   2% /run
/dev/vda2        30G   17G   13G  58% /
tmpfs           480M     0  480M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           480M     0  480M   0% /sys/fs/cgroup
/dev/loop1       92M   92M     0 100% /snap/lxd/24061
/dev/vda1       511M  6.1M  505M   2% /boot/efi
/dev/loop5       64M   64M     0 100% /snap/core20/2264
/dev/loop6       39M   39M     0 100% /snap/snapd/21465
/dev/loop7       64M   64M     0 100% /snap/core20/2318
/dev/loop3       39M   39M     0 100% /snap/snapd/21759
tmpfs            96M     0   96M   0% /run/user/0
```

### 2.2. 显示每个顶级目录的总大小

```
du -sh /*
```

```text
0	/bin
217M	/boot
0	/dev
7.2M	/etc
28K	/home
0	/lib
0	/lib32
0	/lib64
0	/libx32
16K	/lost+found
4.0K	/media
4.0K	/mnt
12K	/opt
0	/proc
5.2G	/root
1.3M	/run
0	/sbin
968M	/snap
4.0K	/srv
3.1G	/swapfile
0	/sys
960K	/tmp
3.6G	/usr
4.2G	/var
```
