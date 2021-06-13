---
title: Linux相关命令
tags: 'Linux'
categories: 
  - 'Linux'
  - 'CentOS 7'
abbrlink: 13330
description: Linux命令
date: 2021-03-27 11:46:28
keywords: 
  - 'Linux'
  - 'CentOS 7'
top_img: images/linux/linux.jpg
cover: images/linux/linux-canva.jpg

---

对于任何一个程序员来说，linux都是非常重要的。

#### 1、文件管理

1. `ls`    

```shell
ls -l     #该目录下面的文件
ls -l /   #/目录下面的文件
ll        #ls -l 的简写
```

2. `cd`

```shell
cd /usr   #切换目录至usr
```

3. `cp`

```shell
cp 1.text /usr/2.txt   #拷贝文件
```

4. `mv`

```shell
mv 1.txt /usr/2.txt   #将1.txt移动到/usr下面并改名为2.txt
```

5. `rm`

```shell
rm -rf 1.txt      # -r说明是目录或者文件  f说明不提示确定信息
```

6. `pwd`

```shell
pwd     # 显示当前所在目录
```

7. `clean`

```shell
clean      #清除屏幕信息
```

8. `mkdir`

```shell
mkdir d     #创建d目录
```

9. `touch`

```shell
touch 1.txt     #创建1.txt文件
```



#### 2、系统

1. `passwd`

```shell
passwd root   #用于设置用户密码
```

2. `su`

```shell
su -      #q切换至超级用户
```

3. `man`

```shell
man ls      #显示帮助命令
```

4. `who`

```shell
who -r       #显示当前的运行级别
who -buT     #显示当前登录的系统用户
```

#### 3、文件查看

1.`vim和vi`

```shell
vim 1.txt    #查看编辑1.txt文件
vi 1.txt
```

进入后常用操作：i进行插入    esc退出插入     :wq保存并退出   :!q强制退出

- 跳到最后一行     :$
- 查找    /zhansan     n    向下查找。    N   向上查找    

2. `cat`

```shell
cat -Ab /var/log/boot.log     #用于查看文件，例如查看Linux启动日志文件文件，并标明行号,只能显示最后一屏内容
```

3. `more`

```shell
more -c -10 /var/log/boot.log    #用于分页查看文件，例如每页10行查看boot.log文件,可以显示百分比，回车可以向下一行，	空格可以向下一页，q可以退出查看
```

4. `less`

```shell
less /var/log/boot.log    #可以使用键盘上的PgUp和PgDn向上	和向下翻页，q结束查看
```

5. `tail`

```shell
tail -f ../log/catalina.log     #实时查看文件加载内容，例如查看tomcat启动日志，实时监测是否成功
tail -10 /etc/sudo.conf         #查看文件的后10行，Ctrl+C结束
```

#### 4、解压与压缩

##### 4.1、tar类型

1. 分页查看压缩包中内容

```shell
tar -ztvf /demo.tar.gz |more -c -10
```

2. 用``gzip`压缩文件夹`/etc`中的文件到文件`etc.tar.gz`

```shell
tar -zcvf /demo.tar.gz /home
```

3. 用`bzip2`压缩文件夹`/etc`到文件`/etc.tar.bz2`

```shell
tar -jcvf /demo.tar.bz2 /home
```

4. 解压文件到当前目录（gzip）

```shell
tar -zxvf /demo.tar.gz
```

5. 解压文件到指定目录（gzip）

```shell
tar -zxvf /demo.tar.gz -C /usr/local
```

##### 4.2、zip类型

1、查看zip文件中的内容

```shell
zipinfo -1 -M  filename.zip
```

参数说明：

- -1 只列出文件名称。
- -2 此参数的效果和指定"-1"参数类似，但可搭配"-h","-t"和"-z"参数使用。
- -h 只列出压缩文件的文件名称。
- -l 此参数的效果和指定"-m"参数类似，但会列出原始文件的大小而非每个文件的压缩率。
- -m 此参数的效果和指定"-s"参数类似，但多会列出每个文件的压缩率。
- -M 若信息内容超过一个画

2. 解压zip文件

```shell
unzip filename.zip
```

3. 对文件进行zip压缩

```shell
zip filename.zip filename.jar   #将filename.jar压缩为文件名为filename.zip的压缩文件
```

#### 5、系统服务管理

拿达梦服务做演示

1. 输出系统中各个服务的状态

```shell
systemctl list-units --type=service
```

![输出各个服务状态](/blog/images/linux/systemctl_see_service.png)

2. 查看服务运行状态

```shell
systemctl status DmServiceDMSERVER.service
```

![查看服务运行状态](/blog/images/linux/systemctl_status.png)

3. 关闭服务

```shell
systemctl stop DmServiceDMSERVER.service
```

4. 启动服务

```shell
systemctl start DmServiceDMSERVER.service
```

5. 重新启动服务（不管当前服务是启动还是关闭）

```shell
systemctl restart DmServiceDMSERVER.service
```

6. 重新载入配置信息而不中断服务

```shell
systemctl reload DmServiceDMSERVER.service
```

7. 禁止服务开机自启动

```shell
systemctl disable DmServiceDMSERVER.service
```

8. 设置服务开机自启动

```shell
systemctl enable DmServiceDMSERVER.service
```

#### 6、内存与磁盘相关命令

##### 6.1、free

 **free命令用以显示当前系统内存使用情况，其数据取自/proc/meminfo文件。**

1. 使用方式

```shell
cat /proc/meminfo
free -m   #是快速查看上一个命令的方法
free -h -s 3   #表示每隔三秒输出一次内存情况
```

![free命令](/blog/images/linux/free.png)

参数：

-  `-b, –bytes`， 以Byte为单位显示内存使用情况
-  
-  `-k, –kilo`， 以KB为单位， 这也是默认值
- `-m, –mega`， 以MB为单位显示内容使用情况
- `-g, –giga`， 以GB为单位显示内存使用情况

```shell
free -h    # human    换为人类可以读懂的方式
```

![free命令](/blog/images/linux/free_h.png)

2. 内容解读

- **第一列**
   `Mem` 内存的使用信息
   `Swap` 交换空间的使用信息
-  **第一行**
   `total` 系统总的可用物理内存和交换空间大小。
   `used` 已经被使用的物理内存和交换空间。
   `free` 还有多少物理内存和交换空间可用使用，是真正尚未被使用的物理内存数量。
   `shared` 被共享使用的物理内存大小
   `buff/cache` 被 buffer（缓冲区） 和 cache（缓存） 使用的物理内存大小。
   `available` 还可以被 ***应用程序\*** 使用的物理内存大小

`free` 是真正尚未被使用的物理内存数量。
`available` 是应用程序认为可用内存数量，`available = free + buffer + cache` (注：只是大概的计算方法)

**如何判断系统内存不足：** 如果Swap used值大于0，代表服务器物理内存已经遇到内存瓶颈了，已开始使用虚拟内存了，要么优化代码，要么加内存

- **什么是交换空间？**

​       swap space 是磁盘上的一块区域，当系统物理内存吃紧时，Linux 会将内存中不常访问的数据保存到 swap 上，这样系统就有更多的物理内存为各个进程服务，而当系统需要访问 swap 上存储的内容时，再将 swap 上的数据加载到内存中，这就是常说的换出和换入。交换空间可以在一定程度上缓解内存不足的情况，但是它需要读写磁盘数据，所以性能不是很高。

##### 6.2、ps

- 显示系统进程运行动态

```shell
ps -ef
```

- 查看`java`进程的运行动态

```shell
ps -ef|grep java
```
- 查看特定进程的数量

如查看java进程的数量,`ps -ef | grep java| wc -l`：

```shell
ps -ef | grep java| wc -l
```

- 查看线程是否存在死锁

查看线程是否存在死锁，`jstack -l pid`：

```shell
[root@localhost ~]# jstack -l 124146
2020-05-02 10:13:38
Full thread dump OpenJDK 64-Bit Server VM (25.252-b09 mixed mode):

"C1 CompilerThread1" #6 daemon prio=9 os_prio=0 tid=0x00007f27f013c000 nid=0x1e4f9 waiting on condition [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

   Locked ownable synchronizers:
        - None

"C2 CompilerThread0" #5 daemon prio=9 os_prio=0 tid=0x00007f27f012d000 nid=0x1e4f8 waiting on condition [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

   Locked ownable synchronizers:
        - None

"main" #1 prio=5 os_prio=0 tid=0x00007f27f004b800 nid=0x1e4f3 waiting on condition [0x00007f27f7274000]
   java.lang.Thread.State: TIMED_WAITING (sleeping)
        at java.lang.Thread.sleep(Native Method)
        at java.lang.Thread.sleep(Thread.java:340)
        at java.util.concurrent.TimeUnit.sleep(TimeUnit.java:386)
        at demo.MathGame.main(MathGame.java:17)

   Locked ownable synchronizers:
        - None
...
```

- 查看某个进程的线程数

`ps -efL | grep [PID] | wc -l`，如：

```shell
[root@localhost ~]# ps -efL | grep 124146 | wc -l
12
```

- 查看具体有哪些线程用`ps -Lp [pid] cu`:

```shell
[root@localhost ~]# ps -Lp 124146 cu
USER        PID    LWP %CPU NLWP %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root     124146 124146  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:00 java
root     124146 124147  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:01 java
root     124146 124148  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:00 VM Thread
root     124146 124149  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:00 Reference Handl
root     124146 124150  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:00 Finalizer
root     124146 124151  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:00 Signal Dispatch
root     124146 124152  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:00 C2 CompilerThre
root     124146 124153  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:00 C1 CompilerThre
root     124146 124154  0.0   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:00 Service Thread
root     124146 124155  0.1   11  2.5 2489116 35724 pts/0   Sl+  09:13   0:05 VM Periodic Tas
root     124146 125362  0.0   11  2.5 2489116 35724 pts/0   Sl+  10:13   0:00 Attach Listener
```

- 统计所有的log文件中，包含Error字符的行

`find / -type f -name "*.log" | xargs grep "ERROR"`，这个在排查问题过程中比较有用：

```shell
[root@localhost ~]# find / -type f -name "*.log" | xargs grep "ERROR"
/var/log/tuned/tuned.log:2020-03-13 18:05:59,145 ERROR    tuned.utils.commands: Writing to file '/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor' error: '[Errno 19] No such device'
/var/log/tuned/tuned.log:2020-03-13 18:05:59,145 ERROR    tuned.utils.commands: Writing to file '/sys/devices/system/cpu/cpu1/cpufreq/scaling_governor' error: '[Errno 19] No such device'
/var/log/tuned/tuned.log:2020-04-28 14:55:34,857 ERROR    tuned.utils.commands: Writing to file '/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor' error: '[Errno 19] No such device'
/var/log/tuned/tuned.log:2020-04-28 14:55:34,859 ERROR    tuned.utils.commands: Writing to file '/sys/devices/system/cpu/cpu1/cpufreq/scaling_governor' error: '[Errno 19] No such device'
/var/log/tuned/tuned.log:2020-04-28 15:23:19,037 ERROR    tuned.utils.commands: Writing to file '/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor' error: '[Errno 19] No such device'
...
```

##### 6.3、top

查看即时活跃的进程，类似Windows的任务管理器。

```shell
top
```

![top](/blog/images/linux/top.png)

内容及参数说明：

![](/blog/images/linux/top_info.png)

第一行：`22:07:24 up 110 days,  9:19,  1 user,  load average: 4.01, 4.07, 4.06` ：22:07:24 系统时间，up 110 days 运行时间，1 user 当前登录用户数，load average 负载均衡情况，分别表示1分钟，5分钟，15分钟负载情况。

第二行：`Tasks: 315 total,1 running, 313 sleeping, 0 stopped,1 zombie`：总进程数315，运行数1，休眠 313，停止0，僵尸进程0。

第三行：`%Cpu(s): 50.8 us, 0.5 sy, 0.0 ni, 48.6 id, 0.0 wa,0.0 hi,0.0 si,0.0 st`：用户空间CPU占比50.8%，内核空间CPU占比0.5%，改变过优先级的进程CPU占比0。0%，空闲CPU占比48.6%，IO等待占用CPU占比0.0%，硬中断占用CPU占比0。0%，软中断占用CPU占比0.0%,当前VM中的cpu 时钟被虚拟化偷走的比例0.0%。

第四和第五行表示内存和swap区域的使用情况。

第七行表示：

- `PID`: 进程id
- `USER`:进程所有者
- `PR`:进程优先级
- `NI`:nice值。负值表示高优先级，正值表示低优先级
- `VIRT`:虚拟内存，进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES
- `RES`:常驻内存，进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA
- `SHR`:共享内存，共享内存大小，单位kb
- `S`:进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程
- `%CPU`:上次更新到现在的CPU时间占用百分比
- `%MEM`:进程使用的物理内存百分比
- `TIME+`:进程使用的CPU时间总计，单位1/100秒
- `COMMAND`:进程名称（命令名/命令行）

##### 6.4、uptime

```shell
uptime
```

![](/blog/images/linux/uptime.png)

参数分别为：当前时间  系统运行天数   当前登录用户个数   系统负载（即任务队列的平均长度）：1mim   5mim  15mim到现在的平均值  

##### 6.5、df

查看磁盘空间占用情况

```shell
df -hT
```

![](/blog/images/linux/df.png)

##### 6.6、du

`du -sh`命令是查看磁盘已使用空间的情况，这里的“已使用的磁盘空间”意思是指定的文件下的整个文件层次结构所使用的空间，在没给定参数的情况下，`du`报告当前目录所使用的磁盘空间。其实就是显示文件或目录所占用的磁盘空间的情况：

```shell
du -sh
```

- `-h`：输出文件系统分区使用的情况，例如：10KB，10MB，10GB等。
- `-s`：显示文件或整个目录的大小，默认单位是KB。

> **!!** `du`的详细信息可以通过 `man du`查看。

查看当前目录下的文件及文件夹所占大小

```shell
du -h --max-depth=1 ./*
```

![](/blog/images/linux/du.png)

##### 6.7、vastat（重要）

虚拟内存统计，是Linux中监控内存的常用工具，可对操作系统的虚拟内存、进程、CPU等的整体情况进行监视，推荐使用。

```shell
vmstat
vmstat 5 3   # 表示每隔5秒统计一次，一共统计三次。
```

![](/blog/images/linux/vmstat.png)

 **procs**

- `r`：表示运行和等待CPU时间片的进程数（就是说多少个进程真的分配到CPU），这个值如果长期大于系统CPU个数，说明CPU不足，需要增加CPU。
- `b`：表示在等待资源的进程数，比如正在等待I/O或者内存交换等。

**memory**

- `swpd`：表示切换到内存交换区的内存大小，即虚拟内存已使用的大小（单位KB），如果大于0，表示你的机器物理内存不足了，如果不是程序内存泄露的原因，那么你该升级内存了或者把耗内存的任务迁移到其他机器。
- `free`：表示当前空闲的物理内存。
- `buff`：表示缓冲大小，一般对块设备的读写才需要缓冲
-  `Cache`：表示缓存大小，一般作为文件系统进行缓冲，频繁访问的文件都会被缓存，如果cache值非常大说明缓存文件比较多，如果此时io中的bi比较小，说明文件系统效率比较好。

**swap**

- `si`：表示数据由磁盘读入内存；通俗的讲就是每秒从磁盘读入虚拟内存的大小，如果这个值大于0，表示物理内存不够用或者内存泄露了，要查找耗内存进程解决掉。
- `so`：表示由内存写入磁盘，也就是由内存交换区进入内存的数据大小。

> **!!** 注意：一般情况下si、so的值都为0，如果si、so的值长期不为0，则说明系统内存不足，需要增加系统内存

**io**

- `bi`：表示由块设备读入数据的总量，即读磁盘，单位kb/s `bo`：表示写到块设备数据的总量，即写磁盘，单位kb/s

> **!!** 注意：如果bi+bo的值过大，且wa值较大，则表示系统磁盘IO瓶颈。

**system**

- `in`：表示某一时间间隔内观测到的每秒设备终端数。
- `cs`：表示每秒产生的上下文切换次数，这个值要越小越好，太大了，要考虑调低线程或者进程的数目。例如在apache和nginx这种web服务器中，我们一般做性能测试时会进行几千并发甚至几万并发的测试，选择web服务器的进程可以由进程或者线程的峰值一直下调，压测，直到cs到一个比较小的值，这个进程和线程数就是比较合适的值了。系统调用也是，每次调用系统函数，我们的代码就会进入内核空间，导致上下文切换，这个是很耗资源，也要尽量避免频繁调用系统函数。上下文切换次数过多表示你的CPU大部分浪费在上下文切换，导致CPU干正经事的时间少了，CPU没有充分利用，是不可取的。

> **!!** 注意：这两个值越大，则由内核消耗的CPU就越多。

**CPU**

- `us`：表示用户进程消耗的CPU时间百分比，us值越高，说明用户进程消耗CPU时间越多，如果长期大于50%，则需要考虑优化程序或者算法。
- `sy`：表示系统内核进程消耗的CPU时间百分比，一般来说us+sy应该小于80%，如果大于80%，说明可能存在CPU瓶颈。
- `id`：表示CPU处在空间状态的时间百分比。
- `wa`：表示IP等待所占用的CPU时间百分比，wa值越高，说明I/O等待越严重，根据经验wa的参考值为20%，如果超过20%，说明I/O等待严重，引起I/O等待的原因可能是磁盘大量随机读写造成的，也可能是磁盘或者监控器的贷款瓶颈（主要是块操作）造成的。

##### 6.8、定位线上最耗CPU的线程

**准备工作**

启动一个程序。`arthas-demo`是一个简单的程序，每隔一秒生成一个随机数，再执行质因数分解，并打印出分解结果。

```shell
curl -O https://alibaba.github.io/arthas/arthas-demo.jar
java -jar arthas-demo.jar
[root@localhost ~]# curl -O https://alibaba.github.io/arthas/arthas-demo.jar
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  3743  100  3743    0     0   3022      0  0:00:01  0:00:01 --:--:--  3023
[root@localhost ~]# java -jar arthas-demo.jar
1813=7*7*37
illegalArgumentCount:  1, number is: -180005, need >= 2
illegalArgumentCount:  2, number is: -111175, need >= 2
18505=5*3701
166691=7*23813
105787=11*59*163
60148=2*2*11*1367
196983=3*3*43*509
illegalArgumentCount:  3, number is: -173479, need >= 2
illegalArgumentCount:  4, number is: -112840, need >= 2
39502=2*19751
....
```

**通过`top`命令找到最耗时的进程**

```shell
[root@localhost ~]# top
top - 11:11:05 up 20:02,  3 users,  load average: 0.09, 0.07, 0.05
Tasks: 225 total,   1 running, 224 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.7 sy,  0.0 ni, 99.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  1421760 total,   135868 free,   758508 used,   527384 buff/cache
KiB Swap:  2097148 total,  2070640 free,    26508 used.   475852 avail Mem
Change delay from 3.0 to
   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
 98344 root      20   0 2422552  23508  12108 S   0.7  1.7   0:00.32 java
     1 root      20   0  194100   6244   3184 S   0.0  0.4   0:20.41 systemd
     2 root      20   0       0      0      0 S   0.0  0.0   0:00.12 kthreadd
     4 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 kworker/0:0H
     6 root      20   0       0      0      0 S   0.0  0.0   0:20.25 ksoftirqd/0
```

找到进程号是98344。

**找到进程中最耗CUP的线程**

使用`ps -Lp #pid cu`命令，查看某个进程中的线程CPU消耗排序：

```shell l
[root@localhost ~]# ps -Lp 98344 cu
USER        PID    LWP %CPU NLWP %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root      98344  98344  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:00 java
root      98344  98345  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:04 java
root      98344  98346  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:01 VM Thread
root      98344  98347  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:00 Reference Handl
root      98344  98348  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:00 Finalizer
root      98344  98349  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:00 Signal Dispatch
root      98344  98350  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:05 C2 CompilerThre
root      98344  98351  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:00 C1 CompilerThre
root      98344  98352  0.0   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:00 Service Thread
root      98344  98353  0.1   10  4.1 2422552 59060 pts/0   Sl+  11:09   0:19 VM Periodic Tas
```

看`TIME`列可以看出那个线程耗费CUP多，根据`LWP`列可以看到线程的ID号，但是需要转换成16进制才可以查询线程堆栈信息。

**获取线程id的十六进制码**

使用`printf '%x\n' 98345`命令做进制转换：

```shell l
[root@localhost ~]# printf '%x\n' 98345
18029
```

**查看线程堆栈信息**

使用jstack获取堆栈信息`jstack 98344 | grep -A 10 18029`：

```shell
[root@localhost ~]# jstack 98344 | grep -A 10 18029
"main" #1 prio=5 os_prio=0 tid=0x00007fb88404b800 nid=0x18029 waiting on condition [0x00007fb88caab000]
   java.lang.Thread.State: TIMED_WAITING (sleeping)
        at java.lang.Thread.sleep(Native Method)
        at java.lang.Thread.sleep(Thread.java:340)
        at java.util.concurrent.TimeUnit.sleep(TimeUnit.java:386)
        at demo.MathGame.main(MathGame.java:17)

"VM Thread" os_prio=0 tid=0x00007fb8840f2800 nid=0x1802a runnable

"VM Periodic Task Thread" os_prio=0 tid=0x00007fb884154000 nid=0x18031 waiting on condition
```

通过命令我们可以看到这个线程的对应的耗时代码是在`demo.MathGame.main(MathGame.java:17)`

```
grep -C 5 foo file 显示file文件里匹配foo字串那行以及上下5行
grep -B 5 foo file 显示foo及前5行
grep -A 5 foo file 显示foo及后5行
```

#### 7、查看磁盘读写情况

##### 7.1、查看磁盘总体读写情况

通`iostat`查看磁盘总体的读写情况：

```shell
[root@localhost ~]# iostat
Linux 3.10.0-1062.el7.x86_64 (localhost.localdomain)    2020年05月02日  _x86_64_        (2 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.17    0.00    0.20    0.46    0.00   99.17

Device:            tps    kB_read/s    kB_wrtn/s    kB_read    kB_wrtn
sda               1.56        30.45        39.61    4659620    6060644
scd0              0.00         0.02         0.00       3102          0
dm-0              1.96        30.01        38.42    4591998    5878155
dm-1              0.09         0.09         0.30      13840      45328
```

- `tps`：该设备每秒的传输次数。
- `kB_read/s`：每秒从设备（drive expressed）读取的数据量；
- `kB_wrtn/s`：每秒向设备（drive expressed）写入的数据量；
- `kB_read`：读取的总数据量；
- `kB_wrtn`：写入的总数量数据量；

##### 7.2、查看磁盘详细读写情况

通过`iostat -x 1 3`可以看到磁盘详细读写情况，没隔一秒输出一次一共输出3次，当看到I/O等待时间所占CPU时间的比重很高的时候，首先要检查的就是机器是否正在大量使用交换空间，同时关注`iowait`占比cpu的消耗是否很大，如果大说明磁盘存在大的瓶颈，同时关注`await`，表示磁盘的响应时间以便小于5ms：

```shell
[root@localhost ~]# iostat -x 1 3
Linux 3.10.0-1062.el7.x86_64 (localhost.localdomain)    2020年05月02日  _x86_64_        (2 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.17    0.00    0.20    0.46    0.00   99.16

Device:         rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
sda               0.01     0.49    0.63    0.95    30.59    39.78    89.58     0.34  214.23   49.16  323.48   8.55   1.34
scd0              0.00     0.00    0.00    0.00     0.02     0.00    98.48     0.00    1.21    1.21    0.00   0.95   0.00
dm-0              0.00     0.00    0.62    1.35    30.15    38.59    69.70     0.91  460.67   49.12  648.54   6.66   1.31
dm-1              0.00     0.00    0.02    0.07     0.09     0.30     8.52     0.04  442.74   95.43  521.17   6.91   0.06
```

`avg-cpu`表示总体cpu使用情况统计信息，对于多核cpu，这里为所有cpu的平均值：

- `%user`：CPU处在用户模式下的时间百分比。
- `%nice`：CPU处在带NICE值的用户模式下的时间百分比。
- `%system`：CPU处在系统模式下的时间百分比。
- `%iowait`：CPU等待输入输出完成时间的百分比，如果%iowait的值过高，表示硬盘存在I/O瓶颈。
- `%steal`：管理程序维护另一个虚拟处理器时，虚拟CPU的无意识等待时间百分比。
- `%idle`：CPU空闲时间百分比，如果%idle值高，表示CPU较空闲；如果%idle值高但系统响应慢时，可能是CPU等待分配内存，应加大内存容量；如果%idle值持续低于10，表明CPU处理能力相对较低，系统中最需要解决的资源是CPU。。

`Device`表示设备信息：

- `rrqm/s`：每秒对该设备的读请求被合并次数，文件系统会对读取同块(block)的请求进行合并
- `wrqm/s`：每秒对该设备的写请求被合并次数
- `r/s`：每秒完成的读次数
- `w/s`：每秒完成的写次数
- `rkB/s`：每秒读数据量(kB为单位)
- `wkB/s`：每秒写数据量(kB为单位)
- `avgrq-sz`：平均每次IO操作的数据量(扇区数为单位)
- `avgqu-sz`：平均等待处理的IO请求队列长度
- `await`：平均每次IO请求等待时间(包括等待时间和处理时间，毫秒为单位)
- `svctm`：平均每次IO请求的处理时间(毫秒为单位)
- `%util`：一秒中有百分之多少的时间用于 I/O如果%util接近100%，说明产生的I/O请求太多，I/O系统已经满负荷。`idle`小于70% IO压力就较大了，一般读取速度有较多的wait。

> **!!** `iostat -xmd 1 3`：新增`m`选项可以在输出是使用`M`为单位。

#### 8、查看最耗IO的进程

一般先通过`iostat`查看是否存在io瓶颈，再使用`iotop`命令来定位那个进程最耗费IO：

```shell
[root@localhost ~]# iotop
Total DISK READ :       0.00 B/s | Total DISK WRITE :       0.00 B/s
Actual DISK READ:       0.00 B/s | Actual DISK WRITE:       0.00 B/s
   TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND
123931 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.02 % [kworker/1:30]
 94208 be/4 xiaolyuh    0.00 B/s    0.00 B/s  0.00 %  0.00 % nautilus-desktop --force [gmain]
     1 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % systemd --system --deserialize 62
     2 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kthreadd]
 94211 be/4 xiaolyuh    0.00 B/s    0.00 B/s  0.00 %  0.00 % gvfsd-trash --spawner :1.4 /org/gtk/gvfs/exec_spaw/0
     4 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kworker/0:0H]
     6 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [ksoftirqd/0]
     7 rt/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [migration/0]
     8 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_bh]
     9 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_sched]
    10 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [lru-add-drain]
...
```

通过`iotop -p pid`可以查看单个进程的IO情况：

```shell
[root@localhost ~]# iotop -p 124146
Total DISK READ :       0.00 B/s | Total DISK WRITE :       0.00 B/s
Actual DISK READ:       0.00 B/s | Actual DISK WRITE:       0.00 B/s
   TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND
124146 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % java -jar arthas-demo.jar
```

#### 9、网络

##### 9.1、`netstat`

- 查看当前路由信息：

```shell
netstat -rn
```

- 查看所有有效TCP连接：

```shell
netstat -an
```

- 查看系统中启动的监听服务：

```shell
netstat -tulnp
```

- 查看处于连接状态的系统资源信息：

```shell
netstat -atunp
```

##### 9.2、定位丢包，错包情况

`watch more /proc/net/dev`用于定位丢包，错包情况，以便看网络瓶颈，重点关注drop(包被丢弃)和网络包传送的总量，不要超过网络上限：

```shell
[root@localhost ~]# watch -n 2 more /proc/net/dev
Every 2.0s: more /proc/net/dev                                                                                                                                                   Fri May  1 17:16:55 2020

Inter-|   Receive                                                |  Transmit
 face |bytes    packets errs drop fifo frame compressed multicast|bytes    packets errs drop fifo colls carrier compressed
    lo:   10025     130    0    0    0     0          0         0    10025     130    0    0    0     0       0          0
 ens33: 759098071  569661    0    0    0     0          0         0 19335572  225551    0    0    0     0       0          0
```

- 最左边的表示接口的名字，Receive表示收包，Transmit表示发送包；
- `bytes`：表示收发的字节数；
- `packets`：表示收发正确的包量；
- `errs`：表示收发错误的包量；
- `drop`：表示收发丢弃的包量；

##### 9.3、查看网络错误

`netstat -i`可以查看网络错误：

```shell
[root@localhost ~]# netstat -i
Kernel Interface table
Iface             MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
ens33            1500   570291      0      0 0        225897      0      0      0 BMRU
lo              65536      130      0      0 0           130      0      0      0 LRU
```

- `Iface`: 网络接口名称;
- `MTU`: 最大传输单元，它限制了数据帧的最大长度，不同的网络类型都有一个上限值，如：以太网的MTU是1500；
- `RX-OK`：接收时，正确的数据包数。
- `RX-ERR`：接收时，产生错误的数据包数。
- `RX-DRP`：接收时，丢弃的数据包数。
- `RX-OVR`：接收时，由于过速（在数据传输中，由于接收设备不能接收按照发送速率传送来的数据而使数据丢失）而丢失的数据包数。
- `TX-OK`：发送时，正确的数据包数。
- `TX-ERR`：发送时，产生错误的数据包数。
- `TX-DRP`：发送时，丢弃的数据包数。
- `TX-OVR`：发送时，由于过速而丢失的数据包数。
- `Flg`：标志，B 已经设置了一个广播地址。L 该接口是一个回送设备。M 接收所有数据包（混乱模式）。N 避免跟踪。O 在该接口上，禁用ARP。P 这是一个点到点链接。R 接口正在运行。U 接口处于“活动”状态。

##### 9.4、包的重传率

`cat /proc/net/snmp`用来查看和分析240秒内网络包量，流量，错包，丢包。通过`RetransSegs`和`OutSegs`来计算重传率`tcpetr=RetransSegs/OutSegs`。

```shell
[root@localhost ~]# cat /proc/net/snmp
Ip: Forwarding DefaultTTL InReceives InHdrErrors InAddrErrors ForwDatagrams InUnknownProtos InDiscards InDelivers OutRequests OutDiscards OutNoRoutes ReasmTimeout ReasmReqds ReasmOKs ReasmFails FragOKs FragFails FragCreates
Ip: 1 64 241708 0 0 0 0 0 238724 225517 15 0 0 0 0 0 0 0 0
Icmp: InMsgs InErrors InCsumErrors InDestUnreachs InTimeExcds InParmProbs InSrcQuenchs InRedirects InEchos InEchoReps InTimestamps InTimestampReps InAddrMasks InAddrMaskReps OutMsgs OutErrors OutDestUnreachs OutTimeExcds OutParmProbs OutSrcQuenchs OutRedirects OutEchos OutEchoReps OutTimestamps OutTimestampReps OutAddrMasks OutAddrMaskReps
Icmp: 149 0 0 50 99 0 0 0 0 0 0 0 0 0 147 0 147 0 0 0 0 0 0 0 0 0 0
IcmpMsg: InType3 InType11 OutType3
IcmpMsg: 50 99 147
Tcp: RtoAlgorithm RtoMin RtoMax MaxConn ActiveOpens PassiveOpens AttemptFails EstabResets CurrEstab InSegs OutSegs RetransSegs InErrs OutRsts InCsumErrors
Tcp: 1 200 120000 -1 376 6 0 0 4 236711 223186 292 0 4 0
Udp: InDatagrams NoPorts InErrors OutDatagrams RcvbufErrors SndbufErrors InCsumErrors
Udp: 1405 438 0 1896 0 0 0
UdpLite: InDatagrams NoPorts InErrors OutDatagrams RcvbufErrors SndbufErrors InCsumErrors
UdpLite: 0 0 0 0 0 0 0
```

重传率=292/223186≈0.13%

- 平均每秒新增TCP连接数：通过/proc/net/snmp文件得到最近240秒内PassiveOpens的增量，除以240得到每秒的平均增量；
- 机器的TCP连接数 ：通过/proc/net/snmp文件的CurrEstab得到TCP连接数；
- 平均每秒的UDP接收数据报：通过/proc/net/snmp文件得到最近240秒内InDatagrams的增量，除以240得到平均每秒的UDP接收数据报；
- 平均每秒的UDP发送数据报：通过/proc/net/snmp文件得到最近240秒内OutDatagrams的增量，除以240得到平均每秒的UDP发送数据报；

#### 10、文件上传下载

- 安装上传下载工具`lrzsz`；

```shell
yum install -y lrzsz
```

- 上传文件，输入以下命令`XShell`会弹出文件上传框；

```shell
rz
```

- 下载文件，输入以下命令`XShell`会弹出文件保存框；

```shell
sz fileName
```

#### 11、rpm

> RPM是`Red-Hat Package Manager`的缩写，一种Linux下通用的软件包管理方式，可用于安装和管理`.rpm`结尾的软件包。

- 安装软件包：

```shell
rpm -ivh nginx-1.12.2-2.el7.x86_64.rpm
```

- 模糊搜索软件包：

```shell
rpm -qa | grep nginx
```

- 精确查找软件包：

```shell
rpm -qa nginx
```

- 查询软件包的安装路径：

```shell
rpm -ql nginx-1.12.2-2.el7.x86_64
```

- 查看软件包的概要信息：

```shell
rpm -qi nginx-1.12.2-2.el7.x86_64
```

- 验证软件包内容和安装文件是否一致：

```shell
rpm -V nginx-1.12.2-2.el7.x86_64
```

- 更新软件包：

```shell
rpm -Uvh nginx-1.12.2-2.el7.x86_64
```

- 删除软件包：

```shell
rpm -e nginx-1.12.2-2.el7.x86_64
```

#### 12、yum

> Yum是`Yellow dog Updater, Modified`的缩写，能够在线自动下载RPM包并安装，可以自动处理依赖性关系，并且一次安装所有依赖的软件包，非常方便！

- 安装软件包：

```shell
yum install nginx
```

- 检查可以更新的软件包：

```shell
yum check-update
```

- 更新指定的软件包：

```shell
yum update nginx
```

- 在资源库中查找软件包信息：

```shell
yum info nginx*
```

- 列出已经安装的所有软件包：

```shell
yum info installed
```

- 列出软件包名称：

```shell
yum list nginx*
```

- 模糊搜索软件包：

```shell
yum search nginx
```

#### 13、其他命令

- 杀死进程

```shell
kill -9 pid     #pid是进程的id
```

- 关机开机

```shell
reboot     #重启命令
halt       #立即关机
```

- 修改某一个文件的权限

```shell
chmod u=rwx,g=rw,o=r aaa.txt   #修改下的aaa.txt的权限为属主有全部权限，属主所在的组有读写权限，其他用户只有读的权限
chmod 764 aaa.txt     #也可以表示为
```

- 用户相关

```shell
useradd test               #添加test用户
useradd test -d /home/t1   #指定用户home目录
passwd                     #设置、修改密码
passwd  test               #为test用户设置密码
su – 用户名                 #切换登录
userdel test               #删除test用户(不会删除home目录)
userdel –r test            #删除用户以及home目录
```

[部分参考](https://mp.weixin.qq.com/s/48Z_niFVb2AVk2zDWkK-WA)

