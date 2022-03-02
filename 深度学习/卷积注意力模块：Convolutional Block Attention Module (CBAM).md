# 卷积注意力模块：**Convolutional Block Attention Module (CBAM)**

- 给定中间特征图，BAM按顺序推导出沿通道和空间两个独立维度的注意力图，然后将注意图相乘到输入特征图进行自适应特征细化。
- CBAM可以无缝集成到任何CNN架构中，开销可以忽略不计，并且可以与基础CNN一起进行端到端训练。
- ==目的：==增强特征的表达，关注重要特征并抑制不重要特征。

# 1.CBAM一般性结构



![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFkRVRaUjZmR3d4RDZwYXA5WmNmelVndnlyVkNlNDlTQWswc3ZyeUdXQjcyNkh5ZDFJdXJzeXcvNjQw?x-oss-process=image/format,png)

CBAM依次推断出一个==1D的通道注意图Mc==，尺寸为Cx1x1，和一个==2D的空间注意力图Ms==，尺寸为1xHxW。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFzVVBGMDlvcnRMVXdPOEllVFBuVTkyZFNuUFhITmxxU21qNnZVZmV1enhBREtNb2pNZm5nU0EvNjQw?x-oss-process=image/format,png)

其中 ==⨂ 表示元素乘法==，F’’是最终的细化输出。

（F是一开始输入的特征，F‘是经过通道注意力模块后的特征，F''是经过空间注意力模块后的特征，也就是最终的输出结果）

这两个模块可以以并行或顺序的方式放置。结果表明，**顺序排列的结果比并行排列的结果好**。对于排列的顺序，实验结果表明，通道在前面略优于空间在前面。下面是一个ResBlock中CBAM的例子：

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDE3d1BURGRnbG83MlZXZTh5djFrU2lhaEc4SkhWUlU0N2UyREVmUktwZTlkaWIzaWNINkN5bWhQdXcvNjQw?x-oss-process=image/format,png)

# 2.通道注意力模块

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFEV2liUjlxU0ZLUE5yNFNmWXBsTzZIYXZocHdzamRLZGo4M2hUcUJSSnhlQWI3ZzVZYU1VRkRnLzY0MA?x-oss-process=image/format,png)

通道注意力模块

**通道注意力聚焦在“什么”是有意义的输入图像**，为了有效计算通道注意力，需要对输入特征图的空间维度进行压缩，对于空间信息的聚合，常用的方法是**平均池化**。但有人认为，**最大池化**收集了另一个重要线索，关于独特的物体特征，可以推断更细的通道上的注意力。因此，平均池化和最大池化的特征是同时使用的。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFIaEtXWWhzQzJ2YWxYWW9Za1JyaWF6cTdMUk5jYTZBVUV5ZlJodTBFVnJublVSOFZ6bzFPYm9RLzY0MA?x-oss-process=image/format,png)

**Fcavg**和**Fcmax**，分别表示**平均池化特征**和**最大池化特征**。然后，这两个描述符被转发到一个共享网络，以产生我们的==通道注意力图*Mc*==。==共享网络==由一个多层感知器(MLP)组成，其中有一个隐含层。为减少参数开销，隐藏层的激活大小设为*R*/*C*=*r*×1×1，其中*R*为下降率。将共享网络应用到每个描述符后，输出的特征向量使用element-wise求和进行合并。*σ*表示sigmoid函数。这个*Mc*(*F*)与*F*进行元素相乘得到*F’*.。

> 通道注意力系数的计算是从通道角度出发，压缩特征图的空间维度，将每一个通道看成一个特征检测器。

# 3.空间注意力模块

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFtNnRKcHNDSk9QekV5UEg5R1pZUmNOZU1BNzNFTjhKVTdwdEN0OHZrR2liZlhCQURlMU93U2ZnLzY0MA?x-oss-process=image/format,png)

空间注意力模块

**空间注意力聚焦在“哪里”是最具信息量的部分**，这是对通道注意力的补充。为了计算空间注意力，沿着通道轴应用平均池化和最大池操作，然后将它们连接起来生成一个有效的特征描述符。然后应用卷积层生成大小为*R*×*H*×*W* 的空间注意力图*Ms*(*F*)，该空间注意图编码了需要关注或压制的位置。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFWdmtLODNpYVFycE5YRXhaOXNVY1BTdDhvaWE0aDFFdlBwSHhkM1BhNXNpYkY3cjB0WXVLMjI3ZVEvNjQw?x-oss-process=image/format,png)

具体来说，使用两个pooling操作聚合成一个feature map的通道信息，生成两个2D图: **Fsavg**大小为1×*H*×*W*，**Fsmax**大小为1×*H*×*W*。*σ*表示sigmoid函数，**f7×7**表示一个滤波器大小为7×7的卷积运算。

> 空间注意力模块是从空间角度出发，压缩特征图的通道维数。

# 4. ImageNet上的消融研究

## 4.1. Max Pool 还是 Avg Pool

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDEzSlJqeDFETzBFMk5iUnJpYTU2Y2ljNnFRd1lPYUp3aWNVUmZDcjk5QVY2ZlhiRXNjbURvYjRWaWNBLzY0MA?x-oss-process=image/format,png)

对比不同的通道注意力模型

最大池化编码了最显著的部分，而平均池化编码了全局的统计信息。因此，这两个特征被同时使用，并对这些特征应用一个共享网络。在SENet中的SE部分使用CAM是一种进一步提升的有效的方法。

## 4.2. 空间和通道注意力

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFzQ21OSUtzQjd3TUZqTU5tWUFXRlg5Q29aaWExS3Vxand1NlVZU2h2QXBJOGlibHRSR29McWcwUS82NDA?x-oss-process=image/format,png)

对比不同的通道注意力方法

**通道池化产生更好的准确性**，表明显式建模的池化导致更好的注意力推断，而不是可学习的加权通道池化。在这两种情况下，采用更大的内核大小(k=7)可以产生更好的精度。这意味着需要一个开阔的视野(即大的感受野)来决定重要的空间区域。简单的说，我们使用了通道轴上卷积核大小为7的平均和最大池化特征作为我们的空间注意模块。

## 4.3. 通道和空间注意力的排列

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFLUm1QOVBQZkFFMVdyNU9Nc1dOVUNPRUNHYm9lcndLaWNVVm5WbjQ5dDB1anZxYTNKRnFIbjR3LzY0MA?x-oss-process=image/format,png)

从空间的角度来看，通道注意力是全局的，而空间注意力是局部的。研究发现，按顺序生成注意力图比并行生成注意力图更好。此外，通道在前面的性能略优于空间在前面。最终模块的top-1误差达到22.66%，大大低于SE。

# 5. SOTA对比

## 5.1. ImageNet

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFuOXZWZTBxcWZmUm1pYTZ3bkk2NkE0eWdVMzBHSmlhbXVKUlJEdG9Vdk1ieWFqYVZoUm1oQ1JKUS82NDA?x-oss-process=image/format,png)

在ImageNet-1K上的分类结果

ResNet，WideResNet，ResNeXt使用了CBAM后显著优于基线。这意味着CBAM是强大的，显示了新的池化方法的有效性，它产生更丰富的描述符和空间注意力图，有效地补充了通道注意力。CBAM不仅大大提高了基线的准确性，而且也很好的提高了SE的性能。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFTRjBrYmpkSXdjV3M4MHhhR2JmQmliZXQ0OVhiaEZFZzBUcjRFblVSTktQcVFKSmxSdkNvemlhQS82NDA?x-oss-process=image/format,png)

在ImageNet-1K上使用轻量网络MobileNet的分类结果

CBAM的总体开销在参数和计算方面都非常小。CBAM非常适合于轻量级网络MobileNetV1。以上改进显示了CBAM在低端设备上应用的巨大潜力。

## 5.2. 使用Grad-CAM进行网络可视化

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDE5QkxPS3VjSXJGTE5pY1ZrcjNyUWYxNk90VmZQOUtuZmZLa2lhNTJsWlNzWlhsakZmaWNyNGlibkx3LzY0MA?x-oss-process=image/format,png)

Grad-CAM可视化结果

Grad-CAM是最近提出的一种可视化方法，它使用梯度来计算卷积层中空间位置的重要性。Grad-CAM结果清晰地显示了网络关注的区域。我们可以清楚地看到集成了CBAM的网络的Grad-CAM mask对于目标区域的覆盖要比其他方法更好。

## 5.3. MS COCO Object Detection

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFqdTNQZGJlTFpUbENld0Y1TnFva0Q1Ynh6eTNmQmxiaWIybllRamdTdWVtUmNSRGYxNEo3bTZRLzY0MA?x-oss-process=image/format,png)

在MS COCO验证集上的物体检测mAP

我们的检测方法是Faster R-CNN，基线网络是ImageNet上预训练过的ResNet50和ResNet101，可以看到，较基线有显著改善，展示了CBAM在其他识别任务上的泛化性能。

## 5.4. VOC 2007 Object Detection

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9tbWJpei5xcGljLmNuL21tYml6X3BuZy9LWVNEVG1PVlp2b2VYOEV3YVFMemlhU0pEcVEwNDVteDFpYnU2blFKclhvR0EydHQ1TnJyRnMxZlRHWkJMU0dzY2JsaGljUmljdjdpY0NwSHdra0JpY21Id1Q4dy82NDA?x-oss-process=image/format,png)

PASCAL VOC 2007测试集

物体检测器为SSD和StairNet，我们可以清楚地看到，CBAM对两个骨干网络的所有基线的准确性都有提升。

CBAM精度的提高带来的参数开销可以忽略不计，这表明增强不是由于简单的容量增加，而是由于有效的特征细化。``