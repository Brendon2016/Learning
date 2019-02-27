# 定义
实时操作系统（RTOS，RealTime Operation System）是指能够在给定的截止时间前对内部或者外部的异常事件做出正确响应的操作系统。另个一被Donald Gillies提出定义为：一个实时系统是指计算的正确性不仅取决于程序的逻辑正确性，也取决于结果产生的时间,如果系统的时间约束条件得不到满足,将会发生系统出错。实时系统对响应时间有严格要求。
比如在一个PID计算程序中，PID的计算是一部分，计算完立即输出到执行设备也是一部分，非实时系统中，计算完的结果有可能不会理解输出到执行设备，其受CPU性能，系统载荷影响，当CPU性能好，系统任务少时，也能在很短很短时间内响应输出指令，因此，这是受性能影响一个不确定的事件。

# [使用RTOS的场合](https://www.element14.com/community/thread/7254/l/%E9%80%89%E6%8B%A9%E5%AE%9E%E6%97%B6%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9Frtos%E5%89%8D%E5%BF%85%E9%A1%BB%E4%BA%86%E8%A7%A3%E7%9A%84%E5%87%A0%E4%B8%AA%E8%A6%81%E7%82%B9?displayFullThread=true)：
1. 基本通信:

实时响应设备输入：指不管CPU性能、系统载荷等各种影响实时性的因素，当实时任务指定多长时间执行一次读取设备输入就能在该规定时间内执行，这种情况下，输入延时得到保证，最大即为任务周期。

实时响应输出到设备指令：发出输出指令后，立即将其输出设备。
- 网络通讯
- 串口等设备通讯
- 消息系统
2. 资源管理
3. 保护RTOS
4. 可感知OS的调试器

综上，没有基本通讯的场合下一般不用RTOS；与设备的时间同步较好，且不会出现系统过载的情况下，输入设备读取任务无需设置成实时任务。
# 安装PREEMPT_RT patch
https://wiki.linuxfoundation.org/realtime/documentation/howto/applications/preemptrt_setup
https://stackoverflow.com/questions/51669724/install-rt-linux-patch-for-ubuntu
# 编写realtime task
https://wiki.linuxfoundation.org/realtime/documentation/howto/applications/start
# 测试实时性
https://www.cnblogs.com/klb561/p/9123457.html
