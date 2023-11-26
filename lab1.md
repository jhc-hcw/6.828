# Lab 1:Booting a Pc

## 安装所需要的实验环境

首先这个项目最好要在linux下面运行，要有gcc。

需要下载的东西有此项目补丁过的，方便测试的qemu，还有jos仓库代码。

qemu仓库：

> https://github.com/mit-pdos/6.828-qemu.git

jos仓库

> https://pdos.csail.mit.edu/6.828/2018/jos.git

```shell
$:sudo apt-get install -y build-essential gdb #也就是安装编译环境
$:sudo apt-get install gcc-multilib #安装32位的支持
$:sudo apt-get install zlib1g-dev
$:sudo apt-get install libglib2.0-dev
$:sudo apt-get install libpixman-1-dev
#必须有python2
$:sudo apt-get install python2
#然后进入qemu目录中，执行编译前配置
$:./configure --disable-kvm --disable-werror --target-list="i386-softmmu x86_64-softmmu" --python=python2.7
$:make && sudo make install
#如果编译失败，提示某个符号为找到，就坑爹了，可能最新版的ubuntu改动导致的。
#/usr/bin/ld: qga/commands-posix.o: in function `dev_major_minor':
#/home/jhc/temp1/q2/qga/commands-posix.c:633: undefined reference to `major'
#/usr/bin/ld: /home/jhc/temp1/q2/qga/commands-posix.c:634: undefined reference to `minor'
#collect2: error: ld returned 1 exit status
#make: *** [Makefile:288：qemu-ga] 错误 1

#需要去修改源码，在出错文件里面加入#include <sys/sysmacros.h>
#然后就编译通过啦


```

我用的是ubuntu23,