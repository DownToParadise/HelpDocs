| LinuxName | UserName | Password | Ros
| ----- | -------|-------| ----|
| Ubuntudzwcar | xia| 123| Yes|
| qingzhou | learningx| 123456|Yes|
| ubuntu18.04 | ccyeung| qwer159 |No|

[参考文档](http://www.autolabor.com.cn/book/ROSTutorials/)
[安装参考2](https://blog.csdn.net/qq_44830040/article/details/106049992)

### ROS安装
#### rosdep update出错解决方案
[参考连接](https://blog.csdn.net/weixin_44023934/article/details/121242176)

#### ROS命令行使用(打开多个终端)
1，打开一个终端，输入roscore ，开启ros
2，打开另一个终端rosrun + 功能报名 + 节点名，如rosrun turtlesim turtlesim_node，在开启另一个键盘控制结点 rosrun turtlesim turtle_teleop_key
3，创建工作空间记得将工作空间的环境变量加入devel/setup.bash，并source一下
4，在工作空间的src创建功能包catkin_make_pkg <package_name> [depend1] [depennd2] depend3..... 

#### 常用命令行工具
*命令行工具的功能都可以通过编写代码完成*
##### 通信工具

* rqt_grap，
可视化显示结点通信，以qt开头的基本上都是可视化的工具
*  rosnode
用来显示所有结点相关结点信息，rosnode info也可以查看具体结点的信息
*  rostopic
查看ros中的话题，通过rostopic pub可以向具体话题发布指令
* rosmsg
* rosservice
查看所有ROS服务，并控制产生服务，逻辑
* rosbag
记录仿真器的运作的数据，rosbag record -a -O cmd_record(文件名)，rosbag play cmd_record.bag（重现服务）
bag文件用于将导航或者建图的文件进行记录，在没有环境的情况下可以对情况进行复现，就相当与拍摄的视频。
* rossrv可以用于查看msg，消息的结构，如rossrv show std_srvs/Trigger 查看Trigger的结构，rossrv show turtlesim/Spwan，查看turtlesim中的消息
* 键盘控制命令rosrun teleop_twist_keyboard eleop_twist_keyboard.py
##### 可视化工具
* qt工具箱
rqt，总的可视化窗口，可以显示其他rqt工具，并进行管理。
rqt_console，日志管理工具，可以自动捕捉当前ROS服务器中的日志信息
rqt_graph，计算图可视化工具，可以查看对应结点和通道关系
rqt_plot，数据绘图工具，可以监控选择的topic（通道）数据变化
rqt_imge_view图像渲染工具。
* rviz 3D可视化界面
rviz是数据显示界面，必须要现有数据，再通过对应的驱动和数据通道，对数据进行显示。87 8-=0
* gazebo 3D物理仿真平台9，
##### 其他工具
* rosparam用于命令行更改参数


#### 编写功能包
* 1，建立工作空间

![avatar](G:\HelpDocs\ROS\pics\QQ截图20211229154910.png)
catkin_ws make后可能没有install包，需要输入catkin_ws install手动创建

* 2，创建功能包

一个工作空间中可以创建多个功能包，我们在src目录下创建功能包。
![avatar](G:\HelpDocs\ROS\pics\QQ截图20211229155906.png)
~~~txt
注：
1，一个工作空间下的功能包名不能够重复。

2，要让ROS找到功能包必须source setup.bash文件，将当前工作空间加到环境变量中

3，通过echo $ROS_PACKAGE_PATH查看当前系统中有哪些工作空间

4，使用catkin_make编译后，一定要source devel/setup.bash，如果报错首先考虑是否执行该条命令，可以将其放入home/.bashsrc中

5，两种通信模式没有如此界限分明，可以相互嵌套和引用。

6，roscore建议在运行新的程序时重启一下，因为关闭了结点，它还会保留结点和通道信息，导致一些同名错误或一些莫名其妙的错误。

7，服务端的callback回调函数中中给response赋值，会自动返回给服务端，并在服务端控制台显示

*8，callback函数相当于中断函数，一定要易于执行，不能有复杂逻辑。

9，Ros工程文件夹没有强制命名规定，rosrun会扫描工作空间，以找到匹配的包，只有习惯命名，建议使用习惯命名，方便工程管理。
msg(自定义消息)，srv(自定义服务消息)，launch(存放launch文件)

10，Ros坐标其只允许单继承，及一个父集，但可有多个子集
~~~

* 3，文件说明
	工作空间中有：
	src			存放源码，配置文件，依赖等其他文件
		package.xml存放相关头文件
		CmakeLists.txt配置工作空间	
	build 		  存放中间编译文件
	devel		存放开发中版本
	install		   存放发行版本

* CmakeLists.txt参数解释
add_excutable(XXX XXX.cpp)将xxx.cpp编译成相关的可执行程序XXX
target_link
#### 通信方式--异步机制 话题+消息
![avatar](G:\HelpDocs\ROS\pics\3.png)
*其中有两个节点，turtlesim和我们自定义的publisher。*

其中Publisher和Subscriber是ROSNode，需要向RosMaster注册，通过Topic（管道机制）将消息（数据结构体）从一个发布者（Publisher）传入到订阅这（Subscriber），两者都可不唯一，执行逻辑，其中使用到的四个我们都可以自定义，但是每个自定义的结点都要先向RosMaster注册。

注：
1，可以使用Python或者C++两种语言，前者可以执行，脚本语言，后者必须编译成可执行文件后再执行
2，Ros Master用于帮助节点建立连接，一旦建立连接ROS Master就没啥作用了
3，.py文件记得更改文件为可执行程序，可使用命令 chmod 771 XXX.py

#### 编写发布者
#### 编写订阅者
#### 自定义消息与服务数据
##### msg
首先在相关dpk_package包名的src文件下生成msg文件夹，建立XXX.msg文件，再配置相关文件，回到工作空间目录catkin_make重新编译
生成的消息头文件在devel/learing_topic/XXmsg.h下
##### srv
首先在相关dpk_package包名的src文件下生成srv文件夹，建立XXX.srv文件，数据分为两部分，上面为请求数据，下面为响应数据，用"---"间隔符分开。
再配置相关文件，回到工作空间目录catkin_make重新编译
~~~srv
string name
uint8 age
uint8 sex

uint8 unknown = 0
uint8 male = 1
uint8 female = 2
---
string result
~~~
#### 自定义管道
ROSMaster会根据你的指出，自动生成一个管道，发布者和订阅者的管道必须相同，才能接受数据


* spin()与spinOne()
Python中没有SpinOne()，需要使用多线程实现SpinOnce()的功能，而C++中两者都有，前者为循环执行
[参考](https://blog.csdn.net/u012029332/article/details/80591646)

#### 参数设置使用与编程方法
* 参数模型（全局字典）
相当于ROS大环境下的环境变量，所有节点都可以访问，并作出修改
* 使用.yaml文件存储参数
* rosparam用于命令行更改参数
* 可通过C++或Python编程实现
~~~shell
#列出当前所有参数
$rosparam list
#显示某个参数的值
$rosparam get param_key
#设置某个参数的zhi
$rosparam set param_key param_value
#保存当前系统参数到文件，默然当前终端路径
$rosparam dump file_name
#从文件中读取参数
$rosparam load file_name
#删除参数
$rosparam delete param_key
~~~

#### 机器人坐标变换（TF变换）
* TF功能包，用于管理所有坐标系
* 坐标系通过，树新型结构保存
* 坐标变换最重要的一个目的就是让其他Link可以跟随基坐标轴运动，或者说驱动轮，运动时，其他坐标轴可以根据坐标变换进行运动
* 坐标变换运用在单独个体就是各个连杆，根据关节连接的坐标进行变换。运用在不同个体，可以产生跟随运动，即可以实现多智能体系统


#### launch文件
* 通过XML文件实现多节点配置与启动，文件名声明成xxx.launch在./ws/pkg_name/src/launch文件夹下
* roslaunch命令行运行launch文件
[launch官方语法文档](http://wiki.ros.org/roslaunch/XML)
* roslaunch pkg_nam XXX.launch
##### 语法
~~~xml
<launch>
<!-- launch文件的根元素，所有标签在其内定义，该标签也表示自定义启动roscore(Ros Master)!-->
</launch>

<node>
<node pkg="turtlesim" type="turtlesim_node" name="turtlesim_node"/>
<!--等于 $rosrun turtlesim turtlesim_node !-->
</node>

<param name="turtle_name1" value="Tom">
<!--param 和 rosparam设置Ros服务参数器的值 !-->
<!--arg声明launch文件内部的局部变量，仅限于launch文件内部使用，注意param和arg都是设置参数，两者设置的参数分别为全局和局部 !-->

<!--remap 重映射，相当于给参数服务器中的某一个参数更改名字，其对应引用的地方不会改变，谨慎使用!-->

<!--include 包含其他launch文件，类似C语言中的头文件包含 !-->
~~~

#### 机器人仿真
* 通过URDF，Rviz，Gazebo三者聚合实现对机器人的模拟仿真实现相关需求
* 实体机器人可以用URDG和Rviz就行


URDF是一种文件格式 * 标准化机器人描述格式 *，类似前端中的HTML语言必须依托Rviz和Gazebo才能发挥作用，其本质是xml文件

RVIZ适用于读取数据，通过ROS服务器中的通道可视化显示数据，如雷达，深度相机，摄像头等

Gazebo用于模拟机器人，构建模拟地形

##### urdf语法及其注意事项
[urdf官方文档](https://wiki.ros.org/urdf/XML)
<robot></robot>为根结点
1，将配置文件关联到launch文件中时就可以通过launch文件直接修改参数，而不再每次在rviz中进行配置
2，link的偏移量一般设置成xyz=“0 0 0”，如果需要偏移则在joint时设置偏移量，为了避免tf坐标系复杂，rpy一般在link中设置，xyz一般在joint中设置
3，rpy偏移量单位为弧度
4，link中坐标及旋转设置以地面为坐标系，joint中中坐标及旋转设置以parent link为坐标系
##### xacro语法及其注意事项
1，可以定义材料进行宏定义和函数空间定义（在对应的空间直接进行定义），也可以定义常量进行复用xacro:property
2，xacro可以进行函数式子编程，以便重复利用代码（xacro:macro name= param=）
3，xacro不适用与check_urdf进行语法检查，目前只能通过运行来检查
4，如果机器人有多个部件，可以在不同xacro文件中进行编写，最后用一个xacro将多个文件绑定，xacro:include，对于这几个xacro文件可以不用相互include就可以调用互相自己的宏变量和宏定义。

##### Rviz注意事项
在可视化窗口配置完通道和相关设置后，建议保存当前配置，并将其保存到相关launch文件中，以免每次都要重新配置

##### Gazebo注意事项
1，如果有joint则link的<material>属性要放到joint之后才会生效
2，惯性矩阵算法设置的是inertialshuxing
3，改写的外观<collision>和惯性要放到<link>中


#### 错误记录
* 颜色设置没有显示
查看报错no transform from map to base_link，在global option中将map改为base_link。



#### 定位
导航的前提，通过计算到当前点的位置（相对参考点，一般为起始点）。
* 两种定位方式 里程计定位和传感器定位
![avatar](G:\HelpDocs\ROS\pics\两种定位.png)
*有点糊建议看原图
##### 里程计定位
里程计定位类似通过查找日志文件来计算位置
优点：连续，无跳变
缺点：累计误差
##### 传感器定位
通过传感器，查找自身与标志点的位置，因为标志点是提前在地图上标注了的，所以能够结合地图计算出位置（一般而言标志点越多越准确）。
优点：精准
缺点：容易跳变，有误差（不稳定）
** 所以一般使用两者结合起来一起使用

#### 地图
##### slam建图
1，slam建图最终结果，白色为可通信区域，黑色为障碍区域，蓝灰为未知区域。

#####代价地图
代价地图分为全局地图和本地地图，全局地图是针对整个环境建立的地图，而本地地图是针对当前机器人一定范围内的地图。(两种地图都可能由四层构成)
一般而言代价地图都有四层
![avator](G:\HelpDocs\ROS\pics\代价地图.png)
建议看原图
1，假死情况：机器无法进行移动，原因，全局膨胀空间和本地膨胀空间无空隙，无法通过。（最终决定机器人运动的是本地路径规划）
解决办法：将全局膨胀空间和代价系数设置大一些，本地膨胀空间和代价系数设置小一些，则当机器人进入全局膨胀空间，机器还未进入本地膨胀空间，可以通过。




## 报错
##### UnicodeEncodeError: 'ascii' codec can't encode characters in position 30-31: ordinal not in range(128)
编码问题导致关节结点和图形化控制结点无法使用
[参考](https://blog.csdn.net/qq_38313901/article/details/120263894)

##### 在机器人上加载仿真功能，如运动，摄像头，雷达，深度相机等
[官方文档](http://gazebosim.org/tutorials?tut=ros_gzplugins)
###### rviz报错记录RobotModel status error多个坐标为检测到
解决方法缺少关节结点发布
~~~xml
<!-- launch文件中只添加rviz结点-->
<node pkg="rviz" name="rviz" type="rviz" />

<!-- 增加下述部分-->
<node pkg="joint_state_publisher" name="joint_state_publisher" type="joint_state_publisher" />
<node pkg="robot_state_publisher" name="robot_state_publisher" type="robot_state_publisher" />
~~~

#### cartographer使用
https://www.bilibili.com/read/cv3103182
[创客制造](https://www.ncnynl.com/)


#### /cmd_vel运动控制命令
键盘控制 rosrun teleop_twist_keyboard teleop_twist_keyboard.py
规律运动 rostopic pub -r 10 /cmd_vel geometry_msgs/Twist '{linear: {x: 0.2, y: 0, z: 0}, angular: {x: 0, y: 0, z: 0.5}}'