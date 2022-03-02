# GIT 笔记

## 介绍

git是一个分布式版本控制工具

版本控制最重要的就是可以记录文件的修改历史，从而让用户能够查看历史版本。

分布式的意思是每一个电脑客户端就是一个代码库，都可以在本地做版本控制工具。

有一个远程库（代码托管中心），想用的时候克隆一份下来自己改，改完了后再推送到远程库中，保证远程库中的代码永远是最新的。

>  分布式比集中式的优点：
>
> 1.服务器断网的情况下也可以进行开发（因为版本控制是在本地进行的）
>
> 2.每个客户端保存的也都是整个完整的项目，包含历史记录



### Git工作机制

![1645770172530](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645770172530.png)

把工作区的代码添加到暂存区，暂存区的代码提交到本地库了后就会生成历史版本，生成历史版本之后这代码就删不掉了。（git的版本是基于上一个版本的，所以不能删掉上一个版本）

==还有一步是将代码从本地库推送到远程库（push）==



### Git和代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般简称为远程库



## Git命令

![1645783098521](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645783098521.png)

新安装的git必须要设置用户签名和邮箱来区分是谁提交的，否则后面会报错

只是代表了本地的客户端

- ==git init==初始化本地目录

  每次新建一个工程文件夹后都要在该文件夹内初始化，初始化完后会生成一个.git文件夹

- ==git status== 查看本地库状态

  ![1645783700129](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645783700129.png)

  第一句话表示为当前的git是在master这个分支里面

  第二句话表示目前还没有提交过东西

  第三句就是库是空的，什么都没有



>  可以在vim中创建一个txt文件`vim hello.txt`,进去后按开始输入，esc取消，yy复制，p粘贴，：进入命令模式， `:wq`保存并退出 
>
>  `ll`：查看当前目录下的文件，已经有hello.txt了
>
>  `cat hello.txt`: cat查看刚才创的文件 
>
>  `ctrl+l`：清屏
>
>  复制：双击鼠标左键  粘贴：鼠标中键

​	现在再看一下本地库的状态![1645784669786](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645784669786.png)

发现第三行变了，多了一个未被追踪的文件（红色），提醒我们把这个未被追踪的文件添加到暂存区

- ==git add <file>==

  ![1645784866783](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645784866783.png)

  这个警告就是提示自动给换了换行符，从linux的lf换行符转换到windows的crlf换行符



添加了之后，再看本地库的状态：

![1645785058517](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645785058517.png)

此时文件只是存在暂存区里，可以用git rm --cached hello.txt删掉



下一步就是要提交到本地库

- 将暂存区的文件提交到本地库 ==git commit -m "日志信息 " 文件名==

![1645785435080](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645785435080.png)

会显示有几个文件被更改，改了多少行，需要注意的是一个7位的版本号，此时为70e91a8

此时再查看本地库状态：

![1645785610491](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645785610491.png)

已经提交过了，有自己的版本信息了，第二行表示为在提交过以后这个文件既没有新增也没有修改，工作的树是干净的，没有东西需要再次提交

然后就可以查看提交的版本号和日志信息了

- ==git reflog==

![1645785806237](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\1645785806237.png)

也可以通过==git log==查看详细日志，不仅能看到版本，还能看到是谁在什么时间提交的





### 版本更替

当修改本地库中的文件后，再次查看本地库：

![image-20220226161104142](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226161104142.png)

它会提示hello.txt文件被修改了，但是是红色的还没有到暂存区，我们再将它添加到暂存区后这个文件就变绿了

![image-20220226161259317](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226161259317.png)

再放到本地库，修改了一行就相当于是一行新增一行删除

![image-20220226161427502](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226161427502.png)



### 版本穿梭

基本语法：`git reset --hard 版本号` 

先通过reflog看想退回去的版本号，通过这个版本号reset回去

![image-20220226162313420](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226162313420.png)

git的切换版本。底层其实就是移动的HEAD指针



## Git分支

### 分支特性

就比如用户在用一个服务器，同时服务器还需要程序员对服务器进行开发测试维护，但是不能直接动用户的服务器，所以代码就是要多复制几个分支，比如一个分支用户正在用着，一个分支测试，一个分支运维等等

![image-20220226163201666](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226163201666.png)

在版本控制中，有时候会需要同时推进多个任务，为每个任务我们可以创建单独的分支。使用分支以为着程序员可以将自己的工作从开发主线上分离开来，开发自己的分支的时候不会影响主线分支的运行，可以简单的理解为一个分支就是一个单独的副本。

![image-20220226163558460](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226163558460.png)

各个分支是并行的，互不影响，失败的分支直接删掉就行。



### 分支的操作

![image-20220226163807449](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226163807449.png)



#### 分支创建 git branch <分支名>

如果紧急发现有个bug，可以添加一个热修复分支，再查看分支就发现有两个分支了。

![image-20220226164047142](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226164047142.png)

#### 分支转换 git checkout <分支名>

![image-20220226164256162](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226164256162.png)

在hot-fix分支上就可以对文件进行修改，修改完后记得上传暂存区和本地库

此时再切回master分支发现还是原来master分支的内容



#### 分支合并 git merge <分支名>

注意，如果想要b分支合并到a上，就得在a分支下进行操作，如想将hot-fix合并到master上，就在master分支上`git merge hot-fix`

![image-20220226205228355](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226205228355.png)

显示一个文件被修改，1行新增一行删除。然后打开文件就发现两个文件合并了。

> 注意此时是没有合并冲突的，即在hot-fix中没有修改master分支内的代码，仅仅只是增添。



#### 删除分支 git branch -d <分支名>

如果当前分支历史记录太多了可以创建一个新的分支然后把这个很多历史记录的分支删掉，或是创建了一个没用的分支直接将它删掉

![image-20220227094703358](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220227094703358.png)

### 代码合并冲突解决

当多个分支对同一个文件做了多处不同的更改，git无法替我们决定使用哪一个，必须人为决定新代码内容，如两个分支都修改了最后一行，它会报代码冲突

> 好像是同一个文件被同时修改无论是不是同一个位置都会冲突

![image-20220226212412885](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226212412885.png)



现在的状态也发生了变化：master后边多了一个merging表示正在合并中，此时就不能自动合并代码了，得打开文件手动合并了

![image-20220226212445486](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226212445486.png)

![image-20220226212622976](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220226212622976.png)

自己手动选择需要部分的代码，将不需要的部分手动删掉保存，之后还要再提交到暂存区和本地库

> 此时提交到本地库就不能带文件名了

## Idea集成Git





# GitHub

如果想要团队协作，就需要一个代码托管中心，将自己想要clone下来到自己的本地库，将更新完的push回去。这样就可以用pull拉取下来更新本地库代码

或是使用fork将你的远程库的代码叉到我的远程库中，这使就可以操纵远程库来进行自己代码的更新以及席间





## 创建远程库

![image-20220228094025158](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220228094025158.png)

创建远程库别名：远程链接太长了，创建一个别名，以后拉取或者克隆就可以直接对别名使用。可以在穿件之前看一下都有什么别名

![image-20220228094756203](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220228094756203.png)

- 如果想要删除别名：`git remote rm <想要删除的别名>`

## 代码推送 Push

`git push <别名> <分支>`    注意推送的时候最小单位是分支，需要指定推送的分支

由于网络原因可能得推好几次，推上去之后就直接可以在github上看到了

![image-20220228122115733](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220228122115733.png)

![image-20220228122134382](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220228122134382.png)



## 代码拉取 Pull

拉取也可以使用别名来拉取，拉的也是分支

![image-20220302144659075](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302144659075.png)

此时看本地库状态，发现拉取动作会自动提交到本地库

## 代码克隆 Clone

克隆的时候先要拿到github远程库的链接

![image-20220302145023717](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302145023717.png)

然后直接在想放的文件夹内打开git直接进行克隆就行，不需要输入github的账号和密码

![image-20220302145611056](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302145611056.png)

克隆会干三件事：1.拉取代码，2.初始化本地库，3.创建别名

![image-20220302145738690](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302145738690.png)



## 团队协作

### 团队内协协作

多账号协作时想要将代码提交到别人的仓库中需要别人先给权限，需要先加到团队里面

在指定仓库点设置，然后找到Manage access成员管理

![image-20220302150343049](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302150343049.png)

然后找到想加的人把他加进来，加进来后成员管理这就有一个地址函，也是一个链接，把这个链接发给那个人让他打开这个网址然后同意就算加到组里了就可以提交了。这时在这个人的github中也能看到远程库中的项目代码了。

![image-20220302150422419](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302150422419.png)

### 团队外协作

团队外协作就要用fork了，可以把别人的项目叉一份到自己的账户中了，叉过来之后就可以自己进行修改了

![image-20220302151222115](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302151222115.png)

但此时的一切修改都是在自己的账号，如果想要让拉取的地方的人收到自己的代码，可以点这个pull request，把想给的人放到这个里面，然后这个人就会显示有一个拉取请求，可以选择将改的代码合并进来。

![image-20220302153436613](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302153436613.png)

## SSH免密登录

在对远程库进行操作时，除了直接用https链接进行拉取和推送外，还可以使用ssh链接，但第一次会报警告不能用，没有公共的ssh key

![image-20220302154018232](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302154018232.png)

要创建ssh key需要在本地的c盘用户下创建一个.ssh文件.

在下面的文件夹中打开git![image-20220302154338055](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302154338055.png)

然后输入

```git
ssh-keygen -t rsa -C 1169414163@qq.com
```

什么都不用输入，敲3下回车

![image-20220302154655362](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302154655362.png)

然后就会在该文件夹下生成一个.ssh文件夹，里面有一个公钥(.pub)一个私钥,公钥如下：

![image-20220302155353450](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302155353450.png)

我们需要把公钥复制到github账户中，之后这台电脑就可以免密登录这个账号了。

![image-20220302155508106](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302155508106.png)

![image-20220302155636234](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220302155636234.png)

## Idea集成GitHub

（idea是java编辑器）



## Tips

- 如果本地库中不小心放入了大文件那么整个git就显得十分的臃肿，此时可以将整个git删掉再创一个，

  **删掉这个文件夹的整个git：**`find -name ".git" | xargs rm -Rf`

- 如果多次push github上不去 可以试试下面这俩：

  ```csharp
  git config --global http.sslVerify "false"
  git config --global http.postBuffer 524288000
  //这俩分别是解除服务器ssl限制和解除默认限制的推送大小
  ```



# Gitee码云

## 码云创建远程库



## idea集成码云



## 码云链接GitHub进行代码的复制和迁移



# GitLab 基于局域网的代码托管中心



## Gitlab服务器的搭建和部署



## idea集成GitLab









