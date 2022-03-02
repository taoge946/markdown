# Ajax

是一种**异步 ** **无刷新技术**，异步和同步的概念如下：

- 同步指的我必须等我给你的请求返回结果了我才能接着往下操作
- 异步就是我发送一个请求出去然后继续做我的事情，等你的响应给我了再去操作你的数据

比如当前我有烧水扫地洗衣服三件事要做，同步就是我在烧水我就必须等着水烧开了才能去干别的，异步就是水去烧，我去扫地等水烧好了我再去处理水

再看**无刷新**：

我们目前有几种请求方式如a标签超链接请求或是表单传输数据的请求，这两个请求鼠标一点页面就刷新了。

就比如说我翻了好久看到了一个之前的说说想点个赞结果一点页面刷新了，我就又要翻好久才能翻到这条说说了，无刷新就是我点个赞我立马就在这个位置看到了我点赞的记录，这就是无刷新结合dom来实现的操作，**ajax经常会与dom一同使用**

就比如说页面上的查看更多，点击后页面并没有刷新只是将下面的内容有通过dom展示出来了



会讲四种请求方式，这四种已经被JQuery封装好了，我们只需要知道参数含义以及如何使用就可以了



## 1.  $.ajax({})

最原始的封装，也是最麻烦的一种，需要填很多的参数,需要指明是get请求还是post请求

![image-20211027140558809](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211027140558809.png)

其中最重要的就是**type**请求方式以及请求的地址**url**和发送到服务器的数据**data**以及请求成功是调用的函数**success**

> 因为ajax是基于JQuery的，所以我们得先将jQuery.js引进来，从官网上下保存下来jquery-3.6.0.min.js后将其导入所需要用的html文件中
>
> ```html
> <script src="jquery-3.6.0.min.js" type="text/javascript" charset="utf-8"></script>
> ```
>
> 

然后就可以在js中调用$.ajax({})了 

  ==注意==：是一个小括号中再加一个大括号

```java
$.ajax({
        type:"post",//请求方式
        url:'data.txt', //请求地址，可以是网页也可以是本地文件，先以本地文件为例
        data:{//请求的数据，json对象
            Username:'testeradmin',//如果没有参数，则不需要设置
            Password:'testerpassword',
        },
        // username:'testeradmin',
        // password:'testerpassword',
        success:function (data){//请求成功时调用的函数，data是一个形参名，代表的是返回的数据
            console.log(data);
            alert('访问成功')
        },
        error:function (data){
            alert('访问失败')
        }
    })
```

![image-20211027151113667](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211027151113667.png)

![image-20211027151047495](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211027151047495.png)

可以看到，访问成功

这里返回的是一个字符串，我们要将其转换为json对象，就变成了json数组了，拿数据就方便了，直接可以根据数组下标拿数据了

```javascript
success:function (data){//请求成功时调用的函数，data是一个形参名，代表的是返回的数据
            console.log(data);
            alert('访问成功');
            var obj=JSON.parse(data) 
            		//将字符串类型的数据转换成json格式，就变成了json数组了，拿数据就方便了，直接可以根据数组下标拿数据了
            console.log(obj);
        },
```



![image-20211027151812922](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211027151812922.png)

>  如果后台返回的数据本身就是json对象读取后就直接是json了不需要再进行转换了，甚至转换了会报错
>
> 这时候们就要用到dataType的属性，表示预期（期望）返回的数据类型。如期望要的是json，在接受到返回值时会自动封装成json对象`dataType:'json',`

拿到这个数据后可以使用dom JQuery操作来创造一个列表

```javascript
//使用JQuery和Dom将获取的数据创一个列表
            var ul=$("<ul></ul>") //使用JQuery可以很轻松的创建列表
            for(var i=0;i<data.length;i++){//遍历所有的对象，得到数组中的每一个元素
                var user=data[i];
                var li="<li>"+user.username+user.userage+"</li>";//创建li
                ul.append(li);//将li放到ul中
            }
            $('body').append(ul);//使用元素选择器“$”将ul放到body标签中去
```

![image-20211027154505537](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211027154505537.png)

此时界面中就有了所创建的列表，也可以点一个按钮来显示数据

## 2.   $.get()

我们已经确定了请求的类型，我们只需要给出请求的地址，请求的参数以及返回的结果就可以了

![image-20211027180759503](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211027180759503.png)

参数的顺序一般都是$.get("请求地址"，“请求参数”，function(形参，用来接受返回的数据){

})

## 3.   $.post()

post就是只是将get换成post就行

##   4.   $.getJSON

要求后台返回一个json格式的数据，语法也与上面的一模一样，但要求返回的数据格式满足json格式(json字符串)

只识别json格式的，如果返回的数据不是json格式的则无法获取



# TIPs

- 在JQuery中，符号"$"为元素选择器，可以直接通过这个符号来选择元素，如`$('body')`就是选择了body标签，如`$("#btn")`就是选择了ID为btn的元素