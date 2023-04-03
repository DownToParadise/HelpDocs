## Hadoop注意事项
### Linux配置

### 密码
*用户分为root用户和普通用户，前者为管态*
* root密码（hadoop100）
qwer159
* 用户密码（ccyeung）
qwer159

### 网络配置
*这里我们需要将Hadoop100虚拟机，设置成我们的服务器，所以需要固定其IP地址*
![test](G:\HelpDocs\hadoop\ip配置.jpg)

1，配置虚拟机网络

2，配置电脑上window10的vmnet8的网络
*这儿我们配置的是整个虚拟机集群子网的网关*

3，配置虚拟机上的网络
*我们这儿配置的都是服务器的网络，所以只要配置成同样的值，为了后期更改方便可以设置一个hadoop100网络的全局变量*

** 使用Xshell如果连接不上虚拟机，考虑重启windows10上的VMnet8网络连接，真搞人**
*参考https://blog.csdn.net/weixin_44080445/article/details/110714332*

* hadoop中的所有集群的配置文件应该相同，在配置文件中规定好NN，2NN，RM等

	*只要是hadoop命令开头，一般都是针对于集群的操作*
* hadoop fs -put 本地文件地址 hadoop集群地址 	#将本地文件上传至hadoop集群 
* hadoop fs -get hadoop集群地址 本地文件地址	#将hadoop集群文件下载到本地

* 目前Hadoop课程有点像计算机网络，代码量很少，大部分是理论

### Hadoop通信网络

* HDFS内部通信网址：hdfs://hadoop102:9000
* Hadoop web端网址：http://hadoop102:9870
* Hadoop 历史服务器web端地址：http://hadoop102:19888


### Hadoop MapReduce自定义逻辑处（按照处理逻辑顺序）
* 0，**数据结构**能够自定义，需要满足序列化，还需要能够写Writeable，如果要作为key必须实现ComparebleWriteable接口，和ToString方法
* 1，**切片**，先对数据进行切片，可以自定义逻辑处理切片，每个文件执行一次切片，对于小文件而言我们可以统筹聚合，决定mapTaskNum
* 2，mapper阶段读入数据格式可以自定义逻辑，**InputFormat**，也可以对应
* 3，**mapper**可自定义逻辑
* 4，**Sort**排序法则也可以自定义逻辑，默认字典排序，使用快排，主要更改数据结构的CompareTo方法
* 5，分区法则**Partition**也可以自定义，分区大小决定reduceTaskNum
* 6，map之后，reduce之前，**combiner**结构可以自定义逻辑（可有可无），用于聚合单个结点的数据以减小网络传输量。
* 7，**reduce**自定义逻辑
* 8，文件格式**OutputFormat**可自定义逻辑
* 源码中一般使用XXthread方法初始化的，为线程，应该看起相关的run()方法，所以本质上mapper和reducer是线程