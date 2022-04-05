# VUE

VUE可以提供现代web开发中常见的高级功能，例如：

- 逻辑视图与数据
- 可复用的组件
- 前端路由
- 状态管理
- 虚拟dom

**MVVM模式**：

模型-视图-视图模型。模型指的是后端传递的数据，视图指的是html页面，视图模型是MVVM的核心，它是链接View和model的桥梁。

MVVM有两个方向：

- 一是将模型装换成视图，即将后端传递的额数据转化成所看到的页面，实现的方式是数据绑定
- 二是将视图转换为模型，即将所看到的页面转化成后端的数据，实现的方式是DOM事件监听

如果这两个方向都是想，称之为数据的双向绑定



在MVVM框架中，视图和模型是不能直接通讯的，它们通过viewmodel来通讯，ViewModel通常要扮演一个监听者的角色，当数据发生变化时，ViewModel能够监听到数据的变化，然后通知对应的视图做自动更新；当用户操作视图时，ViewModel也能监听到视图的变化，然后通知数据做改动。

Vue就是基于MVVM模式实现的一套框架。在Vue中，Model指的是js中的数据，如对象数组等，View指的是页面视图，ViewModel指的是Vue实例化对象



Vue是一个渐进式的js框架，渐进式的意义如下：

- 可以一步一步的有阶段性的使用Vue
- 可以将Vue作为一个模块加到其他程序中
- Vue允许用户将一个网页分割成可复用的组件，每个组件都包含属于自己的HTML，CSS，JS



可以看出Vue可大可小，Vue本身具有响应式编程和组件化的特点

- 响应式：保存状态和视图的同步，也被称为数据绑定，修改数据视图也会跟着改变
- 组件化：一切都是组件，可以将任意封装好的代码注册成标签，配合Vue的插件vue-loader可以将一个组件的css，html,js都卸载一个文件里，做到模块化的开发。



> 安装Vue.js：去官网下然后导入 `<script src='vue.js'> </script>`



## 第一个Vue程序

引入vue框架后，在`<body>`底部使用new Vue()的方式创建一个实例，就可以开始使用vue了

```html
<body>
<div id='app'>
  <p>大家好，我是 <b>{{name}},</b></p>
  <p>今年 <b>{{age}}</b>岁。</p>
</div>
</body>
<script>
  //创建实例
  var app=new Vue({
    el:'#app',
    data:{
      name:'王老师',
      age:'30'
    }
  })
</script>
```

![image-20220317201456715](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220317201456715.png)

>  在创建的Vue实例中，
>
> - el选项用于指定一个页面中已经存在的DOM元素来挂载Vue实例，它可以是HTMLElement，也可以是CSS选择器。
> - data选择用于声明应用需要双向绑定的数据，建议所有会用到的数据都预先在data中声明，这样不用将数据散落在业务逻辑中，难以维护

Vue实例代理了data对象里的所有属性，所以可以像上面例子那样进行访问，也可以指向一个已有的变量，并且他们之间默认建立了双向绑定。

```html
<script>
  var my_data={
    a:123
  }
  //创建实例
  var app=new Vue({
    el:'#app',
    data:my_data
  })
  console.log(app.a) //此时的输出为123
  app.a=456
  console.log((my_data.a)) //此时就变成了456，这就是双向绑定
</script>
```

就相当于app.a = my_data.a，随便修改一个，另一个也会跟着变，数据和DOM已经被建立了关联，所有东西都是响应式的

可以在网页的控制台直接进行更改：

![image-20220318093312048](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220318093312048.png)

![image-20220318093335913](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220318093335913.png)

app.name和app.age中的app是我们创建的实例名称

> vue很适合创建单页面应用，单页面应用(SPA)是指只有一个主页面的应用，单页面的优点有以下：
>
> - 用户不需要重刷新页面，数据通过ajax异步获取，页面显示流畅
> - 前后端分离，前端负责页面显示，后端负责数据存储和计算，不会把前后端的逻辑混杂在一起
> - 减轻服务端压力，服务器只需要提供API接口不用管理页面额逻辑和页面的拼接
> - 共用一套后端程序代码，适配多端同一套后端代码，不用修改就可以适用于web，手机，平板
>
> 单页面应用的缺点：
>
> - 不利于SEO的优化。因为页面数据都是前端异步加载的方式，不利于搜索引擎的抓取
> - 首屏加载过慢。单页面首次加载需要将所有页面所依赖的css和js合并统一加载，所有css和js文件会较大，影响页面首次打开的时间



## Vue实例和模板语法

### Vue实例

使用Vue都会创建一个Vue的实例对象并挂载到指定DOM上，每个Vue应用都是通过用Vue函数创建一个新的Vue实例开始的：

```vue
var app=new Vue({
	//选项
})
```

当创建一个Vue实例时，可以传入一个选项对象，这些选项用来创建想要的行为 (methods,computed,watch等)

一个Vue应用由一个通过new Vue创建的根Vue实例以及可选的，嵌套的，可复用的组件树组成

我们需要明白所有的Vue组件都是Vue实例，并且接受相同的选项对象

#### 数据与方法

当一个Vue实例被创建时，它将data对象中的所有属性加入到Vue的响应式系统中，当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

就入上例所示，修改vue实例app中的属性，页面中的对应属性也会一起被修改

需要注意的是，只有当实例被创建时data中存在的属性才是响应式的，如果添加一个新的属性例如：`app.b=10`那么对b的改动将不会触发热河视图的更新。如果后期需要一个属性，但是一开始它为空或不存在，可以先在data中定义好留好空的地方

>  响应式唯一的例外是使用Object.freeze()方法，该方法会冻结现有的属性，也意味着响应系统无法再追踪变化
>
> 一个被冻结的对象再也不能被修改，也不能向这个对象添加新的属性或删除已有属性

除数据属性外，Vue实例还有一些有用的实例属性与方法。它们都有前缀 `$` ,以便和自己定义的属性区分开，如：

```javascript
var data={a:1}
var app=new Vue({
    el:'#example',
    data:data
})
app.$data===data//true
app.$el===document.getElementById('example')//true
//$watch是一个实例方法
app.$watch('a',function(newValue,oldValue){
    //这个回调函数将在app.a改变后调用
})
```

> `$`在JS中本身只是一个符号而异，在JS里什么也不是。
> 但在JS应用库JQUERY的作者将之做为一个自定义函数名了，这个函数是获取指定网页元素的函数，使用非常之频繁，所以好多新手不知道，还以为$是JS的什么特殊语法。
> 后来，可能有些程序员JQUERY用得多了，发现$这个函数很好用，很方便，所以，在不用JQUERY的情况，一般自己也会自定义一个$函数。
> ```javascript
> function $(Nid){
>  	return document.getElementById(Nid);
> }



##### 实例声明周期钩子

每个Vue实例在被创建时，都要经过一系列的初始化过程，在这个过程中也会运行一些叫做声明周期钩子的函数，这给了开发者在不同阶段添加自己的代码的机会。

常用声明周期钩子函数如下

| 钩子函数                  |                             说明                             |
| ------------------------- | :----------------------------------------------------------: |
| **beforeCreated(创建前)** | 在实例初始化之后，数据观测和事件配置之前被调用，此时组件的选项对象还未创建，el 和 data 并未初始化，因此无法访问methods， data， computed等上的方法和数据。 |
| **created(创建后)**       | 实例已经创建完成之后被调用，在这一步，实例已完成以下配置：数据观测、属性和方法的运算，watch/event事件回调，完成了data 数据的初始化，el没有。 然而，挂在阶段还没有开始, $el属性目前不可见，这是一个常用的生命周期，因为你可以调用methods中的方法，改变data中的数据，并且修改可以通过vue的响应式绑定体现在页面上，，获取computed中的计算属性等等，通常我们可以在这里对实例进行预处理，也有一些童鞋喜欢在这里发ajax请求，值得注意的是，这个周期中是没有什么方法来对实例化过程进行拦截的，因此假如有某些数据必须获取才允许进入页面的话，并不适合在这个方法发请求，建议在组件路由钩子beforeRouteEnter中完成 |
| **beforeMount(挂载前)**   | 挂在开始之前被调用，相关的render函数首次被调用（虚拟DOM），实例已完成以下的配置： 编译模板，把data里面的数据和模板生成html，完成了el和data 初始化，注意此时还没有挂在html到页面上。 |
| **mounted(挂载后)**       | 挂在开始之前被调用，相关的render函数首次被调用（虚拟DOM），实例已完成以下的配置： 编译模板，把data里面的数据和模板生成html，完成了el和data 初始化，注意此时还没有挂在html到页面上。 |
| **beforeUpdate(更新前)**  | 在数据更新之前被调用，发生在虚拟DOM重新渲染和打补丁之前，可以在该钩子中进一步地更改状态，不会触发附加地重渲染过程 |
| **update(更新前)**        | 在由于数据更改导致地虚拟DOM重新渲染和打补丁只会调用，调用时，组件DOM已经更新，所以可以执行依赖于DOM的操作，然后在大多是情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环，该钩子在服务器端渲染期间不被调用 |
| **beforeDestory(销毁前)** | 在实例销毁之前调用，实例仍然完全可用，<br/>这一步还可以用this来获取实例，<br/>一般在这一步做一些重置的操作，比如清除掉组件中的定时器 和 监听的dom事件 |
| **destoryed(销毁后)**     | 在实例销毁之后调用，调用后，所以的事件监听器会被移出，所有的子实例也会被销毁，该钩子在服务器端渲染期间不被调用 |

![img](https://img-blog.csdnimg.cn/20210307202117827.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2N6ajEwNDk1NjE2MDE=,size_16,color_FFFFFF,t_70#pic_center)

这些钩子与el和data类似，也是作为选项写入Vue实例内，并且钩子的this指向的是调用它的Vue实例。

#####  实例化多个对象

实例化多个vue对象和一个是一样的，只要绑定到指定的位置就可以

```html
<div id="one">
  {{title}}
</div>
<div id="two">
  {{title}}
</div>

<script>
var one=new Vue({
    el:'#one',
    data:{
      title:'one'
    }
  })
  var two=new Vue({
    el:'#two',
    data:{
      title:'two'
    }
  })
</script>
```

除了可以展示data属性的内容，也可以展示computerd计算属性的内容

```vue
<div id = 'one'>
    {{say}}
</div>

var one=new Vue({
	el:'#one',
	data:{}	,
	computered:{
	say:function(){
		return 'hello one!'
}
}
})
```

如果想在第二个实例对象中，定义一个方法，通过事件触发，在事件中调用第一个对象，更改其中的title属性

```vue
<div id='two'>
	...
    <button v-on:click='changeTitle'>
        改变第一个对象中的值
    </button>
</div>

var two=new Vue({
	el:'#two',
	data:{},
	mathods:{
		changeTitle:function(){
		one.title='已经改名了'
}},
	computerd:{}
})
```

也可以直接在外边改 `two.tittle=''`

### 模板语法

vue使用了基于HTML的模板语法，允许开发者声明式的将DOM绑定至底层Vue实例的数据上。所有Vue模板都是合法的HTML

在底层的实现上，Vue将模板编译成虚拟DOM渲染函数。结合响应系统，vue能智能的计算出Uzi少需要重新渲染多少组件，并把DOM操作次数减到最少

#### 插值

插值的语法有以下三种

##### 1.文本

数据绑定最常见的形式就是使用“Mustache”方法（双大括号`{{ }}`）的文本插值

Mustache标签将会替代为对应数据对象上所绑定属性的值。无论何时发生了改变插值处的内容都会更新

通过v-once指令，也能执行一次性的插值，当数据改变时，插值处的内容不会更新，但这会影响到该节点上的其他数据绑定

```vue
<span v-once>这个将不会改变： {{message}}</span>  //这个的意思就是只能定义一次，不能修改
```

##### 2.原始HTML

双大括号会将数据解释为普通文本，而非html代码，为了输出真正的HTML，我们需要使用v-html指令

```vue
<div id='app'>
<p>{{website}} </p>
<p v-html='website'></p>
</div>

<script>
  var app=new Vue({
    el:'#app',
    data:{
      website:'<a href='https://www.baidu.com'>百度一下</a>'
    }
  })
</script>
```

这样上面显示的就是这行代码而下面显示的是一个超链接

> 注意：站点上动态渲染的任意HTML值可能会非常危险，因为它很容易导致XSS攻击，请只对可信内容使用html插值，绝对不要对用户提供的内容使用插值

##### 3.使用JS表达式

对于所有的数据绑定，Vue都提供了完全的JS表达式支持

```vue
<div id='app'>
    <p>三条鱼总共{{fish*number+data}}元</p>
</div>

<script>
  var app=new Vue({
    el:'#app',
    data:{
      	fish:10,
        num:20,
        data:10
    }
  })
</script>
```

### 指令

指令是带有 `v-` 前缀的特殊特性。指令特性的值预期是个单个js表达式（v-for是例外情况，当表达式的值改变时，将其产生的影响响应式的作用于DOM）

`<p v-if='boole'>现在你看到我了</> ` 这行代码中`v-if`将根据表达式布尔值的真假来插入或移除p元素

#### 参数

一些指令能接收一个‘参数’ ，在指令名称之后以冒号表示。例如，v-bind指令可以用于响应式的更新html特性

`<a v-bind:href='url'>..</a>`  这里href是参数，告知v-bind将该元素的特性与表达式url的值绑定

- `v-on` 指令用于监听DOM事件，如：

  `<a v-on:click='dosomething'>...</a>` 其中参数click是监听的事件名，就相当于onclick=

#### 修饰符

修饰符是以半角句点' . ' 指明的特殊后缀，用于之处一个指令应该以特殊方式绑定，例如 `.prevent`修饰符告诉`v-on`指令对于触发的事件调用`event.preventDefault()`  :  `<form v-on:submit.prevent='onsubmit'>...</form>`



### 缩写

`v-`  前缀作为一种视觉提示，用来识别模板中Vue特定的特性。Vue为`v-bind`和`v-on`两个最常用的指令提供了特定简写。

v-bind -> :

```html
<a v-bind:href="url">   
<a :href='url'>
    
<a v-on:click='dosomenthing()'>
<a @click='aaa()'>
```



## 计算属性，监听器和过滤器

在vue中，可以很方便的将数据使用插值表达式的方式渲染到页面元素中，但是插值表达式的设计初衷适用于简化运算，不应该对插值做过多的操作。当需要对插值做进一步文档处理时，就应该使用Vue中的计算属性来完成这一操作。同时，当插值数据变化时，执行异步或开销较大的操作时，可以采用监听器的方式来达到目的。

### 计算属性computed:{}

计算属性在computed选型中定义。计算属性就是当其依赖的属性的值发生变化时，这个属性的值会自动更新，与之相关的dom也会同步更新。这里的依赖属性值是data中定义的属性。（就相当于把函数放到computed当中）

```html
<div id='app'>
    输入内容：<input type='text' v-model='message'><br>
    反转内容：{{aa}}
</div>

<script>
  var app=new Vue({
    el:'#app',
    data:{
      	message:''
    },
    computed:{
        aa:function(){
            return this.message.split('').reverse('').join('')
        }
    }
  })
</script>
```

![image-20220321105503943](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220321105503943.png)

可以在输入的同时进行反转

### 方法methods:{}

方法和计算属性类似，都是用来放函数的

```javascript
computed:{
        aa:function(){
            return this.message.split('').reverse().join('')
        }
method:{
    aa:function(){
        ...
    }
}
```

计算属性的本质就是一个方法，只不过在使用计算属性的时候，把计算属性的名称直接作为属性来使用，并不会把计算属性作为一个方法去调用

（就是调用计算属性直接`{{aa}}`而方法就得`{{aa()}}`）

> 区别：
>
> 计算属性当依赖项（data中的属性）发生改变时才会重新求值，只要message的值没有发生改变，多次访问aa计算属性会立刻返回之前的计算结果而不是再次进行计算，而在methods每次调用都会重新计算
>
> 调用methods中的一个方法时，所有方法都会被调用。
>
> ```html
> <div id="app3">
>   <button @click="a++"> a+1</button>
>   <button @click="b++">b+1</button>
>   <p>number+a={{add1()}}</p>
>   <p>number+b={{add2()}}</p>
> </div>
> 
> <script>
>   var app3=new Vue({
>     el:'#app3',
>     data:{
>       a:0,
>       b:0,
>       number:30
>     },
>     methods:{
>       add1:function (){
>         console.log('number+a')
>         return this.a+this.number
>       },
>       add2:function (){
>         console.log('number+b')
>         return this.b+this.number
>       }
>     }
>   })
> </script>
> ```
>
> 无论点击哪个按钮都会打印出number+a和number+b

计算属性相当于优化了的方法，使用时只会使用对应的计算属性。但不是什么情况下都使用计算属性，在触发事件时还是使用对应的方法，计算属性一般在数据量比较大，比较耗时的情况下使用(例如搜索)，只有虚拟dom与真实dom不同的情况下才会执行computed

### 监听属性watch:{}

可以使用watch监听器的方法来检测某个数据发生的变化，不同的是，计算属性仅仅是对于依赖数据(data)的变化后进行的数据操作,而watch更加侧重于对于检测中的某个数据发生变化后执行的一系列的功能逻辑操作。

监听器以key-value的形式定义，key是一个字符串，他是需要被检测的对象，而value则可以是字符串（方法的名称），函数，或是一个对象

```html
<div id='app4'>
    输入内容：<input type='text' v-model='message'><br>
</div>

<script>
  var app4=new Vue({
    el:'#app4',
    data:{
      message:''
    },
    watch:{
      message:function (new_,old_){
        console.log('old:'+old_+'--->new:'+new_)
      }}})
</script>
```

这样的话每次message中的值改变时都会显示出老的和新的，如输入51346（没输入一个数字都算发生了一次变动）：

![image-20220322101651569](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220322101651569.png)

watch中也可以通过方法名调用mathods里的方法：

```javascript
methods:{
    way:function(){...}
}
watch:{
    message:'way'//调用方法，直接用函数名字的字符串而不能way()
}
```

当监听的数据为对象或数组时，new和old是相等的。

### 过滤器fliters:{}

过滤器可以对数据进行筛选，过滤，格式化。例如事件格式化，英文大小写转换等。它与上面的那些的不同的是，**它不能改变原始值**

Vue允许自定义过滤器，可被用于一些常见的文本格式化。过滤器可以用在两个地方：

- 双大括号的插值
- v-bind表达式

过滤器应该被添加在js表达式的尾部，由‘管道’符号指示

```html
{{message|capitalize}}  <!--在双大括号中-->
<div v-bind:id="rewId|formatId"></div>  <!--在v-bind中-->
```

可以在一个组件的选项中定义本地的过滤器

```javascript
fliters:{
    capitailize:function(value){
        if(!value) return ''
        value=value.toString()
        return value.charAt(0).toUpperCase+value.slice(1)
    }
}
//或者在创建Vue实例之前全局定义过滤器
Vue.fliter('capitailize',function(){...})
```

当全局过滤器和局部过滤器重名时，会采用局部过滤器,return回来的就是格式改变后的值了

过滤器函数总接受表达式的值作为第一个参数如`mes|cap`中mes就是cap的输入参数，过滤器也可以串联

`{{message|fliterA|fliterB}}`

过滤器是js函数，因此可以接受参数

`{{message|flaterA('arg1',arg2)}}` 此时message为第一个输入参数，'arg1'为第二个输入参数

下面的案例为使用过滤器格式化时间

```html
<div id='app'>
    <h1>当前时间：{{data|format}}</h1>
</div>
<script>
var app=new Vue({
	el:'#app',
    data:{
        data:new Data()
    },
    fliters:{
        fotmat:function(){
            //按照需求改变时间格式
            return year+'-'+month+'_'+day...
        }   
    },
    created:function(){
        var that=this //作用域一致，获取创建时本身的this值，因为会随时间更新，之后的this就不是它自己了，所以创建时先获取
        this.timer=setInterval(function(){
            that.data=new Data()
        },1000)   //在被创建后就定义一个计时器开始每1s传入当前日期
    },
    beforeDestory:function(){
        if(this.timer){
            clearInterval(this.timer)//在结束时定时器如果没关的话就给他关了
        }
    }
})
</script>
```



## 内置指令

指令是Vue模板中最常用的一项功能，它带有前缀v-,主要职责是当其表达式的值改变时，相应的将某些行为应用在DOM上。本节会介绍基本指令，条件渲染，列表渲染和自定义指令。

### 基本指令

Vue的各种指令可以更加方便去实现数据驱动DOM，一些基本指令包括`v-cloak` `v-bind` `v-on` `v-model` `v-once` `v-text` 和`v-html`等

#### v-cloak

v-cloak是在vue.js文件完全导入前被渲染的地方的样式（如{{message}}),可以通过对v-cloak进行css样式的设置

```html
<style>
    [v-cloak]{
        display:none;
    }
</style>
```

#### v-once

v-once指令只渲染元素和组件一次，随后的所有渲染都会跳过这个使用了词指令的元素，被当做静态内容，这可以用于优化性能

```html
<div id="app5">
  <p v-once>不可改变{{meg}}</p>
  <p>可以改变 {{meg}}</p>
  <p><input type="text" v-model="meg"></p>
</div>
<script>
    var app5=new Vue({
  el:'#app5',
  data:{
    meg:'hello'
  },
})
</script>
```

![image-20220322155906279](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220322155906279.png)

#### v-text与v-html

这两个都可以更新页面元素的内容，不同的是v-text会将数据以字符串文本的形式更新，而v-html则是将数据以html标签的形式更新。

我们也可以使用插值表达式进行数据更新，插值表达式只会占据插值所在的地方，而这两条指令会替换掉整个内容

```html
<p>***{{meg}}</p>
<P v-text="message">****</P>
<P v-html="html">****</P>

<script>
data:{
    message:'hello',
        html:'<h3 style='color:blue'> </h3>'
}
</script>
```

#### v-bind属性

v-bind可以用来在标签上绑定标签的属性（例如img的src）和样式。对于绑定的内容作为一个js变量，可以写js表达式。

就相当于将一个标签给动态化了，放到了Vue实例当中可以实时更改了，如：

```html
<div id="app6">
  <img v-bind:src="img" alt=""><br>
  <button @click="change">改变图片</button>
</div>
<script>
var app6=new Vue({
  el:'#app6',
  data:{
    img:'jjlin2.jpg'
  },
  methods:{
    change:function(){
      app6.img='jjlin1.jpg'
    }
  }
})
</script>
```

这样就可以对标签的一些属性进行操作了

#### v-on

在Vue中，对于DOM的操作，全部让Vue替我们完成，我们只关注业务代码实现，使用Vue内置的v-on指令来完成事件的绑定。v-on是绑定一个方法。

原生的html代码对按钮进行绑定：

```html
<input type='button' value='单击事件' id='btn'>
<script>document.getElementById('btn').onclick=function(){..}</script>
<!--而在vue中-->
<input type='button' value='单击事件' v-on:click=function(){}>
```

在Vue中许多事件的逻辑会十分的复杂，所以直接吧js代码写在v-on的指令中是不可行的。所以我们可以在methods中写下方法，再在v-on调用

`v-on:click='alert()'` `method:{alert:function(){...}}`

使用v-on指令接受的方法名称也可以传递参数，只需要在methods中定义方法时说明这个形参即可。

### 条件渲染

v-if,v-show可以实现条件渲染，还有可以与v-if搭配的v-else,v-else-if指令

#### v-if和v-else

在指令的表达式返回true时被渲染。如：

```html
<h3 v-if='value'>aaaa</h3>
<h3 v-else>bbb</h3>
data:{
	value:true
}
```

因为v-if是一个指令，所以必须将它添加到一个元素上，但是如果想切换多个元素，此时可以把一个`<template>`元素当做不可见的包裹元素，并在上面使用v-if,最终渲染结果将不包含`<template>`元素。(控制台中的html代码中没有`<template>`这个标签)

> template中可以放执行语句，一般常和v-for和v-if一起结合使用，这样可以是的整个html结构没有那么多多余的元素，整体结构更加清晰

```html
<template v-if="value">
<h3>aaa</h3>
<p>bbbb</p>
</template>
```

v-if可以直接放表达式如`<div v-if='value>0.5'>  data:{value:Math.random()}`

v-else必须紧跟在v-if或者v-else-if之后，否则将不会被识别。



#### 用key管理可复用的元素

Vue会尽可能高效的渲染元素，通常会复用已有元素而不是重头开始渲染，这可以使Vue非常快，也允许用户在不同登录方式之间切换。但当我们想让一些元素重新渲染时就可以使用key元素了。

不使用key属性:

```html
<div id="app7">
  <template v-if="logintype==='username'">
    <label>姓名</label>
    <input type="text" placeholder="输入用户名">
  </template>
  <template v-else>
    <label >邮箱</label>
    <input type="text" placeholder="输入邮箱">
  </template>
  <button @click="change()">切换</button>
</div>
<script>
    var app7=new Vue({
        el:'#app7',
        data:{
            logintype:'username'
        },
        methods:{
            change:function(){
                return this.logintype= this.logintype==='username'?'email':'username' //这是一个条件判断
                //相当于如果logintype为username就切换到email，如果是email就切换到username
            }
        }
    })
</script>
```

如果按照上面这么写，切换将不会清除用户已经输入的内容，因为这两个模板使用了相同的元素，`<input>`不会被替换掉(Vue不会重复渲染)，仅仅是替换掉了它的placeholder.

key可以实现在两个元素完全一样但是想让他们独立，不复用它们。只需添加一个具有唯一值的key属性即可。

```html
<input type="text" placeholder="输入用户名" key='value1'>
<input type="text" placeholder="输入邮箱" key='value2'>
```

此时点切换之后就能看到设为默认值的placeholder了，此时label元素仍会被高效的复用，因为他们没有添加key属性。

> V-else放到tempale中非常好用，直接一整块可以控制

#### v-show

与v-if类似，不同的是带有v-show的元素始终会被渲染并保留在DOM中（仅仅是根据条件设置现不显示）而v-if会将这个元素的DOM直接销毁或重建

v-show只是简单的切换元素的CSS属性display,当为true时显示，为false时不显示

v-show不支持< template>语法，也不支持v-else

```html
<h3 v-show='value'>aaaa</h3>
```

一般来说，v-if有着更高的切换开销，v-show有着更高的初始渲染开销。



### 列表渲染

#### v-for

使用v-for指令，必须使用特定语法，其中，items是源数据数组，而item是被迭代的数组元素的别名，具体格式如下：

```html
<div v-for='item in items'>
    {{item.text}}
</div>
<li v-for='a in items'> {{a}}</li>
data:{
	items:[a,b,c,d]
}
```

v-for指令还支持一个可选的第二参数作为当前项的索引如

```html
<li v-for='(item,i) in items'>{{i}}---{{item}}</li>
```

如果遍历的对象为对象时，第二参数索引就是对象的属性名，此时也可以用第三参数来当索引

```html
<li v-for='(value,name,i) in object'></li>
```

> v-for案例：创建动态表格
>
> 使用template将一行包裹起来，我这里使用的是数组，定义一个计数器每次添加新元素加一，每添加一个新元素push进数组新的元素，使用v-for循环这个计数器的次数来当序号依次取出数组中的各个位数
>
> ```vue
> <table class="table_i" >
>    <tr>
>      <th width="10%">序号</th>
>      <th width="15%">姓名</th>
>      <th width="25%">职位</th>
>      <th width="30%">联系方式</th>
>      <th width="20%">操作</th> <!--在表头定义好宽度后下面就直接都是按照这个宽度来的了-->
>    </tr>
>    <template v-for="i in num">  <!--如果是数字的话就直接循环这么多的次数-->
>    <tr>
>      <td>{{i}}</td>
>      <td>{{people.names[i-1]}}</td>
>      <td>{{people.works[i-1]}}</td>
>      <td>{{people.emails[i-1]}}</td>
>      <td><button>修改</button><button @click="del(i)" >删除</button>/td>
>    </tr>
>    </template>
>    <tr height="20px">
>      <td></td>
>      <td></td>
>      <td></td>
>      <td></td>
>      <td></td>
>    </tr>
>  </table>
> 
> <script>
> 	data:{
>      num:0,
>      name:'',
>      work:'',
>      email:'',
>      people:{
>        names:[],
>        works:[],
>        emails:[],},
>  },
>  methods:{
>    up:function(){
>      this.num+=1
>      this.people.names.push(this.name)
>      this.people.works.push(this.work)
>      this.people.emails.push(this.email)
>    },
>        del:function(i){
>            this.people.names.splice(i+1,1)
>            this.people.works.splice(i+1,1)
>            this.people.emails.splice(i+1,1)
>            this.num-=1
>        },}
> </script>
> ```
>
> 



#### 维护状态

当Vue正在更新使用v-for渲染的元素列表时，它默认使用'就地更新'的策略。如果数据项的顺序被改变，Vue将不会移动DOM元素来匹配数据项的书序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。

这个默认的模式是高效的，但是值适用于不依赖子组件状态或是临时DOM状态（例如表单输入值）的列表渲染输出。

为了给Vue一个提示，以便他能跟踪每个节点的身份，从而重用和重新排序现有元素，需要为每项提供一个唯一key属性，如：

```html
<div v-for='item in items' v-bind:key="item.id">
    ...
</div>
```

尽可能的在使用v-for时提供key属性，除非遍历输出的DOM的内容非常简单或者是刻意依赖默认行为以获得性能上的提升。

注意不要使用对象或数组之类的非基本类型值作为key的key，请使用字符串或是数值类型的值

#### 数据更新检测

Vue为了增强列表渲染的功能，增加了一组观察数组的方法，而且可以显示一个数组的过滤或排序的副本。

##### 1.变异方法

Vue将被监听的数组的变异方法进行了包裹，所以他们也将会触发视图更新，这些被包裹的方法如下：

- push():接受任意数量的参数，把他们诸葛添加到数组末尾，并返回修改后数组的长度
- pop():移除数组的最后一项，返回移除的项
- shift():移除数组第一项并返回该项
- unshift():在数组前端添加任意个项并返回新数组的长度。
- splice():删除原数组的一部分成员，并可以在被删除的位置加入新的数组成员
- sort():调用每个数组项的.toString(),然后比较得到的字符串并排序
- reverse():翻转数组的顺序

```javascript
{{items}}
data:{
    items:{'a','b','c'}
}
app.items.push('d')
```

##### 2.替换数组

上面的方法会直接改变原数组，接下来的方法不会改变原始数组，而是返回一个新数组

- concat():先创建当前数组的一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组

- slice():基于当前数组中的一个或多个项创建一个新数组，接收一个或两个参数（要返回项的起始和结束位置），最后返回新数组。

  （用的最多，可以在指定位置删除或添加成员如`a.splice(0,1)`就是删除a[0]一个，其他序号补上，详情请见js权威指南数组方法）

- map():对数组的每一项运行给定函数，返回每次函数调用结果组成的数组

- fliter():对数组的每一项运行给定函数，该函数会将所有返回值为true的项组成一个数组并返回

```javascript
<li v-for='n in items'>{{n}}</li>
data:{
    numbers:[1,2,3,4,5]
}
computed:{
    items:function(){
        return this.numbers.fliter(function(number){
            return number<4
        })
    }
}
```

此时的返回结果就是123



> 如果Vue想通过索引来直接设置数组的话可以通过Vue.set()来实现
>
> ```javascript
> Vue.set(app.items,3,'d') //在app这个vue实例中data的item中的第3个位置添加一个d元素
> ```



#### 对象变更检测注意事项

由于JS的限制，Vue不能检测对象属性的增加或删除。

Vue 实现数据双向绑定的过程：当把一个普通的JS对象传给Vue实例的data选项，Vue将遍历此对象所有的属性，然后将这些对象的属性全部转换为getter/setter.当setter被调用时，会通知watcher重新计算从而实现更新。

若一个对象的属性没有在data中声明，则它就不是响应式的，如下app.a就是响应式的，app.b就不是响应式的

```javascript
data:{
    a:1
}
app.b=2
```

对于已经创建的实例，Vue不允许动态添加跟级别的响应式属性，但是可以使用`Vue.set(object,propertyName,value)`方法向嵌套对象添加响应式属性，例如

```javascript
data:{
    object:{
        name:'小明'
    }
}
Vue.set(app.object,'age',27) //这样data中的响应式属性就又多了一个age,也可以用Vue.set的别名app.$set
app.$set(app.object,'age',27)

```

若同时想对对象赋予多个属性，可以使用Object.assign(),用两个对象的属性创建新的对象

```javascript
app.user=Object.assign({},app.object,{
    age:32,
    sex:'男'
})
```

#### v-for与v-if一起使用

当他们处于同一节点时，v-for 的优先级比v-if更高，意味着v-if将分别重复运行于每个v-for循环中。当指向为部分项渲染节点时，这种优先级的机制会十分有用。

```html
<li v-for='n in items' v-if='!n.values'> {{n.name}}</li>
<script>
var app=new Vue({
    el:'#app',
    data:{
        items:{
            {name:'a'},
        	{naeme:'b'},
    		{name:'c',value:'已报到'}
        }
    }
</script>
```

这样就会只显示没有报道的a和b

> 不推荐在同一元素上使用v-if和v-for,必要情况下应该替换成计算属性computed
>
> ```html
> <li v-for='n in student'> {{n.name}}</li>
> <script>
> var app=new Vue({
>     el:'#app',
>     data:{
>         items:{
>             {name:'a'},
>         	{naeme:'b'},
>     		{name:'c',value:'已报到'}
>         },
>     computed:{
>         student:function(){
>     		return this.items.fliter(function(n){
>                 return !n.value
>             })
> }
>                 }
>     }
> </script>
> ```

### 自定义指令

自定义指令的注册方法和组件很像，也分为全局注册和局部注册，如注册一个v-focus指令用于在< input>,< textarea>元素初始化时自动获得焦点，两种写法分别是：

```javascript
//全局注册：
Vue.directive('focus',{
              //指令选项
              })
//局部注册：
var app=new Vue({
    el:'#app',
    directives:{
        focus:{
            //指令选项
        }
    }}）
```

指令的各个选项为：

- bind：只调用一次，指令第一次绑定到元素时调用
- update:被绑定的元素所在的模板更新时调用
- inserted：被绑定元素插入父节点时调用（父节点存在即可调用)
- componentUpdated:被绑定元素在模板完成一次更新周期时调用
- unbind:只调用一次，指令与元素解绑时调用

可以根据需求在不同的钩子函数内完成逻辑代码，如上面的v-focus就希望在元素插入父节点时就调用，那最好用inserted选项

```javascript
<input v-focus>
Vue.directive('focus',{
    inserted:function(el){
        el.focus()
    }
})
//目前全局注册的没有用，局部注册的有用
var app=new Vue({
directives:{
      inserted:function(el){
        el.focus()
      }
```

每个钩子函数都有几个参数可以用，例如上面使用到的el,它们的含义如下：

- el:指定所绑定的元素，可以用来直接操作DOM
- binding：一个对象，包含以下属性：
  - name:指令命，不包含v-前缀
  - value：指令的绑定值，如`v-a='1+1'`,那么value的值就是2
  - oldValue:指令绑定前的一个值，仅在update和componentUpdated钩子中可用
  - expression:绑定值的字符串形式如'1+1'
  - arg: 传给指令的参数
- vnode：Vue编译产生的虚拟节点
- oldVnode:上一个虚拟节点，仅在update和componentUpdated钩子中可用

> 除了el之外，其他参数都是只读的，请勿进行修改

```javascript
<div v-demo:foo.a.b='message'>
Vue.directive('demo',{
    bind:function(el,binding,vnode){
        el.InnerHtml=
            binding.name+binding.value...
    }
})
```



## 页面元素样式的绑定

在vue中，操作元素的class列表和内联样式是数据绑定的一个常见需求。因为他们都是属性，所以可以使用v-bind来处理他们。在将v-bind用于class和style时，Vue做了增强，表达式结果的类型除了字符串之外，还可以是对象或数组

### 绑定HTML样式

在vue中，动态的样式类在v-on:class中定义，静态的类名卸载class样式中

#### 数组语法

vue中提供了使用数组进行绑定样式的方式，可以直接在数组中写上样式的类名

>  注意：如果不适用单引号包裹类名，它其实代表的还是一个变量的名称，会报错

clsaa数组用法(将多个style合并展示)：

```html
<div id="app">
  <div class="style" v-bind:class="['style1','style2']">{{message}}</div>
</div>

<style>
  .style{
    color: white;/*定义字体颜色*/
  }
  .style1{
    background: #4f43ff;
  }
  .style2{
    width:200px;
    height: 100px;
  }
</style>

<script>
  var app=new Vue({
    el:'#app',
    data:{
      message:'数组语法'
    }
  })
</script>
```

如果想以变量的方式，就需要先定义好这个变量

```vue
<div class="style" v-bind:class="[class1,class2]">{{message}}</div>
data:{
	message: ,
	class1:'style1',
	class2:'style2'
}
```

在数组语法中也可以使用对象语法来控制样式是否使用

```vue
<div class="style" v-bind:class="[{style1:boole},'style2']">{{message}}</div>
data:{
	message:'',	
	boole:true
}
```

#### 对象语法

在上面通过在数组中使用了对象来设置样式，在vue中可以直接使用对象来设置样式。对象的属性为样式的类名

```vue
<div class='style' v-bind:class={'style1':boole1,'style2':boole2}>{{message}}</div>
data:{
	message:aaa,
	boole1:true,
	boole2:false,
}
```

这样就可以动态的选择用哪些类的样式了,直接修改app.boole1就可以了

如果想要一块显示的样式过多，此时可以在元素上只写对象变量，在Vue中进行定义，如
```vue
<div class='style' v-bind:class='objstyle'>
    {{message}}
</div>
data:{
	message:'a',
	objstyle:{
	style1:true,
	style2:false
}}
```

也可以绑定一个返回对象的计算属性，这是一个常用且强大的模式

```vue
<div class='style' v-bind:class='classobj'>
    {{message}}
</div>
computed:{
	classobj:function(){
	return{
		style1:this.boole1,
		style2:this.boole2
}}}
```

#### 在自定义组件上使用class

在自定义组件上使用class时，这些类将被添加到该组件的根元素上面不会被覆盖。例如声明组件如下：

```Vue
Vue.component('my-component',{ //这是自定义组件
	template:'<p class='style1 style2'>Hello</p>'
})
```

然后在使用它的时候添加一些class样式，如style3,style4:

```vue
<my-component class="style4 style4"></my-component>
<!--html会渲染为-->
<p class='style1 style2 style 3 style4'>Hello</p>
```

对于被绑定的class也是一样的

### 绑定内联样式

内联样式是将css样式编写到元素的style属性中

#### 对象语法

`v-bind:style`的对象语法十分直观

```vue
<div v-bind:style="{color:'red',fontSize:'30'}">对象语法</div>
```

也可以在Vue实例中 定义属性来代替样式值，如：

```vue
<div v-bind:style="{color:stylecolor,fontSize:font}">对象语法</div>
data:{
	stylecolor:'blue',
	fontsize:'40px'
}
```

> 在vue中不能加`-`而是将第二个单词的首字母大写如fontSize

同样对象语法也常常结合返回对象的计算属性使用

```vue
<div v-bind:style='styleobj'>对象语法</div>
computed:{
	styleobj:function(){
	return {
	color:'',
	fontSize:''
}}}
```

#### 数组语法

`v-style`的数组语法可以将多个样式对象应用到同一个元素上，样式对象可以是data中定义的样式对象和计算属性中的return的对象

```vue
<div v-bind:style="[style1，style2]">数组语法</div>//因为此时是变量所以不用加单引号
data:{
	style1:{
	color:'red'
}
```

> 当`v-bnd:style`使用需要添加浏览器前缀的css属性时（如transform)，Vue会自动侦测并添加相应的前缀。

### tips

- 数组语法用的是中括号，如果其中的元素是对象的话必须用单引号引起来，如果不用单引号就是变量

  ```vue
  <div class="style" v-bind:class="['style1','style2']">{{message}}</div>
  <div class="style" v-bind:style="[style1,style2]">{{message}}</div>
  .style1{//这里就是对象
  }
  data:{
  	style1:{//这里是变量
  	color:'red'
  }}
  ```

- 如果想根据条件切换列表中的class，可以使用三元表达式：

  ```vue
  <div v-bind:class='[isActive? classa:'',classb]'></div>
  data:{
  	isActive:true,
  	classa:'color1',
  	classb:'color2'
  }
  .color1{}
  .color2{}
  ```

  这样就是在满足条件时将classa加上，不满足就只有classb
  
- 想用v-bind绑某个样式的单个属性的话（如长度width）要用大括号括起来如`v-bind:style="{width:50px}"`



## 事件处理

本章将详细介绍Vue实现绑定事件的方法，使用v-on指令监听DOM事件来触发一些js代码，可以触发的js指令有：

`click`单击`dblclick`双击`mouseover`鼠标在元素内移动

### 监听事件

事件就是在程序运行当中，可以调用方法去改变对应的内容，如下：

```vue
<button v-on:click='age++'>增加一岁</button>
<button v-on:click='age--'>减少一岁</button>
```

Vue所有的事件处理方法和表达式都严格绑定在当前视图的ViewModel上，它不会导致任何维护上的困难。实际上，使用v-on有3个好处

- 可以轻松定位在js代码中的方法
- 无需在js中手动绑定事件，是非常存粹的逻辑，和DOM完全解耦，更易于测试
- 当一个viewmodel被销毁时，所有的事件处理器都会自动销毁，无需担心后续的处理

### 事件处理方法

在上例中，我们直接对属性进行操作的，但在实际的项目开发中是不可能直接对属性进行操作的。所以一般都是v-on接一个方法名，在方法中完成复杂的逻辑

```javascript
methods:{
    add:function(){
        this.age+=10
    }
}
```

也可以传入参数来控制变化的大小

`v-on:click='add(10)'`

和js一样，如果想要双击按钮就`v-on:dblclick=''`

下面的例子是在一个设计好的区间内移动鼠标会实时返回鼠标在当前div内的位置：

```vue
<div id="app2" class="area" @mousemove="position">
  {{x}},{{y}}
</div>
<style>
.area{
  width: 400px;
  height: 200px;
  background-color: green;
  border: 2px solid black;
  text-align: center;
  line-height: 200px;/*通过调整行高和整个div模块的大小一致从而达到在中间显示字体的效果*/
  font-size: 20px;
}
</style>
<script>
    var app2=new Vue({
    el:'#app2',
    data:{
      x:0,
      y:0
    },
    methods: {
      position:function(event){
        this.x=event.offsetX
        this.y=event.offsetY
      }}})
</script>
```

![image-20220328174932760](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220328174932760.png)

> 本例中通过event事件对象获取鼠标的位置，event代表事件的状态，例如事件在其中发生的元素，键盘按键的状态，鼠标的位置，鼠标的按键状态等。当一个事件发生时，和当前这个对象发生的这个事件有关的一些详细信息都会被临时保存到一个指定的地方：event对象,供我们再需要的时候调用。这个对象是在执行事件时，浏览器通过函数传递过来的。
>
> （event可以随便起名，起个a,b都可以）

### 事件修饰符

对事件添加一些通用的限制，例如阻止事件冒泡，Vue则对这种事件的限制提供了特定的写法，语法如下：`v-on:事件.修饰符`

在事件处理程序中调用event.preventDefault()（阻止默认行为）或event.stopPropagation()（阻止事件冒泡）是非常常见额需求。

在Vue中事件修饰符处理了许多DOM事件的细节，让我们不再需要花大量的事件去处理这些烦恼的事，而能有更多的精力去专注于程序的逻辑处理，Vue中的事件修饰符主要有以下几个：

- `.stop`:相当于js中的event.stopPropagation()阻止事件冒泡
- `.capture`:与事件冒泡的方向相反，事件捕获由内到外
- `.self`:只会触发自己范围内的事件
- `.once`:只会触发一次
- `.prevent`:等同于js中的event.preventDefault()，阻止默认事件的发生。
- `.passive`:执行默认行为

#### stop修饰符

stop用来阻止事件冒泡，在下例中创建了一个div，在其内部也创建了一个div并分贝为它们创建单击事件。根据**事件的冒泡机制**可以得知，当单击了内部的div元素之后，会扩散到父元素div，从而触发父元素的单击事件。

```vue
<div id="app3">
  <div class="out" @click="out">
    <div class="inside" @click="inside">冒泡事件</div>
  </div>
</div>
```

![image-20220329105012859](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220329105012859.png)

这样的话点击内部的div也会触发外部的div指令，如果不希望冒泡，可以使用vue的内置修饰符stop。因为是单击内部div元素后产生的事件冒泡，所以只需要在内部div元素的单击事件上加上stop修饰符即可。这样单击里面的就不会再触发外面的了。

```vue
<div id="app3">
  <div class="out" @click="out">
    <div class="inside" @click.stop="inside">冒泡事件</div>
  </div>
</div>
```

#### capture修饰符

**事件捕获模式**和事件冒泡模式是一对相反的事件处理流程，当想要页面元素的事件流改为事件捕获模式时，只需要在父级元素的事件上使用capture修饰符即可，若有多个该修饰符，则由外而内触发

```vue
<div class="out" @click.capture="out">
    <div class="mid" @click.capture="mid">
    	<div class='in' @click='inside'>内</div>中</div>外</div>
```

#### self修饰符

self修饰符可以理解为跳过冒泡事件和捕获事件，只有直接作用在该元素上的事件才可以执行。self修饰符会监视事件是否直接作用在元素上，若不是则冒泡跳过该元素。

```vue
<div class="out" @click="out">
    <div class="mid" @click.self="mid">
    	<div class='in' @click='inside'>内</div>中</div>外</div>
```

此时要是点内部的div则冒泡会跳过中间的div，直接显示外部的div，点中间层还是会正常冒泡。

#### once修饰符

有时只需要执行一次的操作如微信朋友圈点赞，这时变可以使用once修饰符来完成。

> 不像其他只能对原生的DOM事件其作用额修饰符，once修饰符还能被用到自定义的组件上。

```vue
<button @click.once='add'>点赞{{age}}</button>
```

#### prevent修饰符

用于阻止默认行为，如`<a>`标签，当单击标签时，默认行为会跳转到对应的链接，如果添加上.prevent修饰符则不会跳转到对应的链接。

```vue
<a @click.prevent='alert' href="">超链接</a>
```

#### passive修饰符

浏览器只有等内河线程执行到事件监听器对应的js代码时，才能知道内部是否会调用preventDefault函数来阻止事件的默认行为，所以浏览器本身是没有办法对这种场景进行优化的，这种场景下用户的手势事件无法快速产生，会导致页面无法快速执行华东逻辑从而让用户感到页面卡顿。

通俗的说就是每次事件产生浏览器都会去查询一下是否有preventDefault阻止该次事件的默认动作，加上pssive就是为了告诉浏览器，不用查询了没有设置阻止默认事件的发生。

passive修饰符一般用在滚动监听，@scroll和@touchmove中。因为滚动监听过程汇中移动每个像素都会产生一次事件，每次事件都查询prevent会使华东卡顿，通过passive修饰符将内河线程查询跳过，可以大大提升滑动的流畅性。

> passive修饰符尤其能提升移动端的性能
>
> 不要将passive和prevent一起用，可能会导致浏览器报错

#### 多个修饰符连用

多个修饰符可以连用，如`@click.prevent.self`会阻止与这个元素有关的所有的单击动作

（点击自己被阻止默认（prevent阻止单击自己的事件），冒泡也被self阻止）

但是在连用时，修饰符的顺序非常重要，如上面的修饰符连用如果这么写：`@click.self.prevent`只会阻止对元素自身的单击，而不会阻止冒泡

### 按键修饰符

在Vue中可以使用以下3种键盘事件。

`keydown` 按键按下`keyup`按键抬起 `keypress`按键按下和抬起的间隔期间触发

在js中往往通过监听对应的keyCode,然后判断keyCode得知用户按下了哪个按键。

Vue提供了大部分常用按键所对应的keyCode如：

`.enter, .tab, .delete .esc .space .up .down .left .right`

```vue
<input v-on:keyup.enter='name' type='text'>
```

### 系统修饰键：

可以用下面的修饰符来实现仅在按下响应按键时才触发鼠标或键盘事件的监听器，可以与按键修饰符组合使用，比如按下ctrl+C这些组合键的监听器

`.ctrl .alt .shift .meta`

系统修饰键与常规按键不同，在和keyup事件一起使用时，事件触发时修饰键必须处于按下状态。只有在按住ctrl键的情况下释放其他按键，才能触发keyup.ctrl,而单单释放ctrl键也不会触发事件。

```vue
<input v-on:keyup.shift.enter=''>
```

这样写就是得先按shift再按enter才能触发





## 表单输入绑定（双向数据绑定）

对于Vue来说，使用v-bind并不能解决表单域对象双向绑定的需求，所谓双向绑定，就是无论通过input还是通过Vue对象都能修改绑定的数据对象的值。Vue提供了v-model进行双向绑定。

### 双向绑定

数据的绑定，不管是使用插值表达式{{}}还是v-text指令，对于数据间的交互都是单向的，只能将Vue实例中的值传给页面，页面对数据值的任何操作却无法传递给model。

可以用v-model指令在表单< input>,< textarea>,以及< select>元素上创建双向诗句绑定。它会根据空间类型自动选取正确的方法来更新元素。

v-model会忽略所有表单元素的value，checked，selected特性的初始值，而总是将Vue实例的数据作为数据来源。我们应该通过JS组件的data选项中声明初始值

### 基本用法

v-model在内部为不同的输入元素，使用不同的属性并抛出不同的事件。

- text和textarea元素使用value属性和input属性
- checkbox和radio使用checked属性和change事件
- select字段将value作为prop并将change作为事件

> 对于需要使用输入法如中文日文等的语言时，会发现v-model不会再输入法组合的文字过程汇总得到更新。如果想处理这种情况，可使用input事件

#### 文本

在下面的实例中，绑定了name和age两个属性

```vue
<div id="app">
  <label for="name">姓名</label>
  <input type="text" v-model="names" id="name">
  <p>{{names}}</p>
  <label for="age">年龄</label>
  <input type="text" v-model="ages" id="age">
  <p>{{ages}}</p>
</div>
<script>
  var app=new Vue({
    el:'#app',
    data:{
      names:'阿涛',
      ages:'15'
    }
  })
</script>
```

![image-20220330104224790](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220330104224790.png)

此时就完成了双向绑定，可以根据输入来改变页面内容了。

把input标签换成textarea标签，即可实现多行文本的绑定。

> v-model是跟data中的数据的，用来跟data中的数据进行双向绑定。

#### 复选框

单个复选框绑定到布尔值

```vue
<input type='checkbox' id="checkbox" v-model="checked">
  <label for="checkbox">{{checked}}</label>
data:{
checked:true
}
```

通过修改checked的值（true或false）来更改显示和是否选中，同样更改是否选中可以修改显示的值为true或false

![image-20220330105413065](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220330105413065.png)![image-20220330105422398](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220330105422398.png)

如果有多个复选框，可以绑定到同一个data中的数组上，被选中的会按照选中的顺序将value的值添加到数组中

```vue
<input type='checkbox' id="name1" value="阿涛" v-model="checkname">
  <label for="name1">阿涛</label>
  <input type='checkbox' id="name2" value="涛哥" v-model="checkname">
  <label for="name2">涛哥</label>
  <input type='checkbox' id="name3" value="啊啊啊" v-model="checkname">
  <label for="name3">还是涛</label>
  <p><span>哪些人特别帅：{{checkname}}</span></p>
data:{
checkname:[]//定义空数组用来放选中的
}
```

![image-20220330110415372](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220330110415372.png)

注意：绑定的是复选框的value值，数组中的顺序就是点击的顺序

data中必须是数组（[]）才能储存那些选项的value值，如果直接是空(' ')就只会返回true

#### 单选按钮

单选按钮一般都有多个条件可供选择，既然是单选按钮，自然希望实现互斥效果，可以使用v-model指令配合单选按钮的value来实现。

在下面的示例中，多个单选按钮绑定到同一个数组，被选中的添加到数组中。

```vue
<h3>单选题</h3>
  <input type="radio" id="one" value="A" v-model="picked">
  <label for="one">A</label>
  <input type="radio" id="two" value="B" v-model="picked">
  <label for="two">B</label>
  <input type="radio" id="three" value="C" v-model="picked">
  <label for="three">C</label>
  <input type="radio" id="four" value="D" v-model="picked">
  <label for="four">D</label>
  <p>选择：{{picked}}</p>

data:{
picked:''
}
```

![image-20220330111606083](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220330111606083.png)

#### 选择框

##### 单选框：

```vue
<h3>选择你最喜欢吃的水果</h3>
  <select v-model="selected">
    <option  disabled value="">可以选择的水果如下</option> <!--可以这么设置默认显示但是不可选中-->
    <option value="apple">苹果</option>
    <option value="banana">香蕉</option>
    <option value="orange">橘子</option>
    <option>西瓜</option><!--或者直接就不设置value值也是一样的-->
  </select>
  选择结果：{{selected}}
data:{
	selected:''
}
```

![image-20220330112609559](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220330112609559.png)

> 如果v-model表达式的初始值未能匹配任何选项，`<select>`元素将被渲染为未选中状态。在ios中这回使用户无法选择第一个选项，因此推荐像上面这样提供一个值为空的禁用选项。

##### 多选框：

为select标签添加multiple属性即可实现多选

`<select v-model='selected' multiple style='height:100px'>`

![image-20220330113459605](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220330113459605.png)

##### 用v-for渲染的动态选项

在实际应用场景中，select标签中的option一般是通过v-for指令动态输出的，其中每一项的value或text都可以使用v-bind动态输出。

```vue
<select v-model="sel"><!--相当于把value的值给了v-model-->
    <option v-for="a in options" v-bind:value="a.value">{{a.text}}</option>
</select>
<span>选择结果：{{sel}}</span>
data:{
	option:[
		{text:'apple',value:'苹果'},
        {text:'banana',value:'香蕉'},
        {text:'orange',value:'橘子'}]
}
```



#### tips

- 所有单选的值都可以设置为空`select:''`，多选的值必须设置为数组`checknames:[]`
- 绑定的值为data中的指定值和表单的value，要将value设置成想要表述的。相当于把value的值给了v-model所双向绑定的对象。

### 值绑定

对于上述的单选按钮，复选框以及选择框的选项，v-model绑定的值通常是静态字符串或是布尔值，但是有时可能想把值绑定到vue实例的一个动态属性上，这是可以用v-bind实现，并且这个属性的值可以不是字符串。

#### 绑定复选框

在下例中，true-value和false-value并不会影响控件的value特性，因为浏览器在提交表单时并不会包含未被选中的复选框。这样就可以在选中或是被选中时获取自己设定好的值了。

```vue
<input type="checkbox" v-model="toggle" true-value="a" false-value="b">
  <span>{{toggle}}</span>
data:{
toggle:'c'/c是初始值
}
```

![image-20220401095523070](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220401095523070.png)![image-20220401095530871](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220401095530871.png)![image-20220401095541832](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220401095541832.png)

#### 绑定单选按钮

首先为单选按钮绑定一个属性a，然后用v-model指令为单选按钮绑定pick属性，当单选按钮选中后，pick的值等于a的属性值

(就相当于把value的值送到了v-model中，不过value的值也与vue实例中的数据向绑定)

```vue
<input type="radio"v-model="pick" v-bind:value="a">{{pick}}
data:{
	  pick:'还未被选中',
      a:'该单选按钮已被选定',
}
```

![image-20220401100919755](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220401100919755.png)![image-20220401100927717](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220401100927717.png)

绑定选择框也是同理，将value值绑定设置到vue实例的data中，然后在select标签中绑定v-model

> 在表单中，提交的都是各个输入标签的value值，将它们的value绑定就可以动态自定义提交内容，v-model就是要提交的对象，也是data中的一个数据



### 修饰符

对于v-model指令还有3个常用的修饰符：lazy,number和trim

#### lazy修饰符

在输入框中v-model默认是同步数据，使用lazy修饰符会转变为在change事件中同步，也就是在失去焦点或按下enter时才更新。

```vue
<input type="text" v-model.lazy="message">{{message}}
```



![image-20220401101816584](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220401101816584.png)

#### number修饰符

可以将输入的值转化为number类型，否则虽然输入的是数字，但它的类型其实是string，此修饰符在数字输入框比较有用。

如果想自动将用户的输入值转为数值类型，可以给v-model添加number修饰符，因为即使在type='number'时，html元素的值也总是会返回字符串

#### trim修饰符

可以自动过滤用户输入的首尾空格

```vue
<input type="text" v-model.trim="val">值为：{{val}}val的长度是：{{val.length}}
```



![image-20220401102655111](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220401102655111.png)

## 组件技术

以上的所有操作，在使用Vue的整个过程中，最终都是在对Vue实例进行的一系列操作。这里就又会引出一个问题，把所有对于vue的操作全部写在一起，这必然会导致这个方法又长又不好理解。而解决方法就是用到组件技术

### 组件介绍

组件是Vue中的一个重要概念，是一个可复用的Vue实例，拥有独一无二的组件名称，可以拓展HTML元素，以组件名称的方式作为自定义的HTML标签。

因为组件是可复用的Vue实例，所以他们与new Vue()接收相同的选项如data,computed等以及生命周期钩子等，仅有的例外是想el这样根实例特有的选项。

就相当于是函数，在编程中将重复的内容打包成函数，在vue中打包成组件，都可以重复调用。

vue的组件化更多的是为了实现对于前端UI组件的重用。



### 组件的注册

在vue创建一个新的组件之后，为了能在模板中使用，这些组件必须先进行注册，以便Vue能够识别，在Vue中有两种组件的注册类型：全局注册和局部注册。

全局注册的组件可以用在通过new Vue新创建的根实例当中，也可以在组件树中的所有子组件的模板中使用。

而局部组件只能在当前注册的Vue实例中进行使用

#### 全局注册

在Vue中创建全局则兼，通常的做法是先使用Vue.extend方法构建模板对象，然后通过Vue.component方法来注册组件。

> 组件最后会被解析成自定义的html代码，因此，可以直接在HTML中使用组件名称作为标签来使用

```vue
<div id="app">
  <aaa></aaa>
</div>
<script>
  //1.使用Vue.extend构建模板对象
  var comElement=Vue.extend({
    template:'<div><h3>这是我们创建的全局组件</h3></div>'
  })
  //2,使用component注册全局组件
  Vue.component('aaa',comElement)
  var app=new Vue({
    el:'#app',
    data:{
    },
  })
</script>
```

模板对象和全局组件的名称都可以自己设置，效果如下：![image-20220402124447157](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220402124447157.png)

当然也可以在Vue.component中以匿名对象的方式直接注册全局组件。

```javascript
  //直接以匿名的形式不构建模板直接创建组件
  Vue.component('bbb',Vue.extend({
    template:'<div>直接在vue.component中创建组件</div>'
  }))
```

上面的实例中，只是在template属性中输入了一个简单的HTML代码，在实际的使用中，template属性执行的模板内容可能包含很多的元素，而使用Vue.extend创建的模板必须有且只有一个根元素，当出现多个根元素时，默认只渲染第一个根元素的内容。因此当需要创建具有复杂元素的模板时，可以在最外层再套一个div。如下面就是一次错误的示范：

```javascript
var aaa=Vue.extend({
    template:'<h3>aaa</h3><p>bbb</p>'
})
Vue.component('my-com',aaa)
```

此时调用时只会渲染了h3标签，p标签没有被渲染，而解决办法是在最外边添加一个div来吧这两个标签包起来

```javascript
var aaa=Vue.extend({
    template:'<div><h3>aaa</h3><p>bbb</p></div>'
})
```

当tamplate属性中包含很多元素时，不能使用代码提示会显得很不方便，此时可以使用template标签俩定义模板，通过id来确定组件的模板信息。

```vue
<template id="tmp">
  <div>
    <h3>aaa</h3>
    <p>bbb</p>
  </div>
</template>

Vue.component('my-com',{
    template:'#tmp'     //使用id来确定组件的模板信息
  })
```

#### 局部注册

有些时候注册的组件只想在一个vue实例中使用，可以通过components属性注册仅在当前作用域下可用的组件

```javascript
<template id ='aaa'> 
	....    
</template>
var app=new Vue({
    el:'#app',
    components:{
        'my-com':{
        template:'#aaa'
    }}
})
```

### 组件中的data选项

当一个Vue实例被创建后，实例中的data选项的属性值就与页面的视图做了一个绑定，组件作为一个特殊的Vue实例，在创建组件实例中额data选项时，返回的是一个实例对象的方法：

```javascript
Vue.component('my-com',{
    template:'#tmp'     //使用id来确定组件的模板信息
    data:function(){
     	return {name:'马云'}
}}})
```

然后就可以在组件中调用组件中的data数据了，如：

```vue
<template id=tmp>
	<p>{{name}}</p>
</template>
```

> 在Vue的官方文档中说明：一个组件的data选项必须是一个函数，因此每个实例可以维护一份被返回对象的独立拷贝。

在组件中也可以使用methods,watch等方法并调用，组件就相当于一个小的Vue模块用的时候放哪都行。

### 组件中的props选项

组件的props选项时在组件上注册的一些自定义特性，将一个值传递给props选项中的特性时，那个props特性就变成组件实例的一个属性，这时就可以获取到这个值了。因此组件中props经常用于将父组件的值传递早子组件或是将Vue实例中的属性值传递到组件中使用。

在父组件引用子组件时，通过属性绑定的方式（v-bind）将需要传递给子组件的数据进行传递，从而在子组件内部，通过绑定的属性值获取到父组件的数据。

在下例中实现了一个局部组件，将实例的title属性绑定到组件的parenttitle属性上，同时将parenttitle属性值赋给组件的content属性。

> 就是相当于想将实例中的值穿透到实例中的组件中

```vue
<h3>请输入要传给子组件的值：<input type="text" v-model="title"></h3>
  <childnode :parenttitile="title"></childnode>

<template id="child">
  <h3>Vue实例中的属性值为：{{content}}</h3>
</template>

<script>
data:{
      title:'',
    },
    components:{
      'childnode':{
        template:'#child',
        props:['parenttitle'],
        data:function(){
          return {
            content:this.parenttitle
          }}}}
</script>
```

上面的代码是在自定义组件childnode标签上增加了一个parenttitle属性，将这个属性绑定到vue根实例中。在组件中根据这个设置的属性来获取vue根实例中data的值

相当于是输入框输入的值传给了根实例的title，然后在组件中将title与组件的这个属性进行绑定，这样修改组件的这个属性就可以修改外部的根实例中data的值了。

但是网页上无法同步更新组件的content属性。因为组件的data选项中的content属性是一个string，在创建时就已经将数据值写入到内存栈中，所以之后不管怎么着组件的data中的content都不会变。有两个解决办法：

- 将vue根实例中的title属性改为一个对象，输入的值作为对象中的一个属性
- 采取watch监听parenttitle的方式来更新实例中的connet属性

第二种方法如下所示：

```vue
<div id="app">
  <input type="text" v-model="title"/>
  <childnode :p="title"></childnode>
</div>
<template id="child">
  <div>输入的值为：{{content}}</div>
</template>

<script>
  var app=new Vue({
    el:'#app',
    data:{
      title:''
    },
    components:{
      'childnode':{
        template:'#child',
        props:['p'],
        data(){
          return {content:this.p}
        },
        watch:{
          p(){
            this.content=this.p
   			  }}}}})
</script>
```

结果为组件可以根据外面vue根实例的值来改变自身组件内data 的值![image-20220402223507550](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220402223507550.png)

> 一个组件的props可以有很多个如`props:['a','b']`,data方法中储存的数量也可以有很多
>
> 所有的props都是的父子props之间形成了一份单向下行绑定：父级props的更新会向下流动到子组件中，但是翻过来不行，这样会防止从子组件恶意改变父级组件的状态

### 组件的复用

创建好一个组件后，就可以使用组件定义的标签来无限次使用，它们之间是相互隔绝的，如下：

```javascript
Vue.component('click',{
  data:function (){
    return {
      count:0
    }
  },
  template:'<button @click="count++">你单击了{{count}}次</button>'
})
```

`<click></click> <click></click>`像这样就复用了两个这个组件，这两个组件之间不会互相影响，当单击按钮时，每个组件都会各自独立维护它的count，因为每用一次组件，就会有一个它的新实例被创建。

![image-20220402221909424](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220402221909424.png)

### 组件间的数据通信

#### 父组件向子组件通信

如上例props例子所述，用v-bind绑定了组件的一个元素到父组件上的一个数据，用watch来监听这个父组件 上的数据从而达到实时更新的效果。

#### 子组件向父组件通信

因为vue存在着单向的下行绑定，如果想要实现子组件向上传数据，可以在子组件数据发生变化后，触发一个事件方法，告诉父组件数据更新了，父组件只需要监听这个事件，当捕捉到这个事件运行后，再对父组件的数据进行同步变更。

可以使用v-on事件监听器监听事件，通过`$emit`去触发当前实例上的事件。这个事件可以是js中的原生DOM事件，也可以是自定义事件。

> 目前有问题



> ### vue组件的通信方式
>
> - `props`/`$emit` 父子组件通信
>
>   父->子`props`，子->父 `$on、$emit` 获取父子组件实例 `parent、children` `Ref `获取实例的方式调用组件的属性或者方法 父->子孙 `Provide、inject` 官方不推荐使用，但是写组件库时很常用
>
> - `$emit`/`$on` 自定义事件 兄弟组件通信
>
>   `Event Bus` 实现跨组件通信 `Vue.prototype.$bus = new Vue()` 自定义事件
>
> - vuex 跨级组件通信
>
>   Vuex、`$attrs、$listeners` `Provide、inject`

### 插槽

插槽也就是slot,他是组件的一块html模板，这块模板显不显示以及怎样显示由父组件来决定。

#### 认识插槽

从三个方面来认识一下插槽：插槽内容，编译作用域和默认内容

##### 插槽内容

将`<slot>`元素作为承载分发内容的出口，它允许合成组件，代码如下：

```vue
<nag url="/profile">你的个人信息</nag>
```

然后在nag的模板中编写以下代码：

```javascript
Vue.component('neg',{
    template:'<div><a :href="url"><slot></slot></a></div>'
  })
```

当组件渲染的时候`<slot></slot>`会被替代为‘你的个人信息’。插槽内可以包含任何的模板代码，包括html，甚至可以是其他组件的标签

> 就相当于可以在组件内的任意位置放一个可以放任何东西的块，这个块的位置就是`<slot></slot>`放的位置，只有在放了插槽之后，在组件的自定义标签内才可以写东西，如neg组件内有`<slot></slot>`时，才能在`<neg> </neg>`中添加内容并将内容放到slot的位置，否则的话该组件标签内的所有内容都不会被渲染。可以需要的时候就插进去，不需要的时候就拔出来，所以叫插槽。

##### 编译作用域

想在一个插槽中使用数据时，例如：`<nag >登录：{{name}}</nag>`,此时访问的是vue根实例中的data而不是组件中的data

##### 默认内容

在slot标签中写一些当这个插槽的默认值，在没有用这个插槽的时候会显示默认值如`<slot>默认值</slot>`



#### 具名插槽：v-slot

它取代了slot和slot-scope特性。

在上面我们只用到了一个插槽，但有时需要多个插槽，例如对于一个带有如下模板的`<base-layout>`组件：

```vue
<div id="container">
  <header><slot name="header"></slot></header>
  <main><slot></slot></main>
  <footer><slot name="footer"></slot></footer>
</div>
```

`<slot>`元素有一个特性：name，这个特性可以用来定义额外的插槽，一个不带name的slot出口会带有隐含的名字default.

在向具名插槽提供内容的时候，可以在一个template元素上使用v-slot指令，并以v-slot的参数的形式提供其名称。

```vue
<base-layout>
  <template v-slot:header>
    <h1>这是头部</h1>
  </template>
  <p>这是一段内容</p>
  <template v-slot:footer>
    <p>这是一些联系方式</p>
  </template>
</base-layout>
```

组件的创建如下：

```javascript
Vue.component('base-layout',{
    template:'<div><header><slot name="header"></slot>\n' +
      '  </header>\n' +
      '  <main><slot></slot></main>\n' +
      '  <footer><slot name="footer"></slot></footer></div>'
  })
```

在组件的创建中留下了三个插槽位，通过`<template v-slot:> </template>`来向指定name的插槽中插入指定的内容，如果插槽slot没写name就是默认的剩下内容，这些内容与位置无关，只认name。

v-slot也有简写，为`#`，`v-slot:header`可以被简写为`#header`

#### 作用域插槽

有时让插槽内容能够访问子组件汇总才有的数据是很有用的



## 使用webpack打包

高效的开发离不开基础工程的搭建。webpack是js应用程序的模块打包工具，需要先安装node.js和NMP

### 前端工程化与webpack

通常，前端自动化工程主要解决以下问题：

- js，css代码的合并和压缩
- css预处理：less，Sass，stylus的编译
- 生成雪碧图（css Sprite）
- ES6转ES5
- 模块化

![img](https://img0.baidu.com/it/u=3202904112,1274829769&fm=253&fmt=auto&app=138&f=PNG?w=857&h=500)

如上图，左边是在业务中写的各种格式的文件，如typescript，less，.vue格式的文件等。这些格式的文件通过特定的加载器（Loader）编译后，最终统一生成为.js, .css, .png等静态资源文件。

在webpack的世界里，一张图片，一个css甚至一个字体都称为模块彼此存在依赖关系。webpack就是用来处理模块之间的依赖关系的，并把它们进行打包。

举个简单的例子，平时加载css大多通过`<link>`标签引入css文件，而在webpack里，直接在一个.js文件中导入，例如：

```javascript
import 'src/styles/index.css'
```

import是es2015的语法，也可以写成require('src/styles/index.css')。在打包时，index.css会被打包进一个.js文件里，通过动态创建`<style>`的形式来加载css样式，当然也可以进一步配置，在打包编译时把所有的css都提取出来，生成一个css的文件。

webpack主要的应用场景是单页面复应用（SPA）。SPA通常是由一个HTML文件和一堆按需要加载的js组成，它的html结构可能会非常简单，例如

```html
<link href='dist/main.css'>
<div id='app'></div>
<script src='dist/main.js'></script>
```

代码中只有一个div节点，所有的代码都集成到了main.js中，但它可以实现像知乎淘宝这样的大型项目。

在介绍webpack之前，先介绍两个ES6中的语法：`export`和`import`

export是导出模块用的，import是导入模块用的。一个模块就是一个js文件，它拥有独立的作用域，里面定义的变量外部是无法获取的，此时就可以使用export将想导出的内容导出，包括函数，数组，常量等

```javascript
//这个js文件是config.js
var config{
    version:'1.0.0'
}
export{config}
//或是直接导出
export var config={
    version:'1.0.0'
}

//add.js
export function add(a,b){
    return a+b
}
```

模块导出之后，在需要使用模块的文件再使用import导入，就可以在这个文件内使用这些模块了，如：

```javascript
//这个文件是main.js
import{{config}} from './config.js'
import {{add}} from './add.js'
```

如果使用NPM安装了一些库，在webpack中可以直接导入，如：

```javascript
import Vue from 'vue'
import $ from 'jquery'
```

这样就分别导入了vue和jQuery的库并命名为Vue和$了，在这个文件中就可以使用者两个模块了。



### webpack基础配置

首先创建一个目录，使用NPM初始化配置`npm init`然后会有一系列选项，可以根据需求填写也可以直接按enter一直跳过，完成后会在当前目录下生成一个package.json文件。之后就可以在本地局部安装webpack

` npm install webpack --save -dev`  --save-dev会作为开发依赖来安装webpack，安装成功后在package.json中的devDependencies会多一项配置

![image-20220404152237580](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404152237580.png)

> npm install 在安装npm包时，有两种命令参数可以把它们的信息写入package.json文件，一个是`npm install --save`，一个是`npm install --save-dev`

如果是webpack4+版本还需要**安装脚手架**

 `npm install --save -dev webpack-cli`

>  通过以下的npm安装方式，将使webpack在全局环境下可用`npm install --global webpack`但是不推荐安装全局webpack，这会将项目中的webpack锁定到指定版本，在使用不同的webpack版本的项目中，可能会导致构建失败。

接着需要安装`webpack-dev-server`,他可以在开发环境中提供很多服务，如启动一个服务器，热更新，接口代理等，配置起来也很简单，在本地局部安装的代码如下：

`npm install webpack-dev-server --save-dev`



### webpack5个核心概念：

- Entry：入口，指示webpack以哪个文件作为入口起点开始打包，分析结构内部依赖图
- output：输出，指示webpack打包后的资源bundles输出到哪里去，以及如何命名
- loader：让webpack能够去处理那些非js文件，如css，img文件等（webpack本身只能理解js）
- plugins：插件，可以用于执行范围更广的任务，插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量等。
- Mode：模式，指示webpack使用相应模式的配置，包括开发模式和生产模式。



## 项目脚手架vue-cli

vue-cli是一个官方发布的Vue项目脚手架，使用vue-cli可以快速创建vue项目

### 脚手架的组件

脚手架致力于将Vue生态中的工具基础标准化。它确保了各种构建工具能够基于智能的默认配置平稳衔接，这样开发人员可以专注于撰写应用上，而不必话好几天去纠结配置的问题，于此同时，它也为每个工具提供了调整配置的灵活性，无需ejecy

vue-cli有几个独立的部分：

- **cli**：是一个全局安装的npm包，提供了终端里的vue命令。它可以通过cue create命令快速创建一个新项目的脚手架，或直接通过vue serve命令构建新想法的原型。也可以使用vue ui 命令，通过一套图形化界面管理所有项目。
- **cli服务**：是一个开发环境依赖，是一个npm包，局部安装在每个@vue/cli创建的项目中。

​		cli服务是构建与webpack和webpack-dev-server之上的，它包含以下内容：	

		1. 加载其他cli插件的核心服务
		1. 一个针对绝大部分应用优化过的内部webpack配置
		1. 项目内部的vue-cli-service命令，提供serve,build ,和inspect命令

- **cli插件**：是向vue项目提供可选功能的npm包，vue-cli插件的名字以@vue/cli-plugin-(内置插件)或vue-cli-plugin-(社区插件)开头，使用非常方便。在项目中运行vue-cli-service命令时，它会自动解析并加载package.json中列出的所有cli插件。

  插件可以作为项目创建过程的一部分，或在后期加入到想目中。它们也可以被归成一组可复用的preset

### 脚手架的安装

首先去官网下载最新的node.js,然后用以下的命令来安装脚手架

`npm install -g @vue/cli`

安装完成后，可以通过`vue --version`查看是否安装上，版本是否正确：

![image-20220404205237815](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404205237815.png)

### 创建项目

脚手架的环境配置完成后便可以使用脚手架来快速创建项目

#### 使用命令

首先打开到想要创建项目的路径文件夹内，输入指令

```vue
vue create cli_test //注意项目的名字不能大写，否则无法创建
```

输入这行指令后，它会问我们使用默认的配置还是手动配置，我们选择默认配置直接按enter即可创建好cli_test项目，是一个文件夹

![image-20220404205831501](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404205831501.png)

可以在该目录下输入`npm run server`命令启动项目，项目启动后会给我们提供本地的测试域名

![image-20220404210110533](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404210110533.png)

可以在浏览器中输入这个地址来打开这个项目

#### 使用图形化界面

可以在指定的文件夹地址内输入`vue ui`命令，即可在默认的浏览器上打开图形化界面

![image-20220404210528289](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404210528289.png)

然后就可以跟着图形化界面一步步的完成创建，创建完成后，文件夹内就可以看到新创建的项目文件夹，浏览器显示如下：

![image-20220404222000344](C:\Users\tao'ge\AppData\Roaming\Typora\typora-user-images\image-20220404222000344.png)

四个部分为插件，依赖，配置和任务。可以装一些其他人的插件和配置依赖项

> 不知道为什么，好像现在只能在c盘内通过vue ui创建项目

## tips

- 使用vue指令(如v-on,v-bing等)的最大用处就是将vue中的data中的数据与该条html语句绑定上或是使用data中的属性，如`<button @click="a++">`就是点一下就将data中的a属性加1

- 在Vue事件中，可以使用事件的名称直接进行调用(如add)，也可以在事件后加括号调用(add())，但是在有参数时必须加括号，在双大括号{{}}中时也必须加括号add()

- 如果想让一个文字在div中居中，可以设置文字的text-align:center,然后使文字的行高与div的高度一致，这样就可以实现文字在中间了。

  如果一个div想在另一个div中居中，可以通过设置margin来达到这个效果，如果是正方形就统一设置，如果是矩形就分别设置各个边的margin
  
- 如果想以块为单位进行vue操作如使用v-for来一块一块的创建列表，要使用==template标签==来将这一块包裹起来，不要使用div进行包裹，会出现问题。

- 对于事件的命名，因为在不同的场景可能是否区分大小写是不一定的，所以建议使用驼峰式命名:a-b而不是aB
