![avater](G:\HelpDocs\opencv\现实坐标与opencv中的坐标.png)
**生活中图片的读法是width*height，而读入的图片是以height*width，以方便numpy数组处理，两者的坐标轴是刚好镜像的，我们不需要特殊处理，因为cv2.imread()和cv2.imshow()会帮我们处理好，我们只需要知道有这一会事，避免混淆或弄巧成拙**

*numpy和tf中的array，和cv2的size是相反的，即图像的列为a，行b，cv2中的图像size为axb，而numpy中bxa。

### 注意事项

* HSV格式经常用来图像增强
* YcrCb格式经常由于压缩图片，利于图像传输
* opencv默认读取图片格式为BGR
* matplotlib默认图像显示格式为RGB，注意两个的转换
* 图像旋转使用了仿射变换
* 图像增强：增强对比度（图像均衡）
* 图像均衡化的本质是将像素的变化范围增大，得到整个范围的图像
* img.canny边缘检测算子，两个threshold需要针对不同的图像和任务进行不同的调整
* [waitkey(0与waitkey(1)的差异](https://www.coder.work/article/2024795)，说明waitkey(n)中的n代表了刷新帧率，如果为0则一直是静止的图片，为其他则是等待一定时间（所以这个地方要设置循环），waitkey返回键盘输入的八进制数所以有常用判断语句
  
  ```python
    if cv2.waitkey(1) == ord("q"):
    break
  ```
