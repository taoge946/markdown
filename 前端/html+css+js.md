# HTML基础

([web前端开发展示](file:///D:/Markdown笔记/前端/web前端开发.html))可以对着这个看

<link href="D:\webstorm\html project\dist\test.css" type="text/css"rel="stylesheet">

#### 标签

在HTML中标签不区分大小写

- 单独标签：只有一个组成如< br>

- 成对标签：如< p>  < /p>

- 使用标签对某个元素的完整定义语法如下：`<元素名称 属性1=‘值1’.。>元素资料</元素名称>`

- 头部标签< head>< /head>:

  习惯把HTML文件分为文件头和主体文件两个部分，文件头不放置网页的任何内容，而是放置关于HTML文件的信息，包含文件的标题，编码方式以及url等信息，这些信息大部分是用于提供索引，辨认或其他方面的应用

  - 文件标题标签<title></title>定义显示的窗口名称
  - 元信息标签<meta></meta>:meta提供的信息是用户不可见的，一般用于定义页面信息的名称，关键字，作者等。一个head中可以有多个meta，其中name属性主要用于描述网页，以便搜索引擎机器人查找分类。

- 主体标签<body></body>

  属性：

  - text:设定页面文字的颜色
  - bgcolor：设定页面的背景颜色
  - alink(活动链接颜色)
  - link(未访问链接颜色)
  - vlink(已访问链接颜色)

  颜色的设定方法： {rgb(r,g,b);rgb(r%,g%,b%);#rrggbb;#rgb;colorname}

  - topmargin(文档中上边距的大小)
  - leftmargin(文档中左边距的大小)

- 页面的注释： 

  - 在html中：<!--注释的文字-->
  - 在css中：/* 注释的文字*/
  - 在js中：//注释的文字n

#### 文本

###### 文本修饰标记

b:**粗体;**
i：*定义斜体*
u：定义下划线
del：~~定义删除线~~
sup：<sup>定义上标</sup>
sub：<sub>定义下标</sub>
strong：**定义着重文字（和b效果相同）**
em：*定义加重语气（和i效果相同）*
small：<small>变小字号</small>
big：<big>变大字号</big>

###### 计算机输出标记

<p>code：<code>定义计算机代码</code>

kbd：<kbd>定义键盘码</kbd>

samp：<samp>定义计算机代码样本</samp>

tt：<tt>定义打字机代码</tt>

var：<var>定义变量</var>

###### 其他

- `&nbsp`为空格占字符

- 段落`<p> </p>`

- 换行符:但标签`<br>`

- 段落中想要使用复制过来的原有格式使用`<pre> </pre>`

  会将你写的空格换行和字体大小等都原封不动的显示出来

#### 标题和水平线标签

###### h1到h6

越来越小

<h1 align=center>h1</h1>

<h2>h2</h2>

标题的对齐方式：

align属性

center,left,right,justfy(两端对齐)

###### hr

分界线，是个单标签，`<hr>`就可以了

<hr>

有如下属性：

width:px或百分比
size:定义的高度 * px
noshade(无阴影)
color
align



#### 图像和超链接

##### 图像

是单标签

- 图像的添加 <img src='1.jpg' height="200">

  `<img src='1.jpg' height="200">`
  
- 设置边框 `border=""`单位是像素,设置的是边框的大小

- 图像的间距与对齐方式：

  如果不进行换行图片就会紧紧的跟在文字的后面如上图所示 ，所以可以添加图片的水平间距和垂直间距

  - hspace:水平间距，单位是像素
  - vspace:垂直间距

- 图像相对于文字的对齐方式：align:top,middle,bottom,left,center,right

- 图像的提示文字：title="" 鼠标在图像上停留一会后会显示出来的文字

- 图像的替换文字：alt=“” 图像无法显示时所显示的文字<img src="" alt="就像这样">![image-20211013102540833](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211013102540833.png)

  

##### 文本连接（超链接）

是双标签，路径可以是网址也可以是本地的文件

- 基本用法：< a href ="地址"name=" " title=“提示信息”(指向链接的提示信息) target=“窗口名称”>超链接标题< /a >

  target:

  - _self:在当前的框架中打开链接;
  - _blank:在一个全新的空白窗口打开链接
  - _top:在顶层框架中打开链接,也接来理解为在跟框架下打开链接.
  - _parent:在当前框架的上一层打开链接
  - framename:在指定的浮动框架中打开链接，框架名称可自定义

  <a href='http://www.baidu.com' title="百度" target="_self">百度一下</a>

- 书签连接：在网页中添加书签连接，单击文字时特面跳转到指定的位置

  - 第一步：建立书签
  - 第二步：为书签制作连接

- 图像的超链接：< a href=""  target="">< img src="">< /a>

- 图像的热区链接：将图像划分成不同的区域进行不同的链接设置

  用法：

  ```html
  < img src=""usemap="#映射图像名称">
  < map name="映射图像名称">
  < area shape="热区形状"coords="热区坐标"href="URL">
  < /map>
  ```

  shape属性：         		coords属性：
  rect:矩形属性        		x1,y1,x2,y2代表矩形两个顶点坐标
  circle:圆形区域       		x,y,r:圆心坐标和半径。
  poly:x1,y1,x2,xy...xn,yn 代表各顶点的坐标（首尾坐标需相同，形成封闭图形）

> 可以使用超链接来实现js函数或是页内跳转
>
> ==页内跳转==如下：给想要跳转的地方的标签（如div或p等等)一个id，再在href中写"#id",这样就可以实现页内跳转了，代码如下
>
> ```html
> <a href="#dd">点击跳转到最后一个div块</a>
> <div id="dd"></div>
> ```
>
> ==实现js函数==如下：格式为href="javascript:function()",若是不想设置函数可以直接void()使用空函数
>
> ```html
> <script>
> 	function test(){
>         alert("你点击了这个链接")		
>     }
> </script>
> <a href="javascript:test()">单击这个链接触发test函数</a>
> ```
>
> 





#### 表格

表格的标签是<table>  </table>,下一级是<tr>行标签和<td>单元格标签，<th>是表头标志（就是第一行加粗）

<caption> 为表格的标题 </caption>

如下所示，可以单击查看源码，大概样式如下

```html
<table>
    <caption> 表格标题 </caption>
    <tr>
        <th>表头</th>
    </tr>
    <tr>
        <td></td>
    </tr>
</table>
```



<table>
  <caption> 测试表格 </caption>
  <tr>
    <th>第一列</th>
    <th>第二列</th>
    <th>第三列</th>
  </tr>
  <tr>
    <td >11</td>
    <td>12</td>
    <td>13</td>
  </tr>
  <tr>
    <td>21</td>
    <td>22</td>
    <td>23</td>
  </tr>
</table>

##### 表格的样式：

可以设置表格的宽高，对齐方式等，也可以单元格是图片。可以直接在tr或td中进行设定，如

`<tr align="" height="" bgcolor="" >`

> 同时设置tr和td时，该td单元格的属性会替换整行的tr属性
>
> ![image-20211017150659760](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211017150659760.png)

##### 表格的合并与分组：

在复杂的表格中，有些单元格是跨多个列或多个行的，可以使用以下语法进行合并：

`<td colspan="跨的行数">``<td r`

`="跨的列数">`

<table>
  <caption> 测试表格 </caption>
  <tr>
    <th>第一列</th>
    <th>第二列</th>
    <th>第三列</th>
  </tr>
  <tr>
    <td colspan="2">11</td>
    <td rowspan="3">12</td>
    <td>13</td>
  </tr>
  <tr>
    <td>21</td>
    <td>22</td>
    <td>23</td>
  </tr>
</table>

在tr上使用css只能控制行，所以可以使用<colgroup>标签对表格中的列进行控制，可以分别控制每一列的样式

```html
<table>
	<colgroup>
    	<col class=>
        <col class=>
        ...           <!--有几列就设置几个<col>-->
    </colgroup>
</table>
```

表格的边框可以直接用<table border="">不过现在基本都用css来定义边框了



#### 列表

列表的主要标签有：

- `<ul>`无序列表

- `<ol>`有序列表
- `<dir>`目录列表
- `<dl>`定义列表
- `<menu>`菜单列表
- `<dt>` `<dd>`定义列表的标签
- `<li>`列表项目的标签



##### 无序列表

```html
<ul type=“”>  <!-- disc为实心圆，circle为空心圆 square为实心方块-->
    <li type="disc">1</li>
    <li type="circle">2</li>
    <li type="square">3</li>
</ul>
```

<ul type=“”>  <!-- disc为实心圆，circle为空心圆 square为实心方块-->
    <li type="disc">1</li>
    <li type="circle">2</li>
    <li type="square">3</li>
</ul>



##### 有序列表

```html
<ol type=""> <!--type取值：1,a,A,i,I-->
    <li type="1">1</li>
    <li type="a">2</li>
    <li type="i">3</li>
    <li type="I">3</li>
</ol>
```

<ol type=""> <!--type取值：1,a,A,i,I-->
    <li type="1">1</li>
    <li type="a">2</li>
    <li type="i">3</li>
    <li type="I">3</li>
</ol>

> 如果不需要显示前面的符号或数字就将其设成none就行

##### 列表的嵌套

使用dl,dt,dd来实现一种嵌套

```html
 <dl>
    <dt>标题1</dt>
        <dd>内容1</dd>
        <dd>内容1</dd>
    <dt>标题2</dt>
        <dd>内容2</dd>
        <dd>内容2</dd>
  </dl>
```



#### div与span标签

div是块定义，定义一块的内容，span是行内定义，可以在标签内部任意地方使用如

`<p>啊啊啊<span style="color:red;font-size:30px">呃呃呃</span>哦哦哦</p>`div就不能这么用，div直接就生成了一个块,效果如下

<p>啊啊啊<span style="color:red;font-size:30px">呃呃呃</span>哦哦哦</p>

下面是div和span的style属性，大部分和css重合了，现在基本都直接使用css了

<table border="1">
  <tr>
    <th>style属性</th>
    <th>值</th>
    <th>说明</th>
  </tr>
  <tr>
    <th rowspan="5">position</th>
    <th>static</th>
    <th>表示静态定位，默认设置</th>
  </tr>
  <tr>
    <th>absolute</th>
    <th>表示绝对定位，与位置属性配合使用</th>
  </tr>
  <tr>
    <th>relative</th>
    <th>表示相对定位，图层不可层叠</th>
  </tr>
  <tr>
    <th>fixed</th>
    <th>表示图层位置固定，不滚动</th>
  </tr>
  <tr>
    <th>inherit</th>
    <th>规定应该从父元素继承 position 属性的值。</th>
  </tr>
  <tr>
    <th>border</th>
    <th>线粗细，线型，颜色</th>
    <th>边框，可设置风格，粗细，颜色等属性，可按照宽度，样式，颜色一齐定义，如:<a href="http://www.w3school.com.cn/cssref/pr_border.asp">border:5px solid red;</a></th>
  </tr>
  <tr>
    <th>background-color</th>
    <th>rgb(),#ffffff,英文颜色名</th>
    <th>背景颜色</th>
  </tr>
  <tr>
    <th>left(top)</th>
    <th>px或%</th>
    <th>规定层左边(顶部)的距离</th>
  </tr>
  <tr>
    <th>width(height)</th>
    <th>px或%</th>
    <th>规定层的宽度（高度）</th>
  </tr>
  <tr>
    <th><a href="http://www.w3school.com.cn/cssref/pr_class_float.asp">float</a></th>
    <th>right，left，none</th>
    <th>允许浮动元素在左右以及不浮动。float 属性定义元素在哪个方向浮动。以往这个属性总应用于图像，使文本围绕在图像周围，不过在 CSS 中，任何元素都可以浮动。浮动元素会生成一个块级框，而不论它本身是何种元素。如果浮动非替换元素，则要指定一个明确的宽度；否则，它们会尽可能地窄。</th>
  </tr>
  <tr>
    <th>clear</th>
    <th>left,right,both,none</th>
    <th>分别清除左边右边左右两边的浮动和允许左右两边有浮动</th>
  </tr>
  <tr>
    <th>z-index</th>
    <th>auto或数字</th>
    <th>表示子层会按照父层的属性显示/无单位的整数或负数</th>
  </tr>
  <tr>
    <th>overflow</th>
    <th>scroll,visible,auto,hidden</th>
    <th>内容溢出控制。分别表示显示滚动条，不显示滚动条，但超出部分可见，内容超出时显示滚动条，超出时隐藏内容</th>
  </tr>
  <tr>
    <th><a href="http://www.w3school.com.cn/cssref/pr_class_display.asp">display</a></th>
    <th>block,inline,none</th>
    <th>表示按块元素显示，行内方式显示和隐藏</th>
  </tr>
</table>



#### 表单

表单是与用户交互的一个种最有效的方式，在网页种最常见的表单形式主要包括文本框，单选按钮，复选框，按钮等

##### 表单标签`<form>`

表单是网页上的一个特定的区域，这个区域通过`<form> </form>`来定义，这里面的内容可以包含所有的表单控件，还有任何必须的伴随数据，如控件的标签，处理数据的脚本或程序的位置等。

在表单的`<form>`中，还可以设置表单的基本属性，包括表单的名称，处理程序，传送方式等，其格式语法如下：

```html
<form action="" name="" method="" enctype="" target="">
    ...
</form>
```

- action:表单的处理程序，就是将表单中收集到的资料提交到哪，可以是绝对地址也可以是相对地址或其他地址如邮箱地址
- name:这个表单的名称
- method：定义处理程从表单中获取信息的方式，有get和post
- enctype:表单信息提交的编码方式，其属性有text/plain等3种属性
- target:目标窗口的打开方式，可以选择在本窗口打开或新窗口打开

> 可以先通过document获取表单，再用表单名称.某个输入的名称.value获取其输入值
>
> ```javascript
> var formdata=[
>          {
>              "name":form.name.value,
>              "describe":form.describe.value,
>              "exclusive":form.exclusive.value,
>              "mobile":form.mobile.value,
>              "email":form.email.value,
>              "wechat":form.wechat.value
>          }
>      ]
> formdata=JSON.stringify(formdata)
> formdata=JSON.parse(formdata)//这样转换成json格式
> ```
>
>  所有的表单元素都可以通过`.value`属性获得用户的输入值,包括但不限于输入框，文本域文件域，单选以及多选框，和菜单
>
> 与选择相关的表单就要设置value值了，这时选的是哪个选项就返回对应选项的value值

##### 输入标签

输入标签是`<input>`标签，通过设置其type属性值来改变输入方式，根据输入方式的不同可以分为文本框，单/多选框，按钮以及文件和图像域

>  都可以使用css来改变其样式

###### 文本框

1.单行文本框

```html
<input type="text" name="input1" size="20" maxlength="5" value="请输入文字">
```

<input type="text" name="input1" size="20" maxlength="5" value="请输入文字">

![image-20211019211424468](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211019211424468.png)

2.密码输入框:输入的字符全部被遮挡

```html
<input type="password" name="input1" size="20" maxlength="5" value="请输入文字">
```

###### 单选框和多选框

1.单选框:

在一个form域中，相同name的所有单选框智能同时选一个值

> name必须一致，value的值为选择该按钮时表单所提交的值

标记了checked的为初始的选择值，如果标了多个以最后一个为准

```html
<form action="">
    <input type="radio" value="单选按钮的值" name="all" checked>全选
    <input type="radio" value="单选按钮的值" name="all" >全不选
    <input type="radio"name="all">其他
</form>
```

<form action="">
    <input type="radio" value="单选按钮的值" name="all" checked>全选
    <input type="radio" value="单选按钮的值" name="all" >全不选
    <input type="radio"name="all">其他
</form>
2，多选框

和单选框类似，不过可以多个属性被checked,也可以不需要name属性了，因为可以多选

```html
<form action="">
    <input type="checkbox" value="单选按钮的值" name="all" checked>全选
    <input type="checkbox" value="单选按钮的值" name="all" >全不选
    <input type="checkbox"name="all" checked>其他
</form>
```

<form action="">
    <input type="checkbox" value="单选按钮的值" name="all" checked>全选
    <input type="checkbox" value="单选按钮的值" name="all" >全不选
    <input type="checkbox"name="all" checked>其他
</form>

###### 按钮

分为普通按钮以及提交按钮和重置按钮

1.普通按钮

```html
<input type="button" value="所显示的按钮的值" name="按钮名" onclick="js的处理程序">
```

<input type="button" value="所显示的按钮的值" name="按钮名" onclick="js的处理程序">

![image-20211019212935326](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211019212935326.png)

2.提交按钮

```html
<input type="submit" name="按钮名" value="提交">
```

<input type="submit" name="按钮名" value="提交">![image-20211019213252532](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211019213252532.png)

>  点击提交后会将这个表单内的所有值给提交，不需要设置onclick属性

3.重置按钮

```html
<input type="reset" name="按钮名" value="重置">
```

<input type="reset" name="按钮名" value="重置">![image-20211019213640417](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211019213640417.png)

> 点击重置后会将这个表单的所有内容恢复至默认值

###### 文件域和图像域

1.图像域

指可以应用在提交按钮位置上的图片，这个图片具有按钮的功能，语法如下：

```html
<input type="image" src="jjlin1.jpg" name="" class="image-input">
```

![image-20211020162522601](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211020162522601.png)

> 需要在图片上ps上需要的文字，这个不显示文字
>
> name属性来设置所要代表的按键，如submit提交，button普通按钮等，默认为button

2.文件域：

在上传文件时常常用到，可以通过表单将本地中的文件上传，语法如下：

```html
<input type="file" accept="" name="touxiang">
```

<input type="file" accept="" name="touxiang">![image-20211020163403200](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211020163403200.png)

- accpet:所接受的文件类别，有26种选择，可以省略但不能自定义文件类型
- name:文件传输的名称，和其他控件加以区分，其他控件可以通过这个名称来使用这个上传的文件

> 获取所上传的文件的方法为：
>
> ```javascript
> var file=document.getElementById('file').files[0]//file为设置的文件域的id
> //如果想在页面中预览，可以创建一个div再用fileReader来展示
> var reader=new FileReader()
> reader.readAsDataURL(file)
> reader.onload=function (e){
>  var result=document.getElementById('result')
>  result.innerHTML='<img src="'+this.result+'"alt="" style="height: 480px;width: 360px"/>'
> }
> ```
>
> 如果想同时上传多个文件，只需要在input中加一个`multiple`就可以同时上传多个文件了（用shift一次选中多个文件同时进行上传而不是一次一张上传很多次），想要获取它们的内容可以：
>
> ```javascript
> var file=document.getElementById('file')
> for(var i=0;i<file.files.length;i++){
> 	file_now=file.files[i]
> }
> ```
>
> 大部分的服务器都是以文件file格式的对象来处理数据的，所以我们要将图片转换为文件格式，首先是通过fileReader获取base64格式的图片内容`reader.result`,再通过函数转换为文件格式上传到服务器。
>
> ```javascript
> var reader=new FileReader()
> reader.readAsDataURL(file)
> reader.onload=function (e){
>   var result=document.getElementById('result')
> 	 var file=dataURLtoFile(reader.result)  //这就是所获得的file格式的文件
>      
> function dataURLtoFile(dataurl, filename) {
>         var arr = dataurl.split(','),
>             mime = arr[0].match(/:(.*?);/)[1],
>             bstr = atob(arr[1]),
>             n = bstr.length,
>             u8arr = new Uint8Array(n);
>         while (n--) {
>             u8arr[n] = bstr.charCodeAt(n);
>         }
>         return new File([u8arr], filename, { type: mime });
>     }
> ```
>
> 

###### 文本域和列表菜单

1.文本域：可以输入很多的文字，类似于留言板

```html
<textarea name="文本域名称" cols="30" rows="5" >文本域的默认输入内容</textarea>
```

<textarea name="文本域名称" cols="30" rows="5" >文本域的默认输入内容</textarea>

2.列表，菜单

是通过`<select>`和`<option>`来实现的，有以下属性：

- name
- size：在页面中显示的长度
- multiple:是否可以多选
- value:选项的值
- selected:默认被选中的选项



```html
<select >
      <option value="" selected>选项1</option>
      <option value="">选项2</option>
      <option value="">选项3</option>
</select>
```

<select >
      <option value="" selected>选项1</option>
      <option value="">选项2</option>
      <option value="">选项3</option>
</select>


#### HTML5多媒体

可以看这个<a href="D:\webstorm\html project\dist\视频.html">多媒体操作案例</a>

在html5中使用video和audio两个标签来进行多媒体的操作

```html
  <video src="1.mp4" width="640px" height="360px" controls  muted autoplay>您的浏览器不支持video元素</video>
  <audio src="1.flac" controls loop>您的浏览器不支持audio元素</audio>
```

  <video src="1.mp4" width="640px" height="360px" controls  muted autoplay>您的浏览器不支持video元素</video>
  <audio src="1.flac" controls  loop>您的浏览器不支持audio元素</audio>

也可以使用source元素来为同一个媒体文件指定多个播放格式与编码方式

```html
<video width="640" height="360">
	<source src="sample.ogv" type="video/ogg">
    <source src="sample.mp4" type="video/mp4">
</video>
```

type代表媒体类型，其属性值为播放文件的MIME类型



##### 多媒体元素基本属性

- src:媒体文件的地址，可以是本地地址也可以是网络地址

- autoplay:自动播放，视频得有一个mated才能无声播放，音乐不能自动播放

- preload:是否对媒体文件进行预加载，使用预加载可以加快播放速度，其有三个属性

  - none：不进行预加载
  - metedata:值预加载媒体文件的元数据（如字节数，第一帧，播放列表，持续时间等）
  - auto:预加载全部视频或音频

- poster：当视频不可用时可以通过这个属性相用户展示一张图片而不是空白

  ```html
  <video src='' poster='jjlin3.jpg' controls></video>
  ```

  ![image-20211020211944925](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211020211944925.png)

- loop:指定是否循环播放视频或音频，都可以直接用但在typroa中不能循环播放

- controls:为媒体文件添加浏览器自带的播放用的控制条，最好都加上除非自己写了一个控制条

- width,height:定义视频的宽高 

###### 用于获取或修改视频当前状态的属性

- currentTime：获取当前媒体的播放位置，也可以通过更改这个属性来修改播放的位置

  (直接video.currentTime=20;)就是跳转到20s

- startTime:用来读取或设置媒体播放的开始时间，通常为0

- duration:来读取媒体文件的总播放时间

- played,pasued,ended**:都是只读属性**，分别用来读取媒体已播放部分的时间段，媒体是否暂停，是否结束

- defaultPlaybackRate:用来读取或修改媒体默认的播放速率

- playbackRate:用于读取或修改媒体当前的播放速率

- volume：用于读取或修改媒体的当前音量，范围为0~1,0为静音，1为最大音量

- muted：用于读取或修改媒体的静音状态，True为静音



###### 多媒体播放时的方法

- 使用play()方法播放视频，并将pasused()方法的值强行设置为0
- 使用pause()的方法暂停视频，并将pasused()方法强行设置为true
- 使用load()的方法重新载入视频，并将playbackRate属性的值强行设置为defaultPlaybackRate的值，并强行将error的属性的值设为null

> > ==***注意：***==
>
> - 若想播放视频，得先用格式工厂将视频转码成MP4的avc格式
>
> ![image-20211020203945908](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211020203945908.png)
>
> - 最好加上controls这个控件，要不然视频或音乐没法播放
>
> - 如果想视频自动播放，得加一个muted,这样网页打开的时候就会自动播放视频了，但是没有声音
>
>   对于音乐好像是浏览器禁止自动播放背景音乐，可以后期通过js实现自动播放
>
> 

###### 实现方法：

```html
<div class="video">
  <video src="1.mp4" width="600px" height="480px" id="videoPlayer" ontimeupdate="progressUpdate()">
  </video>
</div>
<!--进度条和时间显示-->
<div id="barContainer">
  <div id="durationBar">
    <div id="positionBar"><span id="displayStatus">进度条</span></div>
  </div>
</div>
<!--6个工作按键-->
<div class="btn">
  <button onclick="play()">播放</button>
  <button onclick="pause()">暂停</button>
  <button onclick="stop()">停止</button>
  <button onclick="speedUp()">加速播放</button>
  <button onclick="slowDown()">减速播放</button>
  <button onclick="normalSpeed()">正常速度</button>
</div>
<script>
  var video;
  var display;
  window.onload=function (){
    video=document.getElementById("videoPlayer") //通过id来获取指定元素
    display=document.getElementById("displayStatus")
  }
  function play(){
    video.play() ; //定义函数来对应按钮的按动来控制视频
  }
  function pause(){
    video.pause() ;
  }
  function stop(){
    video.pause() ;
    video.currentTime=0; //将视频暂停并将进度条拖到开头
  }
  function speedUp(){
    video.play() ;
    video.playbackRate=2; //将视频的播放速度变为2倍
  }
  function slowDown(){
    video.play() ;
    video.playbackRate=0.5;
  }
  function normalSpeed(){
    video.play() ;
    video.playbackRate=1;
  }
  //进程更新函数
  function  progressUpdate(){
    var positionBar=document.getElementById("positionBar")
    //时间转换成进度条的长度
    positionBar.style.width=((video.currentTime/video.duration) * 100)+"%"
    //将播放时间通过innerHtml方法添加到进度条的span内部，让他显示于页面
    display.innerHTML=(Math.round(video.currentTime*100)/100)+"秒"
  }
</script>
```

<div class="video">
  <video src="1.mp4" width="600px" height="480px" id="videoPlayer" ontimeupdate="progressUpdate()">
  </video>
</div>

<div id="barContainer">
  <div id="durationBar">
    <div id="positionBar"><span id="displayStatus">进度条</span></div>
  </div>
</div>
<div class="btn">
  <button onclick="play()">播放</button>
  <button onclick="pause()">暂停</button>
  <button onclick="stop()">停止</button>
  <button onclick="speedUp()">加速播放</button>
  <button onclick="slowDown()">减速播放</button>
  <button onclick="normalSpeed()">正常速度</button>
</div>
<script>
  var video;
  var display;
  window.onload=function (){
    video=document.getElementById("videoPlayer") //通过id来获取指定元素
    display=document.getElementById("displayStatus")
  }
  function play(){
    video.play() ; //定义函数来对应按钮的按动来控制视频
  }
  function pause(){
    video.pause() ;
  }
  function stop(){
    video.pause() ;
    video.currentTime=0; //将视频暂停并将进度条拖到开头
  }
  function speedUp(){
    video.play() ;
    video.playbackRate=2; //将视频的播放速度变为2倍
  }
  function slowDown(){
    video.play() ;
    video.playbackRate=0.5;
  }
  function normalSpeed(){
    video.play() ;
    video.playbackRate=1;
  }
  //进程更新函数
  function  progressUpdate(){
    var positionBar=document.getElementById("positionBar")
    //时间转换成进度条的长度
    positionBar.style.width=((video.currentTime/video.duration) * 100)+"%"
    //将播放时间通过innerHtml方法添加到进度条的span内部，让他显示于页面
    display.innerHTML=(Math.round(video.currentTime*100)/100)+"秒"
  }
</script>
##### 多媒体元素的重要事件

在利用video或audio元素读取或播放媒体数据时，会触发一系列的事件，如果用js脚本捕捉这些事件，就可以对这些事件进行处理了，对于这些事件的捕捉以及处理，可以按两种方式来进行：

- 一种是监听的方式`addEventListenser(事件名，处理函数，处理方式)`来对事件的发生进行监听，一般处理方式为false，采用bubbing响应方式

- 另一种是直接赋值的方式，事件处理方式为js脚本中常见的获取事件句柄的方式，代码如下：

  ```html
  <video id="video1" src="" onplay="begin_playing()"></video>
  <script>
  function begin_playing(){
    ...
  }
  </script>
  ```



###### 事件介绍：

- play事件：当执行了play()方法时被触发，或元素被设置为autoplay
- pause事件：当执行了pause()方法时被触发
- loadedmetadata:浏览器已加载当前播放位置的媒介数据时触发
- playing事件:正在播放时一直触发
- canplay事件：浏览器能够开始播放媒体，但估计以当前的塑料布不能直接将整个媒体播放完，播放期间还需要缓冲
- canplaythrough事件：浏览器能够播完且不需要缓冲
- timeupdate事件：当前播放位置（currentTime属性）发生改变，可能是自然改变也可能是人为的改变或由于播放不能连续而发生的跳变
- ended事件：将媒体播放完毕所触发的事件
- ratechange事件:默认播放速率或当前播放速率发生了改变时触发
- volumechange：音量发生改变或被静音

###### 事件实例

浏览器在请求媒体数据，下载媒体数据，播放媒体数据，一直到播放结束会触发很多的事件，下面的例子表明了使用listener监听时间更新，播放，暂停和结束并设置了相应的处理函数

```html
<!--使用事件监听所实现的对视频的操作-->
<video src="1.mp4" width="600px" height="480px" id="video2"  ontimeupdate="progressUpdate()"></video>
<!--设置播放按钮和播放时间-->
<button id="playbutton"  style="float: left">播放</button>
<span id="time">进度条</span>

<script>
  //播放暂停功能
  var play2=document.getElementById("playbutton")
  var video2=document.getElementById("video2")
  //显示时间进度
  video2.addEventListener('timeupdate',function (){  //建立一个对于时间更新的监听，随着时间而随时更新
    var timeDisplay=document.getElementById("time");
    timeDisplay.innerHTML=Math.floor(video2.currentTime)+"/"+Math.floor(video2.duration)+"秒"; //显示当前进度和总进度，通过innerHTML来改变这个span中的值从而使它显示出来
  },false)

  play2.onclick=function(){
    if(video2.ended){
      video2.currentTime=0;  //如果媒体播放结束播放时间从0开始
    }
    video2[video2.paused? 'play':'pause']()   //通过三元运算执行播放和暂停
  };
  video2.addEventListener('play',playEvent,false);
  video2.addEventListener('pause',pauseEvent,false); //监听播放和暂停事件
  video2.addEventListener('ended',function (){    //播放结束后停止播放
    this.pause();
  },false);


  //绑定onclick事件，使这一个按钮既能播放又能暂停，还能显示出不同的字
  function  playEvent(){
    video2.play();
    play2.innerHTML="暂停"  //点了播放后播放按键就变成暂停了
  }
  function  pauseEvent(){
    video2.pause();
    play2.innerHTML="播放"
  }

</script>
```

<a href="视频.html">代码案例</a>

可以实现按一下按钮播放，按钮上的值变为暂停，再按一下视频暂停，字变成开始，进度条随时间更新，显示当前的秒数和视频总共的秒数






## TIPS

- 标签的多个属性之间没有逗号，加一个空格就可以了==（一定要加空格，不要加逗号）==，如

  `<img src='测试图片.jpg' height="200">`

- 引入网页超链接时一定不要忘了加https://要不然打不开那个网页



# CSS3

利用CSS技术可以有效的对页面布局，字体，颜色，背景和其他效果实现更加精准的控制



我们所要做的就是告诉CSS１.改变谁　２．改什么　３.怎么改

1.改变谁：就是通过class,id或是att来选择要使用这种css样式的对象，可以是任何的标签

2.改什么：选择要更改标签的属性，如颜色，大小，字体等

3.怎么改：改成什么样，如红色，宋体，5号字体等

- 和html中的**属性名=“属性值”**不同，css中是**属性名：属性值**

- 多个属性值之间用分号隔开

- css导入html的方式：在head中写

  `<link href="test.css" type="text/css"rel="stylesheet">`
  
- 简单的属性也可以直接在标签上用style写出来

  ```html
  <p>啊啊啊<span style="color:red;font-size:30px">呃呃呃</span>哦哦哦</p>
  ```

  

### CSS中的选择器：

- 不同类型 的选择器也可以<del>集体声明</del>(不是集体声明而是包含关系)

  可以集体声明不过得加逗号如h1,h2等，若不加逗号直接空格是包含关系

- 一些要改的多的属性可以写在css文件中，一些小改的属性可以直接`<p style="属性名:属性值">`

#### 属性选择器  [属性=名称]{}

既可以是HTML中的默认属性如<p>的color,font等，也可以是自定义属性

在css文件中：

使用中括号包住属性选择器，可以多个一起定义

```css
[att=a],[att=b],[att=c]{
    width:180px;
    height:182px
}
[color=heiheihei]{
    color:green
}
```

在html文件中

```html
<p color="heiheihei">aaa</p>
<img src="tile-wide.png" att="a">
```

#### 类和ID选择器

- ID选择器：#名称{}
- 类选择器：.名称{}

```css
#max{
  color: aqua;
  font-size: 50px;
}
.bgcolor{
  background-color: blueviolet;
}
```

在使用时就直接将要使用的标签的id=""或是class=""

```html
<p id="max" class="bgcolor">aaa</p>
```

效果为：![image-20211013152240629](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211013152240629.png)



#### 伪类和伪元素选择器

> 注意，使用方法为类名或id名或是标签加冒号“：”再说这些属性，如.test:hover{}

​	当鼠标放在某个元素上，这些元素就会发生变化如当鼠标滑过导航栏时展开导航栏里的内容，这些都离不开伪类选择器，

​	而为元素选择器则是用来修改普通标记无法轻易修改的部分，如一段文字中的第一个文字等

##### 伪类选择器


是css3中已经定义好的选择器，我们不能随意命名，用来对应某种特殊状态的元素如正在单击的元素，鼠标正在经过的元素等，主要有以下四类

- : link:超链接未访问前的样式

- :visited：超链接在被访问后的样式（以上都两种是对“a”标记的伪类选择器）

- :hover：元素在鼠标悬停时的位置

- :active：表示用户正在单击的元素

  `a:link{color:green;}   a:visited{color:yellow;}     a:hover{color:black;}`

这几个是有顺序的，L　V　H　A

使用方法如下：

```css
.test:hover{
  background-color: brown;
  color: white;
}
```

```html
<p class="test"> aaa </p>
```

这样当鼠标移到这个aaa上时背景颜色和字体颜色就会改变

![image-20211014102459298](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211014102459298.png)

![image-20211014102509542](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211014102509542.png)

> ==注意：==若是想对某个大类下的所有小类应用伪类选择器的话:
>
> ```css
> .class1:hover .class2{  /*中间要加一个空格*/
>     float:right
> }                                                                                        
> ```
>
> ```html
> <div class="class1">
>   <div class="class2">aaa</div>
> </div>
> ```
>
> 

##### 伪元素选择器

是用来改变文档中特定部分的效果样式，常用的四种如下：

- :first-letter:设置第一个字符的样式
- :first-line：设置第一行的样式
- :before:在指定内容内部的前端插入内容
- :after:用于在指定对象内部的尾端添加内容

使用如下：

```css
.txt:first-letter{
  font-size: 35px;
  height: 50px;
  line-height: 50px;
  color: brown;
}
```

```html
<p class="txt">我真的是</p>
```

效果如图所示：![image-20211014102651620](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211014102651620.png)

> 通过伪类和伪元素选择器我们可以对所有的自定义的类,id或是标签进行进一步的更改



#### 其他选择器

- E F 包含选择器:匹配所有包含在E标签内部的F标签,可以是任意的合法选择器的组合

  ```css
  ul li{ 	/*这就是对于所有ul内的li的样式进行了定义*/
      
  }
  ul .mr-li{  /*对ul里的所有mr-li类进行定义*/
      
  }
  .mr-cont .mr-block1{
      
  }
  .mr-cont div:hover{ /*对mr-cont类下的所有div块的鼠标滑过实践进行定义*/
      
  }
  ```

  ```html
  <div class="mr-cont">
      <div class="mr-block1">aaaa</div>
    
      
  ```

### CSS样式属性

css属性值中的单位

1. 绝对单位：绝对单位在网页中很少使用，但在特殊场合用绝对单位是必要的，绝对单位包括：英寸(in)厘米(cm)毫米(mm)磅(pt)pica(pc)(1pc=12pt)
2. 相对单位：显示大小不固定，受分辨率或浏览器设置等因素的影响，css中常使用的相对单位包括em，ex，px，%
   - em:表示元素的字体高度，他能根据父元素的font-szie值来确定
   - ex:em的值除以二
   - px:根据屏幕像素点来确定的，不同的分辨率下显示的样式不同。建议整个网页中只出现px或em来实现单位的统一。
   - 是一个相对单位值，一般参考父元素中相同属性的值。

#### 文本属性

1.css字体样式:使用font标记对页面元素进行字体的样式的编辑

| 属性         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| font- size   | 设置字体的大小                                               |
| font-style   | 设置字体的风格:normal,italic(使用斜体文字),oblique(表示使用倾斜字体显示) |
| font-variant | 设置小型的大写字母字体                                       |
| font-family  | 设置字体名（如宋体，黑体等）                                 |
| font-weight  | 设置字体的粗细:normal(表示正常的字体)bold(表示标准的粗体)bolder(表示特粗体(为相对参数))lighter(表示细体（为相对参数）)整数(取值为100,200...900.100最细，400为normal，700为bold) |

2.css文本样式

- 字符间距letter-spacing:长度单位，一般为正数，也可为负数（看浏览器是否支持）
- 行距line-height:length（百分比，数字）
- 首行缩进text-indent:长度（绝对相对长度皆可）单位或百分比单位

3.字符装饰text-decoration：主要用来给文字加上下划线和删除线：none,underline,overline,line-through

```html
<font style="text-decoration:underline">underline</font>
```

4.水平对齐text-align属性:left，right，center，justify（表示两端对齐）

5.垂直对齐vertical-align:top,middle,bottom,text-top,text-boot

	- top:把元素的顶端与行中最高的元素的顶端对齐
	- middle:把此元素放在父元素的中部
	- 把元素的顶端与行中最低的元素的顶端对齐
	- text-top:把元素的顶端与父元素中字体的

#### css颜色与背景

- 颜色： color：

- 背景background属性：

  - background-color：可以是颜色值或是transparent透明

  - background-image:url("图片路径")

  - background-repeat:背景团的重叠覆盖方式，有4种属性：

    background-repeat: repeat/no-repeat（不重复填充）/repeat-x(从左到右填充)/repeat-y（从上到下填充）

  - background-size:背景图像所占背景的大小，可以设置百分比或是像素值

  - background-attachment:设置背景图像是否随滚动条一起滚动。scroll(一起滚动)fixed(文字内容滚动是背景附件固定不滚动。)

    fixed就是这种效果,图像被钉了上去就不动了，你动页面就相当于动图片

    <img src="C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211014200156221.png" alt="image-20211014200156221" style="zoom:33%;" /><img src="C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211014200204089.png" alt="image-20211014200204089" style="zoom: 33%;" />

  - background-position:设置背景图像的具体起始位置，基本用法：background-position:百分数/长度/关键字
    说明：图像的位置一般需要两个值，且用空格分割，两个值的单位用百分比或长度单位。第一个值表示水平位置，第二个值表示垂直位置。也可只设一个位置，另一个值自动为50%或居中。(**定义了attachment后这个属性就不起作用了**)
    关键字取值表：

    - left/center/right:表示水平方向的三个不同的位置
    - top/center/bottom:表示垂直方向的三个不同位置，如果水平竖直仅规定了一个值，则另一个值的默认为center
    - x%,y%:x是水平位置，y是竖直位置左上角是0% 0%
    - xpos,ypos:xpos表示水平位置,ypos表示竖直位置，左上角是0 0

    位置是由两个参数决定的

> background的复合属性：可以使用它一次性的完成背景颜色，图像，重复，位置和附件的设置。
> 基本语法：
>
> `background:background-color background-image background-repeat background-attachment background-positiion;`
> 如：background:rgb(48,146,209) url("名片.jpg") no-repeat center center;



### css的盒模型（框模型）

在网页设计中，每个元素都是长方形的盒子，盒式模型中重要的概念有：边界(margin),边框（border）填充（padding）内容（content）。边界又称为外边界(也称为外补丁，外空白)是盒子边框与页面边界或其他盒子之间的距离。填充又称为内边界，即内容与边框之间的距离。

![image-20211015154934136](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211015154934136.png)

> 我们一般定义的宽和高是content 的宽和高

定义方法：

- 外边距**margin**:对象与对象之间的距离

  `margin-top : `可以分别定义top,bottom，left和right ，也可以一起定义

  定义4个则从顶端开始顺时针`margin:t r b l` 

  如果只定义三个的话`margin:t r l`就是上，左右

  如果定义两个就是上下，左右 

- 内边距**padding**:对象的内容与其边框之间的距离

  定义方法与margin相同，不过padding没有auto，而且不能是负值，margin可以是负值

- 边框**border**:(必须得给样式style才能显示出边框来，否则就显示不出来)

  - 边框的颜色border-color:

    可以直接设成一个颜色，也可以四个边框颜色不同如`border-top-color`

  - 边框的样式（==必须设置此项才会显示边框==）`border-style:`

    - dashed:虚线
    - dotted(点状边框)
    - solid(定义实线)
    - double(定义双线，双线的宽度等于border-width的值)
    - groove(定义3d凹槽边框，其效果取决于border-color的值)
    - ridge(定义山脊状边框，其效果取决于border-color的值)
    - inset(定义使页面沉入感边框，其效果取决于border-color的值)
    - outset(定义使页面浮出感边框，其效果取决于border-color的值)

    >  边框的样式也可以像颜色一样设置上下左右如border-top-style:

  - 边框的宽度**border-width:**可以是medium,thin,thick或者是具体的长度值

  > 也可以对border直接一步定义
  >
  > `border: width style color`或者对单条边框进行设置 `border-top:`



### css布局常用属性

**浮动float**:在当前块挨住最左边的元素

float: left/right/none

```css
.class1:hover .class2{
  float:right
}
.class1:active .class2{
  float:left
}
```

![image-20211016193043339](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211016193043339.png)

![image-20211016193050440](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211016193050440.png)

![image-20211016193057948](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211016193057948.png)

**定位position**:

position: staic/absolute/fixed/relative

- staic:无特殊定位

- absolute:绝对定位，使用top: right: 等四个方位的属性来确定绝对位置,使用该属性可以让对象漂浮在页面之上，不管嵌套关系和位置

  （就是说用绝对定位就放哪里都行，是按整个网页来定位的）

- fixed:绝对定位，且对象不随滚条移动而改变位置

- relative：相对定位，吃当前块的位置

  > 这个位置可以是负值



如果想确定当前属性在浏览器中的位置可以直接用

```css
.class1{
    left:50px;
    top:100px;
    /*或是*/
    bottom:
    right:
}
```



### CSS的动画与特效

#### **变换tramsform**:

实现平移，缩放，旋转和倾斜等2d变换，有以下属性：

- translate(x px,y px)：2d平移，参数为平移的值
- translateX(),translateX()：只沿一个方向的平移
- scale（X倍数，Y倍数）scaleX(倍数)，scaleY(倍数):沿X轴/Y轴缩放
- skew(X角度 ，Y角度 )，skewX(角度),skewY(角度)：在X轴或是Y轴上的倾斜
- roate(角度)：2d顺时针旋转

> 角度单位为deg,位移单位为px，倍数没有单位

使用如下

```css
.aaa{
    transform:rotate(30deg);
    transform:translate(20px,30px);
    transform:scaleX(2)
}
```

#### **过渡transition:**

实现变换效果的过渡，定义使用什么样的形式进行变换。参数如下：

- transition-proprtey:all/none/指定的进行过渡的css属性
- transition-duration:时间  用于指定过渡的时间
- transition-timing-function: 指定过渡的动画类型
  - linear：线性过渡，也就是匀速过渡
  - ease：平滑过渡
  - ease-in/ease-out :   逐渐加速/逐渐减速
  - ease-in-out:先加速再减速

> 也可以集体定义
>
> ```css
> transform:rotate(30deg)；
> transition:all 1s ease；
> ```
>
> 就是缩放这个旋转平滑过渡持续1s

![image-20211016220348385](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211016220348385.png)

#### **动画animation:**

将上面的变换操作加上数个关键帧，关键帧之间添加变化效果和过渡方法就构成了动画。

需要先定义关键帧：

```css
@-webkit-keyframes aaa {
  from{opacity: 0}
  to{opacity: 1;}
}
```

定义了aaa这个关键帧从完全透明到完全不透明，这样使用from和to可以实现一个状态的转变，from和to种都可以有很多个属性值

第二种办法可以使用百分比来定义关键帧

```CSS
@-webkit-keyframes bbb {
  0%{opacity: 0}
  20%{opacity: 1}
  50%{-webkit-transform: scale(0.8)}
  80%{opacity:1}
  100%{opacity: 0}
}
```

使用时可以在想要使用的css模块中加入一个animation属性

```css
.pic{
    animation: bbb 10s linear infinite
}
```

###### **动画属性：**

- animation:复合属性，下面所有属性的综合
- animation-name:名字
- animation-duration:持续时间 (s) 
- animation-timimg-function:过渡类型如linear，ease等
- animation-delay:动画的延迟时间（s）
- animation-iteration-count:循环多少次，可以填一个数或是infinite无限循环
- animation-direction:是否反向运动,nomarl为正常方向，alternate为反向（好像是这样就从100%->0%）
- animation-play-state:设置动画播放(running)或暂停(paused)
- animation-fil-mode:指定对象动画之外的状态，为动画结束时的状态forwards，开始时的状态backwards,或是默认none以及都both



### TIPs

- 使用css时一定要准确的指定到想要改变样式的对象，比如想改变表格中某一行的所有图片的大小，就不能仅仅只定义一个类然后给tr或是给tr中的td,应该给tr 之内的img,因为要改的就是图片的样式。

  或是直接定义一个类给图片也行，不过那样得一个一个的给所有图片都

  ```css
  .img-background img{
    width: 200px;
    height: 200px;
  }
  ```

  ```html
  <tr class="img-background">
      <td><img src="jjlin1.jpg" alt=""></td>
      <td><img src="jjlin2.jpg" alt=""></td>
      <td><img src="jjlin3.jpg" alt=""></td>
  </tr>
  ```

  

# JavaScript

## JavaScript基础

可以对照着这个看<a href="D:\webstorm\html project\dist\js.html">js案例</a>

### js在html中的使用

在网页中实现js有两种办法，

- 一种是写在网页内部，写在`<script> </script>`这俩之间，这个可以随便放放哪都行（head,body都行），而且还可以放好多个js块，同一个Html中多个js块之间参数和方法共通

- 另一种是从外部文件导入`<script type="text/javascript" src="test.js"></script>`

- 当下的很多库或是框架就是基于js的，我们可以将它们保存下载下来放到项目文件夹中，当js文件来引入，如JQuery库：

  ```html
  <script src="jquery-3.6.0.min.js" type="text/javascript" charset="utf-8"></script>
  ```




### JS的基本内容

1. 执行顺序：

   js程序按照在HTML文件中出现的顺序逐行执行，如果需要在整个HTML文档中执行（如函数，全局变量等）最好将其放在文件的head中

2. JS大小写敏感

3. 每行结尾的分号可有可无

4. 常量使用`const`定义，变量通过`var`定义

5. 如果对一个变量重复定义新的定义会覆盖旧的定义

6. 赋值时null表示一个变量被赋予了一个空值，而undefined则表示这个变量尚未被赋值

### js中的运算符		

1. == 与 ===的区别： 

   == 只对数据表面值是否相等进行，而不判断值得数据类型是否相等，而 ===不仅对值进行判断而且对数据类型也进行判断

   !=与!==也是同理，!=仅仅判断值是否相等而! ==为不绝对等于，值和数据类型都会进行判断

2. 条件运算符：`操作数？结果1：结果2  ` 是js所支持的一种特殊的三目运算符，操作数为真则输出结果1，操作数为假则输出结果2，如之前所用的

```javascript
video2[video2.paused? 'play':'pause']() //如果视频在暂停状态则播放，如果在播放则暂停
										//为真就变成了video2.play()了
```

3. typeof运算符：

   用于返回它的操作数当前的数据类型

4. new运算符：通过new来创建一个新的对象，具体使用方法如下：

   ```javascript
   Object1=new Object //创建一个新的对象
   arr=new Array()//创建一个新的数组对象
   data3=new Data("August 8 2008")//创建一个新的日期对象并给其赋值JS
   ```



### JS中的函数

函数的定义语句通常被放在head中或是外接的js文件中，而函数的调用语句通常会放在body中，如果在函数定义之前调用函数，执行将会出错。

函数的调用方法：

1. 直接在js块内调用，直接写

2. 通过事件触发函数，如单击事件

3. ***通过链接来调用函数***：可以在超链接< a>中调用函数，在< a>的标签中的href值为`"javascript:关键字"`来调用函数，当用户单击该连接时，相关函数将被执行，如下所示：

   ```html
   <script>
   	function test(){
           alert("你点击了这个链接")
       }
   </script>
   <a href="javascript:test()">单击这个链接触发test函数</a>
   ```

   

我们可以在函数中再去定义函数，叫做**嵌套函数**，这样可以使内部函数可以轻松的获得外部函数的参数以及函数的全局变量



#### <p id="p1">JS中的全局函数</p>

- eval():如果参数是表达式，则 eval() 计算表达式。如果参数是一个或多个 JavaScript 语句，则 eval() 执行这些语句
- isNaN():
- parseInt():将字符型转换为整形数字，可以转换为不同的进制，如果字符串不易数字开头则返回NaN
- parseFloat():将字符串转换为浮点型
- encodeURI():将字符串转换为有效的URL链接
- decodeURI():对上面的URL进行解码成字符串，这两个互为逆向操作。



### JS对象编程

最主要的两个对象为Window窗口对象和Document文档对象

- window对象代表的是打开的浏览器窗口，通过window对象可以控制窗口的大小和位置。

- document对象代表浏览器窗口中的文档，是window对象的子对象

#### window对象的使用

(如果只有当前一个窗口使用window对象的方法时可以把window省略)

window对象可以直接调用其方法和属性，语法为

```javascript
window,属性名
window.方法名(参数列表)

window.alert("您暂停了")  //弹出警示框（只有一个确认按键）  可以直接alert()
window.document.write("啊啊啊")//将创建一个新的页面内容只有啊啊啊

window.prompt("请输入您的地址","格式为XX省XX市") //弹出输入框，返回值为你的输入内容，如果没输入或是点取消则返回null
+

window.confirm("请确认") //带取消的确认框,有返回值，点击确认则返回Ture

//也可以这么用
<button onclick='window.alert("您按下了这个按钮")'>点一下试试？</button>
```

![image-20211023212521296](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211023212521296.png)

![image-20211023213603956](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211023213603956.png)

![image-20211023213751481](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211023213751481.png)

<button onclick='window.alert("您按下了这个按钮")'>点一下试试？</button>

> 注意：
>
> 警告对话框是由当前正在运行的页面弹出的，在对该对话框进行处理前不能对当前页面进行操作，并且其后面的代码也不会被执行，只有将警告对话框进行处理后（如单击“确定”按钮或关闭对话框）才能继续对当前页面进行操作，后面的代码才能继续执行，
>
> ```javascript
> function zuhe(){
>   if(window.confirm("你确定要买么？")){
>     var cont=window.prompt("请输入地址","格式为XX省，XX市");
>     if(cont!=null){
>       window.alert("购买成功,订单马上发往"+cont);
>     }else{
>       alert("那真是太可惜了")
>     }
> 
>   }else{
>     alert("那真是太可惜了")
>   }
> ```
>
> 就是先确认再输入再警告，除了alert外，其他的两个函数都有返回值，null就代表为空



还有以下常用的window对象的方法：（windows 下的子类都能用，如表单中输入框可以直接`form1.user.focus()`）

- open():打开新的网址或是本地文件

  ```javascript
  myWindow=window.open('url','target','width=200,height=100');//创建了一个名为mywindow的窗口，额外的参数如长和宽需要用单引号包起来
  ```

  

- close():关闭被引用的对话框

  

- focus():使指定窗口获得焦点`mywindow.focus()`焦点就在mywindow这个窗口上了

  > 常用在表单上，可以指定表单首先需要输入什么

- blur():使窗口不获得焦点（如键盘事件等都还是在原来的网页触发，想要在新窗口触发就得点一下这个新窗口）



- scrollTo(x,y):当指定页面有滚动条时使用这个调整滚动条使界面滚动到指定坐标，x,y就是两个数不带单位代表向下或是向左右拖动多少像素的滚动条。

- scrollBy():和上面的相比这是相对位置，相对当前滚动多少

- ==setTimeout(timer)==:在指定的毫秒数后调用函数,只执行一次

  ```javascript
  setTimeout(function(){ alert("Hello"); }, 3000);
  ```

- ==setInterval(timer)==:每过指定的时间，都会触发函数

  ```javascript
  setInterval(function(){ alert("Hello"); }, 3000);
  ```

- moveTo(x,y):将目标窗口移动到指定位置

- moveBy(x,y):将目标窗口相对移动

- resizeTo(x,y):改变目标窗口的大小。（不能设置那些不是通过 window.open 创建的窗口）

- resizeBy(x,y):改变当前窗口的大小，可以是负值如`MyWindow.resizeBy(-100,100)`就是使宽减100高加100变成了100*300了

> 改变窗口的基本上都对主窗口没有用，只对使用open打开的窗口有用



##### screen对象：

screen对象时js中的屏幕对象，用来返回屏幕的各种参数，有以下属性width,height为当前屏幕的宽和高，pixelDepth为当前屏幕的每个像素的位数，colorDepth为当前显示器的色深，availWidth和availHeight为当前显示器的可用宽度和高度（除去任务栏之后的高度）



##### 访问窗口历史

利用history对象可以实现访问窗口历史，history对象是一个只读的URL字符串数组，主要用来储存一个最近所访问的网页的URL地址的列表，常用的属性以及方法如下：

- length:历史列表的长度
- current:当前文档的URL
- next：历史列表的下一个URL
- previous：历史列表的前一个url

方法：

- back():退回到前一页
- forward():重新进图下一页
- go():进入指定的网页,参数为数字，正数为向下移动，负数为向前移动

> 可以利用超链接标签a 和js来实现在页面中跳转
>
> ```html
> <a href="javascript:window.history.forward()">forward</a>
> <a href="javascript:window.history.go(1)">forward</a>
> 
> <a href="javascript:window.history.go(window.history.length-1)">末尾</a>//可以这样跳转到最新的网页
> ```
>
> 



#### Document文档对象

文档对象（Document）代表浏览器窗口中的文档，该对象是window的子对象（可以直接window.document来访问），document对象可以访问HTML中的包含任何HTML标记中的内容，如表单，图像，表格和超链接等。

其常用属性有：（括号中的内容可以省略）

- alinkColor属性：`(参数名=)document.alinkcolor(=设定的颜色)`用来获得或改变当鼠标放在链接上的颜色
- linkColor属性：`(参数名=)document.linkColor(=设定的颜色)`:用来改变或获取页面中未被单击的链接的颜色
- vlinkColor属性：`(参数名=)document.vlinkColor(=设定的颜色)`:用来获取或改变被点击过的链接的颜色

> 以上三个属性都已经废弃了，有些浏览器可能不支持，可以直接使用css进行编辑

可以使用document对象来获取当前页面的信息

```javascript
document.title  :获取页面标题
document.domain  ：获取页面域名
document.URL：获取页面URL
```

![image-20211024205848640](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211024205848640.png)

##### document对象的方法：

- document.open（）：打开一个文档，并接收write和writeln方法创建的页面内容
- close():
- write():向文档中写入HTML或是js语句
- writeln:也是写入，但是以换行符结束（在最后自带一个换行符）
- createElement（）:创建一个HTML标记
- getElementById（）:获取指定ID 的HTML标记



##### document对象的常用事件

事件可以直接使用不用加括号如`a.onblur=function(){}`,方法才用加括号如`a.blur()`是清除a的焦点

- onblur:元素或窗口本身失去焦点时触发

  > 焦点指的是文本输入时的那个一闪一闪的输入杠，如定义一个文本输入框，点击它准备输入的时候它就获得了焦点，点其他的地方使这个输入杠消失了就是失去焦点事件了。

- onchange:改变< select>元素种的选项或其他表单元素失去桥店，并在其获取角点后内容发生改变时触发

- onclick:鼠标单击触发

- **ondblclick**:鼠标双击时触发

- onfocus:任何元素或是窗口本身获得焦点时触发

  （通常和blur()方法一起使用，使其获得焦点后执行相应函数再取消焦点，否则会一直触发这个事件）

  ```html
  <input type="text" id="focus">
  <script>
  	var f=document.getElementById('focus')
      f.onfocuse=function(){
          alert('明智的选择')
          f.blur()//必须加这个否则会无限循环触发焦点事件
      }
  </script>
  ```

  

- `onkeydown`,`onkeypress`,`onkeyup`:键盘时间

- `onmousedown`,`onmousemove`,`onmouseout`,`onmouseover``onmouseup`:鼠标事件

- onload：界面加载完后触发

- onunload:界面卸载后触发

- onreset:单击重置按钮时，在form上触发(form.reset=function(){})

- onsubmit:单击提交按钮时在form上触发

- onresize:窗口的大小发生变化时触发（窗口操作或事件只对使用open打开的生效）

- ***onscroll***:滚动条发生滚动时触发（可以在主窗口生效）

- ***onslect***:选中表单中的文本时触发，如输入文本框或是文本域等所有可以输入文本的地方内容被选中了都会触发。



#### JavaScript事件处理

js是事件驱动的，可以使得在图形界面环境下的一切操作变得简单化，常将鼠标或热键的动作称为事件（Event），对事件进行处理的程序或是函数称为事件处理函数

##### 鼠标事件

鼠标点击或是移动或是停留在对象上锁触发的事件

- 鼠标单击事件`onclick`：鼠标被单击时被触发的事件，是指在鼠标按下之后鼠标在目标上没有移动直到放开鼠标健的这一过程

  单击事件一般应用于button对象，checkbox对象，Image对象，Link对象，Radio对象，Reset对象和Sumbit对象

- 鼠标的按下和松开事件：`onmousedown`和`onmouseup`,前者是在鼠标按下时触发，后者是在鼠标松开后触发

  - 鼠标的移入移出事件：`onmouseover` 和`onmousemove`以及`onmouseleave`前者是当鼠标移动到这个对象上时触发的动作，后者是当鼠标在对象上移动时触发的事件，最后一个是离开对象时触发的事件

  在鼠标移动事件`onmousemove`中，可以用document对象实时读取鼠标在页面中的位置
  
  ```javascript
  event.clientX
  event.clientY//读取鼠标当前所在位置的坐标
  ```
  
  

鼠标事件实例如下

```html
<!--可以通过按键来使用事件-->
<button onmousedown="change()">改变div的值</button>
function change(){
    a.style.width='500px'
}



```

```javascript
var a=document.getElementById('aa')

//也可以直接在指定元素上使用事件
a.onmousemove=function (){
  a.style.backgroundColor='blue'
}
a.onmouseleave=function (){
  a.style.backgroundColor='purple'
}

a.onmousedown=function (){
  a.style.fontSize="100px"
}
a.onmouseup=function (){
  a.style.fontSize="10px"
}
```

> 可以在HTML文件中使用onmousedown来当一个触发，在下面的键盘事件中也同理，当发现你鼠标被点击后进入js程序，在js中根据event.button的值来确定单击的是左键（0）还是右键（2）或是中间(1)
>
> ***注意***：在不同的浏览器中可能会代表不同的意义，如在ie中0为没有按键，1为按下左键
>
> ```html
> <div class="mouse" id="bb" onmousedown="danji_shuangji()">分别用左右键点击试试？</div>
> ```
>
> ```javascript
> var b=document.getElementById('bb')
> function  danji_shuangji(){
> var i=event.button
> if(i==2){
>  b.style.backgroundColor='red'
> }
> if(i==0){
>  b.style.backgroundColor='green'
> }
> }
> ```
>
> **下面的键盘事件也是同理，首先使用键盘按下来触发，再在js函数中判断按下的是什么键**

##### 键盘事件

使用`event.keyCode`来获取键码值，对于一些特殊的键位可以直接用`event,altKey`或`event.ctrlKey`键盘事件包括如下：

- onkeypress事件：键盘上的某个键被按下且释放所触发的事件，一般用于键盘上的单键操作
- onketdown事件：按下时所触发的事件
- onkeyup事件：松开时所触发的事件

> 后两种事件一般用于快捷键的操作

键盘上有键码值，我们可以根据键码值来判断按下的是哪个按键。

**26个常用字母以及数字的键码值**

| **按键** | **键值** | **按键** | **键值** | **按键** | **键值** | **按键** | **键值** |
| -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| A        | 65       | J        | 74       | S        | 83       | 1        | 49       |
| B        | 66       | K        | 75       | T        | 84       | 2        | 50       |
| C        | 67       | L        | 76       | U        | 85       | 3        | 51       |
| D        | 68       | M        | 77       | V        | 86       | 4        | 52       |
| E        | 69       | N        | 78       | W        | 87       | 5        | 53       |
| F        | 70       | O        | 79       | X        | 88       | 6        | 54       |
| G        | 71       | P        | 80       | Y        | 89       | 7        | 55       |
| H        | 72       | Q        | 81       | Z        | 90       | 8        | 56       |
| I        | 73       | R        | 83       | 0        | 48       | 9        | 57       |

**小键盘以及功能键的键码值**

| **按键** | **键值** | **按键** | **键值** | **按键** | **键值** | **按键** | **键值** |
| -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| 0        | 96       | 8        | 104      | F1       | 112      | F9       | 120      |
| 1        | 97       | 9        | 105      | F2       | 113      | F10      | 121      |
| 2        | 98       | *        | 106      | F3       | 114      | F11      | 122      |
| 3        | 99       | +        | 107      | F4       | 115      | F12      | 123      |
| 4        | 100      | Enter    | 108      | F5       | 116      |          |          |
| 5        | 101      | -        | 109      | F6       | 117      |          |          |
| 6        | 102      | .        | 110      | F7       | 118      |          |          |
| 7        | 103      | /        | 111      | F8       | 119      |          |          |

**各种控制键的键码值**

| **按键**  | **键值** | **按键**   | **键值** | **按键**        | **键值** | **按键** | **键值** |
| --------- | -------- | ---------- | -------- | --------------- | -------- | -------- | -------- |
| Backspace | 8        | Esc        | 27       | Right Arrow(->) | 39       | -_       | 189      |
| Tab       | 9        | Spacebar   | 32       | Down Arrow      | 40       | .>       | 190      |
| Clear     | 12       | Page Up    | 33       | Insert          | 45       | /?       | 191      |
| Enter     | 13       | Page Down  | 34       | Delete          | 46       | `~       | 192      |
| Shift     | 16       | End        | 35       | Num Lock        | 144      | [{       | 219      |
| Control   | 17       | Home       | 36       | ;:              | 186      | \|       | 220      |
| Alt       | 18       | Left Arrow | 37       | =+              | 187      | ]}       | 221      |
| Cape Lock | 20       | Up Arrow   | 38       | ,<              | 188      | ""       | 222      |

==键盘的触发一般可以放在body里这样不管目前的焦点在哪都可点击键盘触发事件==

```html
<body class="bg" id="bg" onkeydown="jianpan()">
    <div class="mouse" id="cc" >按按ctrl和alt或a试试？</div>
```



```javascript
function jianpan(){
  if(event.ctrlKey){
    c.style.backgroundColor='yellow'
    c.style.color='black'
  }
  if(event.altKey){
    c.style.backgroundColor='white'
    c.style.color='black'
  }
  if(event.keyCode=='65'){
    c.style.color='red'
  }
}
```

如果想在页面中屏蔽按键或是鼠标的话在body中加了触发后可以使用以下代码：

```javascript
//禁用键盘上的某个按键 
if (event.keyCode==13){
     event.keyCode=0;
     event.returnValue=false;
     alert("当前页面不允许使用回车键")
 }
//也可以禁用组合快捷键
if((event.ctrlKey)&&(event.keyCode==67)){
    event.returnValue=false;
    alert("当前页面不允许使用快捷键复制")
  }

//或是禁用鼠标的左键或右键
function  pingbi(){
  if(event.button==2){
    event.returnValue=false;
    alert("本页面禁止使用鼠标右键")
  }
```

> 注意：在屏蔽键盘单键或是组合键是可以不同alert直接屏蔽就行了，但是屏蔽鼠标右键时要是不加alert就屏蔽失败。





#### JavaScript与表单事件

在扫描检测与操作表单域之前，首先应当确定要访问的表单，JS中有三种方式来访问表单

1. 通过`document.forms[]`按编号访问（从0开始）
2. 通过名称name访问如`document.form1`
3. 通过Id访问`document.getElementById(form)`

如果想继续访问表单中的各个表单元素的某些属性，可以先获得表单，再`.name.属性值`，如下所示：

```html
<form name='form1' id='form'>
    <textarea name=text cols="30" rows="10">ssss</textarea>
</form>
<script>
	document.form1.text.value="aaaaa" //此时文本域中所显示的就是aaaa了而不是ssss
</script>

<!--或是直接设置id，通过ID来确定元素-->
```

>  所有的表单元素都可以通过`.value`属性获得用户的输入值,包括但不限于输入框，文本域文件域，单选以及多选框，和菜单
>
> 与选择相关的表单就要设置value值了，这时选的是哪个选项就返回对应选项的value值



### JavaScript内部对象

js中的内部对象按照使用方法可以分为动态对象和静态对象，在引用动态对象的属性和方法时，必须先使用new关键词来创建一个对象实例，然后才能使用`对象实例名.成员`的方式来访问其属性和方法。

引用静态对象时，不需要先new一个，可以直接访问其属性和方法

#### 1.Object对象

Object对象提供了对象的基本功能，这些功能构成了所有其他对象的基础，而且构造简单，不需要再定义构造函数。

使用object对象可以在程序运行时为js对象随意添加属性，因此可以容易的创建自定义对象

```javascript
obj=new Object([value])//创建一个新的object对象,value为可选项，可以是任意的js数据类型
```

##### Object对象的属性

1. prototype属性：为指定对象添加一个方法，如下所示

   ```javascript
   function array_max(){
     var i,max=this[0]
     for(i=1;i<this.length;i++){
       if(max<this[i]){
         max=this[i]
       }
     }
     return max
   }
   Array.prototype.max=array_max;
   var x=new Array(1,2,3,4,5)
   var y=x.max()
   ```

   正如这个案例所示，为Array对象添加了一个函数`array_max()`作为一个方法，之后对于array的数组对象就可以使用max的方法来求一个数组中的最大值了

2. constructor属性：获得对象声明时的声明类型，如返回事件对象Data,数组对象Array,字符串对象String等

   ```javascript
   x=New String("hi")
   if(x.constructor==String) //就这样可以进行对象类型的判断
       
   //也可以对使用函数创建的对象进行判断
   function MyFnc{
       
   }
   y=new MyFnc;
   if(y.constructor==MyFnc)
   ```

Object对象的方法

1. toLocaleString()方法：有两种用处，

   ​	1. 将指定对象的数据类型转换为字符串类型

   ​	2. 将一堆数组连起来,使用地区特定的分隔符把生成的字符串连接起来，形成一个字符串

   ```javascript
   var arr = new Array(3)
   arr[0] = "George"
   arr[1] = "John"
   arr[2] = "Thomas"
   document.write(arr.toLocaleString())//输出为：George, John, Thomas，因为是中国所以使用逗号链接
   ```

   还有一个toString()方法，直接用`,`来分割或准换类型，不管地区

2. valueOf():返回指定对象的原始值



## JavaScript权威指南

### 1.类型，值和变量

js中的数据类型分为两类，**原始类型**和**对象类型**。原始类型包括数字，字符串和布尔值还有两个特殊的原始值：`null（空）`和`ubdefined(未定义)`

**对象**是属性(property)的集合，每个属性由`属性名=属性值`构成，还有全局对象(global object).

​	普通的js对象(Object对象)是命名值的无序集合。JS同样定义了一种特殊的对象:数组array,表示带有编号的有序集合，数组拥有一些和普	通对象不同的特有行为特性

​	js还定义了另一组特殊的对象：函数，函数和其他对象都不一样，js可以将函数当做普通对象来对待



如果函数用来初始化（使用new来构造）则将其称作**构造函数**（constructor）,每个构造函数都定义了一**类**(class)对象，**类**可以看成对象类型的的子类型。除了数组类（Array）和函数类（Function）外，js还定义了其他三种有用的类：

- 日期Data类：定义了代表日期的对象
- 正则RegExp类：定义了正则表达式
- 错误Error类：定义了表示js程序中运行时的错误和语法错误的对象
- 也可以通过定义自己的构造函数来定义需要的类



JS的类型可以分为原始类型和对象类型，也可以分为可以拥有方法的类型和不能拥有方法的类型，也可以分为可变类型和不可变类型，可变类型的值是可以修改的，如对象和数组；不可变类型为数字，布尔值，null和undefined。**在js中字符串是不可变的**，可以访问字符串的任意位置的文本，但不能修改字符串的内容。



JS可以自动自由的进行数据类型的转换，如在期望使用字符串的地方使用了数字，js会自动将数字转换为字符串（如alert(12345)）



JS的变量是无类型的，变量可以被赋予任何类型的值，不在函数内声明的变量叫做全局变量



在JS中不区分整形与浮点型，所有的数都由浮点型表示



#### JS中的算术运算

js中的复杂运算通过作为***Math***对象的属性顶底函数和常量实现

- `Math.pow(2,53)`,`Math.sqrt(3)`:幂运算，表示2的53次方和开根运算（也可以直接分数次幂来计算开根如：`Math.pow(10,1/3)`就是10开3次根）
- `Math.round()` `Math.ceil()`  `Math.floor` :四舍五入，向上取整以及向下取整
- `Math.abs()`:求绝对值
- `Math.max(a,b,c)`,`Math.min()`:返回最大/最小值 
- `Math.random()`:生成一个0~1的伪随机数
- `Math.E`,`Math.PI`:e和π
- `Math.sin()`，`Math.cos()`:三角函数
- `Math.log(10)/Math.LN2`: log<sub>2</sub>10
- `Math.exp(3)`:e<sup>3</sup>

在js中被零除并不会报错，而是返回一个无穷大(Infinity)或负无穷大，或是用零除以零返回NaN（not-a-number）



#### 日期和事件

使用Data创建事件对象，具体创建方法如下所示：

```javascript
var then=new Data(2011,0,1)//2011年1月1日（顺序是年，月，日，其中月是从0开始到11）
var later=new Date(2021,0,2,17,10,30)//加了小时分钟和秒
var now=new Date()//什么都不加就是获取当前的时间
var elapsed=now-then//日期减法，计算时间间隔的毫秒数
```

结果如下：


```tex
Fri Jan 01 2021 00:00:00 GMT+0800 (中国标准时间)
Sat Jan 02 2021 17:10:30 GMT+0800 (中国标准时间)
Tue Nov 02 2021 19:10:18 GMT+0800 (中国标准时间)
26421018744
```

获取Data对象的指定内容：

```javascript
now.getFullYear()       =2021
now.getMonth()			=10//获取当前的月份(当前是11月但是月份显示要减一，所以11-1=10)
now.getDay()			=2
now.getHours()			=19
```

> 对data对象使用valueOf()会返回从1970年1月1日以来的毫秒数 now.valueOf(),对其他对象使用的话 只是简单返回对象本身



#### 字符串

字符串可以调用的方法：`var s="hello,world"`

- `s.length`:获得字符串的长度，为11（标点也占位置）
- `s.charAt(n)`:字符串中第n+1个元素，等价于`s[n]`
- `s.substring(a,b)`或`s.slice(a,b)`:字符串中第a+1到b之间的所有元素
- `s.slice(-3)`:最后3个字符，rld
- `s.indexOf("l")`:字符l首次出现的位置，为2
- `s.indexOf("l",3)`:在位置3及以后最先出现l的位置，为3
- `s.lastIndexOf("l")`:字符l最后出现的位置，为10
- `s.split(',')`:以逗号","将字符串分开
- `s.replace("h","H")`:全字符替换
- `s.toUpperCase()`:全部变成大写



#### 全局对象

全局对象的属性时全局定义的符号，js程序可以直接使用

- 全局属性：如undefined,Infinity和NaN
- 全局函数：比如eval()；isNaN()；parseInt()等
- 构造函数：如Date(),RegExp(),String(),Object().和Array()
- 全局对象：如Math和JSON

在代码的最顶层--不再任何函数内的js代码，可以使用使用js关键字`this`来引用全局对象：

```javascript
var global=this
```

#### 包装对象

如果直接给数字，字符串或者布尔值属性的话，就像下面所示：

```javascript
var s='aaa'
s.len=3//直接给s这个字符串一个len属性
var t=s.len//这样写的话在运行时t的值为undefined
```

js会忽略你这么直接给他们属性，修改只是发生在临时对象上，而这个临时对象并没有保存下来，存取字符串，数字或是布尔型时创建的对象称作**包装对象**

字符串，数字，布尔值的属性是只读的，不能给他们新的属性

但是若是创建了对象的话就可以给与他们属性值了，如下所示

```javascript
var ss=new String(sssss)
ss.len=5
var t=ss.len//此时就会返回5了
```



#### 原始值和对象

js中的**原始值**（undefined，null，布尔值，数字和字符串）与**对象**（如数组和函数）有着根本的区别。原始值是不可更改的，任何方法都无法更改一个原始值，原始值的比较是值的比较，他们的值相等时他们才相等

对象和原始值不同，首先，他们的值是可以修改的，如下：

```javascript
var o={x:1}//定义一个对象,并有一个x的属性，值为1
o.x=2   //修改这个对象
o.y=3	//再次修改这个对象，为其增加一个新的属性y

var a=[1,2,3] //数组也是可以修改的
a[0]=0    //可以修改数组中的元素的值
a[3]=4	  //也可以给数组添加一个新的元素
```

> 用大括号`{ }`包起来的是对象，用中括号`[ ]`包起来的是数组

对象的比较并非值的比较，即使两个对象包含相同的属性和值他们也不是相等的

我们通常将对象称为引用类型以此来与js中的基本类型相区分,对象的比较是引用的比较，当且仅当他们引用同一个基对象时，他们才相等

```javascript
var a=[]
var b=a //变量b引用同一个数组
b[0]=1  //通过变量b来修改引用的数组
//a[0]此时也变成1了
//a==b 为TRUE因为他们都是引用的同一个数组
```

如果我们想比较两个单独的对象或是数组，就得循环比较他们所有的元素或是属性，全部相同时才是一样的（元素或属性值比较时就同时判断了是不是同一个引用对象了）



#### 格式转换

js中会自动进行格式转换，但是在一些特殊情况或是为了使代码更方便阅读而做**显示类型转换**

```javascript
Number("3")

String(sss)  //或是 sss.toString()  除了null和undefined之外任何值都拥有这种方法,就算是函数或是数组也可以这么用
[1,2,3].toString()//=>"1,2,3"
(function(x){f(x)}).toString//=>"function(x){\n f(x) \n}"

Boolean([]) //只要不是空就是true
object(3)   //=>new Number(3)
```

**隐式的类型转换**：js中的某些运算符会做隐式的类型转换，

如`+`运算符的一个操作数是字符串，他将会把另一个操作数也化为字符串。

一元`+`操作符将字符串转换为数字，

一元`!`运算符将其操作数转换为布尔值并取反，例子如下：

```javascript
x+'' //等价于String(x)
+x   //等价于Number（x）,也可以写成x-0
!!x  //等价于Boolean(x),注意是双感叹号，否则会取反

typeof(now +1)//=>string +将日期转换为字符串
typeof(now -1)//=>number -将日期对象转换为数字

```

**控制输出的小数的格式：**

```javascript
var n=12345.678
//toFixed(n)是直接控制小数点后的位数为n
n.toFixed(0) //不要小数点后面的，而且会四舍五入，返回值为12346
n.toFixed(2)//12345.68
n.toFixed(5)//12345.67800 位数不够会补零
//toPrecision(n)是控制整个数的长度，长度不够的话会使用科学计数法，不足时也会补零,也会四舍五入
n.toPrecision(6)//12345.7
```

还可以使用`paresInt()`和`parseFloat()`



#### 变量

如果在局部变量的作用域内定义了与全局变量同名的局部变量，则局部变量会遮盖全局变量

> 定义全局变量时可以不写var,但声明局部变量时必须用var

> ==注意==：
>
> 看下面的例子，判断js程序输出到底是什么
>
> ```javascript
> var scope='global'
> function(){
>     console.log(scope)//猜一猜这一行会输出什么
>     var scopr='local'
>     console.log(scope)
> }
> ```
>
> 第一个输出不是意象中的global而是undefined,因为局部变量在整个函数体始终是有定义的，只要在作用域内定义了同名的局部变量，就会直接覆盖掉全局变量，但在var时才对同名的局部变量进行赋值，以上代码相当于
>
> ```javascript
> function(){
>     var scope
>     console.log(scope)
>     var scopr='local'
>     console.log(scope)
> }
> ```
>
> 所以一般将函数中声明的局部变量都放在最顶端



### 2.表达式和运算符

初始化数组：`var a=[[1,2],[2,3],[3,4]]`

初始化对象：`var p={x:1.2,y:2.3}`  对象也可以嵌套`var rect={up:{x:2,y:3},down:{x:4,y:6}}`

​	对象的属性的值可以是表达式，属性的名字也可以是字符串(`'rec':4+o.len`)

#### 属性访问表达式：

通过属性访问表达式所得到的是一个对象属性或是一个元租的值，js有两种方法可以获得属性：

```javascript
expression.identifier  //元素.属性
e[a]//元素[属性]

//如下所示：
var o={x:1,y:{z:3}}
var a=[o,4,[5,6]]
o.x 	//=>1
o.y.z	//=>3嵌套的可以这么点下去来求嵌套内的属性
o['x']  //=>1

a[2]["1"]//=>6 a[2]中索引为1的值，与a[2][1]，a['2'][1]结果相同
a[0].x   //=>1 a[0]即o的x属性的值
```



#### 运算符

1.**++**：

`i++`和`++i`是不同的,差别如下

```javascript
var i=1 ,j=++i  //i和j的值都是2
var i=1, j=i++  //i是2，j是1
//--也同理
```

2.**in运算符**：

如果右侧的对象拥有一个名为左操作数的属性名则表达式返回true

```javascript
var point={x:1,y:1}
"x" in point //true

var data=[7,8,9]
'0' in data //true，因为数组有0这个属性值,相当于是data[0]
2 in data   //true 同上，数组的属性可以是数字或是字符串
3 in data   //false 因为这个数组长度是3，只有0,1,2三个属性，没有3这个属性
```

> 这个in不能用来判断一个字符串中是否有某个元素，只能判断有没有指定的属性值

3.**instanceof运算符**：

判断对象是什么类型的对象

```javascript
var d=new Data()
d instanceof Data //true
d instanceof Object//True 所有的对象都是Object的实例
d instanceof Number//false
```

4.**typeof运算符**：

是一元运算符，放在单个操作数的前面，返回值为操作数类型的一个字符串，typeof最常用的用法是写在表达式中：

```javascript
(typeof value=='string')?"'"+value+"'":value//如果value的类型是字符串则给他加上单引号，不是则不加
```

也可以用在Switch语句中。

对于所有的对象和数组的typeof运算结果是object,如果想区分对象的类，则需要使用其他手段如`instanceof`运算符，class特性以及constructor属性

5.**delete运算符**：

用来删除对象属性或是数组元素，没有返回值

```javascript
var o={x:1,y:2}
delete o.x
x in o //=>false

var a =[1,2,3]
delete a[2]
2 in a //=>false ,将a[2]=3这个属性删了
a.length//=>3 注意数组的长度没有改变，虽然上边删了一个数，但是留下了一个空洞' ',数组的长度没有变，可以通过in看这个这个属性中有值么
```

删的是属性而不是元素，更不能直接删var定义的变量



6.**void运算符**：

就是空，可以当做一个空函数在超链接中调用来以此来使得超链接点击后会变颜色

```html
<a href="javascript:void" > </a>
```



7.**逗号运算符**：

可以使for循环多次循环

```javascript
for(var i=1,j=0;i<j;i++,j--)
```





#### **eval()**

一般情况下，eval（）会执行括号内的表达式或是函数，但是==eval()还具有更改局部变量和全局变量的能力==

```javascript
var q='global',p='global'
var geval=eval
function f(){
  var q='local'
  eval('q+="change"')
  return q
}
function g(){
  var p='local'
  geval('p+="change"')
  return p
}
function test(){
  console.log(f(),q)  //输出为 localchange和global改变了局部变量，从local=>localchange 此时有没有eval都无所谓
  console.log(g(),p)  //输出为 local和globalchange改变了全局变量，从global=>globalchange
}
```

> 想要在函数中改变全局变量的话就得先定义一个非限定的eval名字如`var geval=eval`,然后使用这个非限定的eval来处理全局变量`geval('p+="change"')`



### 3.语句

#### 循环

循环可以没有循环体，称为空循环语句，需要加一个分号

for语句不仅可以对数字进行循环，还可以用for来循环遍历链表数据结构，并返回链表中的最后一个对象

```javascript
function tail(o){
    for(;o.next;o=o.next);/*empty*/   //空正文，如果o.next为真就执行o=o.next    就是说如果链表中下一个元素仍存在就使当前元素变为下一个元素
    return o
}
```

和python一样，js也可以使用for(  ' '  in  ' ') for/in循环,可以方便的遍历对象属性成员

```javascript
for (var p in o){//将o中的所有属性名称依次给p
    alert(p+':'o[p]) //输出属性的名字和属性的值
}
```

要注意的是每次循环都会计算for括号里的表达式，如可以用以下的方式将所有对象属性复制至一个数组中：

```javascript
var o={x:1,y:2,z:3}
var a=[],i=0
for(a[i++] in o)/*empty*/ //空正文，但是已经将o中的属性全部给a了 
    
//也可以
for(i in a) console.log(i) 
```

for/in循环并不会遍历对象的所有属性，只有**可枚举**的属性才会被遍历到



#### 跳转以及异常处理

##### 标签语句

语句是可以加标签的，可以通过标签跳转到指定的语句，标签是由标识符和冒号组成（如汇编的跳转）

通过给语句定义标签，就可以在程序的任何地方通过签名引用这条语句，也可以同时对多个语句定义标签，一个语句也可以有多个标签(带有标签的语句还可以带有标签)

```javascript
mainloop: while(){
                ...
                continue mainloop;//跳到下一次循环
                ...
                }
```

break也可以后面跟一个标签跳出当前循环跳到标签语句，但是不管brek带不带标签，它的控制权都无法越过程序的边界，不能从函数内部通过标签来跳转到函数外部。

##### throw语句

异常为当繁盛了某种异常情况或产生错误时产生的一个信号。**抛出异常**就是用信号通知发生了错误或是异常情况，**捕获异常**是指处理这个信号，即采取必要的手段从异常中恢复

在js中，当产生错误或是程序使用throw语句时就会显式的抛出异常，使用`try/catch/finally`语句可以捕获异常

通过throw抛出的异常可以是任意类型的，可以是一个代表错误码的数字，或者包含刻度的错误消息的字符串。一般js中抛出异常时通常采用`Error`类型和其子类型，一个**Error对象**有一个name属性表示错误类型，一个message属性用来存放传递给构造函数的字符串，例子如下所示：

```javascript
function factorial(x){
    //如果输入参数是非法的则抛出一个异常
    if(x<0) throw new Error('x不能是负数')
    //否则计算出一个值并且正常的返回它
    for(var f=1;x>1;f*=x,x--);/*empty*/
    return f
}
```

当抛出异常时，js会立刻停止当前正在执行的程序，并跳转到就近的异常处理程序，如果抛出异常的代码块没有一条相关联的catch从句，解释器会一直向高层检查，如果最后就是找不到，js就将其当做程序错误来处理，并报告给用户。

> 抛异常可以抛中文如`throw "输入不能比设定值小"`



##### try/catch/finally语句

这些语句是js的异常处理机制，try从句定义了需要处理的异常所在的代码块，catch从句跟随在try之后，当try块内部某处发生了异常时，调用catch内的代码逻辑，catch后跟随finally从句，不管try中是否发生异常，finally中的逻辑总是会执行，这三个语块都需要用大括号括起来，实例如下：

```javascript
try{
    //通常这里的代码不会出现任何问题，但有时会抛出一个异常（程序抛或是使用throw抛或是调用方法间接抛）
}
catch(e){
    //try中内容抛出异常时才会来到这里面执行代码
    //这里可以通过局部变量e来获得对Error对象或者抛出的其他值的引用
    //这里可以处理这个异常，也可以忽略这个异常，还可以通过throw重新抛出异常
}
finally{
    //总是会执行，终止try语句块的方法如下：
    //1.正常终止，执行完语句块的最后一条语句
    //2.通过break，continue或return语句终止
    //3.抛出一个异常，异常被catch捕获
    //4.抛出一个异常，异常未被捕获，继续向上传播
}
```

关键字catch后跟了一个小括号中有一个**标识符**e,这个标识符和函数参数很像，当捕获一个异常时 ，把和这个异常相关的值（比如Error对象）赋值给这个参数，它只在catch语句块内有定义

如对上述的factorial函数所抛出的不能是负数异常进行处理：

```javascript
try{
    var n=Number(prompt("请输入一个正整数",""))
    var f=factorial(n)//假如输入是合法的则输出这个数的阶乘
    alert(n+'!='+f)
  }
catch (ex){
    //如果不合法，则执行这里的逻辑
    alert(ex)//告诉用户产生了什么错误，因为之前设置的错误为('x不能是负数')，所以报错也报这个
  }
```

不一定非要用finally，它通常用于清理工作

#### 其他语句类型

##### with语句

在获取网页上的表单中的元素时，可以用如下的方法来访问一个表单的元素：

```javascript
document.forms[0].address.value //这是访问页面中的第一个表单的name为address的用户的输入值
```

如果这种表达式在代码中多次出现，则可以使用with语句将form对象添加至作用域链的顶层：

```javascript
with(document.forms[0]){
    //可以直接访问表单元素
    name.value=''
    address.value=''
    email.value=''
}
```

##### debugger语句

用来在调试程序时产生一个断点方便进行调试，如下：

```javascript
function f(0){
    if (o==undefined) debugger  //这一行代码用于临时调试
}
```

##### 'use strict'

使用严格模式，只能出现在脚本代码的开始或是函数体的开始。严格模型后with不能用，所有变量使用前都得先声明等等等等，代码的规则就变严了



### 4.对象

对象是js的一种基本数据类型，是一种复合值，它将很多值聚合在一起，可以通过名字访问这些值。

对象可以看成属性的无序集合，每个属性都是一个名/值对。属性名是字符串，我们可以把对象看成从字符串到值的映射。

这种数据结构还有很多种叫法，如散列（hash），散列表，字典，关联数组。

> 对象不仅仅是字符串到值的映射，除了可以保持自有的属性，js中的对象还可以从一个称为原型的对象**继承属性**，对象的方法通常是继承的属性，这种==原型式继承==是js的核心特征

js的对象是动态的，可以新增属性也可以删除属性，但他们常用来模拟静态对象以及静态类型语言中的“结构体”

因为对象是可变的，我们通常通过引用而非值来操作对象，如下：

```javascript
var y=x //y和x是对于同一个对象的引用而不是这个对象的副本，所以通过y来修改这个对象也会对x造成影响
```

对象最常见的用法是：创建，设置，查找，删除，检测和枚举。



对于每个属性除了名字和值之外，它们还有一些**属性特性**:可写，可枚举，可配置（是否可以删除或修改属性）



除了包含属性之外，每个对象还拥有三个相关的**对象特性**：

- 对象的原型(prototype)：指向另外一个对象，本对象的属性继承自它的原型对象
- 对象的类（class)：是一个标识对象类型的字符串
- 对象的扩展标记（extensible flag）:指明了是否可以向该对象添加新的属性(ES5)



对象的分类：

- 内置对象：如数组函数，日期和正则表达式都属于内置对象
- 宿主对象(host object):
- 自定义对象：由js代码所创建的对象
- 自有属性：是直接在对象中定义的属性
- 继承属性：是在对象的原型对象中定义的对象



#### 创建对象

可以通过对象直接量，关键字new或Object.create()函数来创建

##### 对象直接量

创建对象的最简单的方式，直接用大括号创建对象，并给出属性名称和属性值

```javascript
var book={
    "main title":"javascript", //因为属性名字中有空格，所以必须加引号用字符串表示
    "for":"all audiences",     //for是保留字（js中有for这个语法），所以必须加引号
    author:{				   //这里的属性值是一个对象
    firstname:"David",   //这里的属性名就可以不加引号了
    lastname:"Flanagan"
	}
}

//对象的属性值可以是任何数据类型，也可以是函数如
var a={
    next:function(){ return 0 },
    t:fllow()
}
//调用这些属性时就相当于调用它们的函数方法 (a.next的值就是0)
```

对象直接量每次运算都会初始化一个新的对象，如果在循环中用了对象直接量会创建很多的对象



##### 通过new来创建对象

直接就new加一个构造函数就可以了，如`var a =new Data()`



##### 原型

每一个js对象（null除外）都和另一个对象想关联，那'另一个对象'就是原型，每一个对象都从原型继承属性。

所用通过对象直接量创建的对象都具有同一个原型对象，并可以通过Object.prototypeKaua获得对原型的引用。通过关键字new创建的对象的原型就是所使用的构造函数的prototype属性的值，如new Array()创建的对象的原型就是Array.prototype



##### Object.crate()

是一个静态函数，使用时只需要传入所需的原型对象就可`var p1=Object.create({x:1,y:2})`      (这里的原型对象就是{x:1,y:2})

下例是通过原型继承来创建一个新的对象

```javascript
function inherit(p){
    if (p==null) throw TypeError()  //首先原型对象不能为空
    if(Object.create)
        return Object.create(p) //如果Object.create方法存在，则直接使用其来创建新的对象，函数到此结束
    var t=typeof p
    if(t!=='object'&&t!=='function') throw TypeError() //必须是函数或是对象才能被继承
    function f(){}  //定义一个空的构造函数
    f.prototype=p   //将原型设置为p
    return new f()	//返回一个原型为p的新的对象
}

inherit(o)//返回了一个继承自原型对象o的属性的新对象
```

> 这个函数返回的新对象继承了参数对象的属性，这个函数的一个作用是防止库函数无意间修改那些不受你控制的对象，从而影响最顶层的对象的属性值。
>
> 像这样继承原型的话更改属性值不会影响原型的属性值，只会影响继承对象自身，而不是原始对象。使用方法如下：
>
> ```javascript
> var o={x:"dont change this value!"}
> library_function(inherit(o)) //这样就可以防止对原型o的修改了，现在是创建了一个新的对象继承o的所有属性值和o没有关系了。
> ```
>
> 通过Object.create()和inherit()可以通过对象来创建的对象，这样创建的对象不会影响其原对象



#### 属性的查询和设置

之前已经提到过，可以使用`.`或是`[]`获得属性的值，获取对象属性的值和给对象的属性赋值时一样的。如果属性名字是非法的（如有空格或是js中的关键字）那就智能通过中括号[]来访问属性的值了，如`a['for']`或是`a['first name']`

##### 继承

js对象具有自有属性，也有一些属性是从原型对象继承而来的。假设要查询对象o的属性x,如果o中不存在x，那么会继续在o的原型对象中查询属性x,若原型对象中也没有x这个属性且自身仍有原型对象，那么就继续向上查询，直到查到x属性或是一个原型是`null`的对象为止，通过这个链可以实现属性的继承

```javascript
var o={}
o.x=1   //给对象o一个x的属性，值为1
var p=inherit(o)//用o作为原型对象创建一个新的p对象
p.y=2
var q=inherit(p)
q.z=3
var s=q.toString() //toString继承自Object.prototype
q.x+q.y  //=>3  虽然在q这个对象中没有定义x和y属性，但它的原型对象中有，在p中找到了y属性，在o中找到了x属性
		 //如果q中有这个属性就不会再向上找了，就是说可以有与原型相同的属性但是不同的值（相同属性名会覆盖，但是原型的属性不会被更改）
```

属性赋值操作先检查原型链，以此判定是否允许赋值操作。例如，如果o继承自一个只读属性x，那么赋值操作时不允许的。

如果允许属性赋值操作，它也总是在院士对象上创建属性或对已有的属性赋值，而不会去修改原型链。

> 在js中，只有查询属性时才会体会到继承的存在，而设置属性和继承无关，这是js的一个==重要的特性==，该特性让程序员可以有选择的覆盖继承的属性
>
> ```javascript
> var a={x:1}
> var b=inherit(a)
> b.y=2
> b.x=5;//覆盖了原来的属性
> a.x //=>1,原型的属性值没有被修改
> ```



如果想获取一个对象的属性的长度但又不知道这个属性有没有被定义可以

```javascript
var len=book&&book.want&&book.want.length  //前两个是看对象和属性值是否存在，如果都存在的话是布尔型的值为1，与长度相与还是长度
```



给内置的构造函数赋值会失败但是不报错

```javascript
Object.prototype=0 //不会报错但也不会进行更改
```



#### 删除属性

delete运算符可以删除对象的属性，它只是断开了属性和宿主对象之间的联系，而不会去操作属性中的属性值，delete只能删除自有属性，而不能删除继承属性，要想删除继承属性得从这个属性的原型上去删除，这样会影响到所有继承自这个对象的对象

> ```javascript
> a={p:{x:1}};
> b=a.p
> delete a.p //这样之后b.x的值仍为1
> ```
>
> 这样已删除的属性的引用依然存在，js在实现时可能会因为这种不严谨的代码而造成内存泄漏，所以==在销毁对象的属性时，要遍历属性中的属性，依次删除==
>
> （因为delete只是断开了链接，这个属性的名字和属性值还在，就可以被b继续调用）

当delete删除成功后或是没有产生任负作用时，会返回一个true

```javascript
delete o.x  //删除成功，返回ture
delete o.x //x属性已经被删除了，无意义，但是也返回true
delete 1 //无意义，但是也返回ture
```

不能删除不可配置的属性，不能删除全局变量或是全局函数



#### 检测属性

js对象可以看成属性的集合。我们经常会检测集合中成员的所属关系来判断某个属性是否存在于某个对象中。

可以通过in运算符，`hasOwnPreperty()`和`propertyIsEnumerable()`方法来完成这个工作，甚至仅通过属性查询也能做到这一点。

> 以下都不能看继承属性，包括in,但是不知道为啥in能看toString...
>
> ```javascript
> var pp={x:1,y:2,z:3}
> var oo=inherit(pp)
> oo.z=5
> ```
>
> 此时看oo的属性就只有z没有x和y，但是如果写oo.x也能返回1，就是使用下面的几种检测方法都查不到x和y除了最后一种!==undefined.最后一种能向上查继承属性



- In运算符：

  ```javascript
  var o={x:1}
  x in o //true
  y in o //false
  "toString" in o //true o继承toString的属性
  ```

- hasOwnProperty()：这个方法用来检测给定的名字是否是对象的自有属性，对于继承属性它将返回false。如`o.hasOwnProperty("x")`为true，`o.hasOwnProperty("toString")`为false

  > 这上下两个方法的属性值必须是字符串，得加引号 
  >
  > （如果是从对象中提取出的属性本身就是字符串了，就不用带了，如`for (i in o)` i为属性就已经是字符串了）

  > 这个与和下面那个与in的区别为**in操作符只要通过对象能访问到属性就返回true。hasOwnProperty()只在属性存在于实例中时才返回true。**
  >
  > 实例化和继承是两个东西，实例就是new了一个新对象。

- propertyIsEnumerable()：是上面那个的升级版，当待检测属性是可枚举的时候才会返回True

  ```javascript
  var o=inherit({y:2})
  o.x=1;
  o.propertyIsEnumerable("x") //true
  o.propertyIsEnumerable("y") //false y是继承来的
  ```

- 还有一种更简单的方法是使用`!==`来判断一个属性是否为undefined  （==这种方法可以查继承属性==）

  ```javascript
  var o={x:1}
  o.x!==undefined //true  o中有属性x
  o.y!==undefined //false o中没有属性y
  ```

  > 注意是`!==`而不是`!=`,两个等号可以区分出undefined和null，出现null时表示为定义了属性但是没赋值，undefined就是没有定义这个属性,有时可以不做区分
  >
  > ```javascript
  > if(o.x !=null) o.x*=2 //如果o有x这个属性且这个属性的值不为空则乘2
  > if(o.x) o.x*=2 //若x不是undefined,null,false," ",0或NaN则乘2
  > ```
  >
  > 



#### 枚举属性

我们经常会遍历对象的所有属性，通常使用for in来循环遍历，ES5中提供了两个更好用的方法

```javascript
var o={x:1,y:2,z:3}
for(p in o) console.log(p) //通过for in循环来遍历

for (p in o){
    if(!o.hasOwnProperty(p)) continue //跳过继承自原型的属性
}
for (p in o){
    if(typeof o[p]==='function') continue //跳过方法
}
```

以下为几个有用的工具函数

```javascript
//复制对象p的所有属性到对象o
function  extend(o,p){  //将对象p的所有属性给o，返回值为对象o (单单执行这个函数就已经改变了对象o的属性了，同时也将对象o返回)
  for(prop in p){
    o[prop]=p[prop]
  }
  return o
}


//复制对象p的所有属性到对象o，如果有重名属性则保留o的属性
function merge(o,p){  //过滤掉o中已存在的属性，只是将o中不存的的p存在的属性给o（不要同名的属性来覆盖本身的属性）
  for(prop in p){
    if(o.hasOwnProperty(prop)) continue; //有同名属性则跳过这个循环，继续下个循环，看下个属性
    o[prop]=p[prop]
  }
  return o
}


//只留下o中与p重名的属性
function restrict(o,p){ //如果o中的属性在p中没有同名属性则从o中删除这个属性
  for (prop in o){
    if(!(prop in p)) delete o[prop]
  }
  return o
}


//删除所有与p重名的o的属性
function subtract(o,p){   //如果o和p存在同名属性，删除o的同名属性
  for (prop in p) delete o[prop]  //因为删除一个空属性不会报错，所以可以这么写
  return o
}

//求o和p的并集，重名对象使用p的属性值
function union(o,p){return extend(extend({},o),p)}
	//返回一个新对象，这个对象拥有在o和p出现过的所有属性（就像是求o和p的并集，如果有重名属性则使用p的属性）

//求o和p的交集，重名对象使用o的属性
function  intersection(o,p){return restrict(extend({},o),p)} 
	//返回一个新对象，这个对象的属性为o和p都有的属性(就像是求o和p的交集，如果有重名属性则使用o的属性)
//之所以要用extend是创建一个新对象来返回，这样的话就不会改变o对象的值了。


//返回一个对象的所有属性名，以数组的形式返回
function keys(o){//返回一个数组，数组中为o中可枚举的所有自有属性的名字
  if(typeof o!=='object') throw  TypeError() //参数必须是对象
  var result=[]  //这是要返回的数组
  for(var prop in o){
    if(o.hasOwnProperty(prop))//判断是否是自有属性
      result.push(prop) //将属性名添加到数组中
  }
  return result
}
```

#### 属性getter和setter

对象是由名字，值和一组特性(attribute)构成的。属性的值可以用getter或是setter代替，由这两种方法定义的属性称作**存储器属性**，它不同于数据属性，数据属性只有一个简单的值。

而储存器属性不具有可写性，如果属性同时具有getter和setter方法那它就是一个读/写属性，如果它只有getter方法name它只有一个可读属性，如果只有一个setter方法，那它是一个只写属性，读取只写属性时总是返回undefined

定义存储器属性最简单的方法时使用对象直接量语法的一种拓展写法：

```javascript
var o={
    data_prop:value,//普通的数据属性
    
    //存储器属性都是成对定义的函数
    get accessor_prop(){/* 这里是函数体*/},
    set accessor_prop(value){/*这里是函数体*/}
}
```

注意，这里没有使用冒号将属性名和函数体分隔开,但在函数体的结束和下一个方法或数据属性之间有逗号分隔。

> 函数体结束要加逗号

存储器属性是可以继承的

存储器属性的应用：智能检测属性的写入值以及在每次属性读取时返回不同值：

```javascript
//这个对象产生严格自增的序列号
var serialnum={
    //这个属性包含下一个序列号
    $n:0, //$符号暗示这是一个私有属性
    
    get next(){return this.$n++;},//返回当前值然后自加
    set next(n){
        if(n>=this.$n) this.$n=n;
        else throw "序列号的值不能比当前值小"
    }
}
```

每次调用serialnum对象的next方法时，相当于读取next属性，就看get，get使返回当前的n并且n加1。

想给序列号n通过next()方法赋值时(如next(5)就是想把n赋成5)就看set，set会判断你想设定的值和当前值的大小，如果你想设定的值大的话就将n的值改为你设定的值，否则抛出异常

> 简单来说就是每次出现`serialnum.next;`都会使n的值加一(可以通过`serialnum.$n`来查看)。如果想给n赋值且给定一些条件（如不能小于现在的n）就可以通过`serialnum.next=n`来赋值
>
> （也可以直接根据serialnum.$n来修改，但是这样就没法加条件了）



#### 属性的特性：

属性除了包含名字和值以外，属性还包含一些表示它们本身是否可写，可枚举和可配置的属性。

所有创建的属性都是可写的，可枚举的和可配置的，且无法对这些特性做修改。本节讲述ES5中查询和蛇者这些特性属性的API，这些API非常重要，因为：

- 可以通过这些API给对象原型添加方法，并将他们设置成不可枚举的，这让他们看起来更像内置方法
- 可以通过这些API给对象定义不能修改或删除的属性，借此锁定这个对象

在本节中，我们将存储器属性的getter和setter方法看成是属性的特性，同样我们可以把数据属性的值同样看成属性的特性。因此，可以认为一个属性包含一个名字和4个特性。数据属性的四个特性是：

- 它的值
- 可写性
- 可枚举性  :指的是使用枚举属性那一章的方法是否可以看到这个属性（如使用for p in o）,p只会显示出可枚举的属性，而获取不了不可枚举的属性。
- 可配置性

存储器属性不具有值特性和可写性，它们的可写性是由setter方法存在与否决定的，所以存储器属性的四个特性是

- 读(get)
- 写入(set)
- 可枚举
- 可配置

为了实现属性特性的查询和设置操作，ES5中定义了一个名为**“属性描述符”**的对象，这个对象代表那4个特性。描述符对象的属性和它们所描述的属性特性是重名的。因此，数据属性的描述符对象的属性有**value**,**writable**,**enumerable**,**configurable**。

存储器属性的描述符对象则用get属性和set属性代替`value`和`writable`。其中`writable`,`enumerable`,`configurable`都是布尔值。get属性和set属性是函数值。

通过调用`Object.getOwnPropertyDescriptor(a,b)`可以获得某个对象a的某个特定属性b的属性描述符：

```javascript
Object.getOwnPropertyDescriptor({x:1},'x')//返回值为{value: 1, writable: true, enumerable: true, configurable: true}

//如果是存储器属性，则前两个属性描述符为get和set
//对于继承和不存在的属性返回undefined
```

> 可以看出Object.getOwnPropertyDescriptor（）只能获得自有属性的描述符，如果要想获得继承属性的特性，需要遍历原型链（Object.getPrototypeOf()）

如果想要设置属性的特性，或是想让新建的属性具有某种特性，需要调用`Object.defineProperty(对象，'属性',{属性描述符})`。传入要修改的对象，要创建或修改的属性的名称以及属性描述符对象：

```javascript
var o={} //创建一个空对象
Object.defineProperty(o,"x",{  //给对象o添加一个不可枚举的属性x
    value:1,
    writable:true,
    enumerable:false,
    configurable:true
});

o.x //=>1
Object.keys(0) //=>[]   属性是存在的，但不可枚举（for/in等方法获取不到x这个属性）

Object.defineProperty(o.'x',{writable:false}) //如果定义对象o的属性x为只读，则对x进行更改时会失败但是不报错
o.x=2 //失败但是不报错

//此时属性依然是可配置的，因此可以通过描述符这种方式对value的值进行更改
Object.defineProperty(o,"x",{value:2})

//现在将x从数据属性修改为存储器属性：
Object.defineProperty(o,'x',{get function(){return 0}})
o.x //=>此时x属性的值就为0了

```

注意，这个方法要么修改已有属性要么修改新建属性，不能修改继承属性。

如果要同时修改或创建多个属性，则需要用

```javascript
Object.defineProperties({}，{
   x:{value:2,writable:true},
   y:{value:3,writable:false},
   r:{get function(){return 0}，
   		enumerable:true}
})
```

这段代码从一个空对象开始，给他添加两个数据属性和一个只读的存储器属性，Object.defineProperties返回修改后的对象。

> 如果对象是不可拓展的，则可以编辑已有的自有属性，但不能给他添加新的属性，
>
> 如果属性时不可配置的，则不能修改它的可配置性和可枚举性（存储器属性则不能修改get和set）。不能将它的可写性从false改为true
>
> 如果数据属性是不可配置且不可写的，则不能修改它的值，但可配置但不可写的可以先通过配置将其改为能写的再改值。



之前实现了一个extend函数可以把对象复制到一个新的对象中，但是这个复制对于属性的描述符并不能进行复制，所以可以对extend方法进行升级

```javascript
Object.defineProperty(Object.prototype,"extend",{ //给Object.prototype添加一个不可枚举的extend方法
  writable:true,
  enumerable:false,//定义为不可枚举的
  configurable:true,
  value:function(o){
    var names=Object.getOwnPropertyNames(o)
    for (var i=0;i<names.length;i++){ //遍历所有的自有可枚举属性
      if(names[i] in this) continue ;//如果属性存在，则跳过
      var desc=Object.getOwnPropertyDescriptor(o,names[i])//获得对象o的所有的属性的描述符
      Object.defineProperty(this,names[i],desc)
    }
  }
})
```



#### 对象的三个属性

每个对象都有与之相关的原型（prototype）,类(class),和可拓展性(extensible attribute)

==property是属性，prototype是原型==

##### 原型属性：

对象的原型属性是用来继承属性的，原型属性实在实例对象创建之初就设置好的。

- 通过对象直接量创建的对象使用`Object.prototype`作为它们的原型
- 通过new创建的对象使用构造函数的prototype属性作为它们的原型（如Data.prototype等）
- 通过Object.create()创建的对象使用其第一个参数作为它们的原型（可以是null）

在ES5中，可以通过`Object.getPrototypeOf()`可以查询它的原型

要想检测一个对象是否是另一个对象的原型（或处于原型链中），请使用`a.isPrototypeOf(b)`方法来判断b是不是继承自a（a是不是b的原型）

> 注意：isPrototypeOf() 和instanceof运算符非常相似 



##### 类属性：

对象的类属性(class attribute)是一个字符串，用以展示对象的类型信息，只有一种简介的方法可以查询它。默认的toString()方法，返回如下格式的字符串

`[object class]`

因此，要想获得对象的类，可以调用对象的toString（）方法,然后提取已返回字符串的第8个到倒数第二个位置之间的字符。所以定义一个classof()函数来进行类的判断



##### 可拓展性：

对象的课拓展性用以表示是否可以给对象添加新属性。所有内置对象和自定义对象都是显式可拓展的，除非将它们转换为不可拓展的。

ES5中定义了用来查询和设置对象可拓展性的函数。通过将对象传入`Object.exExtensible()`来判断对象是否是可拓展的。如果想将对象转换为不可拓展的，需要调用`Object.preventExtensions()`将待转换的参数传进去。

> **注意**：
>
> 1.一旦将对象转换为不可拓展的，就再也无法将其转回可拓展的了
>
> 2.Object.preventExtensions()只影响对象本身的可拓展性，**如果给一个不可拓展的对象的原型添加属性，这个不可拓展的对象同样会继承这些新属性**

可拓展属性的目的是将对象锁定，避免外界的干扰。对象的课拓展性通常和属性的可配置性与可写性配合使用。





`Object.seal()`和`Object.preventExtensions()`类似，Object.seal除了能将对象设置为不可拓展的，还可以将对象所有的自有属性都设置为不可配置的。

也就是说不能给这个对象添加新属性，而且它已有的属性也不能删除或配置，不过它已有的可写属性依然可以设置。对于那些已经封闭(sealed)的对象是不能解封的。可以通过`Object.isSealed()`来检测对象是否封闭。



`Object.fressze()`将更严格的锁定对象--冻结。除了将对象设置为不可拓展的和将其属性设置为不可配置的意外，还可以将它的自有的所有数据属性设置为只读，通过`Object.isFrozen()`来检测对象是否冻结。



`Object.preventExtensions()`,`Object.seal()`和`Object.fressze()`都返回传入的对象，可以通过函数嵌套的方式调用它们

```javascript
var o=Object.seal(Object.create(Object.freeze({x:1}),{y:{value:2,writable:true}})) 
      //创建一个封闭对象包括一个冻结的原型和一个不可枚举的属性
```



#### 序列化对象：

对象序列化是指将对象的状态转换为字符串，也可以将字符串还原为对象。ES5中提供了内置函数`JSON.stringify()`和`JSON.parse()`用来序列化和还原js对象。这些方法都使用JSON作为数据交换的格式。==JSON的全称是JS对象表示法==,它的语法和js对象与数组直接量的语法非常相近 

要注意的是

- JSON.parse()依然只保留字符串形式而不会将它们还原成原始日期对象
- 函数，正则表达式，Error对象和undefined不能序列化和还原
- JSON.stringify()只能序列化对象可枚举的自有属性，对于一个不能序列化的属性来说，在序列化后的输出字符串中会将这个属性省略掉



#### 对象的方法：

所有js的对象都从Object.prototype继承属性（除了那些不是通过原型显式创建的对象）,上文已经提到过一些对象的方法了，如下：

- hasOwnProperty() :看一个对象中是否有某个自有属性
- propertyIsEnumerable():看这个对象中的这个属性是不是可枚举的
- isPrototypeOf()：看这个对象是不是那个对象的原型
- Object.create():创建对象
- Object.getPrototypeOf():查询一个对象的原型

本节将对定义在Object.prototype里的对象方法展开讲解（一些特定的类会重写这些方法）

##### toString()方法：

没有参数，它将返回一个调用这个方法对象值的字符串。在需要将对象转换为字符串的时候，js都会调用这个方法。

默认的toString()方法返回值所带的信息很少(但在检测对象的类型(class)时非常有用)。因此很多类都带有自定义的toString。

- 如当数组转换为字符串时，结果是一个数组元素列表，只是每个元素都转换成了字符串。
- 再比如当函数转换为字符串的时候，得到的是函数的源代码。

有`Array.toString()`,`Data.toString()`以及`Function.toString()`

##### toJSON()方法：

Object.prototype实际上并没有定义这个方法，但对于需要执行序列化的对象来说，JSON.stringify()方法会调用toJSON()方法.如果在待序列化的对象中存在这个方法则调用它，返回值是序列化的结果，而不是原始的对象。

##### valueOf()方法：

与toString()方法非常相似，但往往当js需要将对象转换成为某种原始值而非字符串的时候才会调用它，尤其是转换为数字的时候。

如果在需要使用原始值的上下文中使用了对象，js会自动调用这个方法。和toString（）一样，一些类中内置定义了valueOf（）方法如Data.valueOf()



### 数组

数组是值的有序集合，每个值叫做一个**元素**，而每个元素在数字中有一个位置，以数字表示，称为**索引**。==JS中数组是无类型的，数组元素可以是任意类型==，数组元素甚至也可能是对象或其他数组。JS的数组是动态的，根据需要它们会增长或缩减，并且在创建数组时无需声明一个固定的大小。

JS的数组可能是稀疏的，数组元素的索引不一定要连续。

每个数组都有一个length属性，针对非稀疏数组，该属性就是数组元素的个数。

通过索引访问数组元素一般比通过访问常规的对象属性要快很多。

数组继承自Array.prototype中的属性。

创建数组是通过中括号`[ ]`来创建数组，数组直接量可以是任意的表达式

```javascript
var i=0
var a=[i+1,true,,"a",[4,{x:1}]] //数组中可以有任何东西还可以嵌套，也可以为空如a[2]=undefined

var b=[function(x){return x*x},2,3]//数组中的元素可以为函数，调用时为b[0](x)如b[0](5)=25

var a=new Array(2,4,1,'aa')//也可以通过这种方式来定义数组，如果参数有多个则就是定义数组的元素，如果参数只有一个就是定义一个参数长度的空数组
var b=new Array(5) //定义一个长度为5的空数组
```

> 注意：数组可以使用负数或非整数来索引数组，此时数值将转换为字符串，以这个字符串作为属性名来用，此时这就是常规对象的属性而不是数组的索引了
>
> 但是如果使用非负整数的字符串那就可以直接当做索引来用
>
> ```javascript
> a[-1.23]=true //对a这个数组对象创建一个属性名为'-1.23'的属性且其值为true
> a['1000']=0  //就相当于a[1000]=0
> a[1.0000]   //就相当于a[1]
> ```

越界：当试图查询任何对象中不存在的属性时(如就定义到了a[10]去查询a[11])此时不会报错，但是得到的值为undefined，对象中也存在这种现象。



数组是对象那么就可以从原型中继承元素，在ES5中数组可以定义元素的getter和setter方法。



#### 稀疏数组：

通常数组的length值代表数组中元素的个数，但如果数组是稀疏数组则length的值大于数组个数

注意，当数组直接量中省略值并不会创建稀疏数组，省略的元素在数组中是存在的，其值为undefined,可以用in 操作符检验两者之间的区别

```javascript
var a1=[,,,] //数组是[undefined,undefined,undefined]
var a2=new Array(3) //该数组长度为3但是没有元素
0 in a1 //=>true a1是有0这个属性的，在索引0处有值undefined
0 in a2//=>false a2在索引0处没有元素

var a=[2,] //则a的长度为1，a中没有1这个属性
```

在存在连续逗号的时候，就相当于插入undefined。如[1,,3]和[1,undefined,3]是一模一样的

如果对数组进行跳位赋值隔得位为空(empty)而不是undefined,此时就是稀疏数组了如

```javascript
var a=[1,2,3]
a[4]=3 //此时数组a为[1,2,3,empty,3]
3 in a //=>false 没有3这个属性
4 in a //=>true 有4这个属性
```



#### 数组的长度

每个数组都有一个length属性，它是随着数组的变化动态变化的。

我们还可以对length的值进行更改，可以增加也可以删减，如果设置的length值大于当前的长度会在数组的尾部创建一个空的区域，当设置的length的值小于当前的length时就会将大于length-1的值全删了，如下:

```javascript
var a=[1,2,3]

a.length=5
console.log(a)
a.length=2
console.log(a)
```

结果如下：![image-20211108221014925](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211108221014925.png)

我们也可以对length这个属性设置属性符，如将它改为只读

```javascript
a=[1,2,3]
Object.defineProperty(a,'length',{writable:false}) //此时对length做修改就不起作用了，就相当于与将数组给锁了，无法进行元素的增添了。
```

#### 数组元素的增加删除

添加数组元素萨最简单的方法：为新的索引值赋值如`a[4]='aa'`

也可以使用push（）方法在数组末尾增加一个或多个元素

```javascript
a=[]
a.push("zero","two")//在数组a的末尾添加两个元素,在末尾添加新元素等价于给a[a.length]赋值
```

可以像删除对象属性一样使用delete运算符来删除数组元素：

```javascript
a=[1,2,3]
delete a[1]
1 in a//false 数组索引1并不在数组中定义
a.length//=>3:delete操作并不影响数组长度
```

删除数组元素与为其赋值为undefined是类似的，注意使用delete操作符并不会修改数组的length属性，也不会将元素从高索引处移下来来填充。

- 我们还可以通过设置数组的length值来删除数组末尾的元素。
- 数组还有`pop()`方法，它和push()一起使用，pop以此使数组长度减一，删除最后一个元素并返回被删除元素的值
- 还有一个shift()方法（和unshift()一起使用），从数组头部删除一个元素，但是与delete不同的是shift()将所有的元素向下移1
- sploce()是一个通用的方法来插入，删除或是替换数组元素，它会根据需要修改length属性并移动元素到更高或较低的索引处



#### 数组遍历

使用for循环是遍历数组元素最常见的方法

```javascript
for (var i =0;i<a.length;i++){} //这样的话每次都要查询数组长度，可以优化一下
for (var i=0,len=a.length;i<len;i++){ //这样的话只需要查询一次数组的长度就可以了
 if(!a[i]) continue //跳过null,undefined和不存在的元素
 if(a[i]===undefined) continue //跳过undefined和不存在的元素
 if(!(i in a)) continue //跳过不存在的元素
}
```

还可以使用for/in循环处理稀疏数组：

```javascript
for(var index in sparseArray){
    var value=sparseArray[index] //此时就获取了稀疏数组的索引和值了
}
//因为for in 可以枚举继承的属性名如
var a=[1,2,3]
var b=Object.create(a)	//以a为原型创建b
console.log(b) //此时b没有自有属性，为空{}
for(i in b) console.log(b[i])//但是b[0],b[1]都是存在的，可以直接查询使用b[1]或者用for in来遍历继承的属性名

for(var i in a){
    if(!a.hasOwnProperty(i)) continue //这样就可以跳过继承的属性
}
```

> 通常数组的遍历实现是升序的，但不能保证一定是这样的。特别的如果数组同时拥有对象属性和数组元素，name返回的属性名很可能是按照创建的顺序而不是索引数值的大小顺序。如果算法依赖于遍历的顺序，最好不要使用for in循环而使用常规的for循环。

#### 多维数组

js不支持真正的多维数组，不过可以使用数组的数组来近似。访问数组中的数组只要简单的使用两次中括号[]操作符即可，如`a[x][y]` 



#### 数组方法：

##### 1.join()

Array.join()方法将数组中的所有元素都转换为字符串并链接到一起返回生成的字符串，可以指定一个可选的字符串来在生成的字符串中来分隔各个数组元素，如果不指定则默认使用逗号

```javascript
var a=[1,2,3]
a.join() //=>返回'1,2,3'，默认使用逗号分隔
a.join("")//=>返回'123'

//还可以使用join来进行填充
var b=new Array(5) //创建一个长度为5的空数组
b.join('-')//=>返回'----'
```

Array.join()方法是String.split()方法的逆操作，splite是将字符串按照一定的分割方式将字符串分割成数组

##### 2.reverse()

这个方法将数组中的元素颠倒顺序，返回逆序的数组。它使用的是替换，并没有创建新的数组，而是在原先的数组中重新排列它们如321=>123

##### 3.sort()

这个方法是将数组按照一定的顺序进行排序并返回排序后的数组。当不带参数调用sort（）时，数组元素以字母顺序排序

```javascript
var a=new Arrray('banan','apple','cherry')
a.sort() //返回['apple','banana','cherry']
```

如果数组包含undefined元素，它们会排到数组的尾部

如果数组同时包含大小写的英文字符串，则默认先排大写再排小写

如果想要按照其他方式而非字母表顺序进行排序时必须给sort()方法传递一个比较函数。该函数决定了它的两个参数在排好序的数组中的先后顺序

```javascript
var a=[33,4,1111,222]
a.sort() //返回值按照字母表顺序：1111,222,33,4
a.sort(function(a,b){return a-b}) //按照函数的返回值大于0（a>b，即前面的首数字大于后面的首数字）来进行排序，结果为4,33,222,1111
```

如果要对sort（）设置参数则参数必须为函数

##### 4.concat()

该方法创建并返回一个新数组，它的元素包括调用concat()的原始数组的元素和concat()的每个参数。如果这些参数中任何一个为数组，则链接的是数组的元素而不是数组本身。

注意：concat()不会递归扁平化的数组，也不会修改调用的数组

```javascript
var a=[1,2,3]
a.concat(4,5) //=>返回[1,2,3,4,5],相当于a.concat([4,5])
a.concat([4,5],[6,7])//返回[1,2,3,4,5,6,7]
a.concat(4,[5,[6,7]])//返回[1,2,3,4,5,[6,7]]
//使用concat不会修改a本身，只是返回融合后的数组
```

##### 5.slice()

该方法返回指定数组的一个片段或是子数组，它的两个参数分别指定了片段的开始和结束的位置。返回的第一个参数指定的位置和所有到但不含第二个参数指定的位置之间的所有数组元素。

如果只指定一个参数，返回的数组将包含从参数的位置到数组的末尾

如果参数出现负数，它表示相对于数组末尾的位置

```javascript
var a=[33,4,1111,222]

a.slice(0,2) //返回33,4
a.slice(-2) //返回1111,222
//注意slice也不会改变原数组
```

##### 6.splice()

该方法是在数组中插入或删除元素的常用方法，不同于以上的两种方法concat和slice，splice会改动调用的数组

它的第一个参数指定了插入或删除的起始位置，第二个参数定义了删除元素的个数。如果省略了第二个参数，则将从开始的那个参数之后全删了。

splice()返回一个由删除的元素构成的数组，被更改后的数组仍为原数组

```javascript
var a=[1,2,3,4,5，6,7,8]
a.splice(4) //返回[5,6,7,8] a变为[1,2,3,4]
a.splice(1,2)//返回[2,3],a为[1,4]
```

splice前两个参数指定了需要删除的数组元素，紧接着的后面的任意个数的参数指定为需要插入到数组中的元素

```javascript
var a=[1,2,3,4,5]
a.splice(2,0,'a','b') //第二个位置开始不删元素，添加'a''b'两个元素，返回[].a为[1,2,'a','b',3,4,5]
a.splice(2,2,[1,2],3) //返回['a','b'],a为[1,2,[1,2],3,3,4,5]
//splice可以同时进行删除和增加元素
```

##### 7.push()和pop()

该方法将数组当做栈来使用，push是在数组的末尾添加一个或多个元素(`push(1,2,3)`)，并返回新的数组长度。pop是删除数组的最后一个元素，减小数组长度并返回它删除额值

##### 8.unshift()和shift()

类似于上面的push和pop,不一样的是unshift是在数组的头部而不是尾部进行元素的插入和删除操作。

unshift()在数组的头部添加一个或多个元素，并将已存在的元素移动到更高索引的位置来获取足够的空间，最后返回数组的新长度。

shift()删除数组的第一个元素并将其返回，然后把随后的元素下移一个位置来填充数组头部的空缺

##### 9.toString()和toLocalString()

该方法将其每个元素转化为字符串，并且输出用逗号分隔的字符串列表（和join不一样，这个分隔不能改，只能用逗号）



#### ES5中的数组方法：

ES5中定义了9个新的数组方法来遍历，映射，过滤，检测，简化和搜索数据。

大部分的ES5方法的第一个参数接收一个函数，并对数组的每个元素（或一些元素）调用一次该函数。大多数情况下调用的函数使用三个参数：**数组元素的值**，**元素的索引**和**数组本身**。通常只需要第一个参数值，可以忽略后两个参数。

如果有第二个参数，则调用的函数被看做是第二个参数的方法。也就是说在调用函数时传递进去的第二个参数作为它的this关键字的值来使用。

被调用的函数的返回值非常重要，但是不同方法处理返回值的方式也不一样.

> ES5中的数组方法都不会修改它们调用的原始数组。

##### 1.forEach()

从头至尾遍历数组，为每个元素指定的函数。传递的函数作为forEach()的第一个参数，然后forEach()使用三个参数调用该函数。如果只关心数组元素的值，可以编写只有一个参数的函数

```javascript
var data=[1,2,3,4,5]
var sum=0
data.forEach(function(value){sum+=value}) //将每个值累加到sum上
sum				//为15
data.forEach(function(v,i,a){a[i]=v+1})//数组的每个元素自加一  三个参数分别是v:每个元素的值 i：索引 a：数组本身
data  //[2,3,4,5,6]
```

注意forEach无法在所有的元素都传给调用的函数之前停止遍历，像是break之类的都不好使，如果想提前终止就必须将foreach放到try块中

##### 2.map()

将调用数组的每个元素传递给指定的函数，并返回一个数组，它包含该函数的返回值，例如：

```javascript
a=[1,2,3]
b=a.map(function(x){return x*x}) //b为[1,4,9]  就是将a中的每个元素的值当做参数输入进函数中返回值为b对应位置的元素的值
```

和forEach不同的是map需要有返回值，map返回的是新数组不会修改原来的数组。如果输入为稀疏数组输出也是稀疏数组

##### 3.fliter()

该方法返回的数组元素时调用的数组的一个子集，传递的函数是用来逻辑判定的，返回为true 或是false.如果判断为true或是能转换为true的值，那么当前元素就是这个子集的成员，他将被添加到一个作为返回值的数组中

```javascript
a=[5,4,3,2,1]
smallvalues=a.fliter(function(x){return x<3}) //[2,1]
everyother=a.fliter(function(x,i){return i%2==0}) //[5,3,1] 就是选出能被2整除的索引（a[0],a[2],a[4]）
```

##### 4.every()和some()

是数组的逻辑判定，它们对数组元素应用指定的函数进行判定，返回true或false

```javascript
a=[1,2,3,4,5]
a.every(function(x){return x<10}) //=>true所有的元素的值都小于10
a.every(function(x){return x%2==0})//=>false 不是所有的元素的值都是偶数
```

some()方法就像数学中的’存在‘；当数组中至少有一个元素符合判定条件则返回true，所有元素都不符合则返回false

```javascript
a.some(function(x){return x%2==0})//=>true a中包含偶数
a.some(isNaN) //false a中不包含非数值元素
```

every()在遇见第一个false时停止遍历，some()在遇见第一个true时停止遍历

在空数组上进行遍历时，every返回true，some返回false

##### 5.reduce()和reducceRight()

使用指定的数组元素进行组合，生成单个值，也可称为 ‘注入’ 和 ‘折叠' 

```javascript
var a=[1,2,3,4,5]
var sum=a.reduce(function(x,y){return x+y},0) //数组求和
var product=a.reduce(function(x,y){return x*y},1)//数组求积
var max=a.reduce(function (x,y){return (x>y)?x:y})//数组求最大值
```

reduce需要两个参数，第一个时执行化简操作的函数，化简操作就是用某种方法把两个值组合或者化简为一个值并返回化简后的值。

第二个参数（可选）一个传递给化简函数的初始值，(求和就从0开始加，求积就从1开始乘)，当不设置初始值时它将使用数组的第一个元素作为其初始值

在空数组上不设置初始值调用reduce会报错，如果数组只有一个元素且没有设置初始值则仅仅只会返回那个值而不会进行任何操作



reduceRight和reduce差不多，不过reduceRight是从右向左进行处理

##### 6.indexOf()和lastIndexOf()

搜索整个数组中具有给定值的元素，返回找到的第一个元素的索引，如果没有找到就返回-1.

indexOf()是从头到尾搜索，而lastIndexOf()是从尾到头搜索。

```javascript
a=[0,1,2,1,0]
a.indexOf(1) //1
a.lastIndexOf(1)//3
a.indexOf(3) //-1 没有为3的元素值
```

不同于上面的方法，index不接受一个函数作为其参数。其第一个参数为所需要搜索的值，第二个参数是可选的。它指定数组中的一个索引，从那里开始搜索。如果省略第二个参数则从头开始搜索。对于lastIndexOf()第二个参数也可以是负数,代表与末尾的偏移量。

以下定义一个函数查找在数组中出现过的所有的x，并返回一个包含匹配索引的数组

```javascript
function  findall(a,x){
  var result=[],len=a.length,pos=0;//分别为将会返回的索引值的数组，待搜索数组的长度以及起始位置
  while (pos<len){        //判断是否遍历完整个数组
    pos=a.indexOf(x,pos)  //寻找指定的值
    if(pos===-1)break     //若不存在则直接跳出循环返回空数组
    result.push(pos)      //若在则将索引压进结果中
    pos=pos+1             //位置加一再来一遍看看还有没有
  }
  return result
}
```

注意，字符串也有indexOf()方法和lastIndexOf()方法，功能与数组的类似



#### 数组类型

在ES5中可以通过Array.isArray(a) 来判断a是不是数组

#### 类数组对象

js中的数组有一些特性是其他对象所没有的：

- 当有新元素添加到列表中时，自动更新length属性
- 设置length为一个较小值将截断数组
- 从Array.prototype中继承了一些有用的方法
- 其类属性为"Array"

我们可以将拥有一个数组length属性和对应的非负整数的对象看成一种类型的数组，这种“类数组”虽然不能使用上述的方法也不能通过length完成一些操作，但是仍可以像真正的数组那样去遍历它们。



### 函数

函数的定义包括一个形参，形参在函数体内部像全局变量一样工作，函数调用会为形参提供实参的值，函数使用他们实参的值来计算返回值，成为该函数调用表达式的值。除了实参之外，每次调用还会拥有另一个值--**本次调用的上下文**，这就是**this**关键字的值

> 参数有形参和实参的区别，形参相当于函数中定义的变量，实参是在运行时的函数调用时传入的参数，如
>
> ```javascript
> function test(a,b){   //a,b为实参
>     var i=0;		  //i为形参
> }
> ```

如果函数挂载在一个对象上，作为对象的一个属性，就称它为**对象的方法**。当通过这个对象来调用函数时，该对象就是此次调用的上下文(context)也就是该函数的this值。

用于初始化一个新创建的函数称为构造函数(constructor)

在js里，**函数即对象**，程序可以随意的操控它们。比如js可以把函数赋值给变量，或作为参数传递给其他函数，甚至可以给函数设置属性，调用它们的方法。

js的函数可以嵌套在其他函数中定义，这样它们就可以访问它们被定义时所处的作用域中的任何变量，这意味着js函数构成了一个**闭包(closure)**,它给js带累了非常强劲的变成能力

#### 函数定义

函数使用function关键字来定义，可以有函数名字也可以没有名字作为函数表达式

```javascript
function a(){
    //正常的函数定义方式
}
var a=function(x){return x*x}  //这就是函数表达式的方式定义函数 ，相当于函数名为a,function a(x){return x*x},调用时直接a(x)就可以了

var b=function fact(x){if(x<=1) return 1;else return x*fact(x-1)}//函数表达式也可以有名称，在递归时非常有用

data.sort(function(a,b){return a-b})//函数表达式也可以作为参数传给其他函数
```

通常而言，函数表达式一般不给函数名称，这样会显得比较紧凑，比较适合定义那些只会使用一次的函数。

函数的命名：在js框架jQuery中，就将最常用的方法重命名为`$()`,美元符号和下划线是除字母和数字外两个合法的js标识符



函数声明语句**被提前**到外部脚本或外部函数作用域的顶部，所以function +name()这种方式声明的函数可以被在他定义之前出现的代码所调用，但是函数表达式不能，它得在被定义并赋值给一个变量后，在它下面才可以使用。

大多数函数包含一条return语句，return语句导致函数停止执行并返回它后面的表达式，如果没有表达式则返回undefiend。如果函数中不包含return语句则函数只是按顺序执行每一条代码并最后返回一个undefined给调用者



嵌套函数：在js里，函数可以嵌套在其他的函数里如

```javascript
function test(a,b){
    function square(x){return x*x}
    return Math.sqrt(square(a)+square(b))
}
```

嵌套函数需要注意的是它的变量的作用域规则，它们可以嵌套访问它们的函数的参数和变量。如上面的代码，内部函数square可以读写外部函数test()定义的参数a和b。这些作用域规则对内嵌函数非常重要。



#### 函数调用

构成函数主体的js代码在定义之前并不会执行，只有调用该函数时他们才会执行，有四种方式来调用js函数：

- 作为函数
- 作为方法
- 作为构造函数
- 通过他们的call()和apply()方法间接调用。                    

##### 方法调用

一个方法无非是保存在一个对象属性里的js函数，如果一个函数f和一个对象o，则可以用下面的代码给o定义一个名为m的方法

```javascript
o.m=f//f为函数，o为对象，这是将对象的一个属性赋值为函数
o.m()//这样调用
```

函数调用就是直接调用函数名称，如test(x)

方法调用和函数调用有一个重要的区别：即调用上下文。属性访问表达式由两部分组成：一个对象（o）和属性名称(m)。在像这样的方法调用表达式中，对象o成为调用上下文，函数体可以使用关键字`this`引用该对象，下面是一个例子：

```javascript
var calculator={ //对象直接量
    operand1:1,
    operand2:1,
    add:function(){ //add属性为一个方法，该方法为calculator对象新增了新的属性
        this.result=this.operand1+this.operand2//注意this关键字的用法，this指代当前对象calculator
    }
}
calculator.add() //调用这个属性方法后calculator对象增加一个result属性，值为那两个属性相加，为2
calculator.result //=>2
```

大多数方法调用使用标点 `.` 来访问属性,使用方括号也可以进行属性访问操作，如下：

```javascript
o["m"](x,y) //o.m(x,y)的另一种写法
a[0](z) //在这里a[0]是一个函数   对象不能这么写索引，只有数组能用索引,对象使用中括号只能通过属性名来访问属性
```

方法调用中可以包括更复杂的属性访问表达式

```javascript
customer.surname.toUpperCase() //调用customer.surname的方法
f().m()       //在f()调用结束后继续调用返回值中的方法m() f()方法的返回值是对象，调用对象中的m方法
```

> 函数在代码中出现时可以将它看成这个函数的返回值，当代码运行到这一行时，运行函数，将函数的返回值替代函数代码继续往下进行

方法和this关键字是面向对象编程的核心。任何函数只要作为方法调用实际上都会传入一个隐式的实参，这个实参是一个对象，方法调用的母体就是这个对象，通常来讲，基于那个对象的方法可以执行多种操作，方法调用的语法已经很清晰的表明了**函数将基于一个对象进行操作**，比较下面两行代码：

```javascript
rect.setSize(w,h)
setRectSize(rect,width,height)
```

假设这两行代码功能完全一样，它们都作用于rect对象，可以看出第一行的方法调用语法非常清晰的表明这个函数的执行的载体是rect对象，函数中的所有操作都将基于这个对象

> ==方法链==
>
> 当方法的返回值是一个对象，这个对象还可以再调用它的方法。这种方法调用序列中(通常称为“链”或者”级联“)每次调用的结果都是另一个表达式的组成部分。如JQuery中，我们常常会这样写代码：
>
> ```javascript
> $(":header").map(function(){return this.id}).get().sort()
> //找到所有的header，取得它们的id映射，转换为数组并进行排序
> ```
>
> 当方法并不需要返回值时，最好直接返回this.如果在设计的API中一直采用这种每个方法都返回this的方式，使用API就可以进行“链式调用”风格的编程，在这种编程风格中，只需要指定一次要调用的对象即可，余下的方法都可以基于此进行调用：
>
> ```javascript
> shape.setX(100).setY(100).setSize(50).setOutline("red").setFill("blue").draw()
> //这些函数的对象的返回值都是this，当程序执行到这里时，如对于shape对象的第一个方法setX()返回值是this就是当前对象shape,相当于然后继续shape.setY()..
> ```
>
> 方法的链式调用和构造函数的链式调用不一样

需要注意的是，this是一个关键字，不是变量也不是属性名，js语法不允许给this赋值

和变量不同，关键字this没有作用域的限制，嵌套的函数不会从调用它的函数中继承this。如果嵌套函数作为方法调用，其this的值指向调用它的对象。如果嵌套函数作为函数调用，其this值不是全局对象就是undefined.











## DOM

是文档对象模型的缩写，是浏览器或平台的接口，使js可以通过dom来修改HTML中的代码，如使用dom向页面中添加一张图片或是超链接等。



### DOM对象节点属性

在DOM中使用节点属性可以对节点进行查询，查询出个节点的名称，类型，节点值，子节点和兄弟节点等。常用节点属性如下：

- nodeName:节点的名称
- nodeValue:节点的值，通常只应用于文本节点
- nodeType:节点的类型
- parentNode:返回当前节点的父节点
- childNotes:子节点列表
- firstChild:返回当前节点的第一个子节点
- lastChild:返回最后一个子节点
- previousSibling:返回当前节点的前一个兄弟节点
- nextSibling:返回当前节点的后一个兄弟节点
- attributes:元素的属性列表

访问指定节点：使用`document.getElementById`来访问指定id的节点，再用以上属性看该节点的名称，值和类型

遍历文档树：使用父节点属性，子节点和兄弟节点来实现遍历文档树

### 节点的几种操作

#### 1.节点的创建

创建新的节点首先通过`creatElement()`方法和 `createTextNode()`方法生成一个新的节点并生成文本节点，最后通过使用`appendChild()`方法将创建的新的子节点添加到当前节点的末尾`obj.appendChild(newChild)`

如果想创建多个节点，可以使用循环语句生成多个节点，再都添加到当前节点的后面

#### 2.节点的插入和追加

插入节点通过使用insertBefore()方法实现，将新的子节点添加到当前节点的末尾

```javascript
obj.insertBefore(new,ref)//new为新的节点，ref为指定的一个节点，在这个节点之前插入新的子节点
```

#### 3.节点的复制

复制节点可以使用`cloneNode()`方法实现`obj.cloneNode(deep)`deep是一个布尔值，表示是否为深度复制。深度复制是将当前节点的所有子节点全部复制，deep为TRUE时表示进行深度复制，否则为简单复制，只复制当前节点，不复制其他节点

#### 4.节点的删除与替换

- 删除节点：`removeChild()`:删除一个子节点`obj.removeChild(oldChild)`
- 替换节点：`replaceChild(new,old)`

>  有两种方法可以获取文档中的指定元素，可以通过id来获取也可以通过name来获取（getElementBy...）不过使用name获得的是一个数组而不是一个元素，得再加一个[0]来获取第一个name为这个的元素

使用实例如下：所实现的是网上购物时所留地址的复制和删除

```javascript
function copyAddress(){
  var address=document.getElementById('address')//获得收货地址对象
  var address_copy=address.cloneNode(true)//完全复制对象
  var address_container=document.getElementById('addressContainer')//获得父容器对象（用来放收货地址的最大的那个div）
  address_container.appendChild(address_copy)//为父容器添加复制对象
}
function delClick(obj){
  var address_container=document.getElementById('addressContainer')
  var delOBJ=obj.parentNode  //获取父容器节点
  if(delOBJ.previousElementSibling==null){//就是看有没有兄弟节点（判断还有没有其他的保存的地址）
    alert('无法删除，至少保留一个地址')//如果没有其他保存的地址时就禁止删除
    return ;//这个return就是直接将这个delClick函数返回了，就不再往下进行了
  } 
  address_container.removeChild(delOBJ)//否则若是还有其他保存的地址的话就可以将这个节点给删了
}
```

#### 与DHTML对应的DOM

包括  innerHTML，outerHTML,innerText，outerText

- innerHTML：声明了元素含有的HTML文本，不包括本身的开始和结束标记，该属性可以用于指定某些标签显示内容的更改，如之前的视频的按钮的名字的更改（播放按一下之后变成暂停）
- innerText:只是取出或更改文本信息，对于HTML标记不进行变动

区别如下：

```html
<div id="test"><b>aaaa</b></div> 
<script>
	test=document.getElementById("test")
    test.innerHtml为"<b>aaaa</b>"
    test.innerText为"aaaa"
</script>
//若div内容为
<div id="test"><font color="red"></font></div>
innerHtml为"<font color="red"></font>"
innerText为""空
```

outter的也类似，不过获取或更改的是整个目标节点，就是上述例子的< div>也在outterHTML中了，outterText还是只有文本。



## json相关操作

### json格式：

```html
[
    {
        "userid":1,
        "username":"lijintao",
        "userage":40
    },
   {
           "userid":2,
           "username":"litao",
           "userage":20
       }
]
```

创建时也可以直接按这个格式创建

```javascript
var formdata=[
            {
                "name":form.name.value,
                "describe":form.describe.value,
                "exclusive":form.exclusive.value,
                "mobile":form.mobile.value,
                "email":form.email.value,
                "wechat":form.wechat.value
            }
        ]
```

### json常用函数

```javascript
formdata=JSON.stringify(formdata)
formdata=JSON.parse(formdata)
```

可以使用这个方法将上面创建的对象先转换成字符串再转换成JSON格式

### json常见操作

- 获取json中的指定元素的值，使用eval方法：

  ```javascript
  var myobj=eval(formdata);
          for(var i=0;i<myobj.length;i++){
                  alert(myobj[i].name);
                  alert(myobj[i].describe);}
  ```

- 向JSON数据添加属性：可以直接`formdata.id=1`,这样这个JSON中所有的元素都多了一条属性id且值为1,

- 向JSON数据添加元素：先定义好一个JSON格式的数据a，然后再`formdata.push(a)`

  

### tips

- 在js中，一个[]认为是数组；{}认为是Json对象，创建一个空的json格式的数据可以直接 `var json=[]`



## TIPS

- 导入js的文件最好放在body标签的后面，因为HTML是顺序执行，这样就可以先将HTML中的各种元素加载完毕此时再使用js对其内部的变量或元素进行操作时才不会报错。

- 定义全局变量的时候最好放在最前面或者直接放在head里

- 如果想要使用js改css的属性值，先获得想要改的目标对象，再a.style.你想改的属性,具体如下：

  `a.style.backgroundColor='purple'`

- 在获取目标元素时如果有多个可以在后面加中括号再加数字来选择第几个（就像数组那样）

  ==如果使用类来获取的话 只有一个时最好加上[0]，要不然改属性时会报错不让改==，使用ID就不需要

  ```javascript
  var a=document.getElementsByClassName('mouse')[0]
  a.style.backgroundColor='red'
  
  var a=document.getElementById('aa')
  a.style.backgroundColor='red'
  ```

- JS加不加分号都行

- 当试图查询对象中不存在的属性时，不会报错，只是会得到undefined值



# TIPS

- 在前端代码中连接两个单词时不像编程语言那样使用下划线"_"而是直接用"-"

- JS是按照代码块来进行编译和执行的，代码块间相互独立，但变量和方法共享，按顺序执行。多个`<script>`之间可以变量和方法共享

- 在前端中null就代表空`if(cont!=null)`就是判断cont是否为空

- class可以多个标签使用同一个，但ID最好每个标签单独使用，这样根据id找目标时就可以直接找到了

- 焦点：

  焦点指的是文本输入时的那个一闪一闪的输入杠，如定义一个文本输入框，点击它准备输入的时候它就获得了焦点，点其他的地方使这个输入杠消失了就是失去焦点事件了。

  ![image-20211031194703524](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20211031194703524.png)

  输入杠一直在的话会一直触发焦点事件，要加一句使其焦点消失

- 如果想获取表单的数据，

  1. 可以先通过表单的id获取表单元素，再用表单.选项的name.value获取表单的值，如下：

     ```html
     <form name="form1" enctype="application/x-www-form-urlencoded" id="form1">
         <input type="text" id="name">
         <input type="submit" style="position: relative;left: 50px;" onclick="done()" >
         ...
     </form>    
     <script type="text/javascript">
     var form=document.getElementById("form1")
     function done(){
             alert(form.name.value)
         }
     </script>
     
     ```

## 标签自动补全： 
  （1）纯标签补全 
  例：输入h1,按Tab键， 

  ![img](https://img-blog.csdnimg.cn/20181107095041620.png)
  （2）纯标签+地址“id” 
  例：输入h1#ccg,按Tab键， 

  ![img](https://img-blog.csdnimg.cn/20181107095050395.png)
  （3）纯标签+类“class” 
  例：输入h1.ccg,按Tab键， 

  ![img](https://img-blog.csdnimg.cn/20181107095105718.png)
  （4）标签+子标签+子标签个数 
  例：输入div>p*6,按Tab键， 

  ![img](https://img-blog.csdnimg.cn/20181107095113473.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1ODEyMzgw,size_16,color_FFFFFF,t_70)  （5)标签+类+子标签+子标签个数+子子标签+地址+}HTML} 
  例：输入ul.menu>li*6>a[href=#]{HTML},按Tab键， 

  ![img](https://img-blog.csdnimg.cn/20181107095120695.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1ODEyMzgw,size_16,color_FFFFFF,t_70)

[y]: 