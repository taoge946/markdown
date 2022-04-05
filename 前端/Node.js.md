# Node.js

node.js的核心是由C/C++编写，标准库由js编写而成，它提供网络，文件，事件等操作，可以认为是一层比较薄的API封装层，实际的操作还是由底层来完成。node.js的底层使用了大量的C/C++代码，是高性能的体现。

Node.js服务端的应用是由以下的部分组成的：

- 通过import或require导入依赖模块
- 创建服务器并设置好事件回调
- 启动服务器



NPM是Node.js中的包管理工具，是用来管理Node.js软件包的工具，能够解决node.js开发和部署中软件包依赖的问题，常见的使用场景有以下几种：

- 从NPM服务器下载别人编写的第三方包到本地进行使用
- 将自己编写的软件包上传到NPM服务器供他人使用。



第一步先换源，将github源换到国内的淘宝源

`npm config set registry https://registry.npm.taobao.org`

使用淘宝源之后，无法使用publish和unpublish指令，如果需要发布软件包和撤销发布的软件包则还需要还原为官方镜像

`npm config delete registry`

> `npm config set registry https://registry.npm.taobao.org`
>  // 配置后可通过下面方式来验证是否成功
>  `npm config get registry`
>  // 或npm info express



# Webpack

在一个文件夹中先`npm init`初始化这个文件夹

然后全局安装webpack和webpack-cli ` npm i webpack webpack-cli -g`

再局部安装` npm i webpack webpack-cli -D`,将webpack添加到package.json中的开发依赖中（webpack所有东西都属于开发依赖，不属于生产依赖，所以-d，等价于--save-dev）

新建俩文件夹，一个src作为源代码的放置目录，build作为代码通过webpack处理打包之后的输出目录

打包需要一个入口文件，所以在src中新建一个入口文件index.js，可以在里面写点东西看能不能运行

```javascript
function add(x,y){return x+y}
console.log(add(5,2)) //随便写点代码
```

想要webpack运行，需要写运行指令，运行指令包括

开发环境指令（在终端中运行）：

`webpack ./src/index.js -o ./build --mode=development`

这行代码的意思就是webpack会以前面的文件为入口文件开始打包，打包后输出到后面的文件夹中，创建一个main.js文件；整体打包环境是开发环境

![image-20220404185838683](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404185838683.png)

可以看出来index.js中已经被引进来了

![image-20220404201934325](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404201934325.png)

生成的main.js中有一行eval代码就是刚才index.js中写的

![image-20220404201408282](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404201408282.png)



如果想要整体打包环境是生产环境，就将development换为production，与开发环境相比多了个压缩，生产环境会压缩js代码

可以在终端使用node指令来执行

![image-20220404201657870](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404201657870.png)

可以在build文件夹中创建一个index，然后引入打包后的main.js，就可以直接运行了

> 经过测试，webpack可以导入js和json文件（通过import， import data from './aaa.json'进来）,不能处理css.img等其他资源

# 遇到的问题：

- 执行`webpack ./src/index.js -o ./build/built.js --mode=development`时无法加载文件

  解决方法：管理员身份打开powershell，设置 Set-ExecutionPolicy RemoteSigned为y