* kill -9 3030 杀死进程3030

* chown 更改文件权限

* tar 解压/压缩文件，jar包许多只需要解压后添加环境变量就行，不需要进行“安装”[tar参考](https://blog.csdn.net/Dreamboy_w/article/details/106118118?utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-1.no_search_link&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-1.no_search_link"tar参数参考")

* systemctl centoslinux更改文件权限

* 给用户添加root权限后，要修改系统文件必须在root账户或者在命令前加root

* su root进入root账户

* windows, pycharm命令行用ctrl+c强制结束进程，linux用ctrl+z强制结束进程

* LInux用ctrl+L进行清屏，应该不叫清屏，应该叫做翻页

* shell语言中直接输入一串英文，则表示一个字符串或者是变量名，在变量名前加上$才表示取该变量的值。

* a在linux中的操作是分级的，在root用户和普通用户的配置就不一样，比如在配置ssh免密登录时，root用户和普通用户配置的免密是相对应的，是两个东西

* “ | ”管道命令，可以满足一条命令执行多个操作，并将上一个操作的标准输入，作为下一个命令的标准输入

* 显示cpu和内存占用率   [参考文档](https://blog.csdn.net/weixin_37669089/article/details/85255085)

* **locate**
  查找本地文件库的文件（类似find name），使用前建议先执行sudo updatedb更新本地数据库。如
  locate Pingolin

* **ldconfig**
  每当新安装了一个动态连接库，就要执行一“sudo ldconfig”或者重启虚拟机，不然无法找到对应文件
  [参考链接](https://www.cnblogs.com/my-show-time/p/15250435.html)

* **cat与vim的区别**
  vim相当于一个文本编辑器
  而cat只具有查看文件内容的功能，但是额外的cat具有一定的文件级的操作
  [cat与vim参数参考](https://blog.csdn.net/tanga842428/article/details/52156870"cat与vim参数参考")
  *如果只是查看文件推荐使用cat，修改文本文件内容使用vim*

* **source命令**
  刷新当前的shell环境
  在当前环境使用source执行Shell脚本
  从脚本中导入环境中一个Shell函数
  从另一个Shell脚本中读取变量

* **su命令**
  *switch user用于变更当前用户*
  su    root                     #切换到root用户
  su    XX普通用户名   #切换到普通用户XX

* **ps命令**
  *process status*
  查看当前所有进程状态

* **jps命令**
  *java process status*
  显示当前Java进程名及进程号
  jps  -l显示Java进程的完全路径

* **systemctl**
  用于操作系统程序服务，如防火墙，网络等
  systemctl status xxx    #查看系统程序状态
  systemctl start xxx      #开启系统程序
  systemctl is-enabled xxx #将系统程序设置为开机自启

* **grep命令**
  用于查找文件或标准输入里符合条件的字符串

* ### **Linux中各类括号的用法**
  
    [linux各种符号参考](https://www.cnblogs.com/lidabo/p/4202787.html)
  
  #### 括号
  
    **{}**
  
    **$( )与反引号``等价**
    *主要用于在变量中执行命令*
  
  ```shell
  echo $(pwd)        #先执行pwd命令，然后输出pwd命令的结果
  pdir=$(cd -P $(dirname $file); pwd)
  # 1，获得filename的父目录名
  # 2，;表示连续指令，如同管道"|"一样，cd命令和pwd命令在同一个层级执行
  # 3，最后，将获得的值赋予pdir
  ```
  
    **[ ]**
    *主要是在条件判断是当做分割符使用*
  
  ```shell
  if [ $# -le 1];
  then
      程序
  else
      程序
  ```
  
    ** “$((运算式))”或“$[运算式]” **
  
  ```shell
  S=$[(2+3)*4]
  echo $S
  20
  ```
  
  #### 引号
  
    [参考](https://blog.csdn.net/haohaoxuexiyai/article/details/110914488)
  
  * 单引号
    其中的内容没有实际意义，都表示为字符串
  
  * 双引号
    如果内容中有命令、变量等，会先把变量、命令解析出结果，然后在返回最终内容来。
  
  * 无引号
    不会将含有空格的字符串视为一个整体输出, 如果内容中有命令、变量等，会先把变量、命令      解析出结果，然后在输出最终内容来，如果字符串中带有空格等特殊字符，则不能完整的输出，需要改加双引号，一般连续的字符串，数字，路径等可以用。
  
  * 反引号
    反引号会解析命令，变量等，但是它只对命令响应，
    
    ```shell
    [ccyeung@hadoop103 hadoop-3.1.3]$ `this is $boy`
    bash: this: 未找到命令...
    [ccyeung@hadoop103 hadoop-3.1.3]$ "this is $boy"
    bash: this is pwd: 未找到命令...
    ```

##### 2022/2/10 linux虚拟机无法联网

描述：linux虚拟机无法联网，ifconfig命令无法查找到对应的ip地址，只有本地虚拟机回环
解决方案：

* 应该是将vituralware的服务关闭了，进入Windows菜单，查找服务，找到vitrual的哪几项服务都将其打开。尝试ping，如不行，再进入网络配置中开启当前连接Internet的网络的共享设置，设置为允许共享，网络设置为以太网（包括VMNet1，VMNet8），再尝试ping。
  [参考连接](https://www.xinyueseo.com/linux/270.html)
* 如果上述步骤都没有问题则尝试使用 sudo dhclient ens33 和 sudo sudo ifconfig ens33
  [参考连接](https://blog.csdn.net/weixin_42116341/article/details/81410805)

##### profile 与 barshc的区别

/etc/profile系统环境变量 ~./barshc用户环境变量，两种都可以配置环境变量但影响的范围不同，配置完后都学要source一下[参考链接](https://blog.csdn.net/zou_albert/article/details/112368264)

#### Linux 中【./】和【/】和【.】之间有什么区别

[Linux 中【./】和【/】和【.】之间有什么区别？ - mhq_martin - 博客园 (cnblogs.com)](https://www.cnblogs.com/mhq-martin/p/11523260.html)
./上级目录
../父级目录
/根目录

#### VMWare Ubuntu虚拟机扩容

[参考文档--安装gparted依赖](https://blog.csdn.net/ldzm_edu/article/details/78893721)

输入w
    ifw>=20kg

### 云服务器

使用云服务器一般不能切换到root用户，所以安装包需要使用手动安装
[非root用户安装包](https://blog.csdn.net/qq_41314786/article/details/114273847)

* 添加动态链接库后，某些三方软件才能引用

### Screen 任务托管工具

在远程服务器运行任务时，因为异常原因导致终端关闭或出错，可以使用Screen工具让任务在后台也可以运行