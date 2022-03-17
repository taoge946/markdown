# GAN

目录：

- 使用基本的gan来生成minst数据集
- DCGAN：一系列的训练和优化GAN的技巧，动漫人物的图像
- CGAN：给一个确定的条件生成一个确定类型的图像  texr_to_image 使用关键词生成图片
- info_gan: 无监督模式的条件GAN，可以通过非监督的方式获取特定特征的生成模型，生成图片
- SSGAN：半监督的学习生成对抗网络
- pix2pixGAN： 素描的自动上色，通过分割图生成真实街景
- cycle GAN：没有成对图片时的转换，将图像从一个域转换到另一个域中
- StarGAN：在cycleGAN的基础上实现了多个域的转换



## GAN的原理和公式

### GAN原理简介

不仅可以生成各类图像和声音，还启发和推动了各类半监督学习和无监督学习任务的发展

生成器就是要从真实的图像上学习图像的分布，从而让自身生成的图像更加真实，判别器就是需要打分，打分打到0.5左右就说明判别器判断不出来图像是生成的还是真实的

![image-20220307104809840](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220307104809840.png)

生成器的优化目标是使得判别器的打分为1，判别器的优化目标是使得生成器的样本评分为0，真实图片的样本被评分为1，根据评分的损失来分别优化生成器和判别器

GAN设计的关键就在于损失函数的处理，

判别器就是一个二分类问题，损失函数比较好定义

但对于生成器，因为一张图片用肉眼来看的话很好看出来是不是真的，但是要是用数学表达式来判断的话就很抽象，所以损失函数很难定义，难以用一个数学的公理来泛化的定义，所以将生成器的输出交给判别器去判断

### GAN算法流程

G是一个生成图片的网络，它接收一个随机的噪声z，通过这个噪声生成图片记作G(x)

D是一个判别网络，输入参数是x，x代表一张图片，输出D(x)代表为真实图片的概率，1为100%为真实0为不可能是真实。

能否正确区分生成的图片和真实的图片将作为判别器的损失，而能否生成近似真实的图片并是的判别器将生成的图片判断为真将作为生成器的损失。

> 注意，生成器的损失是通过判别器的输出来计算的，而判别器的损失是一个概率，可以通过交叉熵来计算

Goodfellow从理论证明了GAN算法的收敛性以及在模型收敛时生成数据具有和真实数据相同的分布，公式如下：

![image-20220307111416672](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220307111416672.png)

在这个公式中，x代表真实的图片x~P ~data~ (x)代表从真实图片的分布当中抽出一张图片

z代表噪声，随机输入一个噪声的分布（如正态分布等）中随机取出一个交给模型G(z)来生成一张图片，然后将生成的模型交给判别器D来调用D(*)表示D网络判断图片是否是真实的概率

公式的前半部分代表着生成器对于真实图片的判断，我们希望判别器对于真实图片输出**越大越好**，最好的结果是1，而log1是0，log0是负无穷，所以取一个对数更能方便计算，放大损失。E为期望

公式的后半部分，我们希望判别器对于通过噪声生成的图片打分为0，也就是`log(1-D(G(z))`**越大越好**

> 使用log的原因：
>
> 对数函数是单调递增函数
>
> 对数函数不改变数据之间的相对关系，使用log后可放大损失，便于计算和优化。

前面是对于判别器，对于**生成器**而言，希望`D(G(z))=1`，也就是希望`log(1-D(G(z)))`**越小越好**

可以看出G和D对于`log(1-D(G(z)))`的优化目标是相反的,这就体现出了对抗，所以最前面是min G 和max D 对于生成器我们希望这个公式的结果越小越好，对于判别器则是越大越好（maxV（D,G））。

> GAN 的应用：
>
> - 图像生成：生成一些假的数据，比如海报中的人脸
> - 图像增强：从分割图生成假的真实街景，可以不用上路就可以训练无人汽车（pix2pix）
> - 风格化和艺术的图像创造：风格装换，修补图像（如去马赛克）
> - 声音的转换：将一个人的声音转为另一个声音，去除噪音等

## 基础GAN

先导入基本的几个库

```python
import torch
import torch.nn as nn
import torch.nn.functional as F
import numpy as np
import matplotlib.pyplot as plt
import torchvision
from torchvision import transforms
```

直接加载minist数据集，然后对数据集进行归一化（-1~1）

> 在GAN当中推荐将数据归一到-1~1，
>
> 这与GAN的训练技巧有关，因为生成器最后使用tanh进行激活的效果特别好，tanh输出的结果就是在-1 ~1之间。这样可以使生成的结果和输入的结果在一个取值范围区间内。

```python
transform=transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5,) , (0.5,))#均值和方差设为0.5就是将取值范围从0~1放到了-1~1
    ###注！！！！！Normalize不能直接(0.5,0.5) 要改成上面那样，推测是torch版本导致的
])
```

我们要生成的时候不需要标签，只需要让它生成，将torch中自带的minist下下来放到dl里

```python
train_ds=torchvision.datasets.MNIST('data',train=True,transform=transform,download=True)
dataloader=torch.utils.data.DataLoader(train_ds,batch_size=64,shuffle=True)
```

### 定义生成器

生成器的输入是长度为100的噪声（正态分布随机数），输出是指定大小的图片（minist为1*28*28），可以通过linear层实现

```python
class Generator(nn.Module):
    def __init__(self):
        super(Generator,self).__init__()
        self.main=nn.Sequential( #使用sequntial来快速创建模型,直接按顺序写模型就行了
            nn.Linear(100,256),
            nn.ReLU(),
            nn.Linear(256,512),
            nn.ReLU(),
            nn.Linear(512,28*28),
            nn.Tanh()#根据经验，生成器一般使用tanh进行激活
        )
    def forward(self,x): #x表示长度为100的噪声输入
        img=self.main(x).view(-1,28,28)
        return img
```



### 定义判别器

判别器的输入为一张图片（1 28 28），输出为二分类的概率值，使用sigmoid进行激活(输出0~1之间的概率值)

损失函数使用二分类的损失函数BCELoss计算交叉熵损失

在判别器中一般使用leakyrelu进行激活，因为如果小于0没有梯度的话就非常的难训练，这也是一个训练技巧

```python
class Discriminator(nn.Module):
    def __init__(self):
        super (Discriminator,self).__init__()
        self.main=nn.Sequential( 
            nn.Linear(28*28,512),
            nn.LeakyReLU(),  #leakyrelu 会在负值的时候保留一定的梯度不像relu负值就是0
            nn.Linear(512,256),
            nn.LeakyReLU(),
            nn.Linear(256,1),
            nn.Sigmoid()#最后的输出结果为0~1之间的概率，所以使用Sigmoid进行激活
        )
    def forward(self,x):
        x=x.view(-1,28*28)
        x=self.main(x)
        return x
```

### 初始化模型，优化器以及计算损失函数

```python
device='cuda' if torch.cuda.is_available() else 'cpu'
gen=Generator().to(device)
dis=Discriminator().to(device) #初始化两个模型并且放到gpu上

d_optim=torch.optim.Adam(dis.parameters(),lr=0.0001)
g_optim=torch.optim.Adam(gen.parameters(),lr=0.0001)#定义判别器和生成器的优化器
loss_fn=torch.nn.BCELoss()#使用sigmoid激活的二分类模型损失函数使用BCEloss
```

### 绘图函数

将一个批次当中生成器生成的数据画成图像

```python
def gen_image_plot(model,test_input): #test_input：每次给一个固定的随机数，看它的变化
    pre=np.squeeze(model(test_input).detach().cpu().numpy())#squeeze去掉值为1的维度，再将生成的预测结果放到cpu上 detch是将梯度截断，会得到一个没有梯度的tensor
    fig=plt.figure(figsize=(4,4))
    for i in range(16):
        plt.subplot(4,4,i+1)
        plt.imshow((pre[i]+1)/2) #imshow绘图有两个要求，要么是0~1之间的float 要不是0~255的int 但是生成器租后使用了tanh激活函数结果为-1~1，得化成0~1
        plt.axis('off')
    plt.show()#这样绘图就直接画出来了16张图
    

test_input= torch.randn(16,100, device=device) #因为想要生成16张，每张是一个100的噪声 必须加device否则会报错
											#后面就使用这个确定的噪声放到生成器中看生成图像的质量的优化过程
```



### GAN的训练

```python
D_loss=[]
G_loss=[]#建立两个空列表来存损失
```

模型的训练就是找损失再反向传播，判别器的损失有两部分，分别是对于真实图片的损失和生成的虚假图片的损失，分别按照期望（真实的期望1和生成的期望0）进行反向传播优化。对于生成器损失就只有一个部分，就是期望判别器对于它生成的图片的评分为1

训练模型后将每一个epoch的损失记录下来，取一组固定的噪声来放到生成器模型中来每个epoch生成16张图片观察优化过程。

```python
#训练循环：
for epoch in range(200):
    d_epoch_loss=0
    g_epoch_loss=0
    count=len(dataloader) #a=len(dataloader)会返回batch数，b=len(dataset)会返回样本总数 （b=a*batch_size）

    for step, (img, _) in enumerate(dataloader):#需要epoch号和图像，不需要标签
        img=img.to(device)#先把数据放到GPU上
        size=img.size(0)#相当于batch_size，生成这么多个随机数正好和一个批次的图像向对应
        random_noise=torch.randn(size,100,device=device)
        
        #判别器的损失
        d_optim.zero_grad() #对于判别器而言损失有两个部分,真实图像的损失和生成图像的损失
        real_output=dis(img) #判别器输入真实的图片，得到对真实图片的预测结果，我们希望real_output为1
        d_real_loss=loss_fn(real_output,#因为我们对真实图片希望输出结果是1，所以计算它和全1的数组
                    torch.ones_like(real_output)) #torch.ones_like(a)是输出a的样式那么多个1，如a是5*5的数组，这个就输出5*5的1
        d_real_loss.backward()

        gen_img=gen(random_noise)
        fake_output=dis(gen_img.detach())#判别器输入生成的图片，因为这里也是对判别器的训练，所以使用detach将梯度截取不影响gen的训练，使梯度不再传送到gen的模型中了
        d_fake_loss=loss_fn(fake_output,torch.zeros_like(fake_output))
        d_fake_loss.backward()

        d_loss=d_real_loss+d_fake_loss
        d_optim.step()

        #生成器的损失
        g_optim.zero_grad()
        fake_output=dis(gen_img) #此时就不需要截断了，因为此时就需要梯度来训练优化GAN
        g_loss=loss_fn(fake_output,torch.ones_like(fake_output)) #对于生成器我们希望判别器判断的的结果为1,就是希望生成的图片被判断为真
        g_loss.backward()
        g_optim.step()

        with torch.no_grad():#将每个epoch中批次的的所有loss求和
            d_epoch_loss+=d_loss
            g_epoch_loss+=g_loss
    with torch.no_grad():  #求每个epoch的平均loss再放到列表中
        d_epoch_loss/=count
        g_epoch_loss/=count
        D_loss.append(d_epoch_loss)
        G_loss.append(g_epoch_loss)
        print('Epoch:',epoch)
        gen_image_plot(gen,test_input)#使用一个固定的噪声而不是每个epoch都变的噪声从而更明显的看出来优化变化的结果

```

结果从一开始的特别模糊![image-20220309164403755](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220309164403755.png)

到基本能看出来是什么

![image-20220309164449451](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220309164449451.png)

但是还是比较糊，因为这只是一个基础的GAN，虽然能生成图像不过生成图像的质量非常差，如果想要质量更好的图片，就会使用下一章当中的DCGAN

> 如果想画一个loss的图的话，需要先将loss数据从GPU中取回到cpu中，否则无法画图
>
> ```python
> dloss=torch.tensor(D_loss,device='cpu')
> gloss=torch.tensor(G_loss,device='cpu') #或者直接加一个.item()  d_epoch_loss+=d_loss.item()
> 
> plt.plot(range(1,201),dloss,label='D_loss')
> plt.plot(range(1,201),gloss,label='G_loss')
> plt.legend()
> plt.title('loss')
> ```
>
> ![image-20220309193324830](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220309193324830.png)



## DCGAN深度卷积生成对抗网络

（2016年）使用卷积层加入到了生成对抗网络的模型算法设计当中，替代了全连接层

这篇文章

- 展示了卷积层如何跟GAN一起使用，并为此提供了一系列架构指南
- 讨论了GAN特征的可视化
- 潜在空间差值
- 利用判别器特征来训练分类器，评估结果

后面的所有GAN都是在DCGAN的基础上演变过来的

它对卷积神经网络的结构做了一些改变，提高了样本的质量和收敛的速度，DCGAN极大的提升了原始GAN训练的稳定性以及生成结果质量



***DCGAN的创新改进之处：***

- 生成器和班别器都舍弃了CNN的池化层，判别器保留CNN的整体架构，使用跨度来缩小图像；生成器则是将卷积层替换成了反卷积层

- 在G和D中，都使用了BN层，有助于处理初始化不良导致的训练问题，可以将参数初始化（模型创建后初始随机化的参数）的问题降到最小加速模型训练，提升了训练的稳定性

  （在生成器的输出层和判别器的输入层不使用BN层 这也是一个训练技巧）

- 在生成器中除输出层使用tanh激活，其他全部使用relu激活函数

  在判别器中，除输出层（输出层使用sigmoid或是不激活）外所有层都使用leakyrelu，防止梯度稀疏

![image-20220309200656138](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220309200656138.png)

DCGAN的架构与GAN差不多，就是使用了卷积和反卷积

![image-20220309200829457](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220309200829457.png)

生成器就是将噪声先resize或是linear变得很细很长变成一张张的小图片再反卷积

***DCGAN设计技巧***

- 取消所有的pool层，使用反卷积等方式进行上采样（还可以使用差值等）和跨度(stride)防止梯度的稀疏

- 去掉了所有的FC层，使网络变成了全卷积网络

- G网络使用relu激活，随后一层使用tanh

- D网络中使用Leakyrelu进行激活

- G,D中都使用BN层解决初始化差的问题，帮助梯度传播到每一层，防止G把所有样本都收敛到同一个点（就比如想生成动漫人物图像，收敛到同一个点就是不管输入什么噪声都会收敛到同一个动漫形象上），提高生成图像的多样性

  但是如果将BN层用到所有层会导致样本震荡和模型不稳定，所以G输出和D输入不采用BN层

- 使用Adam优化器且beta1（一阶矩估计的指数衰减率）的值为0.5

- 论文参数： LeakRelu的斜率为0.2    learning rate=0.0002   batch_size是128 可以作为参考



### DCGAN生成minst数据集

前面数据的导入和之前的一样

输入100的噪声，DCGAN使用反卷积将其放大到一张图片，可以先使用一个linear层，可以先把它链接成如7* 7 * 256再reshpe成这么长的小图片，再一步一步反卷积到大图片

定义噪声

```python
#z=torch.randn(batchsize,100,1,1) #可以这么定义噪声，这样就是一个channel为100的1*1的噪声，就不用再s使用linear层和reshape了（在pytorch中第一个维度是c）
batchsize=64
z=torch.randn(batchsize,100)#这里为了更直观一点就加linear层了
```

#### 定义生成器模型：

```python
class Generator(nn.Module):
    def __init__(self):
        super(Generator,self).__init__()
        self.linear1=nn.Linear(100,256*7*7) #为什么选7*&因为两次反卷积之后就是minist的28*28了
        self.bn1=nn.BatchNorm1d(256*7*7)#因为此时是一维的所以用1d
        self.deconv1=nn.ConvTranspose2d(256,128, #我们要使通道数越来越小直到1（灰度图像）
                                kernel_size=(3,3),#卷积核一般都是3*3，也可以定义成其他的
                                stride=1,#7->28只需要反卷积两次，但是为了提高反卷积层的生成能力，可以把跨度设为1，不进行缩放，可以多加几层反卷积
                                padding=1)#要是不进行缩放的话卷积核为3就得进行1的填充
                                    #(128,7,7)
        self.bn2=nn.BatchNorm2d(128)
        self.deconv2=nn.ConvTranspose2d(128,64,kernel_size=(4,4),stride=2,padding=1) #为了使生成图片大小正好是14*14的，所以调整了一下卷积核
                                    #(64，14,14)
        self.bn2=nn.BatchNorm2d(64)
        self.deconv3=nn.ConvTranspose2d(64,1,kernel_size=(4,4),stride=2,padding=1) 
                                    #(1,28,28)

    def forward(self,x):
        x=F.relu(self.linear1(x))
        x=self.bn1(x)
        x=x.view(-1,256,7,7)
        x=F.relu(self.deconv1(x))
        x=self.bn2(x)
        x=F.relu(self.deconv2(x))
        x=self.bn3(x)
        x=torch.tanh(self.deconv3(x))
        return x



```

#### 一个用来看反卷积和卷积输出尺寸的小技巧

> 因为DCGAN中大量使用了卷积和反卷积的stride和padding，要是不确定输出的大小时多少可以把这一层提取出来给个随机输入看看，如
>
> ```python
> self.conv1=nn.Conv2d(1,64,3,stride=2)#想看这一层的输出大小
> 
> lay=nn.Conv2d(1,64,3,stride=2)#直接提出来
> inp=torch.randn(8,1,28,28) #随机一组输入 （8为batch size）
> out=lay(inp)
> out.size() #结果为8,64,13,13 所以需要padding为1才能正好缩小一倍
> 
> #测试反卷积层
> lay=nn.ConvTranspose2d(128,64,kernel_size=(4,4),stride=2,padding=1)
> inp=torch.randn(8,128,7,7)
> out=lay(inp)
> out.size() #结果为（8,64,14,14）正好扩大了一倍
> #输入大小为7*7，stride=2就变成了7+6=13,13*13
> ```

#### 判别器模型

```python
class Discriminator(nn.Module):
    def __init__(self):
        super(Discriminator,self).__init__()
        self.conv1=nn.Conv2d(1,64,3,stride=2) #判别器的输入不能有BN层
        self.conv2=nn.Conv2d(64,128,3,stride=2)
        self.bn=nn.BatchNorm2d(128)
        self.Fc=nn.Linear(128*6*6,1)
    def forward(self,x):
        x=F.dropout2d(F.leaky_relu(self.conv1(x)))#注意在判别器中使用leakyrelu进行激活  使用dropout层来使得判别器不会过强
        x=F.dropout2d(F.leaky_relu(self.conv2(x)))#现在的输出结果为(batch,128,6,6)
        x=self.bn(x)
        x=x.view(-1,128*6*6) #除了batch外将图片的数据展平
        x=torch.sigmoid(self.Fc(x))
        return x

```

#### 初始化和训练

和上面的普通GAN基本类似

```python
device='cuda' if torch.cuda.is_available() else 'cpu'
gen=Generator().to(device)
dis=Discriminator().to(device)
loss_fn=nn.BCELoss()
g_optim=torch.optim.Adam(gen.parameters(),lr=1e-4) #可以使生成器的学习速率大于判别器从而避免判别器过强
d_optim=torch.optim.Adam(dis.parameters(),lr=1e-5)

#绘图以及保存函数
def gen_and_save_img(model,epoch,test_input):
    pre=np.squeeze(model(test_input).cpu().numpy())
    fig=plt.figure(figsize=(4,4))
    for i in range(pre.shape(0)):
        plt.subplot(4,4,i+1)
        plt.imshow((pre[i]+1)/2,cmap='gray')
        plt.axis('off')
        plt.savefig('image_at_epoch_{:04d}.png'.format(epoch))
        plt.show()

#训练(在每一轮的损失当中加了.item()变成了float类型可以直接画图)
test_input=torch.randn(16,100,device=device)
D_loss=[]
G_loss=[]#建立两个空列表来存损失

for epoch in range(40):
    d_epoch_loss=0
    g_epoch_loss=0
    count=len(dataloader) #a=len(dataloader)会返回batch数，b=len(dataset)会返回样本总数 （b=a*batch_size）

    for step, (img, _) in enumerate(dataloader):#需要epoch号和图像，不需要标签
        img=img.to(device)#先把数据放到GPU上
        size=img.size(0)#相当于batch_size，生成这么多个随机数正好和一个批次的图像向对应
        random_noise=torch.randn(size,100,device=device)
        
        #判别器的损失
        d_optim.zero_grad() #对于判别器而言损失有两个部分,真实图像的损失和生成图像的损失
        real_output=dis(img) #判别器输入真实的图片，得到对真实图片的预测结果，我们希望real_output为1
        d_real_loss=loss_fn(real_output,#因为我们对真实图片希望输出结果是1，所以计算它和全1的数组
                    torch.ones_like(real_output)) #torch.ones_like(a)是输出a的样式那么多个1，如a是5*5的数组，这个就输出5*5的1
        d_real_loss.backward()

        gen_img=gen(random_noise)
        fake_output=dis(gen_img.detach())#判别器输入生成的图片，因为这里也是对判别器的训练，所以使用detach将梯度截取不影响gen的训练，使梯度不再传送到gen的模型中了
        d_fake_loss=loss_fn(fake_output,torch.zeros_like(fake_output))
        d_fake_loss.backward()

        d_loss=d_real_loss+d_fake_loss
        d_optim.step()

        #生成器的损失
        g_optim.zero_grad()
        fake_output=dis(gen_img) #此时就不需要截断了，因为此时就需要梯度来训练优化GAN
        g_loss=loss_fn(fake_output,torch.ones_like(fake_output)) #对于生成器我们希望判别器判断的的结果为1,就是希望生成的图片被判断为真
        g_loss.backward()
        g_optim.step()

        with torch.no_grad():#将每个epoch中批次的的所有loss求和
            d_epoch_loss+=d_loss.item() #得到的loss是标量tensor，使用item获取它的值
            g_epoch_loss+=g_loss.item()
    with torch.no_grad():  #求每个epoch的平均loss再放到列表中
        d_epoch_loss/=count
        g_epoch_loss/=count
        D_loss.append(d_epoch_loss)
        G_loss.append(g_epoch_loss)
        print('Epoch:',epoch)
        gen_and_save_img(gen,epoch,test_input)#使用一个固定的噪声而不是每个epoch都变的噪声从而更明显的看出来优化变化的结果
        
```

![image-20220311214826138](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220311214826138.png)

然后可以看一下loss图

```python
#因为之前.item()了，所以可以直接用loss
plt.plot(D_loss,label='D_loss')
plt.plot(G_loss,label='G_loss')
plt.legend()
```

![image-20220311213934791](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220311213934791.png)

通过loss图可以清晰的看出对抗，G和D不能同时上升或下降，互相对抗

有一个对抗过程，G上升的时候D下降，G下降的时候D上升



## CGAN（条件GAN）

### 介绍

GAN和DCGAN无论是生成手写数字还是动漫头像都是随机生成的，我们无法确定，当我们想生成某一类图像的时候，就需要CGAN 了

- 原始GAN的缺点：生成的图像是随机的，不可预测的，无法控制网络输出特定的图片，生成目标不明确，可控性不强

- CGAN的核心：就是将属性信息Y融入生成器G和判别器D中，属性y可以是任何标签信息，例如图像的类别，人脸图像的面部表情等
- CGAN的中心思想：希望可以控制GAN生成的图片，而不是单纯的随机生成图片。具体来说就是在G和D的输入中增加了额外的条件信息,生成器生成的图片只有足够真实且与条件相符才能通过判别器（要求生成真实的狗，生成了真实的猫，但是还应该判断为假）
- CGAN将GAN的无监督学习转化为了有监督学习

---

#### **从公式看：**

对G和D都添加了一个条件

![image-20220314211233446](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220314211233446.png)

---



#### **从网络架构看：**

![image-20220314211653685](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220314211653685.png)

![image-20220314211942190](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220314211942190.png)



在生成器中，作者将输入噪声z和标签y连在一起隐含表示来生成一张图像

在判别器中，图像会和y结合进行判定



CGAN可以生成指定类型的图片，也可以用于图像的自动标注（以图像特征为条件变量（Y）生成该图像的tag词向量）

![image-20220316201341948](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220316201341948.png)

> CGAN的缺点：
>
> 图像边缘模糊，生成的图像分辨率太低，但是它为后面的pix2pix和CycleGAN开拓了道路

### CGAN的构建

和前面的GAN相比，CGAN多了标签，我们需要将标签输入模型之中。一种常用的方法为将标签转换为独热编码。torch内置一种转换为独热编码的方法：torch.eye(),效果如下：可以直接返回对应的独热编码张量

![image-20220317145632121](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220317145632121.png)

所以我们定义一个函数对标签进行处理

```python
def one_hot(x,class_count=10): #输入x为类别值，如x是5就返回第五个类别值；class_count为类型数
    return torch.eye(class_count)[x,:] #是第几类就返回第几行
```

然后在引入minist的时候可以直接将标签转换为独热编码

```python
train_ds=torchvision.datasets.MNIST('data',train=True,
                                    transform=transform,
                                    target_transform=one_hot,#加了这一个参数，现在输出的标签直接就是独热编码的形式了
                                    download=True)
```

### 生成器

生成器和之前相比，多了一个输入condition，现在的输入为一个长度为100的噪声和一个长度为10的条件，在DCGAN的基础上进行修改

多了一个linear层和bn层，独热编码的输入和噪声的输入记过fc和view后变成大小一样的图片然后通过torch.cat方法结合起来

```python
class Generator(nn.Module):
    def __init__(self):
        super(Generator,self).__init__()
        self.linear1=nn.Linear(100,128*7*7) #这个是输入的噪声
        self.bn1=nn.BatchNorm1d(128*7*7) 

        self.linear2=nn.Linear(10,128*7*7)  #这个是输入的独热编码，为了方便结合，都变成128*7*7的类型，view再cat后就又变成256*7*7了，就可以直接反卷积了
        self.bn=nn.BatchNorm1d(128*7*7) 

        self.deconv1=nn.ConvTranspose2d(256,128, 
                                kernel_size=(3,3),
                                stride=1,
                                padding=1)
                                    #(128,7,7)
        self.bn2=nn.BatchNorm2d(128)
        self.deconv2=nn.ConvTranspose2d(128,64,kernel_size=(4,4),stride=2,padding=1) 
                                    #(64，14,14)
        self.bn3=nn.BatchNorm2d(64)
        self.deconv3=nn.ConvTranspose2d(64,1,kernel_size=(4,4),stride=2,padding=1) 
                                    #(1,28,28)

    def forward(self,n,y): #多一个输入，标签(条件)y,噪声n
        n=F.relu(self.linear1(n))
        n=self.bn1(n)

        y=F.relu(self.linear2(y))
        y=self.bn(y)


        n=n.view(-1,128,7,7)
        y=y.view(-1,128,7,7) #y也这么展开
        x=torch.cat([n,y],axis=1)#将独热编码和生成的图像在第一个维度（channel）进行合并 输出的大小为 batch,256,7,7

        x=F.relu(self.deconv1(x))
        x=self.bn2(x)
        x=F.relu(self.deconv2(x))
        x=self.bn3(x)
        x=torch.tanh(self.deconv3(x))
        return x


```

### 判别器

也是在DCGAN中的判别器的基础上进行更改,此时的输入不仅仅是图片，还有长度为10的condition，首先需要把condition链接到和图像一样大的程度，然后与图片进行torch.cat()，变成(2,28,28)的形状

```python
class Discriminator(nn.Module):
    def __init__(self):
        super(Discriminator,self).__init__()

        self.linear1=nn.Linear(10,1*28*28)#将condition变成和图像一样大

        self.conv1=nn.Conv2d(2,64,3,stride=2) 
        self.conv2=nn.Conv2d(64,128,3,stride=2)
        self.bn=nn.BatchNorm2d(128)
        self.Fc=nn.Linear(128*6*6,1)
    def forward(self,x1,x2): #x1为输入图片，x2为condition

        x2=F.leaky_relu(self.linear1(x2))
        x2=x2.view(-1,1,28,28)#与输入的图片大小相匹配
        x=torch.cat([x1,x2],axis=1) #(batch,2,28,28)

        x=F.dropout2d(F.leaky_relu(self.conv1(x)))
        x=F.dropout2d(F.leaky_relu(self.conv2(x)))
        x=self.bn(x)
        x=x.view(-1,128*6*6) 
        x=torch.sigmoid(self.Fc(x))
        return x

```

### 训练部分

和之前几乎没有任何区别,区别在当调用生成器的输入时现在需要两个输入了，一个是noise一个是condition

```python
#绘图部分
def gen_and_save_img(model,epoch,label_input,noise_input):
    pre=np.squeeze(model(noise_input,label_input).cpu().numpy()) #在生成器的forward中第一个参数是noise第二个是condition
    fig=plt.figure(figsize=(4,4))
    for i in range(pre.shape[0]): #这里得用中括号
        plt.subplot(4,4,i+1)
        plt.imshow((pre[i]+1)/2,cmap='gray')
        plt.axis('off')
    #plt.savefig('image_at_epoch_{:04d}.png'.format(epoch))
    plt.show()
    
#创建种子来生成同一批的图像，有利于观察模型的训练情况
noise_seed=torch.randn(16,100,device=device)
label_seed=torch.randint(0,10,size=(16,))#生成16个从0到10的整数
label_seed_onehot=one_hot(label_seed).to(device)#将labelseed装换为独热编码的形式放到GPU上
```

```python
D_loss=[]
G_loss=[]#建立两个空列表来存损失

for epoch in range(100):
    d_epoch_loss=0
    g_epoch_loss=0
    count=len(dataloader) 

    for step, (img, label) in enumerate(dataloader):#此时需要标签值了
        img=img.to(device)

        label=label.to(device)
        
        size=img.size(0)
        random_noise=torch.randn(size,100,device=device)
        
        #判别器的损失
        d_optim.zero_grad() 
        real_output=dis(img,label) #判别器的forward中第一个参数是图片，第二个是标签 
        d_real_loss=loss_fn(real_output,
                    torch.ones_like(real_output)) 
        d_real_loss.backward()

        gen_img=gen(random_noise,label) #生成器中也将label放进来
        fake_output=dis(gen_img.detach(),label)#将生成的图像和标签放入判别器
        d_fake_loss=loss_fn(fake_output,torch.zeros_like(fake_output))
        d_fake_loss.backward()

        d_loss=d_real_loss+d_fake_loss
        d_optim.step()

        #生成器的损失
        g_optim.zero_grad()
        fake_output=dis(gen_img,label)#也是将标签放进来
        g_loss=loss_fn(fake_output,torch.ones_like(fake_output)) 
        g_loss.backward()
        g_optim.step()

        with torch.no_grad():
            d_epoch_loss+=d_loss.item() 
            g_epoch_loss+=g_loss.item()
    with torch.no_grad(): 
        d_epoch_loss/=count
        g_epoch_loss/=count
        D_loss.append(d_epoch_loss)
        G_loss.append(g_epoch_loss)
        print('Epoch:',epoch)
        gen_and_save_img(gen,epoch,label_seed_onehot,noise_seed)
```







## GAN优化技巧

- 判别器容易过强是最常见的问题

>  因为这是对抗网络，所以不能有一方特别的强，如果那样的话会使得另一方训练的效果特别的差。
>
> 如判别器效果特别好的话生成器每次生成的图片都会判断为假，就不会生成梯度，生成器无法学习获得优化

​	解决方法：添加dropout层或是是生成器的学习速率大于判别器




## 风格迁移

**风格迁移分为两部分：内容部分和纹理部分**。

- 内容部分是指生成图像和原图像在内容（语义）上的相似性；
- 纹理部分是指生成图像和目标图像在纹理上的相似性。