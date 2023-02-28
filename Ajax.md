# 第一章、初识Ajax

## 1、Ajax基础

### 1.1 传统网站中存在的问题

- 网速慢的情况下，页面加载时间长，用户只能等待
- 表单提交后，如果一项内容不合格，需要重新填写所有表单内容
- 页面跳转，重新加载页面，造成资源浪费，增加用户等待时间

### 1.2 Ajax 概述

Ajax：标准读音 [ˈeɪˌdʒæks] ，中文音译：阿贾克斯。
它是浏览器提供的一套方法，可以实现 **页面无刷新更新数据，提高用户浏览网站应用的体验**。

### 1.3 Ajax 应用场景

- 页面上拉加载更多数据
- 列表数据无刷新分页
- 表单项离开焦点数据验证
- 搜索框提示文字下拉列表
- ...

### 1.4 Ajax 运行环境

Ajax 技术需要 **运行在网站服务器环境中才能生效**，我们学习 Ajax 可以使用 Node 创建的服务器作为网站服务器。

## 2. Ajax 运行原理及实现

Ajax 相当于浏览器 **发送请求与接收响应的代理人**，以实现在不影响用户浏览页面的情况下，局部更新页面数据，从而提高用户体验。

## 3.URL

URL（全称是UniformResourceLocator）中文叫统一资源定位符，用于标识互联网上每个资源的唯一存放位置。浏览器只有通过URL地址，才能正确定位资源的存放位置，从而成功访问到对应的资源。
常见的URL举例：

+ http://www.baidu.com

**URL地址的组成部分**

URL地址一般由三部组成：
①客户端与服务器之间的通信协议
② 存有该资源的服务器名称
③ 资源在服务器上具体的存放位置

![image-20230222152950102](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230222152950102.png)

# 第二章、jquery中的Ajax

浏览器中提供的 ==XMLHttpRequest 用法比较复杂==，所以 jQuery 对 XMLHttpRequest 进行了封装，提供了一系列 Ajax 相关的函数，极大地==降低了 Ajax 的使用难度==。
jQuery 中发起 Ajax 请求最常用的三个方法如下：

+ $.get()

+ $.post()

+ $.ajax()

## 2.1、$.get()函数的语法

jQuery 中 `$.get()` 函数的功能单一，专门用来发起 get 请求，从而将服务器上的资源请求到客户端来进行使用。
$.get() 函数的语法如下：

```js
$.get(url, [data], [callback])
```

| **参数名** | **参数类型** | **是否必选** | **说明**                 |
| ---------- | ------------ | ------------ | ------------------------ |
| url        | string       | 是           | 要请求的资源地址         |
| data       | object       | 否           | 请求资源期间要携带的参数 |
| callback   | function     | 否           | 请求成功时的回调函数     |

使用 $.get() 函数发起不带参数的请求时，直接提供**请求的 URL 地址和请求成功之后的回调函数**即可，示例代码如下：

```js
$.get('http://www.liulongbin.top:3006/api/getbooks', function(res) {
    console.log(res) // 这里的 res 是服务器返回的数据
})
```

## 2.2、$post()函数的语法

jQuery 中 `$.post()` 函数的功能单一，专门用来发起 post 请求，从而将服务器提交数据。
$.post() 函数的语法如下：

```js
$.post(url, [data], [callback])
```

| **参数名** | **参数类型** | **是否必选** | **说明**                 |
| ---------- | ------------ | ------------ | ------------------------ |
| url        | string       | 是           | 要请求的资源地址         |
| data       | object       | 否           | 请求资源期间要携带的参数 |
| callback   | function     | 否           | 请求成功时的回调函数     |

```js
$.post(
   'http://www.liulongbin.top:3006/api/addbook', // 请求的URL地址
   { bookname: '水浒传', author: '施耐庵', publisher: '上海图书出版社' }, // 提交的数据
   function(res) { // 回调函数
      console.log(res)
   }
) 
```

## 2.3、$ajax()函数的语法

相比于 `$.get()` 和 `$.post()` 函数，jQuery 中提供的 `$.ajax()` 函数，是一个功能比较综合的函数，它允许我们对 Ajax 请求进行更详细的配置。
`$.ajax() `函数的基本语法如下：

```js
$.ajax({
   type: '', // 请求的方式，例如 GET 或 POST
   url: '',  // 请求的 URL 地址
   data: { },// 这次请求要携带的数据
   success: function(res) { } // 请求成功之后的回调函数
})
```



# 第三章、form表单的基本使用

## 1、form简介

### 1.1、什么是表单

表单在网页中主要负责数据采集功能。HTML中的<form>标签，就是用于采集用户输入的信息，并通过<form>标签的提交操作，把采集到的信息提交到服务器端进行处理。

### 1.2、组成

+ 表单标签
+ 表单域  ：包含了文本框、密码框、隐藏域、多行文本框、复选框、单选框、下拉选择框和文件上传框等。
+ 表单按钮

## 2、form属性

| **属性** | **值**                                                       | **描述**                                  |
| -------- | ------------------------------------------------------------ | ----------------------------------------- |
| action   | URL地址                                                      | 规定当提交表单时，向何处发送表单数据      |
| method   | get或post                                                    | 规定以何种方式把表单数据提交到 action URL |
| enctype  | application/x-www-form-urlencodedmultipart/form-datatext/plain | 规定在发送表单数据之前如何对其进行编码    |
| target   | _blank_self_parent_top*framename*                            | 规定在何处打开 action URL                 |

### 2.1、action

action 属性用来规定当提交表单时，向何处发送表单数据。
action 属性的值应该是后端提供的一个 URL 地址，这个 URL 地址专门负责接收表单提交过来的数据。
当 <form> 表单在未指定 action 属性值的情况下，action 的默认值为当前页面的 URL 地址。

==注意：当提交表单后，页面会立即跳转到 action 属性指定的 URL 地址==

### 2.2、target

target 属性用来规定==在何处打开 action URL==。
它的可选值有5个，默认情况下，target 的值是 _self，表示在相同的框架中打开 action URL。

| 值        | 说明                           |
| --------- | ------------------------------ |
| _blank    | 在新窗口中打开。               |
| _self     | 默认。在相同的框架中打开。     |
| _parent   | 在父框架集中打开。（很少用）   |
| _top      | 在整个窗口中打开。（很少用）   |
| framename | 在指定的框架中打开。（很少用） |

### 2.3、method

method 属性用来规定==以何种方式==把表单数据提交到 action URL。
它的可选值有两个，分别是 get 和 post。
默认情况下，method 的值为 get，表示通过URL地址的形式，把表单数据提交到 action URL。

==注意：==
get 方式适合用来提交少量的、简单的数据。
post 方式适合用来提交==大量的、复杂的==、或包含==文件上传==的数据。
在实际开发中，<form> 表单的 post 提交方式用的最多，很少用 get。例如登录、注册、添加数据等表单操作，都需要使用 post 方式来提交表单。

### 2.4、enctype

enctype 属性用来规定在==发送表单数据之前如何对数据进行编码==。
它的可选值有三个，默认情况下，enctype 的值为 application/x-www-form-urlencoded，表示在发送前编码所有的字符。

| 值                                | 描述                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| application/x-www-form-urlencoded | 在发送前编码所有字符（默认）                                 |
| multipart/form-data               | 不对字符编码。
在使用包含文件上传控件的表单时，必须使用该值。 |
| text/plain                        | 空格转换为 “+” 加号，但不对特殊字符编码。（很少用）          |

注意：
在涉及到==文件上传==的操作时，==必须==将 enctype 的值设置为 ==multipart/form-data==
如果表单的提交不涉及到文件上传操作，则直接将 enctype 的值设置为 application/x-www-form-urlencoded 即可！

## 3、表单的同步提交

### 3.1、什么是表单的同步提交

通过点击 submit 按钮，触发表单提交的操作，从而使页面跳转到 action URL 的行为，叫做表单的同步提交。

### 3.2、缺点

 ① form表单同步提交后，整个页面会发生跳转，跳转到 action URL 所指向的地址，用户体验很差。

 ② form表单同步提交后，页面之前的状态和数据会丢失。

==解决方案：==表单只负责采集数据，Ajax 负责将数据提交到服务器。

### 3.3、阻止表单默认提交行为

当监听到表单的提交事件以后，可以调用事件对象的 `event.preventDefault()` 函数，来阻止表单的提交和页面的跳转，示例代码如下：

```js
$('#form1').submit(function(e) {
   // 阻止表单的提交和页面的跳转
   e.preventDefault()
})

$('#form1').on('submit', function(e) {
   // 阻止表单的提交和页面的跳转
   e.preventDefault()
})
```

### 3.4 serialize 方法的使用

**快速获取表单数据**

`serialize()` 方法将表单中的数据自动拼接成字符串类型的参数。

```js
var params = $('#form').serialize();
// name=zhangsan&age=30
```

案例：将表单内容拼接成字符串类型的参数

HTML 结构

```html
<form id='form'>
    <input type='text' name='username'>
    <input type='password' name='password'>
    <input type='submit' value='提交'>
</form>
```

方法一：使用 `serialize()` 将参数拼接成 `name=zhangsan&age=30` 类型字符串。

```js
$('#form').on('submit', function () {
    // 将表单内容拼接成字符串类型的参数
    var params = $('#form').serialize();
    console.log(params)
    return false;
});
```

方法二：使用 `serializeArray()`，通过一定转换，使表单数据转换为 `{name: 'zhangsan', age: 100}` JSON 对象类型。

```js
$('#form').on('submit', function () {
    // 将表单内容拼接成字符串类型的参数
    serializeObject($(this));
    return false;
});

// 将表单中用户输入的内容转换为对象类型
function serializeObject (obj) {
    // 处理结果对象
    var result = {};
    // [{name: 'username', value: '用户输入的内容'}, {name: 'password', value: '123456'}]
    var params = obj.serializeArray();
    // 循环数组 将数组转换为对象类型
    $.each(params, function (index, value) {
        result[value.name] = value.value;
    })
    // 将处理的结果返回到函数外部
    return result;
}
```

# 第四章、模板引擎

## 1、模板引擎基本概念

art-template 是一个简约、超快的模板引擎。中文官网首页为 http://aui.github.io/art-template/zh-cn/index.html

**安装**

在浏览器中访问 http://aui.github.io/art-template/zh-cn/docs/installation.html 页面，找到下载链接后，鼠标右键，选择“链接另存为”，将 art-template 下载到本地，然后，通过 <script> 标签加载到网页上进行使用。

## 2、基本使用

1. 导入 art-template
2. 定义数据
3. 定义模板
4. 调用 template 函数
5. 渲染HTML结构

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- 1.导入模板引擎，在windows全局，多了一个函数，叫做template('模板的Id ,需要渲染的数据对象') -->
    <script src="template-web.js"></script>
    <script src="jquery-3.6.1.min.js"></script>
</head>

<body>

    <div id="container"></div>

    <!-- 3.定义定义模板 -->
    <!-- 3.1模板的标签需要定义在scriot标签中 -->
    <script type="text/html" id="tpl-user">
        <h1>{{name}}</h1>
    </script>
    <script>
        //2.定义数据
        let data = { name: "zs" };

        //4.调用调用模板Id
        let htmlstr = template("tpl-user",data);
        console.log(htmlstr);         //<h1>zs</h1>

        //5.操作DOM元素
        $('#container').html(htmlstr)
    </script>
</body>

</html>
```



### 2.1、标准语法-输出

```js
{{value}}
{{obj.key}}
{{obj['key']}}
{{a ? b : c}}
{a || b}
{{a + b}}
```

在 {{ }} 语法中，可以进行==变量的输出、对象属性的输出、三元表达式输出、逻辑或输出、加减乘除==等表达式输出。

### 2.2、标准语法-原文输出

```js
{{@ value}}
```

如果要输出的 value 值中，包含了==HTML 标签结构==，则需要使用原文输出语法，才能保证 HTML 标签被正常渲染。 

### 2.3、标准语法-条件输出

如果要实现条件输出，则可以在 {{ }} 中使用 ==if … else if … /if== 的方式，进行按需输出。

```
{{if value}} 按需输出的内容 {{/if}}

{{if v1}} 按需输出的内容 {{else if v2}} 按需输出的内容 {{/if}}
```

### 2.4、标准语法-循环输出

如果要实现循环输出，则可以在 {{ }} 内，通过 each 语法循环数组，当前循环的索引使用` $index` 进行访问，当前的循环项使用 $value 进行访问。

```
{{each arr}}
    {{$index}} {{$value}}
{{/each}}
```

### 2.5、标准语法-过滤器

过滤器本质：就是一个function处理函数

```
{{value | filterName}}
```

过滤器语法类似==管道操作符==，它的上一个输出作为下一个输入。
定义过滤器的基本语法如下：

```
template.defaults.imports.filterName = function(value){/*return处理的结果*/}
```

**例子**

```js
<div>注册时间：{{regTime | dateFormat}}</div>

 template.defaults.imports.dateFormat = function(date) {
    var y = date.getFullYear()
    var m = date.getMonth() + 1
    var d = date.getDate()

    return y + '-' + m + '-' + d // 注意，过滤器最后一定要 return 一个值
 }
```

## 3、模板引擎的实现原理

### 3.1、正则与字符串操作

#### 3.1.1、基本语法

exec() 函数用于检索字符串中的正则表达式的匹配。
如果字符串中有匹配的值，则返回该匹配值，否则返回 null。

```js
RegExpObject.exec(string)
```

**示例**

```js
var str = 'hello'
var pattern = /o/
// 输出的结果["o", index: 4, input: "hello", groups: undefined]
console.log(pattern.exec(str)) 
```

#### 3.1.2、分组

正则表达式中 ( ) 包起来的内容表示一个分组，可以通过分组来==提取自己想要的内容==，示例代码如下：

```js
 var str = '<div>我是{{name}}</div>'
 var pattern = /{{([a-zA-Z]+)}}/

 var patternResult = pattern.exec(str)
 console.log(patternResult)
 // 得到 name 相关的分组信息
 // ["{{name}}", "name", index: 7, input: "<div>我是{{name}}</div>", groups: undefined]
```

#### 3.1.3、replace函数

replace() 函数用于在字符串中**用一些字符替换另一些字符**，语法格式如下：

```js
replace() 函数用于在字符串中用一些字符替换另一些字符，语法格式如下：
```

**示例**

```js
var str = '<div>我是{{name}}</div>'
var pattern = /{{([a-zA-Z]+)}}/

var patternResult = pattern.exec(str)
str = str.replace(patternResult[0], patternResult[1]) // replace 函数返回值为替换后的新字符串
// 输出的内容是：<div>我是name</div>
console.log(str)
```

#### 3.1.4、多次replace

```js
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

var patternResult = pattern.exec(str)
str = str.replace(patternResult[0], patternResult[1])
console.log(str) // 输出 <div>name今年{{ age }}岁了</div>

patternResult = pattern.exec(str)
str = str.replace(patternResult[0], patternResult[1])
console.log(str) // 输出 <div>name今年age岁了</div>

patternResult = pattern.exec(str)
console.log(patternResult) // 输出 null
```

#### 3.1.5、while循环替换replace

```
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

var patternResult = null
while(patternResult = pattern.exec(str)) {
   str = str.replace(patternResult[0], patternResult[1])
}
console.log(str) // 输出 <div>name今年age岁了</div>

```

#### 3.1.6、replace替换为真值

```js
var data = { name: '张三', age: 20 }
var str = '<div>{{name}}今年{{ age }}岁了</div>'
var pattern = /{{\s*([a-zA-Z]+)\s*}}/

var patternResult = null
while ((patternResult = pattern.exec(str))) {
   str = str.replace(patternResult[0], data[patternResult[1]])
}
console.log(str)
```



### 3.2、实现简易的模板引擎

+ 定义模板结构
+ 预调用模板引擎
+ 封装 template 函数
+ 导入并使用自定义的模板引擎

#### 3.2.1、定义模板结构

```html
<!-- 定义模板结构 -->
<script type="text/html" id="tpl-user">
   <div>姓名：{{name}}</div>
   <div>年龄：{{ age }}</div>
   <div>性别：{{  gender}}</div>
   <div>住址：{{address  }}</div>
</script>
```

#### 3.2.2、预调用模板引擎

```html
<script>
   // 定义数据
   var data = { name: 'zs', age: 28, gender: '男', address: '北京顺义马坡' }
   // 调用模板函数
   var htmlStr = template('tpl-user', data)
   // 渲染HTML结构
   document.getElementById('user-box').innerHTML = htmlStr
</script>
```

#### 3.2.3、封装template函数

```js
function template(id, data) {
  var str = document.getElementById(id).innerHTML;
  var pattern = /{{\s*([a-zA-Z]+)\s*}}/
  var pattResult = null
  while ((pattResult = pattern.exec(str))) {
    str = str.replace(pattResult[0], data[pattResult[1]])
  }
  return str;
}
```

#### 3.2.4、导入并使用自定义的模板引擎

```html
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>自定义模板引擎</title>
    <!-- 导入自定义的模板引擎 -->
    <script src="./js/template.js"></script>
</head>
```

# 第五章、xhr的基本使用

## 1、什么是XMLHttpRequest

XMLHttpRequest（简称 xhr）是浏览器提供的 Javascript 对象，通过它，可以==请求服务器上的数据资源==。之前所学的 jQuery 中的 Ajax 函数，就是基于 xhr 对象封装出来的。

## 2、使用xhr发送GET请求

### 2.1、步骤

① 创建 xhr 对象

② 调用 xhr.open() 函数

③ 调用 xhr.send() 函数

④ 监听 xhr.onreadystatechange 事件

```js
// 1. 创建 XHR 对象
var xhr = new XMLHttpRequest()
// 2. 调用 open 函数，指定 请求方式 与 URL地址
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
// 3. 调用 send 函数，发起 Ajax 请求
xhr.send()
// 4. 监听 onreadystatechange 事件
xhr.onreadystatechange = function() {
    // 4.1 监听 xhr 对象的请求状态 readyState ；与服务器响应的状态 status
    //注意这里的status和请求回来数据中的status不一样
    //这里的status是响应状态
    //请求回来的数据的status是数据的一个属性
    if (xhr.readyState === 4 && xhr.status === 200) {
        // 4.2 打印服务器响应回来的数据
        console.log(xhr.responseText)
    }
}
```

### 2.2、了解xhr对象的readyState属性

XMLHttpRequest 对象的 readyState 属性，用来表示当前 Ajax 请求所处的状态。每个 Ajax 请求必然处于以下状态中的一个：

| **值** | **状态**         | **描述**                                            |
| ------ | ---------------- | --------------------------------------------------- |
| 0      | UNSENT           | XMLHttpRequest 对象已被创建，但尚未调用 open方法。  |
| 1      | OPENED           | open() 方法已经被调用。                             |
| 2      | HEADERS_RECEIVED | send() 方法已经被调用，响应头也已经被接收。         |
| 3      | LOADING          | 数据接收中，此时 response 属性中已经包含部分数据。  |
| 4      | DONE             | Ajax 请求完成，这意味着数据传输已经彻底完成或失败。 |

## 3、查询字符串

使用 xhr 对象发起带参数的 GET 请求时，只需在调用 xhr.open 期间，为 URL 地址指定参数即可：

```
// ...省略不必要的代码
xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks?id=1')
// ...省略不必要的代码
```

这种在 URL 地址后面拼接的参数==（？id = 1）==，叫做==查询字符串==。

### 3.1、定义

定义：查询字符串（URL 参数）是指在 URL 的末尾加上用于向服务器发送信息的字符串（变量）。
格式：将英文的 ==?== 放在URL 的末尾，然后再加上 ==参数＝值== ，想加上多个参数的话，使用 ==&== 符号进行分隔。以这个形式，可以将想要发送给服务器的数据添加到 URL 中。

### 3.2、本质

无论使用 $.ajax()，还是使用 $.get()，又或者直接使用 xhr 对象发起 GET 请求，当需要携带参数的时候，本质上，都是直接将参数以查询字符串的形式，追加到 URL 地址的后面，发送到服务器的。

```js
$.get('url', {name: 'zs', age: 20}, function() {})
// 等价于
$.get('url?name=zs&age=20', function() {})

$.ajax({ method: 'GET', url: 'url', data: {name: 'zs', age: 20}, success: function() {} })
// 等价于
$.ajax({ method: 'GET', url: 'url?name=zs&age=20', success: function() {} })
```

## 4、URL编码与解码

URL 地址中，只允许出现英文相关的字母、标点符号、数字，因此，在 URL 地址中不允许出现中文字符。
如果 URL 中需要包含中文这样的字符，则必须对中文字符进行**编码**（转义）。
**URL编码的原则**：使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符。
URL编码原则的通俗理解：使用**英文字符**去表示**非英文字符**。

```js
http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=西游记
// 经过 URL 编码之后，URL地址变成了如下格式：
http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=%E8%A5%BF%E6%B8%B8%E8%AE%B0
```

浏览器提供了 URL 编码与解码的 API，分别是：

+ encodeURI()  编码的函数
+ decodeURI()  解码的函数

```js
encodeURI('黑马程序员')
// 输出字符串  %E9%BB%91%E9%A9%AC%E7%A8%8B%E5%BA%8F%E5%91%98
decodeURI('%E9%BB%91%E9%A9%AC')
// 输出字符串  黑马
```

由于浏览器会自动对 URL 地址进行编码操作，因此，大多数情况下，程序员不需要关心 URL 地址的编码与解码操作。

更多关于 URL 编码的知识，请参考如下博客：
https://blog.csdn.net/Lxd_0111/article/details/78028889

## 5、使用xhr发送POST请求

① 创建 xhr 对象
② 调用 xhr.open() 函数
③ ==设置 Content-Type 属性（固定写法）==
④ 调用 xhr.send() 函数，==同时指定要发送的数据==
⑤ 监听 xhr.onreadystatechange 事件

```js
// 1. 创建 xhr 对象
var xhr = new XMLHttpRequest()
// 2. 调用 open()
xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook')
// 3. 设置 Content-Type 属性（固定写法）
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
// 4. 调用 send()，同时将数据以查询字符串的形式，提交给服务器
xhr.send('bookname=水浒传&author=施耐庵&publisher=天津图书出版社')
// 5. 监听 onreadystatechange 事件
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(xhr.responseText)
    }
}
```

# 第六章、数据交换格式

数据交换格式，就是服务器端与客户端之间进行**数据传输与交换的格式。**
前端领域，经常提及的两种数据交换格式分别是 **XML 和 JSON**。其中 XML 用的非常少，所以，我们重点要学习的数据交换格式就是 JSON。

## 1、XML

XML 的英文全称是 EXtensible Markup Language，即可扩展标记语言。因此，XML 和 HTML 类似，也是一种标记语言。

```xml
<note>
  <to>ls</to>
  <from>zs</from>
  <heading>通知</heading>
  <body>晚上开会</body>
</note>
```

### 1.1、XML和HTML的区别

XML 和 HTML 虽然都是标记语言，但是，它们两者之间没有任何的关系。

+ HTML 被设计用来描述网页上的==内容==，是网页内容的载体
+ XML 被设计用来==传输和存储数据==，是数据的载体

### 1.2、XML的缺点

+ XML 格式臃肿，和数据无关的代码多，体积大，传输效率低
+ 在 Javascript 中解析 XML 比较麻烦

## 2、JSON

概念：JSON 的英文全称是 JavaScript Object Notation，即“JavaScript 对象表示法”。简单来讲，==JSON 就是 Javascript 对象和数组的字符串表示法==，它使用文本表示一个 JS 对象或数组的信息，因此，==JSON 的本质是字符串==。

作用：JSON 是一**种轻量级的文本数据交换格式**，在作用上类似于 XML，专门用于存储和传输数据，但是 JSON 比 XML 更小、更快、更易解析。

### 2.1、JSON的两种结构

JSON 就是用字符串来表示 Javascript 的对象和数组。所以，JSON 中包含**对象**和**数组**两种结构，通过这两种结构的相互嵌套，可以表示各种复杂的数据结构。

#### Ⅰ对象结构

对象结构：对象结构在 JSON 中表示为 { } 括起来的内容。数据结构为 { key: value, key: value, … } 的键值对结构。其中，key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是**数字、字符串、布尔值、null、数组、对象**6种类型。

```json
{
    "name": "zs",
    "age": 20,
    "gender": "男",
    "address": null,
    "hobby": ["吃饭", "睡觉", "打豆豆"]
}
```

#### Ⅱ 数组结构

数组结构：数组结构在 JSON 中表示为 [ ] 括起来的内容。数据结构为 [ "java", "javascript", 30, true … ] 。数组中数据的类型可以是**数字、字符串、布尔值、null、数组、对象**6种类型。

```json
[ "java", "python", "php" ]
[ 100, 200, 300.5 ]
[ true, false, null ]
[ { "name": "zs", "age": 20}, { "name": "ls", "age": 30} ]
[ [ "苹果", "榴莲", "椰子" ], [ 4, 50, 5 ] ]
```

### 2.2、注意事项

+ 属性名必须使用双引号包裹
+ 字符串类型的值必须使用双引号包裹
+ JSON 中不允许使用单引号表示字符串
+ JSON 中不能写注释
+ JSON 的最外层必须是对象或数组格式
+ 不能使用 undefined 或函数作为 JSON 的值

### 2.3、JSON和JS对象的关系

JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。例如：

```JS
//这是一个对象
var obj = {a: 'Hello', b: 'World'}

//这是一个 JSON 字符串，本质是一个字符串
var json = '{"a": "Hello", "b": "World"}' 
```

### 2.4、JSON和JS对象的互转

要实现从 JSON 字符串转换为 JS 对象，使用 ==JSON.parse()== 方法：

```js
var obj = JSON.parse('{"a": "Hello", "b": "World"}')
//结果是 {a: 'Hello', b: 'World'}
```

要实现从 JS 对象转换为 JSON 字符串，使用 ==JSON.stringify()== 方法：

```js
var json = JSON.stringify({a: 'Hello', b: 'World'})
//结果是 '{"a": "Hello", "b": "World"}'
```

### 2.5、序列和反序列化

把**数据对象转换为字符串**的过程，叫做序列化，例如：调用 JSON.stringify() 函数的操作，叫做 JSON 序列化。
把**字符串转换为数据对象**的过程，叫做反序列化，例如：调用 JSON.parse() 函数的操作，叫做 JSON 反序列化。

# 第七章、封装自己的Ajax函数

## 1、实现效果

```js
<!-- 1. 导入自定义的ajax函数库 -->
<script src="./itheima.js"></script>

<script>
    // 2. 调用自定义的 itheima 函数，发起 Ajax 数据请求
    itheima({
        method: '请求类型',
        url: '请求地址',
        data: { /* 请求参数对象 */ },
        success: function(res) { // 成功的回调函数
            console.log(res)     // 打印数据
        }
    })
</script>
```

## 2、定义options参数选项

itheima() 函数是我们自定义的 Ajax 函数，它接收一个配置对象作为参数，配置对象中可以配置如下属性：

+ method   请求的类型
+ url           请求的 URL 地址
+ data        请求携带的数据
+ success   请求成功之后的回调函数

## 3、处理data参数

需要把 data 对象，转化成查询字符串的格式，从而提交给服务器，因此提前定义 resolveData 函数如下：

```js
/**
 * 处理 data 参数
 * @param {data} 需要发送到服务器的数据
 * @returns {string} 返回拼接好的查询字符串 name=zs&age=10
 */
function resolveData(data) {
  var arr = []
  for (var k in data) {
    arr.push(k + '=' + data[k])
  }
  return arr.join('&')
}
```

## 4、定义itheima函数

在 itheima() 函数中，需要创建 xhr 对象，并监听 onreadystatechange 事件：

```js
function itheima(options) {
  var xhr = new XMLHttpRequest()
  // 拼接查询字符串
  var qs = resolveData(options.data)

  // 监听请求状态改变的事件
  xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
      var result = JSON.parse(xhr.responseText)
      options.success(result)
    }
  }
}
```

## 5、判断请求类型

不同的请求类型，对应 xhr 对象的不同操作，因此需要对请求类型进行 if … else … 的判断：

```js
  if (options.method.toUpperCase() === 'GET') {
    // 发起 GET 请求
    xhr.open(options.method, options.url + '?' + qs)
    xhr.send()
  } else if (options.method.toUpperCase() === 'POST') {
    // 发起 POST 请求
    xhr.open(options.method, options.url)
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    xhr.send(qs)
  }
```

# 第八章、XMLHttpRequest Level2的新特性

## 1.简介

### 1.1、旧版XMLHttpRequest的缺点

+ 只支持文本数据的传输，无法用来读取和上传文件
+ 传送和接收数据时，没有进度信息，只能提示有没有完成

### 1.2、XMLHttpRequest Level2的新功能

+ 可以设置 HTTP 请求的时限
+ 可以使用 FormData 对象管理表单数据
+ 可以上传文件
+ 可以获得数据传输的进度信息

## 2、设置HTTP请求时限

有时，Ajax 操作很耗时，而且无法预知要花多少时间。如果网速很慢，用户可能要等很久。新版本的 XMLHttpRequest 对象，增加了 timeout 属性，可以设置 HTTP 请求的时限：

```js
 xhr.timeout = 3000
```

上面的语句，将最长等待时间设为 3000 毫秒。过了这个时限，就自动停止HTTP请求。与之配套的还有一个 timeout 事件，用来指定回调函数：

```js
 xhr.ontimeout = function(event){
     alert('请求超时！')
 }
```

## 3、FormData对象管理表单数据

Ajax 操作往往用来提交表单数据。为了方便表单处理，HTML5 新增了一个 FormData 对象，可以模拟表单操作：

```js
      // 1. 新建 FormData 对象
      var fd = new FormData()
      // 2. 为 FormData 添加表单项
      fd.append('uname', 'zs')
      fd.append('upwd', '123456')
      // 3. 创建 XHR 对象
      var xhr = new XMLHttpRequest()
      // 4. 指定请求类型与URL地址
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
      // 5. 直接提交 FormData 对象，这与提交网页表单的效果，完全一样
      xhr.send(fd)
```

FormData对象也可以用来获取网页表单的值，示例代码如下：

```js
 // 获取表单元素
 var form = document.querySelector('#form1')
 // 监听表单元素的 submit 事件
 form.addEventListener('submit', function(e) {
    e.preventDefault()
     // 根据 form 表单创建 FormData 对象，会自动将表单数据填充到 FormData 对象中
     var fd = new FormData(form)
     var xhr = new XMLHttpRequest()
     xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
     xhr.send(fd)
     xhr.onreadystatechange = function() {}
})
```

## 4、上传文件

新版 XMLHttpRequest 对象，不仅可以发送文本信息，还可以上传文件。
实现步骤：

+ 定义 UI 结构
+ 验证是否选择了文件
+ 向 FormData 中追加文件
+ 使用 xhr 发起上传文件的请求
+ 监听 onreadystatechange 事件

### 4.1、定义UI结构

```html
    <!-- 1. 文件选择框 -->
    <input type="file" id="file1" />
    <!-- 2. 上传按钮 -->
    <button id="btnUpload">上传文件</button>
    <br />
    <!-- 3. 显示上传到服务器上的图片 -->
    <img src="" alt="" id="img" width="800" />
```

### 4.2、验证是否选择了文件

```js
 // 1. 获取上传文件的按钮
 var btnUpload = document.querySelector('#btnUpload')
 // 2. 为按钮添加 click 事件监听
 btnUpload.addEventListener('click', function() {
     // 3. 获取到选择的文件列表
     var files = document.querySelector('#file1').files
     if (files.length <= 0) {
         return alert('请选择要上传的文件！')
     }
     // ...后续业务逻辑
 })
```

### 4.3、向FormData中追加文件

```js
   
 // 1. 创建 FormData 对象
 var fd = new FormData()
 // 2. 向 FormData 中追加文件
 fd.append('avatar', files[0])
```

### 4.4、使用 xhr 发起上传文件的请求

```js
   
 // 1. 创建 xhr 对象
 var xhr = new XMLHttpRequest()
 // 2. 调用 open 函数，指定请求类型与URL地址。其中，请求类型必须为 POST
 xhr.open('POST', 'http://www.liulongbin.top:3006/api/upload/avatar')
 // 3. 发起请求
 xhr.send(fd)
```

### 4.5、监听onreadystatechange事件

```js
xhr.onreadystatechange = function() {
  if (xhr.readyState === 4 && xhr.status === 200) {
    var data = JSON.parse(xhr.responseText)
    if (data.status === 200) { // 上传文件成功
      // 将服务器返回的图片地址，设置为 <img> 标签的 src 属性
      document.querySelector('#img').src = 'http://www.liulongbin.top:3006' + data.url
    } else { // 上传文件失败
      console.log(data.message)
    }
  }
}
```

### 4.6、显示文件上传进度（控制台打印）

新版本的 XMLHttpRequest 对象中，可以通过监听 xhr.upload.onprogress 事件，来获取到文件的上传进度。语法格式如下：

```js
 // 创建 XHR 对象
 var xhr = new XMLHttpRequest()
 // 监听 xhr.upload 的 onprogress 事件
 xhr.upload.onprogress = function(e) {
    // e.lengthComputable 是一个布尔值，表示当前上传的资源是否具有可计算的长度
    if (e.lengthComputable) {
        // e.loaded 已传输的字节
        // e.total  需传输的总字节
        var percentComplete = Math.ceil((e.loaded / e.total) * 100)
    }
 }
```

## 5、显示文件上传进度（进度条）

采用bootstrap来制作

### 5.1、导入需要的库

```js
<link rel="stylesheet" href="./lib/bootstrap.css" />
<script src="./lib/jquery.js"></script>
```

### 5.2、基于Bootstrap渲染进度条

```html
<!-- 进度条 --><div class="progress" style="width: 500px; margin: 10px 0;">
   <div class="progress-bar progress-bar-info progress-bar-striped active" id="percent" style="width: 0%">
        0%
    </div>
</div>
```

### 5.3、监听上传进度的事件

```js
xhr.upload.onprogress = function(e) {
    if (e.lengthComputable) {
    // 1. 计算出当前上传进度的百分比
    var percentComplete = Math.ceil((e.loaded / e.total) * 100)
    $('#percent')
        // 2. 设置进度条的宽度
        .attr('style', 'width:' + percentComplete + '%')
        // 3. 显示当前的上传进度百分比
        .html(percentComplete + '%')
    }
 }
```

### 5.4、监听上传完成的事件

```js
xhr.upload.onload = function() {
     $('#percent')
         // 移除上传中的类样式
         .removeClass()
         // 添加上传完成的类样式
         .addClass('progress-bar progress-bar-success')
 }
```

## 6、jQuery实现文件上传

### 6.1、定义UI结构

```html
<!-- 导入 jQuery -->
<script src="./lib/jquery.js"></script>

<!-- 文件选择框 -->
<input type="file" id="file1" />
<!-- 上传文件按钮 -->
<button id="btnUpload">上传</button>
```

### 6.2、验证是否选择了文件

```js
$('#btnUpload').on('click', function() {
     // 1. 将 jQuery 对象转化为 DOM 对象，并获取选中的文件列表
     var files = $('#file1')[0].files
     // 2. 判断是否选择了文件
     if (files.length <= 0) {
         return alert('请选择图片后再上传！‘)
     }
 })
```

### 6.3、向FormData中追加文件

```js
 // 向 FormData 中追加文件
 var fd = new FormData()
 fd.append('avatar', files[0])
```

### 6.4、使用jQuery发起上传文件的请求

```js
 $.ajax({
     method: 'POST',
     url: 'http://www.liulongbin.top:3006/api/upload/avatar',
     data: fd,
     // 不修改 Content-Type 属性，使用 FormData 默认的 Content-Type 值
     contentType: false,
     // 不对 FormData 中的数据进行 url 编码，而是将 FormData 数据原样发送到服务器
     processData: false,
     success: function(res) {
         console.log(res)
     }
 })
```

## 7、jQuery实现loading效果

#### 7.1、ajaxStart(callback)

Ajax 请求开始时，执行 ajaxStart 函数。可以在 ajaxStart 的 callback 中显示 loading 效果，示例代码如下：

```js
 // 自 jQuery 版本 1.8 起，该方法只能被附加到文档
 $(document).ajaxStart(function() {
     $('#loading').show()
 })
```

注意： $(document).ajaxStart() 函数**会监听当前文档内所有的 Ajax 请求。**

#### 7.2、ajaxStop(callback)

Ajax 请求结束时，执行 ajaxStop 函数。可以在 ajaxStop 的 callback 中隐藏 loading 效果，示例代码如下：

```js
// 自 jQuery 版本 1.8 起，该方法只能被附加到文档
 $(document).ajaxStop(function() {
     $('#loading').hide()
 })
```

# 第九章、axios

## 1、简介

Axios 是专注于==网络数据请求==的库。
相比于原生的 XMLHttpRequest 对象，axios ==简单易用==。
相比于 jQuery，axios 更加==轻量化==，只专注于网络数据请求。

## 2、axios发送get请求的语法

```js
 axios.get('url', { params: { /*参数*/ } }).then(callback)
```

示例：

```js
 // 请求的 URL 地址
 var url = 'http://www.liulongbin.top:3006/api/get'
 // 请求的参数对象
 var paramsObj = { name: 'zs', age: 20 }
 // 调用 axios.get() 发起 GET 请求
 axios.get(url, { params: paramsObj }).then(function(res) {
     // res.data 是服务器返回的数据
     var result = res.data
     console.log(res)
 })
```

## 3、axios发送post请求的语法

```js
 axios.post('url', { /*参数*/ }).then(callback)
```

示例：

```js
 // 请求的 URL 地址
 var url = 'http://www.liulongbin.top:3006/api/post'
 // 要提交到服务器的数据
 var dataObj = { location: '北京', address: '顺义' }
 // 调用 axios.post() 发起 POST 请求
 axios.post(url, dataObj).then(function(res) {
     // res.data 是服务器返回的数据
     var result = res.data
     console.log(result)
 })
```

## 4、直接使用axios发送请求

axios 也提供了类似于 jQuery 中 $.ajax() 的函数，语法如下：

```js
 axios({
     method: '请求类型',
     url: '请求的URL地址',
     data: { /* POST数据 */ },
     params: { /* GET参数 */ }
 }) .then(callback)
```

### 4.1、发送get请求

```js
axios({
     method: 'GET',
     url: 'http://www.liulongbin.top:3006/api/get',
     params: { // GET 参数要通过 params 属性提供
         name: 'zs',
         age: 20
     }
 }).then(function(res) {
     console.log(res.data)
 })
```

### 4.2、发送POST请求

```js
axios({
     method: 'POST',
     url: 'http://www.liulongbin.top:3006/api/post',
     data: { // POST 数据要通过 data 属性提供
         bookname: '程序员的自我修养',
         price: 666
     }
 }).then(function(res) {
     console.log(res.data)
 })
```

# 第十章、同源策略和跨域

## 1、同源

### 1.1、什么是同源

如果两个页面的==协议==，==域名==和==端口==都相同，则两个页面具有==相同的源==。
例如，下表给出了相对于 http://www.test.com/index.html 页面的同源检测：

| **URL**                            | **是否同源** | **原因**                                  |
| ---------------------------------- | ------------ | ----------------------------------------- |
| http://www.test.com/other.html     | 是           | 同源（协议、域名、端口相同）              |
| https://www.test.com/about.html    | 否           | 协议不同（http 与 https）                 |
| http://blog.test.com/movie.html    | 否           | 域名不同（www.test.com 与 blog.test.com） |
| http://www.test.com:7001/home.html | 否           | 端口不同（默认的 80 端口与 7001 端口）    |
| http://www.test.com:80/main.html   | 是           | 同源（协议、域名、端口相同）              |

### 1.2、什么是同源策略

==同源策略==（英文全称 Same origin policy）是==浏览器==提供的一个==安全功能==。

通俗的理解：浏览器规定，A 网站的 JavaScript，不允许和非同源的网站 C 之间，进行资源的交互，例如：

+ 无法读取非同源网页的 Cookie、LocalStorage 和 IndexedDB
+ 无法接触非同源网页的 DOM
+ 无法向非同源地址发送 Ajax 请求

## 2、跨域

### 2.1、什么是跨域

==同源==指的是两个 URL 的协议、域名、端口一致，反之，则是跨域。
出现跨域的根本原因：==浏览器的同源策略==不允许非同源的 URL 之间进行资源的交互。
网页：http://www.test.com/index.html
接口：http://www.api.com/userlist

### 2.2、浏览器对跨域请求的拦截

![image-20230225170705468](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230225170705468.png)

注意：浏览器允许发起跨域请求，但是，跨域请求回来的数据，会被浏览器拦截，无法被页面获取到！

### 2.3、如何解决跨域数据请求

现如今，实现跨域数据请求，最主要的两种解决方案，分别是 ==JSONP== 和 ==CORS==。
JSONP：出现的早，兼容性好（兼容低版本IE）。是前端程序员为了解决跨域问题，被迫想出来的一种临时解决方案。缺点是==只支持 GET 请求==，不支持 POST 请求。
CORS：出现的较晚，它是 W3C 标准，属于跨域 Ajax 请求的根本解决方案。支持 GET 和 POST 请求。缺点是不兼容某些低版本的浏览器。

# 第十一章、JSONP

## 1、实现原理

由于**浏览器同源策略**的限制，网页中**无法通过 Ajax 请求非同源的接口数据**。但是 <script> 标签不受浏览器同源策略的影响，可以通过 src 属性，请求非同源的 js 脚本。
因此，JSONP 的实现原理，就是通过 <script> 标签的 src 属性，请求跨域的数据接口，并通过**函数调用**的形式，接收跨域接口响应回来的数据。

## 2、自己实现一个简单的JSONP

定义一个success回调函数：

```js
 <script>
   function success(data) {
     console.log('获取到了data数据：')
     console.log(data)
   }
 </script>
```

通过 <script> 标签，请求接口数据：

```js
<script src="http://ajax.frontend.itheima.net:3006/api/jsonp?callback=success&name=zs&age=20"></script>
```

## 3、JSONP的缺点

由于 JSONP 是通过 <script> 标签的 src 属性，来实现跨域数据获取的，所以，JSONP 只支持 GET 数据请求，不支持 POST 请求。

注意：==JSONP 和 Ajax 之间没有任何关系==，不能把 JSONP 请求数据的方式叫做 Ajax，因为 JSONP 没有用到 XMLHttpRequest 这个对象。

## 4、jQuery中的JSONP

jQuery 提供的 $.ajax() 函数，除了可以发起真正的 Ajax 数据请求之外，还能够发起 JSONP 数据请求，例如：

```js
 $.ajax({
    url: 'http://ajax.frontend.itheima.net:3006/api/jsonp?name=zs&age=20',
    // 如果要使用 $.ajax() 发起 JSONP 请求，必须指定 datatype 为 jsonp
    dataType: 'jsonp',
    success: function(res) {
       console.log(res)
    }
 })
```

默认情况下，使用 jQuery 发起 JSONP 请求，会自动携带一个 ==callback=jQueryxxx== 的参数，jQueryxxx 是随机生成的一个回调函数名称。

## 5、自定义参数以及回调函数名称

在使用 jQuery 发起 JSONP 请求时，如果想要自定义 JSONP 的**参数**以及**回调函数名称**，可以通过如下两个参数来指定：

```js
 $.ajax({
    url: 'http://ajax.frontend.itheima.net:3006/api/jsonp?name=zs&age=20',
    dataType: 'jsonp',
    // 发送到服务端的参数名称，默认值为 callback
    jsonp: 'callback',
    // 自定义的回调函数名称，默认值为 jQueryxxx 格式
    jsonpCallback: 'abc',
    success: function(res) {
       console.log(res)
    }
 })
```

一般改回调函数名称（jsonpCallback: 'abc'）

## 6、jQuery中的JSONP的实现过程

jQuery 中的 JSONP，也是通过 <script> 标签的 src 属性实现跨域数据访问的，只不过，jQuery 采用的是==动态创建和移除 <script> 标签==的方式，来发起 JSONP 数据请求。

+ 在发起 JSONP 请求的时候，动态向 <header> 中 append 一个 <script> 标签；
+ 在 JSONP 请求成功以后，动态从 <header> 中移除刚才 append 进去的 <script> 标签；

# 第十二章、节流和防抖

## 1.防抖

**防抖策略**（debounce）是当事件被触发后，**延迟 n 秒后再执行**回调，如果在这 n 秒内事件又被触发，则重新计时。

### 1.1、应用场景

用户在输入框中连续输入一串字符时，可以通过防抖策略，只在输入完后，才执行查询的请求，这样可以有效减少请求次数，节约请求资源；

### 1.2、输入框的防抖

```js
 var timer = null                    // 1. 防抖动的 timer

 function debounceSearch(keywords) { // 2. 定义防抖的函数
    timer = setTimeout(function() {
    // 发起 JSONP 请求
    getSuggestList(keywords)
    }, 500)
 }

 $('#ipt').on('keyup', function() {  // 3. 在触发 keyup 事件时，立即清空 timer
    clearTimeout(timer)
    // ...省略其他代码
    debounceSearch(keywords)
 })
```

### 1.3、缓存搜索的建议列表

顾名思义，就是请求过的数据不必再次请求，减少请求资源，定义一个对象，存在浏览器中。

```js
1.定义全局缓存对象
// 缓存对象
var cacheObj = {}
2.将搜索结构保存到缓存对象中
 // 渲染建议列表
 function renderSuggestList(res) {
    // ...省略其他代码
  // 将搜索的结果，添加到缓存对象中
    var k = $('#ipt').val().trim()
    cacheObj[k] = res
 }

3.优先从缓存中获取搜索建议
 // 监听文本框的 keyup 事件
 $('#ipt').on('keyup', function() {
    // ...省略其他代码

    // 优先从缓存中获取搜索建议
    if (cacheObj[keywords]) {
       return renderSuggestList(cacheObj[keywords])
    }
    // 获取搜索建议列表
    debounceSearch(keywords)
  })
```

## 2.节流

**节流策略**（throttle），顾名思义，可以减少一段时间内事件的触发频率。

### 2.1、节流的使用场景

+ 鼠标连续不断地触发某事件（如点击），只在单位时间内只触发一次；
+ 懒加载时要监听计算滚动条的位置，但不必每次滑动都触发，可以降低计算的频率，而不必去浪费 CPU 资源；

### 2.2、节流阀的概念

节流阀为**空**，表示**可以执行下次操作**；不为空，表示不能执行下次操作。
当前操作执行完，必须将节流阀**重置**为空，表示可以执行下次操作了。
每次执行操作前，必须**先判断节流阀是否为空**。

### 2.3、使用节流阀右滑鼠标跟随效果

```js
$(function() {
  var angel = $('#angel')
  var timer = null // 1.预定义一个 timer 节流阀
  $(document).on('mousemove', function(e) {
    if (timer) { return } // 3.判断节流阀是否为空，如果不为空，则证明距离上次执行间隔不足16毫秒
    timer = setTimeout(function() {
      $(angel).css('left', e.pageX + 'px').css('top', e.pageY + 'px')
      timer = null // 2.当设置了鼠标跟随效果后，清空 timer 节流阀，方便下次开启延时器
    }, 16)
  })
})
```

## 3、总结

节流和防抖的区别

+ 防抖：如果事件被频繁触发，防抖能保证**只有最有一次触发生效**！前面 N 多次的触发都会被忽略！
+ 节流：如果事件被频繁触发，节流能够**减少事件触发的频率**，因此，节流**是有选择性**地执行一部分事件！

# 第十三章、HTTP协议

## 1、HTTP协议简介

### 1.1、什么是通信

通信，就是**信息的传递和交换**。

通信三要素：

+ 通信的主体
+ 通信的内容
+ 通信的方式

### 1.2、什么是通信协议

**通信协议**（Communication Protocol）是指通信的双方完成通信所**必须遵守的规则和约定**。
通俗的理解：通信双方采用约定好的格式来发送和接收消息，这种事先约定好的通信格式，就叫做通信协议。

#### 1.2.1、互联网中的通信协议

客户端与服务器之间要实现网页内容的传输，则通信的双方必须遵守网页内容的传输协议。

网页内容又叫做超文本，因此网页内容的传输协议又叫做超文本传输协议（HyperText Transfer Protocol） ，简称 HTTP 协议。

### 1.3、HTTP

**HTTP 协议**即超文本传送协议 (HyperText Transfer Protocol) ，它规定了客户端与服务器之间进行网页内容传输时，所必须遵守的传输格式。
例如：

+ 客户端要以HTTP协议要求的格式把数据**提交**到服务器
+ 服务器要以HTTP协议要求的格式把内容**响应**给客户端

#### 1.3.1、HTTP协议的交换模型

HTTP 协议采用了 ==请求/响应== 的交互模型。

![image-20230226154613204](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230226154613204.png)

## 2、HTTP请求消息

由于 HTTP 协议属于客户端浏览器和服务器之间的通信协议。因此，**客户端发起的请求**叫做 HTTP 请求，**客户端发送到服务器的消息**，叫做 HTTP 请求消息。

注意：HTTP 请求消息又叫做 **HTTP 请求报文**。

HTTP 请求消息由==请求行（request line）、请求头部（ header ） 、空行 和 请求体== 4 个部分组成。

![image-20230226154843483](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230226154843483.png)

### 2.1、请求行

请求行由**请求方式、URL 和 HTTP 协议版本** 3 个部分组成，他们之间使用空格隔开。

![image-20230226155043128](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230226155043128.png)

### 2.2、请求头部

请求头部用来描述**客户端的基本信息**，从而把**客户端相关的信息告知服务器**。比如：User-Agent 用来说明当前是什么类型的浏览器；Content-Type 用来描述发送到服务器的数据格式；Accept 用来描述客户端能够接收什么类型的返回内容；Accept-Language 用来描述客户端期望接收哪种人类语言的文本内容。
请求头部由多行 键/值对 组成，每行的键和值之间用英文的冒号分隔。

![image-20230226155148997](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230226155148997.png)

**常见请求头字段**

| **头部字段**        | **说明**                                     |
| ------------------- | -------------------------------------------- |
| Host                | 要请求的服务器域名                           |
| Connection          | 客户端与服务器的连接方式(close 或 keepalive) |
| Content-Length      | 用来描述请求体的大小                         |
| ==Accept==          | 客户端可识别的响应内容类型列表               |
| ==User-Agent==      | 产生请求的浏览器类型                         |
| ==Content-Type==    | 客户端告诉服务器实际发送的数据类型           |
| Accept-Encoding     | 客户端可接收的内容压缩编码形式               |
| ==Accept-Language== | 用户期望获得的自然语言的优先顺序             |

关于更多请求头字段的描述，可以查看 MDN 官方文档：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers

### 2.3、空行

最后一个请求头字段的后面是一个**空行**，通知服务器**请求头部至此结束**。
请求消息中的空行，用来**分隔请求头部与请求体**。

### 2.4、请求体

请求体中存放的，是要通过 ==POST 方式==提交到服务器的数据。

==注意：只有 POST 请求才有请求体，GET 请求没有请求体！==

## 3、HTTP响应消息

响应消息就是**服务器响应给客户端**的消息内容，也叫作**响应报文**。

HTTP响应消息由==状态行、响应头部、空行 和 响应体== 4 个部分组成，如下图所示：

![image-20230226155827663](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230226155827663.png)

### 2.1、状态行

状态行由 **HTTP 协议版本、状态码和状态码**的描述文本 3 个部分组成，他们之间使用空格隔开;

![image-20230226155909475](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230226155909475.png)

### 2.2、响应头部

响应头部用来描述**服务器的基本信息**。响应头部由多行 **键/值**对 组成，每行的键和值之间用英文的冒号分隔。

![image-20230226160003187](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230226160003187.png)

关于更多响应头字段的描述，可以查看 MDN 官方文档：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers

### 2.3、空行

在最后一个响应头部字段结束之后，会紧跟一个**空行**，用来通知**客户端响应头部至此结束。**
响应消息中的空行，用来**分隔响应头部与响应体**。

### 2.4、响应体

响应体中存放的，是服务器响应给客户端的资源内容。

![image-20230226160131344](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230226160131344.png)

## 4、HTTP请求方式

HTTP 请求方法，属于 HTTP 协议中的一部分，请求方法的作用是：用来表明**要对服务器上的资源执行的操作**。最常用的请求方法是 GET 和 POST。

| **序号** | **方法**   | **描述**                                                     |
| -------- | ---------- | ------------------------------------------------------------ |
| 1        | ==GET==    | ==(查询)==发送请求来获得服务器上的资源，请求体中不会包含请求数据，请求数据放在协议头中。 |
| 2        | ==POST==   | ==(新增)==向服务器提交资源（例如提交表单或上传文件）。数据被包含在请求体中提交给服务器。 |
| 3        | ==PUT==    | ==(修改)==向服务器提交资源，并使用提交的新资源，替换掉服务器对应的旧资源。 |
| 4        | ==DELETE== | ==(删除)==请求服务器删除指定的资源。                         |
| 5        | HEAD       | HEAD 方法请求一个与 GET 请求的响应相同的响应，但没有响应体。 |
| 6        | OPTIONS    | 获取http服务器支持的http请求方法，允许客户端查看服务器的性能，比如ajax跨域时的预检等。 |
| 7        | CONNECT    | 建立一个到由目标资源标识的服务器的隧道。                     |
| 8        | TRACE      | 沿着到目标资源的路径执行一个消息环回测试，主要用于测试或诊断。 |
| 9        | PATCH      | 是对 PUT 方法的补充，用来对已知资源进行局部更新 。           |

## 5、HTTP响应状态码

**HTTP 响应状态码**（HTTP Status Code），也属于 HTTP 协议的一部分，**用来标识响应的状态**。
响应状态码会随着响应消息一起被发送至客户端浏览器，浏览器根据服务器返回的响应状态码，就能知道这次 HTTP 请求的结果是成功还是失败了。

### 5.1、HTTP响应状态码的组成以分类

HTTP 状态码由**三个十进制数字**组成，**第一个十进制数字定义了状态码的类型**，后两个数字用来对状态码进行细分。
HTTP 状态码共分为 5 种类型：

| **分类** | **分类描述**                                                 |
| -------- | ------------------------------------------------------------ |
| 1**      | **信息**，服务器收到请求，需要请求者继续执行操作（实际开发中很少遇到 1** 类型的状态码） |
| 2**      | **成功**，操作被成功接收并处理                               |
| 3**      | **重定向**，需要进一步的操作以完成请求                       |
| 4**      | **客户端错误**，请求包含语法错误或无法完成请求               |
| 5**      | **服务器错误**，服务器在处理请求的过程中发生了错误           |

### 5.2、2** 成功相关的响应状态码

2** 范围的状态码，表示服务器已成功接收到请求并进行处理。常见的 2** 类型的状态码如下：

| **状态码** | **状态码英文名称** | **中文描述**                                                |
| ---------- | ------------------ | ----------------------------------------------------------- |
| 200        | OK                 | 请求成功。一般用于 GET 与 POST 请求                         |
| 201        | Created            | 已创建。成功请求并创建了新的资源，通常用于 POST 或 PUT 请求 |

### 5.3、3** 重定向相关的响应状态码

3** 范围的状态码，表示表示服务器要求客户端重定向，需要客户端进一步的操作以完成资源的请求。常见的 3** 类型的状态码如下：

| **状态码** | **状态码英文名称** | **中文描述**                                                 |
| ---------- | ------------------ | ------------------------------------------------------------ |
| 301        | Moved Permanently  | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替 |
| 302        | Found              | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI |
| 304        | Not Modified       | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源（响应消息中不包含响应体）。客户端通常会缓存访问过的资源。 |

### 5.4、4** 客户端错误相关的响应状态码

4** 范围的状态码，表示客户端的请求有非法内容，从而导致这次请求失败。常见的 4** 类型的状态码如下：

| **状态码** | **状态码英文名称** | **中文描述**                                                 |
| ---------- | ------------------ | ------------------------------------------------------------ |
| 400        | Bad Request        | 1、语义有误，当前请求无法被服务器理解。除非进行修改，否则客户端不应该重复提交这个请求。2、请求参数有误。 |
| 401        | Unauthorized       | 当前请求需要用户验证。                                       |
| 403        | Forbidden          | 服务器已经理解请求，但是拒绝执行它。                         |
| 404        | Not Found          | **服务器无法根据客户端的请求找到资源（网页）**。             |
| 408        | Request Timeout    | 请求超时。服务器等待客户端发送的请求时间过长，超时。         |

#### 5.5、5** 服务端错误相关的响应状态码

5** 范围的状态码，表示服务器未能正常处理客户端的请求而出现意外错误。常见的 5** 类型的状态码如下：

| **状态码** | **状态码英文名称**    | **中文描述**                                                 |
| ---------- | --------------------- | ------------------------------------------------------------ |
| 500        | Internal Server Error | 服务器内部错误，无法完成请求。                               |
| 501        | Not Implemented       | 服务器不支持该请求方法，无法完成请求。只有 GET 和 HEAD 请求方法是要求每个服务器必须支持的，其它请求方法在不支持的服务器上会返回501 |
| 503        | Service Unavailable   | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。       |
