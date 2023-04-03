### python画图和数据处理

* matplotlib.pyplot 
* snsborn，plt于sns配合使用功能十分强大
* pyechar，这个能够做许多动态图和特殊的静态图，这些图都比较特殊
  *可以绘制玫瑰图，桑基图，动态排名图，高级折线图等*
* networkx可以用于处理许多图数据，生成或加载图数据

### 数据处理

* cv2，能够进行一些图像处理，与plt配合使用
* pandas，二维数组，支持数据库操作，有大量的api

### 调试包

* pdb
  
  ```python
  import pdb
  pdb.set_trace() #通过这种方式加入断点
  ```
  
 ### plt中有两种方式画子图

* 一种是使用plt.subplots()
  
  ```python
  fig, ax = plt.subplots(2, 3)# subplots返回画图板和子图集合
  
  # 控制图片显示大小
  plt.figure(figsize=(80,80))
  
  ax[0][0].set_title("256 grays") # ax[0, 0]等价
  ax[0][0].imshow(grey_image, cmap="gray")
  ax[0][1].set_title("64 grays")
  ax[0][1].imshow(grey_image_64, cmap="gray")
  ax[0][2].set_title("16 grays")
  ax[0][2].imshow(grey_image_16, cmap="gray")
  ax[1][0].set_title("8 grays")
  ax[1][0].imshow(grey_image_8, cmap="gray")
  ax[1][1].set_title("4 grays")
  ax[1][1].imshow(grey_image_4, cmap="gray")
  ax[1][2].set_title("2 grays")
  ax[1][2].imshow(grey_image_bin, cmap="gray")
  
  # 解决子图坐标重叠等紧凑问题，让画图板更加平滑
  fig.tight_layout()
  
  # 所有子图共享标题
  fig.suptitle("xx")
  
  # 保存图片
  fig.savefig("lena.jpg")
  ```
  
  *其中使用fig可以对plt生成的图进行操作，fig.set_title(), fig.savefig()等与plt.的操作大部分相同，但是名字有时候不相同这需要注意。
  另外plt显示图像不会按照原图像显示，而是适配当前参数等*

* 另外一种是使用（一般是subplot比较方便）
  
  ```python
  ax = plt.figure()
  plt.figure(figsize=(10,10))
  plt.subplot(231)
  plt.title("origin img")
  plt.imshow(img[:, :, ::-1])
  plt.subplot(232)
  plt.imshow(img_gray, cmap="gray")
  plt.title("gray img")
  plt.subplot(233)
  plt.imshow(img_binary_1, cmap="gray")
  plt.title("threshold mean")
  plt.subplot(234)
  plt.imshow(img_binary_2, cmap="gray")
  plt.title("threshold otsu大律")
  plt.subplot(235)
  plt.imshow(img_binary_3, cmap="gray")
  plt.title("threshold Adaptive")
  
  plt.subplot(236)
  plt.imshow(img_binary_4, cmap="gray")
  plt.title("threshold Niblack")
  ```
  
  #### jupyter notebook中显示视频
  
  ```python
  from PIL import Image
  from IPython.display import clear_output, display, HTML
  import matplotlib.pyplot as plt
  import os
  import cv2
  import time
  path = "data/test.mp4"
  def show_video(video_path:str,small:int=1):
    if not os.path.exists(video_path):
        print("视频文件不存在")
  
    video = cv2.VideoCapture(video_path)
    current_time = 0
    while(True):
        try:
            clear_output(wait=True)
            ret, frame = video.read()
            if not ret:
                break
            lines, columns, _ = frame.shape
            # 计算帧率
            if current_time == 0:
                current_time = time.time()
            else:
                last_time = current_time
                current_time = time.time()
                fps = 1. / (current_time - last_time)
                text = "FPS: %d" % int(fps)
                cv2.putText(frame, text , (0,100), cv2.FONT_HERSHEY_TRIPLEX, 0.65, (255, 0, 0), 2)
  
            # 处理图像
            frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
            frame = cv2.resize(frame, (int(columns / small), int(lines / small)))
  
            img = Image.fromarray(frame)
            display(img)
  
            # 控制帧率
            time.sleep(0.001)
        except KeyboardInterrupt:
            video.release()
  show_video(path)
  ```
  
  https://blog.csdn.net/weixin_39560604/article/details/110556580