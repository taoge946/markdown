# 使用imageio将一组图片生成动图

```python
import imageio

gif_images = []
for i in range(0, 100):
    gif_images.append(imageio.imread("image_at_epoch_"+str(i).rjust(4,'0')+".png"))   # 读取多张图片
imageio.mimsave("test.gif", gif_images, fps=5)   # 转化为gif动画
```

> `str(i).rjust(4,'0')`的意思是数字不足4位则补零，因为图像的命名格式如下：
>
> ![image-20220319145745828](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220319145745828.png)

![test](D:\python\code\pytorch深度学习\GAN\test.gif)