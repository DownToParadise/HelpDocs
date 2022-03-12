* ### plt中有两种方式画子图
* 一种是使用plt.subplots()
``` python
fig, ax = plt.subplots(2, 3)
# 控制图片显示大小
plt.figure(figsize=(80,80))
# 让显示更加的平滑
fig.tight_layout()

ax[0][0].set_title("256 grays")
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
fig.savefig("lena.jpg")
```
*其中使用fig可以对plt生成的图进行操作，fig.set_title(), fig.savefig()等与plt.的操作大部分相同，但是名字有时候不相同这需要注意。
另外plt显示图像不会按照原图像显示，而是适配当前参数等

* 另外一种是使用
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
# ax.tight_layout()
ax.show()
```