### jupyter

#### 打开jupyter notebook

* 方法一
  进入anconda promot控制台，将工作目录移到你想要的目录下，输入jupyter notebook，进入浏览器输入localhost::8888（一般是）

* 使用plt画图时Jupyter notebook出现“内核似乎挂掉“问题
  
  ```python
  # 添加代码
  import os
  os.environ["KMP_DUPLICATE_LIB_OK"] = "True"
  ```

#### 关于transforms.ToTensor()中的神奇操作

```python
# 函数中有一句，这个将H*W*C转化为C*H*W，
pic = torch.from_numpy(img.transpose((2, 0, 1)))
# 如果此时将img显示出来，将会得到九张不同亮度的灰图，[0, 255]会被div(255)，被归一化[0,1.0]
# 虽然transpose后的数据没有改变，但是reshpae具体数据与原图相比位置已经发生了改变，这也可能显示灰图的原因
# 认真思考，这里其实对网络提取信息的影响不大，它不显示原图，可能只是人的惯性思维罢了，这也可能是人不能从图片中捕捉到信息的表现形式之一
# 这里涉及到array.reshape的不同处理方式
# 与王讨论了一下，认为数据没有改变只是将RGB的数值在经过reshape轴变换后以同一个维度显示出来了而已，因为RGB中任何一个通道都可以表示原有的图片（只是为灰度图片）
plt.imshow(pic.reshape((H, W, C))

# 如果要显示原图，应该再次进行相同的transpose
plt.imshow(img.transpose((2, 0, 1)).transpose((1, 2, 0)))
```

#### 自动广播机制

  torch中的数据处理部分是模仿numpy产生的。
  其自动广播

#### torch中的乘法

* 广播机制（默认操作）
  由于torch中的广播机制，不同形状的张量可以进行加或者乘，~~先扩展参与运算的张量为相同形状在对应相加或相乘~~（见自动广播机制），A * B默认为元素对应相乘（哈达玛乘法）

* 点积
  形状相同的向量（一维张量）进行乘积，如torch.dot(a, b)

* 矩阵乘法
  满足一定形状要求的张量进行乘积，如torch.mm(A, B)

#### torch中常用的tensor方法

* torch.sum/.mean/...
  这些方法都可以通过指定维度计算想要维度的和值、均值等，其中有keepdims=bool参数计算完后保持原来矩阵的大小，有助于在我们后续使用计算结果进行操作，如果tensor为二维，则dim=0则为行，dim=1则为列。默认一维向量为行向量(nx1)
* a.numel()或a.nelement()
  返回张量的元素总数
* tensor与varizble
  新版pytorch中variable已被tensor合并，即只要是tensor数据就是variable数据，就可以autograd
  [参考链接]( https://www.bilibili.com/read/cv10086776/)

#### 数据获取

* a.detach()
  将数据从计算图中剥离，返回同样数值的数据，requires_grad=False，一般用作他用的数据先要detach操作
* a.numpy()/torch.from_numpy(b)/a.tolist()/a.item()
  tensor转ndarray/ndarray转tensor/tensor转list/获取item中的值
* _ 操作符
  原地操作符，如add_()，resize_()等，这些操作被执行时，本身的tensor也会改变

#### 数据打包与封装（TensorDataset与DataLoader）

[参考链接](https://blog.csdn.net/anshiquanshu/article/details/109398797)

* TensorDataset
  相当于zip作用，可以将X与Y数据进行封装

* ImageFolder
  作用类似TensorDataset，可以读取文件夹内的图片，并按照文件夹作为标签。

```python
img_data = ImageFolder(root="xxx/data", transform..)
# img_data[0][0]可以查看相应图片
```

* 自定义Dataset类
  可以将自己数据处理封装为类，并添加transform处理，**需要重写__getitem(self, id)__和__len__()函数**

* DataLoader
  在TensorDataset的基础上进一步进行打包，能够对数据进行shuffle和for循环批处理

* enumuerate
  使用python自带函数enumerate，进一步将数据封装如：for i, (x, y) in enumerate(data)。

* 如何解决当torchviosion无法下载数据集时[参考链接](https://blog.csdn.net/weixin_44042453/article/details/126065631)
  通过本地下载数据集，让后将下载的压缩包（不要解压）翻入(你的数据集目录)/数据集名/raw下，记住一定要与下载时pytorch显示的文件目录，否则无法通过dataset类导入数据。（当然对于我们自己的数据可以模仿官方数据集的样式编写自己的数据类Dataset）

#### pytorch使用gpu训练

**使用GPU训练要将三个数据转到gpu上**

```python
# 这句代码的等级相当于引入一个包
device = "cuda" if torch.cuda.is_available() else "cpu"
# 设置全局使用哪一个GPU
# 终端运行，官方建议
CUDA_VISIBLE_DEVICE=2 python trian3.py
# 在代码中添加
torch.cuda.set_device(1)
```

* 所有数据集
  [参考链接](https://blog.csdn.net/weixin_45468845/article/details/122971688)
  *注：其中torch.device+tensor.to可以直接改成tensor.to("cuda:0")*
* 网络参数
  一般在网络定义完后加一句代码net.to(device)
* 损失函数
  在定义往后进一步加如device方法

#### pytoch构建网络模型

* nn.Sequential()
  可以快速构建网络，返回网络的实例化对象

* class xx(nn.Moudule)
  **需要继承nn.Module类，还需要实现forward函数**
  定义类模型（具体使用还需实例化对象），可以用于自定义网络层（作为一个部件来构建更复杂的网络），也可以用于构建模型（嵌套构建），但必须实现forward方法和继承nn.Moudle
  为了更加简洁，也可以在类中添加其他方法，如loss，train等

* nn.functional
  其中定义了许多不可自动学习参数的网络层如方法，如激活函数、BN层等

* nn.Dropout
  只能对于上一网络层进行dropout，要对整个网络结构进行dropout还需设计玩网络结构。丢弃概率 p 为超参数，输入单元一般为0.2，隐层单元一般为0.5

* nn.Batchnoraml(k)稳定的加速学习方法
  在深度网络中，随着层数加深，数据分布也不断变化，所以我们除了给输入数据batchnormal之外，还需要给每一层的输出数据进行batchnorm以归一化“量纲”（k为上一个网络层的输出大小），就目前看来batchnormal加在非线性优化（激活函数）之前（前or后？前✔）
  BatchNormal2d(k)为上一个层次的输出滤波器个数
  BN允许更大的学习率

* 尝试其他归一化操作如层归一化等
  Weight Normalization

* 白化操作
  均值方差操作
  
  #### 加载预训练模型

* torchvison.models
  其中有许多模型的参数定义，可以直接获取。其中可以通过vgg.features卷积部分，vgg.classifier分类（线性）部分
  
  ```python
  from torchvision import models
  vgg = models.vgg16()
  vgg_pre = models.vgg16(pretrained=True) # 获取官方预训练参数
  # 加装本地参数
  state_dict = torch.load("your train model path",# 生成参数字典
                          map_location='cpu')     # 只接受在cpu训练的模型参数
  # 这样写是为了对号入座
  vgg.load_state_dict({k:v for k, v in state_dict_items() if k in vgg.state_dict()}]
  # 保存模型
  torch.save({
      'model':mymodel.state_dict(),    # 存放模型参数
      'optimizer':myoptim.state_dict()}# 存放模型超参数
      'path',
      pickle_protocol=4)               # 该设置可以对大型对象有效保存
  
  # 将参数移到cpu后保存
  net.cpu()
  params = net.state_dict()
  torch.save(params, 'path', pickle_protocol=4)
  ```

#### transform使用（用于数据增强，数据预处理等）

*不同的数据增强可以查找相关论文*
训练部分不显著，泛化能力提升

## 理论部分

#### 空洞卷积

空洞卷积是为了图像分割，在保留特征图尺寸不变的情况还可以增加感受野大小（原来是通过池化加上采样）
默认卷积的dilation rate 默认为1，空洞卷积应该dilation rate=2开始，等效卷积核$k'$计算公式为：($k$空洞卷积核大小，$d$为dilation rate)

$$
k'=k+(k-1)*(d-1)
$$
