| Name | UserName  | Password | Ros |
| ---- | --------- | -------- | --- |
| amg  | learningx | 123456   | Yes |

**wifiName：301小车 password：301301301 管理网站：miwifi.com

### ros可视化工具

* rqt，总的可视化窗口，可以显示其他rqt工具，并进行管理。

* rqt_graph，可视化显示结点通信，以qt开头的基本上都是可视化的工具

* rqt_plot，数据绘图工具，可以监控选择的topic（通道）数据变化

* rqt_reconfig，动态调参工具

* rqt_tftree

### ros命令行工具

* rosparam用于命令行更改参数

* rostopic
  查看ros中的话题，通过rostopic pub可以向具体话题发布指令

* rosnode
  用来显示所有结点相关结点信息，rosnode info也可以查看具体结点的信息

* rosparam用于命令行更改参数
  
  *具体运行命令可以在网上查一下，还有很多神奇的插件，建议自行探索

```txt
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

11，所有ros结点都需要向rosmaster注册，所以bringup关闭后，其他终端必须重启。

```

