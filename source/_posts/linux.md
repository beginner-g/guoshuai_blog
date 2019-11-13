---
title: Linux服务器运维常用命令
categories:
  - Linux
date: 2018-03-15 11:23:06
cover_picture: http://img3.imgtn.bdimg.com/it/u=840746699,4253707424&fm=27&gp=0.jpg
tags: linux
---
### 目录操作
- cd - 回到前一目录 
- cd 回到用户目录 
- (cd dir && command) 进入目录dir，执行命令command然后回到当前目录 
- pushd . 将当前目录压入栈，以后你可以使用popd回到此目录
- mkdir –p【递归创建目录】
- pwd【显示当前目录】
- rmdir【删除空目录】
- cp【复制文件到某个目录下】
- cp –r【复制目录】
- cp –p【保留文件属性】
- mv【剪切文件、改名】
- rm【删除文件】
- rm –r【删除目录】
- rm –f【强制执行】

### 命令格式与目录处理命令
- ls –a【查看隐藏文件】
- ls –l【查看文件信息长格式显示】
- ls –d【查看指定目录的详细信息】
- ls –h【显示容量大小】
- ls –i【查看任何文件的I 节点】
- ll 文件名【查看一个文件的详细信息】

### 磁盘空间 (参见FSlint)
- ls -lSr 按文件大小降序显示文件 
- du -s * | sort -k1,1rn | head 显示当前目录下占用空间最大的一批文件. 参见dutop 
- df -h 显示空余的磁盘空间 
- df -i 显示空余的inode 
- fdisk -l 显示磁盘分区大小和类型（在root下执行） 
- rpm -q -a --qf '%10{SIZE}\t%{NAME}\n' | sort -k1,1n 显示所有在rpm发布版上安装的包，并以包字节大小为序 
- dpkg-query -W -f='${Installed-Size;10}\t${Package}\n' | sort -k1,1n 显示所有在deb发布版上安装的包，并以KB包大小为序 
- dd bs=1 seek=2TB if=/dev/null of=ext3.test 建立一个大的测试文件（不占用空间）. 参见truncate 

### 监视/调试
- strace -c ls >/dev/null 总结/剖析命令进行的系统调用 
- strace -f -e open ls >/dev/null 显示命令进行的系统调用 
- ltrace -f -e getenv ls >/dev/null 显示命令调用的库函数 
- lsof -p $$ 显示当前进程打开的文件 
- lsof ~ 显示打开用户目录的进程 
- tcpdump not port 22 显示除了ssh外的网络交通. 参见tcpdump_not_me 
- ps -e -o pid,args --forest 以树状结构显示进程 
- ps -e -o pcpu,cpu,nice,state,cputime,args --sort pcpu | sed '/^ 0.0 /d' 以CPU占用率为序显示进程 
- ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS 以内存使用量为序显示进程. 参见ps_mem.py 
- ps -C firefox-bin -L -o pid,tid,pcpu,state 显示指定进程的所有线程信息 
- ps -p 1,2 显示指定进程ID的进程信息 
- last reboot 显示系统重启记录 
- free -m 显示(剩余的)内存总量(-m以MB为单位显示) 
- watch -n1 'cat /proc/interrupts' 监测文件/proc/interrupts的变化 

### 系统信息 (参见sysinfo)
- hdparm -i /dev/hda 显示关于磁盘hda的信息 
- hdparm -tT /dev/hda 检测磁盘hda的读取速度 
- badblocks -s /dev/hda 检测磁盘hda上所有的坏扇区 
- mount | column -t 显示所有挂载的文件系统并对齐输出 
- cat /proc/partitions 显示所有在系统中注册的分区 
- grep MemTotal /proc/meminfo 显示系统可见的内存总量 
- grep "model name" /proc/cpuinfo 显示CPU信息 
- lspci -tv 显示PCI信息 
- lsusb -tv 显示USB信息 

### 权限管理
- chmod【改变文件或目录权限,u=所有者;g=所有组;o=其他人;a=全部,[{ugoa}{+-=}{rwx}],chmod u+x,o-r或640 文件名,r—4;w—2;x—1,rwx—7(4+2+1)】
- chmod –R【递归修改,子目录的权限也修改】

### 用户组管理
1).添加用户组
groupadd 组名【-g GID:指定组ID】
2).修改用户组
groupmod 组名【-g GID:修改组ID,-n 新组名:修改组名】
3).删除用户组
groupdel 组名
4).把用户添加入组或从组中删除
gpasswd 选项 组名【-a 用户名:把用户加入组,-d 用户名:把用户从组中删除】