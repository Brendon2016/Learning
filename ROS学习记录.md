# ROS学习记录

## 概念理解

* 节点(node)：类似于分布式系统中的一个站点，多个站点间用tcp通讯。
* 节点管理器(Master)：用于管理所有节点，不然都不知道有哪些节点。
* 参数服务器(Parameter server)：类似于节点管理器，管理所有节点，但主要功能是管理节点的某些参数（推荐静态读写），没有节点都有其specified parameters，rosparam用于操作参数服务器，如list、set、get、load、dump、delete
* 消息(message)：消息是节点间通讯时传输的数据，每个消息都有其固定的数据类型，类似PDO。一个节点可以定义自己发送的消息类型，但只能接收其他节点定义好的消息类型，因此节点通讯时，双方节点需约定好所使用的消息类型。消息的操作用rosmsg，不过暂时没用到。
* 话题(topic)：书上解释说是对消息进行路由或消息管理的数据总线，每一条消息都要发布到相应的主题。那不是定义消息的时候，同时要定义主题？不太理解。rostopic用的很多，list,type,pub,hz,echo。
* 服务(service)：消息一般是自动pub的，通常是周期性的，而服务则不同，类似SDO，只有发出请求后才执行，比如rosservice call /clear用于请求小乌龟重设背景。服务和参数通常联系在一起，比如设置参数后，启动相应服务以执行相应改变。rosservice list call type 
## tools
* rqt_console is useful tool which is used to display outputs of nodes, the outputs has several levels: Fatal、error、warn...，use rqt_logger_level which can select logger level and nodes to display to assistant the console.
* roslaunch starts some nodes all at once, which is defined in a launch file。其中.launch第一部分定义启动launch文件时，可设置的参数，调用方法：roslaunch PACKNAME .launch PARA:=VALUE。launch其他用途：
  1. 启动节点；
  2. 启动其他.launch文件，且可以赋值参数，参见kinova_gazebo\launch\robot_launch.launch
* rqt_graph is used to draw up a picture which display that how the existed nodes communicate with each other
## 自定义message或service
1. 编写并添加.msg/.srv文件到msg/srv文件夹下, .msg文件就是变量名定义，一个变量一行： uint8 age；

    .srv文件与.msg相同，只不过有request和response两部分，中间用 ---分开

2. 在package.xml中添加编译和运行依赖:

    <build_depend>message_generation</build_depend>
    <exec_depend>message_runtime</exec_depend>

3. 将message_generation添加到CmakeLists.txt的find_package中

4. 将CATKIN_DEPENDS message_runtime添加到catkin_package中

5. 将.msg/.srv文件添加到add_message_files/add_service_files中

6. 确保generate_messages()会被调用（取消注释）

7. rosmsg show beginner_tutorials/Num查看是否添加成功

8. make package again : catkin_make install
## 遇到的错误
* error 1 : unable to communicate with service [/clear]
  cause : corresponding nodes which offering service had been killed , rosrun it again will work.

* error 2 ： roscd: no such package/stack

  cause:环境变量没设置好，重新source： . ~/catkin_ws/devel/setup.bash

## questions
* usage of rosrun is : rosrun package name node name, but when we use rosnode list, it sometimes display the package name, why? Also when we launch a same node twice ,how to distinguish them, do they have their own name respectively?  when i try to launch two turtlesim_node, the first one had been shutdown automaticly and reason given is :new node registered with the same name. so if we want to launch a same node for more than once, we should specify different name for them respectively. now the question is how to specify its own name when we launch a node? Remapping Argument is suitable approach. but it seems we just can launch one node twice.

* 主题和消息如何区分？

* 在本包内使用自定义消息类型时，只需添加头文件include "package_name/msg_name"即可；当使用其他包的消息类型时，则需在package.xml中添加依赖：

  ​	build_depend>package_name</build_depend> 

  ​	<run_depend>package_name</run_depend> 

  同时在CMakeLists.txt中添加依赖:

  ​	find_package(catkin REQUIRED COMPONENTS package_name )

  ​	add_dependencies();

* 使用自定义节点时，需在Cmakelist文件中添加：add_executable、add_dependencies、target_link_libraries

* 编译整个工作空间：catkin_make

  编译指定包：catkin_make  -DCATKIN_WHITELIST_PACKAGES= "包名"

* 有时用catkin_make时，新写的cpp编译不出来，且不报错，可能是cpp有问题。这时用指定包编译即可查看问题。
* 

  ```
  echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
  ```

  

  

  ​        