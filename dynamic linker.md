# 编译过程：
test.c->test.i->test.s->test.o->test.exe
- Libraries are by default looked for in /lib, /usr/lib and the directories specified by /etc/ld.so.conf
- LD_LIBRARY_PATH="your/boost/directory"
# 如何知道一个可执行程序依赖哪些库
ldd命令可以查看一个可执行程序依赖的共享库，
例如# ldd /bin/lnlibc.so.6
=> /lib/libc.so.6 (0×40021000)/lib/ld-linux.so.2
=> /lib/ld- linux.so.2 (0×40000000)
可以看到ln命令依赖于libc库和ld-linux库
# 可执行程序在执行的时候如何定位共享库文件
当系统加载可执行代码时候，能够知道其所依赖的库的名字，但是还需要知道绝对路径
此时就需要系统动态载入器(dynamic linker/loader)
对于elf格式的可执行程序，是由ld-linux.so*来完成的
它先后搜索elf文件的 DT_RPATH段—环境变量LD_LIBRARY_PATH—/etc/ld.so.cache文件列表—/lib/,/usr/lib目录
找到库文件后将其载入内存
# 在新安装一个库之后如何让系统能够找到他
如果安装在/lib或者/usr/lib下，那么ld默认能够找到，无需其他操作。
如果安装在其他目录，需要将其添加到/etc/ld.so.cache文件中，步骤如下
1.编辑/etc/ld.so.conf文件，加入库文件所在目录的路径
2.运行ldconfig，该命令会重建/etc/ld.so.cache文件