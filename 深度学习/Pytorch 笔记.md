# Pytorch 笔记

#### pandas

主要用于数据的处理，可以处理带标签的数据

- pandas的主要数据结构是series（带标签的一维数据）dataframe(带标签的二维数据)

##### pandas的使用

1. pandas默认生成整数标签，如果想改变标签可以自己定义如图一图二

```python
pd.Series([1,2,3,4])
pd.Series([1,2,3,4],index=['a','b','c','d'])
```

2. dataframe是将多个Series合并起来的如图三

```python
d={'one':pd.Series([1,2,3,4]),'two':pd.Series(['happy','sad','nomarl','sad'])}
df=pd.DataFrame(d)
```

3. dataframe的一些操作

```python
df['one']#选择某一行
df['three']=df['one']*4#可以根据现有元素创造新的列如图4
del df['three'] 
df.pop['three']#删除某一列
df['foo']='bat'#填充元素结果如图5

```

![image-20210909190804710](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210909190804710.png)

- pandas读取进来的数据要想使用的话就得.values,形状就 **.shape**,tensor的形状用 **.size**

  ```python
  import pandas as pd
  data=pd.read_csv(income.csv)
  data.values
  data.shape
  tensor.size
  ```

- pandas读取进来的数据若不需要表头或是将第一行数据当作表头时可以在读取数据时定义`data=pd.read_csv('',header=None)`




---



#### numpy

- 基本对象为ndarray，其属性如下

  | ndim     | 维数            |
  | -------- | --------------- |
  | shape    | 尺寸（n，m）    |
  | size     | 元素总数（n*m） |
  | dtype    | 查看类型        |
  | itemsize | 每个元素的大小  |

- 创建ndarray

  1. 通过现有数组直接创建：`np.array([1,2,3])` 

  2. 给出范围创建：`np.arange(0,1,0.1)`0到1步长为0.1

     ​					   	`np.linespace(0,1,10)`按等差数列在范围内创建10个数

     ​					 	  `np.logspace()`:按等比数列创建

  3. 创建对角阵/求对角线上元素：`np.diag()`

- ndarray的索引和切片

  `ndarray[start:end:step]`若从头开始可以省略一些参数

  可以使用负数代表从后往前数`ndarray(-2)`

- `np.squeeze(a)`:删除a的第一个维度

- `np.unique(image_name)`获得目标种所有不相同的值



---



#### matplotlib

- 使用matplotlib画图（也可以使用opencv画），数据类型必须是numpy类型

```python
import matplotlib.pyplot as plt
#绘制散点图
plt.scatter(data.Education,data.Income) #（横轴和纵轴）
plt.xlabel('education')     
plt.ylabel('income')#改变横纵坐标的名称
Plt.show()
```

![image-20210905193336436](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210905193336436.png)

```python
#绘制直线：
plt.plot(X.numpy(),model1(X).data.numpy(),c='r')
```

- 绘制折线图

```python
plt.plot(range(1,101),train_acc,label='train_acc')
plt.plot(range(1,101),text_acc,label='text_acc')
plt.legend()
plt.title('acc')
```

![image-20210921101629811](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210921101629811.png)

- 创建画布来同时显示多张图片

```python
plt.figure(figsize=(12,8))  #创建个大一点的画布
for i,(img,label) in enumerate(zip(imgs_batch[:6],label_batch[:6])):  # i是序号
    img=(img.permute(1,2,0).numpy() ) #对图像进行变换使其可以被显示，将原本的第0个通道（颜色通道数）放到最后
    plt.subplot(2,3,i+1)  #子图一共2行三列，当次放在第i+1个子图上
    plt.title(idx_to_speces.get(label.item()))  #.get()就是获得对应的类别名称（这就是为什么之前要定义字典并将序号和名称换位置）,.item()获取其数值
    plt.imshow(img)
```

![image-20210921101400077](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210921101400077.png)



---



#### 张量tensor

是pytorch中最基本的操作对象，表示一个多维矩阵，类似于数组，可以在GPU上使用用以加速计算

- 创建张量：

```python
#从矩阵创建
torch.rand(行，列) #构建一个均匀分布的初始化矩阵
torch.randn(行，列)#创建一个正态分布的随机矩阵
torch.zeros(行，列)
torch.ones(个数，行，列)
#从列表创建
x=torch.tensor([6,2],dtype=torch.float32)
```

- 通过`.size` 来看tensor大小

- 张量的变形：`.view(2,3)`,常用该指令将tensor展平`x1.view(-1,1)`

- 内置的函数：求平均：`.mean()`求和：`.sum()`

- 获取tensor的标量值：`.item()`

- 张量的自动微分：将`.requires_grad`设为true,pytorch 将开始跟踪对此张量的所有操作，完成计算后可以调用`.backward()`反向传播计算所有梯度，该张量的梯度将累加到`.grad`中

  ```python
  x=torch.ones(2,2,requires_grad=True)
  y=x+2
  z=y**2+3
  z.mean().backward()#因为只打开了x的自动微分，所以求的是z对x的导
  x.grad
  
  a.requires_grad_(True)#也可以这样使得a被跟踪  
  ```

  若一些x的计算不想跟踪，可以包含在`with torch.no_grad():`中

- 梯度清零：`w.grad.data.zero_()`将w的梯度清零



---



#### 预处理数据

##### 观察数据

- 想看数据集的属性可以`data.info`
- 想看数据中某一列有哪些项`data.salary.unique()`   看salary这一列有哪些项
- `data.groupby() .sum()/.size()`：分组运算，将几列按照需求进行分组，看其和或是个数

<img src="C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210910164950654.png" alt="image-20210910164950654" style="zoom:70%;" />

- `data.left.value_counts()`:可以统计某一列中都有哪些项，每一项有多少个

  ![1645757860749](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645757860749.png)

##### 处理数据

- `.reshape()`:将数据按照要求分割

```python
   X=data.Edu.values.reshape(-1,1) #（行，列） -1是根据个数自动计算，1是每个数据长度是1 意思是分成若干行一列
```

- `.iloc[:,:]`:分割数据  

```python
   X=data.iloc[:,:-1]#使用iloc指令将data中的所有行，除了最后一列外的所有数据分割给了X
   Y=data.iloc[:,-1]#最后一列给Y也同理
```

- `[c for c in data.colomuns  if c!='left']`:使用列表推导式来拆分列表，这个的意思是选择data中除了left之外的所有列

  ```python
  X_data=data[[c for c in data.colomuns  if c!='left']]
  ```

- `.replace(原，新)`：替换指定的元素

```python
   Y=data.iloc[:,-1].replace(-1,0)
```

- `pd.get_dummies()`: 文本特征数值化将某些不是数字的项转变为数字放到列上，通常与`data.join`和`del data[]`一起用

  ```python
  data=data.join(pd.get_dummies(data['salary']))
  del data['part']
  ```

  这个例子就将salary列中的三个文本特征：high，low和medium放到了列上（添加了3个列）并把原来的工资那一列删除

- `pd.factorize()`:将某一列中的所有文字项数转变为数字

  ```python
  data['Species']=pd.factorize(data.Species)[0] #就将三种花的种类变成了0，1，2 再将原来的那一列替换掉
  ```




##### 改变数据类型

- 改变数据类型

  - pandas的数据：`.astype(np.float32)`  # 只能转换成np的类型
  - tensor的数据：`.type(torch.float32) `
  - 如果想看一个数组的类型：`.dtype`

- numpy和tensor的相互转换：

  pytorch的输入必须是tensor类型。

  - np->torch:

    ```python
    X=torch.from_numpy()
    ```
  
  - 其他类型->numpy: `.numpy()`

##### 使用Dataset和Dataloader加载模型数据

要是数据量大的话就得先切片再一个一个训练十分的麻烦，torch中有个方法可以对输入输出同时进行迭代，用来包装张量.

- dataset可以将多个张量同时包装成一个dataset，这样对他的第一个张量进行运算时会对这个dataset里的所有张量一起迭代运算，x,y就不用写两个切片了，写一个就行了
- dataloader：用来管理批次，会自动提供每个batches每个batches的数据，不再需要自己切片了

```python
from torch.utils.data import TensorDataset,DataLoader
HR_ds=TensorDataset(X,Y)#这样每一个元素就是一组切片（HRds[0]中有15个x和一个y）
HR_dl=Dataloader(HR_ds,batch_size=batch,shuffle=Ture)#shuffle是是否乱序

#这样在训练模型时就可以直接从dl集中提取x，y即可
for x,y in HR_dl:
    
```

##### 处理图片数据

- 数据集变形方法：`transformation=transforms.Compose([    ])`

  1. transforms.ToTensor:

    - 将我们读取的图片或是其他类型的数据转换为tensor

    - 将数据归一化，转换到0~1之间

    - ==会将channel这个维度放到第一维度==

      > 在pytorch里图片的表示形式就是这样的[channel,high,width]
      >
      > ToTensor会将channel这个维度放到第一维度，这是和其他方法最大的不同，如果是电脑中的普通图片则是长宽，channel

  ```python
  from torchvision import datasets,transforms
  
  transformation=transforms.Compose([
      transforms.ToTensor()
  ])
  
  #下载minist手写数据集作为ds
  train_ds=datasets.MNIST(
      'data/',
      train=True,
      transform=transformation,
      download=True
  )
  text_ds=datasets.MNIST(
      'data/',
      train=False,
      transform=transformation,
      download=True
  )
  
  train_dl=DataLoader(train_ds,batch_size=64,shuffle=True)
  text_dl=DataLoader(text_ds,batch_size=256) #验证数据集可以切片切的大一点，因为不用反向传播所以占用资源少
  
  img,label=next(iter(train_dl))  #取出一个批次的图片和标签
  image=img[0]#取出一张图片
  image=image.numpy() #想要绘图就得用ndarray
  image=np.squeeze(image) #第一个维度channel没有用，去掉
  plt.imshow(image)# 用matplotlib画出这张图像
  label[0] #查看这张图像的标签
  
  #可以创建一个函数来进行转换并显示图片
  def imshow(img):
      npimg=img.numpy()      #转化为numpy
      npimg=np.squeeze(npimg)#去除第一维度
      plt.imshow(npimg)      #显示图片
  
  #如果要同时显示多个图像可以创建画布
  plt.figure(figsize=(10,1))             #创建画布
  for i,img in enumerate(img[:10]):     #enumerate相当于是每次返回img[i]
      plt.subplot(1,10,i+1)             #创建10张子图  三个参数分别是一行十列绘制img的第几个（img[i]）
      imshow(img)
  ```


#### 从分类的文件夹中创建dataset数据

使用`torchvision.datasets.ImageFolder()` 从分类的文件夹中创建dataset数据，因为用这个需要相同类别在一个文件夹中，所以要先对图片进行操作。

```python
from torchvision import datasets,transforms

base_dir=r'F:/python/dataset/4weather'#定义数据集的基准地址
specises=['cloudy','rain','shine','sunrise']    #数据集有四种类别

#创建存放测试和训练数据的文件夹
if  not os.path.isdir(base_dir):  
    os.mkdir(base_dir)       #如果没有这个目录的话就创建这个目录
    train_dir=os.path.join(base_dir,'train')  #给训练数据和测试数据分类
    text_dir=os.path.join(base_dir,'text')
    os.mkdir(train_dir) 
    os.mkdir(text_dir) 
    
    for train_or_text in ['train','text']:
        for spec in specises:
            os.mkdir(os.path.join(base_dir,train_or_text,spec)) #利用循环创建8个文件夹  放在if里可以防止重复创建

img_dir=r'./weather_dataset'   #定义图片数据集所在地址（图片目录）
os.listdir(img_dir) #这样可以列出所有的图片

#进行训练以及测试数据集的划分
for i,img in enumerate(os.listdir(img_dir)):  #保留序号，分训练和测试数据集的时候用
    for spec in specises:
        if spec in img:       #字符串的应用，若当前的种类在当前的图片名称中出现
            s=os.path.join(img_dir,img)  #这是原始图片目录  如cloudy 在cloudy117中出现
            if i%5==0 :    #如果能被5整除就放进测试数据集中，不能就放入训练数据集
                d=os.path.join(base_dir,'text',spec,img) #图片的目标目录
            else:
                d=os.path.join(base_dir,'train',spec,img)
            shutil.copy(s,d)  #拷贝文件，从s到d
            
#看一下分类完后的各个种类的数量
for train_or_text in ['train','text']:
    for spec in specises:
        print(train_or_text,spec,len(os.listdir(os.path.join(base_dir,train_or_text,spec))))
        
   
#定义变形方法
transform=transforms.Compose([
    transforms.Resize((96,96)), #把图片大小统一成96*96   要加两个括号！！！一个是函数的括号，一个是参数的括号
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.5,0.5,0.5],std=[0.5,0.5,0.5]) #标准化   从0~1转化成-1~1
                                #两个参数分别是均值和方差，如果事先了解数据集的可以直接填上，不了解就写个大概
])

train_dir=os.path.join(base_dir,'train') 
text_dir=os.path.join(base_dir,'text')

#使用ImageFolder从文件夹创建ds数据集
train_ds=torchvision.datasets.ImageFolder(
    train_dir,                      #两个参数，一个是目录地址，一个是变形方法
    transform=transform  
)
text_ds=torchvision.datasets.ImageFolder(
    text_dir,                      
    transform=transform  
)

train_ds.classes    #可以通过.classes看出来ds数据集有哪些类
train_ds.class_to_idx    #每一个类别的编号

train_dl=DataLoader(train_ds,batch_size=16,shuffle=True)
text_dl=DataLoader(text_ds,batch_size=16)

#此时的图片是利于torch处理的(channel,w,h)但如果想要显示就得变换成（w,h,c）
imgs,labels=next(iter(train_dl))
im=imgs[0].permute(1,2,0)  #交换三个数的位置，把原来第一个和第二个放到前面，原来第0个放到最后
im=im.numpy()   #画图需要numpy类型，但此时仍不能画图，因为标准化过了现在是-1~1要转换成0~1
im=(im+1)/2  #这样就变成了0~1之间了
plt.imshow(im)#此时就可以画出来了
labels[0]#还可以看标签

id_to_class=dict((v,k) for k,v in train_ds.class_to_idx.items())  #将顺序换一下，序号放前面，天气放后面

plt.figure(figsize=(12,8))  #创建个大一点的画布
for i,(img,label) in enumerate(zip(imgs[:6],labels[:6])):#取六张图片
    img=(img.permute(1,2,0).numpy() +1)/2
    plt.subplot(2,3,i+1)  #子图一共2行三列，当次放在第i+1个子图上
    plt.title(id_to_class.get(label.item()))  #.get()就是获得对应的类别名称（这就是为什么之前要将序号和名称换位置）
    plt.imshow(img)
```



---





#### 创建模型

使用torch中的高级API **nn**

##### 常用的层

```python
from torch import nn
#单层线性模型
model=nn.Linear(1,1)#创建简单的线性模型，输入特征长度为1，输出特征长度为1

nn.Conv2d(in_channel,out_channel,ksize)#2维卷积层
nn.MaxPool2d((w,h))#最大池化层
F.relu()#激活函数
self.drop=nn.Dropout(0.5) #Dropout层，防止过拟合，区分训练过程和测试过程
                #因为在linear使用的dropout，所以就用普通的就行，参数为丢弃掉的单元数（0.5就是50%）,一般添加在模型的后半部分
self.bn1=nn.BatchNorm2d(16)#参数为上一层输入的层数

nn.ConvTranspose2d(channel,channel//2,kernel_size=3,stride=2)
                            #pytorch内置的反卷积层，其参数与卷积的参数几乎一摸一样，但是有些不同
                            #反卷积需要跨度，没有跨度是实现不了图像的放大的，跨度起到放大的作用,为2表示放大两倍
                            #反卷积的padding指的是输入的起始位置，为2代表从第二个像素开始做反卷积
                            #outkput_padding反卷积之后在外面进行填充，类似于卷积的padding，边缘填充1来使输出图像与输入图像大小相同
```
##### 模型实例

```python
#通过nn.Sequential()创建多层模型
model=nn.Sequential(
            nn.Linear(15,1),
            nn.Sigmoid()
)#也可以通过Sequential来创建小的子模型。

#继承Module类创建模型类别
class Model(nn.Module):
    def __init__(self):                  #初始化这些层
        super().__init__()
        self.linear_1=nn.Linear(20,64)   #多层感知器，创建64个中间层（隐藏层）
        self.linear_2=nn.Linear(64,64)
        self.linear_3=nn.Linear(64,1)
        self.relu=nn.ReLU()              #一个relu激活层
        self.sigmoid=nn.Sigmoid()        #因为是二分类问题，所以再创建一个sigmoid层
    def forward(self,input):             #在forward中使用这些层，对input进行处理
        x=self.linear_1(input)           #利用输入调用第一层得到x
        x=self.relu(x)                   #对第一层使用激活函数
        x=self.linear_2(x)               #调用第二层
        x=self.relu(x)
        x=self.linear_3(x)               #调用第三层
        x=self.sigmoid(x)                #最后一层用sigmoid激活函数
        return(x)
#也可以使用functional模块不用再初始化激活函数了
import torch.nn.functional as F
class Model(nn.Module):
    def __init__(self):                  
        super().__init__()
        self.linear_1=nn.Linear(20,64)   
        self.linear_2=nn.Linear(64,64)
        self.linear_3=nn.Linear(64,1)
        
    def forward(self,input):             
        x=F.relu(self.linear_1(input))    #利用F.relu函数直接对Linear激活                
        x=F.relu(self.linear_2(x))              
        x=torch.sigmoid(self.linear_3(x))     #可以看出这样就简洁了许多           
        return(x)
    
```
##### 创建卷积模型

卷积层定义方法可以依次翻倍：16->32->64一种比较著名的设计方法

```python
class Model(nn.Module):
    def __init__(self):
        super().__init__() 
        self.conv_1=nn.Conv2d(1,6,5)  #初始化一个2d的卷积层，适用在图像的特征提取
                                      # 第一个参数是输入的channel，所用的图像的可以看出是1 
                                      #第二个参数是要输出多少个channel，即你想要用多少个卷积核提取特征
                                      #第三个参数是卷积核的大小，定义了是几乘几的卷积核
       
        self.pool=nn.MaxPool2d((2,2))      #2d的最大池化层 大小是2*2 相当于池化一次长宽各减少一半（2*2的选出最大值就变成了1*1的）
        self.conv_2=nn.Conv2d(6,16,5)   #创建第二个卷积层，输入就是上一个卷积层的输出，输出设置的多一点
        
        
        self.linear_1=nn.Linear(16*4*4,256)  #大小为最后一个卷积层展平之后的大小,不一定是多少，所以下面用了print来打出提取完特征之后的大小
        #self.linear_2=nn.Linear(120,84)   #只用两个线性层得到输出就可以了（最后一层即全连接层）
        self.linear_2=nn.Linear(256,10)  
    def forward(self,input):
       #x=input.view(-1,28*28) #卷积模型不需要展平，保留图像的空间结构，卷积神经网络是在将所有特征提取完之后再展平
        x=F.relu(self.conv_1(input)) #卷积+激活
        x=self.pool(x)        #池化
        x=F.relu(self.conv_2(x))
        x=self.pool(x)  
        #print(x.size())    #看一下x具体多大方便定义第一个线性层的输入是多少  是torch.Size([64, 16, 4, 4])
        x=x.view(x.size(0),-1)#然后再根据x的大小展平
        x=F.relu(self.linear_1(x))
        x=self.linear_2(x) #因为是多分类，用的损失函数CrossEntropyLoss
                          #的输入是未激活的输出
        return x
    

    
#天气分类卷积模型
class Net(nn.Module):
    def __init__(self):
        super(Net,self).__init__()
        self.conv_1=nn.Conv2d(3,16,3)
        self.conv_2=nn.Conv2d(16,32,3)
        self.conv_3=nn.Conv2d(32,64,3)
        self.drop=nn.Dropout(0.5) #因为在linear使用的dropout，所以就用普通的就行，参数为丢弃掉的单元数（0.5就是50%）,一般添加在模型的后半部分
        self.pool=nn.MaxPool2d(2,2)
        self.linear1=nn.Linear(64*10*10,1024)
        self.linear2=nn.Linear(1024,256)
        self.linear3=nn.Linear(256,4)
    def forward(self,x):
        x=F.relu(self.conv_1(x))
        x=self.pool(x)
        x=F.relu(self.conv_2(x))
        x=self.pool(x)
        x=F.relu(self.conv_3(x))
        x=self.pool(x)
       # print(x.size())
        x=x.view(-1,x.size(1)*x.size(2)*x.size(3))
        x=F.relu(self.linear1(x))
        x=self.drop(x)
        x=F.relu(self.linear2(x))
        x=self.drop(x)                            #加在线性层之后
        x=self.linear3(x)
        return x

#模型添加BN层
class Net(nn.Module):
    def __init__(self):
        super(Net,self).__init__()
        self.conv_1=nn.Conv2d(3,16,3)
        self.bn1=nn.BatchNorm2d(16) #第一个参数是有多少个特征，相当于channel数，第一个卷积层输出16个通道，所以这里输入是16
        self.conv_2=nn.Conv2d(16,32,3)
        self.bn2=nn.BatchNorm2d(32)
        self.conv_3=nn.Conv2d(32,64,3)
        self.bn3=nn.BatchNorm2d(64)
        self.drop=nn.Dropout(0.5) 
        self.pool=nn.MaxPool2d(2,2)
        self.linear1=nn.Linear(64*10*10,1024)
        self.bn_f1=nn.BatchNorm1d(1024) #对线性层也可以添加BN层，不过是1d
        self.linear2=nn.Linear(1024,256)
        self.bn_f1=nn.BatchNorm1d(256)
        self.linear3=nn.Linear(256,4)
    def forward(self,x):
        x=F.relu(self.conv_1(x))
        x=self.bn1(x)               #放在卷积或是线性层之后
        x=self.pool(x)
        x=F.relu(self.conv_2(x))
        x=self.bn2(x)
        x=self.pool(x)
        x=F.relu(self.conv_3(x))
        x=self.bn(3)
        x=self.pool(x)
       # print(x.size())
        x=x.view(-1,x.size(1)*x.size(2)*x.size(3))
        x=F.relu(self.linear1(x))
        x=self.bn_f1(x)
        x=self.drop(x)
        x=F.relu(self.linear2(x))
        x=self.bn_f2(x)
        x=self.drop(x)                           
        x=self.linear3(x)
        return x
        
```

##### 线性模型分解写法

```python
w=torch.randn(1,requires_grad=True)#随机初始化一个权重
b=torch.zeros(1.requires_grad=True)#把b初始化为0
learning_rate=0.001#定义学习速率
for i in range(500):
    for x,y in zip(X,Y):
        y_pred=torch.matmul(x,w)+b      #这里matmul是矩阵乘法
                                        #就相当于w*x+b
        loss=(y-y_pred).pow(2).mean()   #求均方误差（实际值减预测值的平方的均值）
        if not w.grad is None:
            w.grad.data.zero_()         #梯度不为空就清零
        if not b.grad is None:
            b.grad.data.zero_()
        loss.backward()       #dloss/dw和dloss/db,谁backward就是让它对跟踪的变量求微分
                              #这样w和b的grad就有值了
        with torch.no_grad():#这里是优化算法，不能改变梯度
            w.data-=w.grad.data*learning_rate
            b.data-=b.grad.data*learning_rate
```

##### 获取模型以及优化函数

每次更新模型之后都需要运行一次这个函数去更新一下模型和优化

```python
def get_model():       #编写一个函数，每次运行这个函数都得到这个模型以及优化方法
    model=Model()
    opt=torch.optim.Adam(model.parameters(),lr=0.001)
    return model,opt
```



##### 逻辑回归

线性回归预测的是连续的值，逻辑回归给出的是是和否的回答，逻辑回归用到了sigmoid函数（概率分布函数），给定一个输入时，输出为0~1的概率值，常用于分类问题

##### 多分类问题

对于多分类问题的处理我们使用softmax这个函数

![image-20210911093034695](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210911093034695.png)

softmax会输出这个样本属于某一个类别的概率，比如我们要分三类，它就会输出一个长度为3的张量，每个位置都标志这个位置的概率 ，且相加是1，看那个位置的概率最高它就是哪一类的。

##### TIPS

- 再每次改完模型之后要重新赋予模型并在运行一遍优化函数



---



#### 损失函数

```python
loss_fn=nn.MSELoss()#均分误差损失函数，多用于回归问题  

loss=nn.BCELoss()#二元交叉熵损失函数 用于二分类

loss_fn=nn.CrossEntropyLoss()#交叉熵损失函数 多用于多分类问题 也被称为softmax函数
```

- 均分误差损失函数(MSELoss):

>  loss(x~i~ ,y~i~ )=(x~i~ -y~i~ )^2^

- 交叉熵损失函数(CrossEntropyLoss)：交叉嫡刻画的是实际输出（概率）与期望输出(概率)的距离，也就是交叉嫡的值越小，两个概率分布就越接近。假设概率分布p为期望输出，概率分布q为实际输出，H(p,q)为交叉嫡,假设概率分布p为期望输出,则：

> ![image-20210910154719568](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210910154719568.png)
>
> 使用log运算来放大损失函数





---



#### 创建优化函数

**优化器**(optimizer)

是根据反向传播计算出的梯度,优化模型参数的内置方法

使用torch中的optim模块

```python
opt=torch.optim.SGD(model.parameters(),lr=0.001)#SGD为随机梯度下降优化算法
opt=torch.optim.Adam(model.parameters(),lr=0.001)#Adam优化器
```

##### SGD:随机梯度下降优化器

随机梯度下降优化器SGD和min-batch是同一个意思，抽取m个小批量（独立同分布)样本，通过计算他们平梯度均值。

##### RMSprop

增加了一个衰减系数来控制历史信息的获取多少,会对学习速率进行衰减,特别适合用来优化序列问题,是训练循环神经网络RNN的不错选择.

##### Adam优化器

结合AdaGrad和RMSProp两种优化算法的优点。对梯度的一阶矩估计（First Moment Estimation，即梯度的均值）和二阶矩估计（Second Moment Estimation，即梯度的未中心化的方差）进行综合考虑，计算出更新步长。

==Adam可以独立设计自适应的学习率==

主要包含以下几个显著的优点：

1. 实现简单，计算高效，对内存需求少

2. 参数的更新不受梯度的伸缩变换影响

3. 超参数具有很好的解释性，且通常无需调整或仅需很少的微调

4. 更新的步长能够被限制在大致的范围内（初始学习率）

5. 能自然地实现步长退火过程**（自动调整学习率）**

6. 很适合应用于大规模的数据及参数的场景

7. 适用于不稳定目标函数

8. 适用于梯度稀疏或梯度存在很大噪声的问题

综合Adam在很多情况下算作默认工作性能比较优秀的优化器。

> 学习速率建议设置为0.001



---



#### 训练

- 最原始的训练方法：

```python
for epoch in range(5000):
    for x,y in zip(X,Y):
        y_pred=model1(x)
        loss=loss_fn(y,y_pred)
        opt.zero_grad()#清零梯度
        loss.backward()#反向传播
        opt.step()#优化参数模型
```

可以通过`model.weight`和`model.bias`看当前的w和b

- 小批次训练

```python
batches=16
no_of_batches=653//16 #//是整除的意思，训练不能训练小数次

epoches=1000

for epoch in range(epoches):      #一共训练多少遍
    for batch in range(no_of_batches):  #训练一遍需要训练多少个小块
        start=batch * batches
        end=start + batches  #使用start和end这样就每次取出16个出来
        x=X[start:end]
        y=Y[start:end]        #这样就取出来了16个x和16个y
        y_pred=model(x)       #把x输入模型，进行预测
        loss=loss_fn(y_pred,y)#通过损失函数计算损失
        opt.zero_grad() #optim里自带的梯度清零的函数，会将模型中变量的梯度全部置为零
        loss.backward() #反向传播，计算每个变量的梯度
        opt.step()      #利用内置函数，使用设定好的优化方法进行优化
    with torch.no_grad():
        print('epoch: ',epoch,'loss: ',loss_fn(model(X),Y).data.item()) #打印出每个epoc的损失
        
#使用DS和DL：
for epoch in range(epoches):
    for x,y in HR_dl:

        y_pred=model(x)
        loss=loss_fn(y_pred,y)
        optim.zero_grad()
        loss.backward()
        optim.step()
```

训练完后可以通过`model.state_dict()`看模型的各个特征值的权重和偏置

对于多分类，使用`torch.argmax(y_pred,dim=1)` 来看出在预测值中哪个维度的概率最大

![image-20210911094754500](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210911094754500.png)



设置了几个维度就能在几个维度上进行对比，如上面数组就只有两个维度，就只能找到行(dim=0)和列(dim=1)中最大的那个数的次序，如果数组有三维，则第一维是数组内数组的个数，比较dim=0就相当于将这两个数组展开，依次比较这两个数组总的每一个元素的大小。

==2维数组的话dim=0为按列比较，dim=1为按行比较==

![1645773447286](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645773447286.png)



- 创建fit函数

  编写一个fit函数，以后训练的时候都可以直接调用，fit的参数为输入模型和输入数据（train_dl,text_dl），对输入数据再模型上做一个训练并且返回loss和acc变化

  fit函数相当于对数据做一个epoch的训练

  函数定义的参数为模型，训练数据集和测试数据集，没有定义train_x,y等等，所以我们采用正确个数除以总个数来表示正确率，对于loss也是同样的方法，计算每一个批次的loss后再除以样本总数就是平均loss了

```python
def fit(epoch,model,trainloader,textloader):   #因为这个函数没有输入train_x和train_y所以直接用train_dl和text_dl来算正确率
    correct=0                            #通过记录预测正确的个数和样本总数之间的比值来看正确率
    total=0                              #总样本的个数
    running_loss=0
    model.train()      #使用dropout层和BN层时一定要加这一句表明模型正处于训练状态下  
    for x,y in trainloader:  
        #y=torch.tensor(y,dtype=torch.long)#将标签转化为torch.long 类型
        #x,y=x.to('cuda'),y.to('cuda') #如果要使用GPU进行加速计算就打开屏蔽 
        y_pred=model(x)
        loss=loss_fn(y_pred,y)
        optim.zero_grad()
        loss.backward()
        optim.step()
        with torch.no_grad():                  #每一个y值进行一次计算，这是对训练数据
            y_pred=torch.argmax(y_pred,dim=1)
            correct+=(y_pred==y).sum().item()  #每一次正确的个数加到correct里
            total+=y.size(0)                   #每一批样本的个数
            running_loss+=loss.item()          #每一批样本的loss
        
    #exp_lr_scheduler.step() #如果定义了学习速率衰减可以打开这个屏蔽
    
    epoch_acc=correct/total                #正确率为正确个数除以样本个数
    epoch_loss=running_loss/len(trainloader.dataset)  #平均loss为一个批次的总loss除以训练的长度
    
    
    text_correct=0                          #这是对测试数据 ,对于测试数据不用反向传播不用优化
    text_total=0                              
    text_running_loss=0
    model.eval()      #告诉模型现在是预测模式，dropout层不需要发挥作用  
    with torch.no_grad():                  
            for x,y in textloader: 
                #y=torch.tensor(y,dtype=torch.long)#将标签转化为torch.long 类型
                #x,y=x.to('cuda'),y.to('cuda') #如果要使用GPU进行加速计算就打开屏蔽 
                y_pred=model(x)
                loss=loss_fn(y_pred,y)
                y_pred=torch.argmax(y_pred,dim=1)
                text_correct+=(y_pred==y).sum().item() 
                text_total+=y.size(0)                   
                text_running_loss+=loss.item()
    
    epoch_text_acc=text_correct/text_total                
    epoch_text_loss=running_loss/len(textloader.dataset)  
    
    print('epoch: ',epoch,'loss: ',round(epoch_loss,3),
                            'accuracy: ',round(epoch_acc,3),
                            'text_loss: ',round(epoch_text_loss,3),
                            'text_accuracy: ',round(epoch_text_acc,3))
    return epoch_loss,epoch_acc,epoch_text_loss,epoch_text_acc  
                                                #这样就会将每个epoch上的这些平均正确率和平均损失返回
```

调用fit函数：

```python
train_loss=[] #创建几个空的列表来存放数据,方便绘图，看看模型怎么样
train_acc=[]
test_loss=[]
test_acc=[]

for epoch in range(epochs):
    epoch_loss,epoch_acc,epoch_test_loss,epoch_test_acc =fit(epoch,model,train_dl,test_dl)
    
    train_loss.append(epoch_loss)
    train_acc.append(epoch_acc)
    test_loss.append(epoch_test_loss)
    test_acc.append(epoch_test_acc)
```

 添加一些逻辑使模型能够保存最优时的参数

```python
import copy
best_acc=0

for epoch in range(epochs):
    epoch_loss,epoch_acc,epoch_test_loss,epoch_text_acc =fit(epoch,model,train_dl,text_dl)
    
    if epoch_test_acc > best_acc:
        best_model_wts=copy.deepcopy(model.state_dict()) #达到目前最高的正确率时复制此时的模型权重
        best_acc=epoch_text_acc
    
    train_loss.append(epoch_loss)
    train_acc.append(epoch_acc)
    test_loss.append(epoch_test_loss)
    test_acc.append(epoch_test_acc)
    
model.load_state_dict(best_model_wts)#在整个模型训练完成后给模型最优情况的权重值，在使用这个模型之前要先设置成																					model.eval()模式
```

图像定位所使用的fit函数

```python
if torch.cuda.is_available():
    model.to('cuda')
def fit(epoch,model,trainloader,textloader):   #因为这个函数没有输入train_x和train_y所以直接用train_dl和text_dl来算正确率
    running_loss=0
    model.train()      #使用dropout层和BN层时一定要加这一句表明模型正处于训练状态下  
    for x,y1,y2,y3,y4 in trainloader:  
        x,y1,y2,y3,y4=(x.to('cuda'),y1.to('cuda'),y2.to('cuda'),y3.to('cuda'),y4.to('cuda')) #如果要使用GPU进行加速计算就打开屏蔽 
        y_pred1,y_pred2,y_pred3,y_pred4,=model(x)
        loss1=loss_fn(y_pred1,y1)
        loss2=loss_fn(y_pred2,y2)
        loss3=loss_fn(y_pred3,y3)
        loss4=loss_fn(y_pred4,y4)
        loss=loss1+loss2+loss3+loss4
        optim.zero_grad()
        loss.backward()
        optim.step()
        with torch.no_grad():                  
            running_loss+=loss.item()          #每一批样本的loss
        
    exp_lr_scheduler.step() #如果定义了学习速率衰减可以打开这个屏蔽
    
    epoch_loss=running_loss/len(trainloader.dataset)  #平均loss为一个批次的总loss除以训练的长度
    
                                
    text_running_loss=0
    model.eval()      #告诉模型现在是预测模式，dropout层不需要发挥作用  
    with torch.no_grad():                  
            for x,y1,y2,y3,y4  in textloader: 
                x,y1,y2,y3,y4=(x.to('cuda'),y1.to('cuda'),y2.to('cuda'),y3.to('cuda'),y4.to('cuda'))
                y_pred1,y_pred2,y_pred3,y_pred4=model(x)
                loss1=loss_fn(y_pred1,y1)
                loss2=loss_fn(y_pred2,y2)
                loss3=loss_fn(y_pred3,y3)
                loss4=loss_fn(y_pred4,y4)
                loss=loss1+loss2+loss3+loss4                    
                text_running_loss+=loss.item()
                    
    epoch_test_loss=running_loss/len(textloader.dataset)  
        
    
    print('epoch: ', epoch, 
        'loss： ', round(epoch_loss, 3),
        'test_loss： ', round(epoch_test_loss, 3),
            )
        
    return epoch_loss, epoch_test_loss
```

图像语义分割中添加IOU指标的函数训练过程

```python
def fit(epoch,model,trainloader,textloader):   #因为这个函数没有输入train_x和train_y所以直接用train_dl和text_dl来算正确率
    correct=0                            #通过记录预测正确的个数和样本总数之间的比值来看正确率
    total=0                              #总样本的个数
    running_loss=0
    epoch_IOU=[]
    model.train()      #使用dropout层和BN层时一定要加这一句表明模型正处于训练状态下  
    for x,y in trainloader:  
        x,y=x.to('cuda'),y.to('cuda') #如果要使用GPU进行加速计算就打开屏蔽 
        y_pred=model(x)
        loss=loss_fn(y_pred,y)
        optim.zero_grad()
        loss.backward()
        optim.step()
        with torch.no_grad():                  #每一个y值进行一次计算，这是对训练数据
            y_pred=torch.argmax(y_pred,dim=1)
            correct+=(y_pred==y).sum().item()  #每一次正确的个数加到correct里
            total+=y.size(0)                   #每一批样本的个数
            running_loss+=loss.item()          #每一批样本的loss

            intersection=torch.logical_and(y,y_pred)#使用torch内置的与运算计算预测值与实际值之间的交集
            union=torch.logical_or(y,y_pred)#使用torch内置的交运算计算预测值与实际值之间的并集
            batch_IOU=torch.true_divide(torch.sum(intersection.cpu()),torch.sum(union.cpu()))
                                    #因为这些都是tensor类型，所以使用torch的求和 和相除方法
                                    #因为之后要求一个epoch中所有IOU的平均值，所以将其放在cpu上这样才能转换成numpy再求平均值
            epoch_IOU.append(batch_IOU)


        
    #exp_lr_scheduler.step() #如果定义了学习速率衰减可以打开这个屏蔽
    
    epoch_acc=correct/(total*256*256)                #正确率为正确个数除以样本个数
    epoch_loss=running_loss/len(trainloader.dataset)  #平均loss为一个批次的总loss除以训练的长度
    
    
    text_correct=0                          #这是对测试数据 ,对于测试数据不用反向传播不用优化
    text_total=0                              
    text_running_loss=0
    test_epoch_IOU=[]
    model.eval()      #告诉模型现在是预测模式，dropout层不需要发挥作用  
    with torch.no_grad():                  
            for x,y in textloader: 
                x,y=x.to('cuda'),y.to('cuda') #如果要使用GPU进行加速计算就打开屏蔽 
                y_pred=model(x)
                loss=loss_fn(y_pred,y)
                y_pred=torch.argmax(y_pred,dim=1)
                text_correct+=(y_pred==y).sum().item() 
                text_total+=y.size(0)                   
                text_running_loss+=loss.item()
                intersection=torch.logical_and(y,y_pred)#使用torch内置的与运算计算预测值与实际值之间的交集
                union=torch.logical_or(y,y_pred)#使用torch内置的交运算计算预测值与实际值之间的并集
                batch_IOU=torch.true_divide(torch.sum(intersection.cpu()),torch.sum(union.cpu()))
                test_epoch_IOU.append(batch_IOU)
    
    epoch_text_acc=text_correct/(text_total*256*256)               
    epoch_text_loss=running_loss/len(textloader.dataset)  
    
    print('epoch: ',epoch,'loss: ',round(epoch_loss,3),
                            'accuracy: ',round(epoch_acc,3),
                            'train_IOU:',round(np.mean(epoch_IOU),3),#在每一个批次结果相同时可以这么写
                            'text_loss: ',round(epoch_text_loss,3),
                            'text_accuracy: ',round(epoch_text_acc,3),
                            'test_IOU:',round(np.mean(test_epoch_IOU),3))
                            
    return epoch_loss,epoch_acc,epoch_IOU,epoch_text_loss,epoch_text_acc,test_epoch_IOU  
                                                #这样就会将每个epoch上的这些平均正确率和平均损失返回
```

```python
for epoch in range(epochs):
    epoch_loss,epoch_acc,epoch_IOU,epoch_test_loss,epoch_test_acc ,test_epoch_IOU=fit(epoch,model,train_dl,test_dl)
    
    train_loss.append(epoch_loss)
    train_acc.append(epoch_acc)
    train_iou.append(epoch_IOU)
    test_loss.append(epoch_test_loss)
    test_acc.append(epoch_test_acc)
    test_iou.append(test_epoch_IOU)
```



---



#### 添加验证

##### 打印正确率以及损失

对于二分类模型：

```python
((model(X).data.numpy()>0.5).astype('int')==Y.numpy()).mean() 
		#对于X的预测值概率大于0.5就看成1再与真实值去比最后求平均就是预测准确率
    
def accuracy(y_pred,y_true):              #定义一个计算正确率的函数
    y_pred=(y_pred>0.5).type(torch.int32) #先把预测值转换为0和1
    acc=(y_pred==y_true).float().mean()   #预测值与真实值进行比较
                        #float是快捷的转换格式的方法，再求平均值就是平均正确率了
    return acc
#以下放在训练中，每一轮的训练都会打印
with torch.no_grad():
        epoch_accuracy=accuracy(model(train_x),train_y)  #每把数据训练一遍就计算一遍正确率
        epoch_loss=loss_fn(model(train_x),train_y).data
        epoch_text_accuracy=accuracy(model(text_x),text_y)  #计算测试数据的正确率
        epoch_text_loss=loss_fn(model(text_x),text_y).data
        print('epoch: ',epoch,'loss: ',round(epoch_loss.item(),3),
                              'accuracy: ',round(epoch_accuracy.item(),3),
                              'text_loss: ',round(epoch_text_loss.item(),3),
                              'text_accuracy: ',round(epoch_text_accuracy.item(),3))
                       #打印结果有点长，可以使用round(a,3)的方法让a保留小数点后三位
            
#创建空的列表来储存损失值和准确率从而可以在图表中展示
train_loss=[] #创建几个空的列表来存放数据,方便绘图，看看模型怎么样
train_acc=[]
text_loss=[]
text_acc=[]
with torch.no_grad():
        。。。#如上
        train_loss.append(epoch_loss)
        train_acc.append(epoch_accuracy)
        text_loss.append(epoch_text_loss)
        text_acc.append(epoch_text_accuracy)
```

##### 使用训练数据以及验证数据

将所有的数据集切分成训练数据以及验证数据，使用python中的机器学习库`sklearn`

```python
from sklearn.model_selection import train_test_split

train_x,train_y,text_x,text_y=train_text_split(X,Y) #顺序不能变，默认时将25%的数据划分为测试数据
#然后分别建立训练以及测试的ds以及dl
```

##### 创建自己的图像数据集

详情请见相应笔记



---





#### 卷积

##### 卷积层`nn.Conv2d(in_channel,out_channel,ksize)`

卷积层有三个参数：

- ksize：卷积核的大小
- strides：卷积核移动的跨度
- padding：是否进行边沿填充

多通道的卷积是所有通道卷积完之后相加再取激活函数

卷积核一般以随机小数矩阵的形式初始化，在网络的训练过程中卷积核将学习得到合理的权值。共享权值(卷积核)带来的直接好处是减少网络各层之间的连接，同时又降低了过拟合的风险

<img src="C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210912091127338.png" alt="image-20210912091127338" style="zoom:150%;" />

##### 池化层`nn.MaxPool2d((w,h))`

也被叫做**子采样**。通常有均值子采样(mean pooling)和最大值子采样(max pooling)两种形式。子采样可以看作一种特殊的卷积过程。卷积和子采样大大简化了模型复杂度，减少了模型的参数

##### dropout层

随机丢弃一些神经元相当于创建了一个新的模型，每次训练都丢弃一些，相当于每次都是新的模型所以可以提高泛化能力，抑制过拟合（dropout只是在训练过程中有效，在使用模型时还是使用全部的神经元进行计算）

1. dropout可以取到取平均的作用

2. 减少神经元之间复杂的共适应关系

3. 增加了模型的适应能力

   减少神经元之间复杂的共适应关系:因为dropout程序导致两个神经元不一定每次都在一个dropout网络中出现。这样权值的更新不再依赖于有固定关系的隐含节点的共同作用，阻止了某些特征仅仅在其它特定特征下才有效果的情况。

***用drop的话一定要区分训练模式和预测模式 (会影响dropout层和BN层)，model.train()代表训练模式，model.eval()代表预测模式***

![image-20210912095617747](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20210912095617747.png)

```python
self.drop=nn.Dropout(0.5) #因为在linear使用的dropout，所以就用普通的就行，参数为丢弃掉的单元数（0.5就是50%）,一般添加在模型的后半部分

model.train()
for x,y in trainloader:  
    ...
model.eval() 
 with torch.no_grad():                  
             for x,y in textloader:
                ...
```

训练完后看结果会发现过拟合现象有了一定的抑制作用，但不是很明显，这时候可以加入更多的dropout层，加dropout2d加在卷积层的后面

##### 批标准化

  在传统的机器学习中也叫归一化，一般是将数据映射到指定的范围，用于去除不同维度数据的量纲以及量纲单位

  有些数据的差距特别大，如体检时的身高体重和红细胞数目相比，这时候就要去量纲，实现归一化

  对机器学习来说，归一化可以让模型能关注数据之间的对应关系或者逻辑而不是数值的取值范围，对于新数据能更方便的读取，有两种方法：标准化和归一化

- 归一化：将数值变成在0~1之间 如ToTensor方法

- 标准化：将数据减均值，除方差，变成一个标准正态分布
- 批标准化：不仅将数据输入模型之前对数据进行标准化，还在网络的每一次变换后考虑标准化，将每一个层的输出结构进行标准化，是一种训练优化方法
  - 批标准化能够解决梯度消失问题：如要使用sigmoid函数，若sigmoid的输入很大梯度就很小学习速率就很慢，所以要将每一层都变到0~1之间
  - 批标准化也可以抑制过拟合，可以提高学习速率

实现批标准化使用BN层`nn.BatchNorm1d()`以及`nn.BatchNorm2d()`

批标准化的实现过程：

1. 求每一个训练批次数据的均值

2. 求每一个训练批次数据的方差

3. 数据进行标准化

4. 训练参数y，β

5. 输出y通过y与β的线性变换得到原来的数值

在训练的正向传播中，不会改变当前输出，只记录下y与β.

在反向传播的时候，根据求得的y与β通过链式求导方式，求出学习速率以至改变权值



***对于一般的网络结构来说，一般是卷积激活批标准化，对于层数比较多的模型，bn层是不可或缺的***

---



#### 使用GPU加速计算



```python
#先将模型放到显卡上
if torch.cuda.is_available():
    model.to('cuda')#直接把整个模型放在了显卡上
    #或是
    model=model.cuda()
#再在fit函数中将x,y放在显卡上
x,y=x.to('cuda'),y.to('cuda')

    
    
    
device=torch.device("cuda:0"if torch.cuda.is_available() else "cpu") #要不就是第0个显卡，要不就是cpu
#再在fit函数中加入(训练和验证都要加)
x.to(device),y,to(device)
```

都要写







---



#### TIPS

- 可以用`next(iter(train_dl))`的方法直接得出切好的每一片的值，可以用来进行测试、

- 在模型训练完毕想要使用时也要先声明模型在测试模式`model.eval()`

- `xml=open(r'{}'.format(path)).read() *#这么做防止输入的字符串转义*`

- 中括号的使用：

  ```python
  X_data=data[[c for c in data.colomuns  if c!='left']]
  
  xml_name=[x.split('\\')[-1].replace('.xml','') for x in anno]
  
  labels=[to_labels(p) for p in anno]
  
  np_img_2[np_img_2>0]=1 #将图像中所有不为0的像素值设成1方便进行二分类。
  
  all_labels=[label_to_index.get(name) for name in image_name]#将字符串编码成数字
  ```

- 一定不要多次使用同一个变量名，否则若是有一个打错了就会死活发现不了

- 注意各种函数方法的括号，不要忘记加了

- 多注意逗号，缩进等小细节处的错误

- 根据数据集的路径获得数据集的所有种类以及将他们进行数字和名字之间的转换：

  ```python
  anno=glob.glob(r'D:\数据集\宠物数据集\dataset\annotations\xmls\*.xml')#获取所有标签目录
  xml_name=[x.split('\\')[-1].replace('.xml','') for x in anno]#首先对地址通过 // 拆开取最后一项再将后缀替换为空，对标签中的所有地址进行这个操作
  
  species=[]
  for i in xml_name:
      a=i.split('_')[0]#观察得知每个数据的名字都是教 ***_10 前面是名字后面是数字构成，所以用_ 分割后取第一个
      if (a not in species):#列表的一个应用
           species.append(a)
              
  species_to_idx=dict((v,k) for k,v in enumerate(species))#根据种类找到序号        ！！注意两个参数要交换位置！！
  idx_to_speic=dict((c,j) for j,c in species_to_idx.items())#根据序号找到种类
  
  #然后使用时使用中括号，就可以方便的准换了
  idx_to_speic[0]=‘Abyssinian’
  species_to_idx["Abyssinian"]=0
  ```

- 模型输入的目标值如果维度为1的话要去掉1这个维度（如256x256x1作为输入的话就要将最后那个1维度去掉变成256x256,数组输入也一样)

	![image-20211001111230831](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211001111230831.png)
	
	还需要转化为long类型来输入模型`name2.long()`或`name2.type(torch.long)`因为必须是整数

- .data返回的是一个tensor
  而.item()返回的是一个具体的数值。

- **kwargs:代表任意一个参数，如

  ```python
  class base_con(nn.Module):
      def __init__(self,in_channel,out_channel,**kwargs):#有很多卷积核参数我们不写了用**kwargs表示
          super().__init__()
          self.conv=nn.Conv2d(in_channel,out_channel,bias=False,**kwargs)
          ...
          
  #在使用时就可以
  self.b1x1=base_con(in_channel,64,kernel_size=1)
  #就可以像这样直接定义这个函数的其他参数
  ```

