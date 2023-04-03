
* 报错：cannot convert 'int (*)[n]‘ to int ** ，数组大小为(row, cols)<=>(x, y)
	定义二维数组，无法由函数形参接受。
	将二维素组传参时进行强制转换，int ** 或者将形参直接改成int * 二维数组也强制转换为
	int *(函数中使用*(arr+x*col+y)取到点(x,y)的值
	[参考链接](https://www.cnblogs.com/cygalaxy/p/6963789.html)

* 经验：函数如果要返回float，则必须在函数声明上定义返回值为float，如果不定义，在函数内部如何尽心强制转换都无用。

* #include<bis/stdc++.h>是一个包含大部分C++常用头文件的头文件
[参考链接](https://blog.csdn.net/prime_lee/article/details/80489284)

* isalnum函数判断字符变量c是否为数字或字母，是返回1，否0

* 使用unique函数进行去重
[参考链接](https://www.cnblogs.com/hua-dong/p/7943983.html)
~~~C++
#include<iostream>
#include<algorithm>
#include<functional>
using namespace std;
int main()
{
	int i;
	int a[10]={0,1,3,3,4,5,8,8,9,0};
	sort(a,a+10,less<int>());//按从小到大的顺序，自定义cmp函数，为真不交换，为假交换
	int n=unique(a,a+10)-a;
	for(int i=0;i<n;i++){
		cout<<a[i]<<" ";
	}
 } 

~~~

* sort函数使用
[参考链接](https://blog.csdn.net/qq_40088702/article/details/89285173)
* 查找最大最小值和下标
[参考链接](https://blog.csdn.net/qq_41508747/article/details/90640948)


### 刷题
**直接上github上搜索leetcode，找几个star最多的**
[labuladong算法小抄](https://labuladong.gitee.io/algo/)
https://github.com/halfrost/LeetCode-Go
https://github.com/changgyhub/leetcode_101

* [pair数据结构](https://www.cnblogs.com/jaszzz/p/12687678.html)

