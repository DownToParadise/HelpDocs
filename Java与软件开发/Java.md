* Java泛型编程
目前看来Java的泛型编程是与C++差不多的，只不过Java几乎所有都是基于，类，接口创建的泛型
另外统配符只能使用在声明泛型对象的地方，创建泛型类和接口时不能使用通配符<?>
[泛型的基本用法](https://www.cnblogs.com/wyb666/p/10349178.html)
[泛型编程概述](https://blog.csdn.net/qq_43450557/article/details/108077875)

* Java接口和继承的使用，以及两者的区别
[接口与继承的区别](https://blog.csdn.net/weixin_42126399/article/details/114280103)

* 反射机制
1，类名.class
2，通过invoke调用方法和属性
3，Java动态代理

* 多线程示例编写

* 类名.class返回什么
通过Class可以完整地得到一个类中的完整结构
获取一个类的对象，如int.class[类名.class的理解](https://www.cnblogs.com/quenvpengyou/p/12879522.html)

*  	继承抽象类和实现接口，需要重写抽象类和接口中的方法，抽象类不能实例化对象只能继承，接口中只可以声明全局变量。（接口用于补充Java不能实现多重继承）
*  	Java序列化
使Java对象能够序列化成字节对象，并在网络中传输（网络中传输的对象要求必须是字节序列，这样不管用什么样的语言或者系统，只要进行反序列化都可以得到相应的数据），Java发主要通过类私实现接口Serializable和Externalizable（一般用后者）
[Java序列化](https://www.cnblogs.com/9dragon/p/10901448.html)

