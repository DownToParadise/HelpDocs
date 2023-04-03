# 关于Dataframe的一些数据操作

> 本文只在转载他人文章的基础上，增加笔者自己的一些理解
> 主要涉及dataframe的基本操作，切片操作，条件筛选等

## 第一项：Dataframe的基础操作

*没啥好说的，欢迎补充*
[Dataframe的基础操作](https://jingyan.baidu.com/article/4b07be3c64483b48b280f35e.html)

## 第二项 Dataframe切片操作

*主要介绍了Dataframe的.iloc, .loc, at, iat等操作

[Dataframe切片操作（1）](https://jingyan.baidu.com/article/e52e3615a43c8940c70c515e.html)
[Dataframe切片操作（2）](https://jingyan.baidu.com/article/a17d52853f879e8099c8f240.html)

**肯定会用人问了那么iloc与loc，at与iat这些类之间有什么区别呢**
那就看这片吧[DataFrame之iloc与loc的一些容易被忽略的区别](https://blog.csdn.net/On_theway10/article/details/87166605)

可以看见这两者之间的区别主要是一个“**i**”的区别，就是index，loc的大部分操作是基于Dataframe中的元素，或者属性，而iloc主要是进行数字操作，前者就像字典的操作，后者就像数组的操作

## 第二项 Dataframe的条件筛选

[Dataframe的条件筛选（1）](https://jingyan.baidu.com/article/0eb457e508b6d303f0a90572.html)
[Dataframe的条件筛选（2）](https://www.cnblogs.com/silentteller/p/10871944.html)
我自己在补充一个例子

```python
    data.head()
       ones      Exam1      Exam2  Admitted
0   100  34.623660  78.024693         0
1   100  30.286711  43.894998         0
2   100  35.847409  72.902198         0
3   100  60.182599  86.308552         1
4   100  79.032736  75.344376         1

    data[data["Admitted"].isin([1])].head() #记住isin中的实参一定是列表哦~
        ones      Exam1      Exam2  Admitted
3    100  60.182599  86.308552         1
4    100  79.032736  75.344376         1
6    100  61.106665  96.511426         1
7    100  75.024746  46.554014         1
8    100  76.098787  87.420570         1
```

**认真观察就会发现，大部分的筛选操作都是在中括号内进行的，而大部分进行切片的操作都有额外的类或方法进行操作，即要进行打“.”**

*最后在给大家，增加两个例子吧*

```python
data.["Admitted"]
0     0
1     0
2     0
3     1
4     1
     ..
95    1
96    1
97    1
98    1
99    1
Name: Admitted, Length: 100, dtype: int64
data.Admitted
0     0
1     0
2     0
3     1
4     1
     ..
95    1
96    1
97    1
98    1
99    1
Name: Admitted, Length: 100, dtype: int64
```

> 