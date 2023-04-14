# 使用jQuery等第三方库的地址：http://staticfile.org/

# 第一章、初始node.js

## 1、什么是node.js

Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine.
Node.js 是一个基于 Chrome V8 引擎的 **JavaScript 运行环境**。

Node.js 的官网地址： https://nodejs.org/zh-cn/

## 2、node.js中的Javascript运行环境

注意：

+ 浏览器是 JavaScript 的前端运行环境。
+ Node.js 是 JavaScript 的后端运行环境。
+ Node.js 中**无法调用 DOM 和 BOM 等浏览器内置 API**。

## 3、node.js可以做什么

Node.js 作为一个 JavaScript 的运行环境，仅仅提供了基础的功能和 API。然而，基于 Node.js 提供的这些基础能，很多强大的工具和框架如雨后春笋，层出不穷，所以学会了 Node.js ，可以让前端程序员胜任更多的工作和岗位：
① 基于 Express 框架（http://www.expressjs.com.cn/），可以快速构建 Web 应用
② 基于 Electron 框架（https://electronjs.org/），可以构建跨平台的桌面应用
③ 基于 restify 框架（http://restify.com/），可以快速构建 API 接口项目
④ 读写和操作数据库、创建实用的命令行工具辅助前端开发、etc…

## 4、查看已安装的Node.js版本号

打开终端，在终端输入命令 `node –v` 后，按下回车键，即可查看已安装的 Node.js 的版本号。

Windows 系统快速打开终端的方式：
使用快捷键（**Windows徽标键 + R**）打开运行面板，输入 **cmd** 后直接回车，即可打开终端。

## 5、常见的终端快捷键

1. 使用 ↑ 键，可以快速定位到上一次执行的命令
2. 使用 tab 键，能够快速补全路径
3. 使用 esc 键，能够快速清空当前已输入的命令
4. 输入 cls 命令，可以清空终端

# 第二章、fs文件系统模块

## 1、什么是fs文件系统模块

fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。
例如：

+ **fs.readFile()** 方法，用来**读取**指定文件中的内容
+  **fs.writeFile()** 方法，用来向指定的文件中**写入**内容

如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：

```js
const fs = require('fs')
```

## 2、fs.readFile()

### 2.1、语法

```js
fs.readFile(path [,option] ,callback)
```

参数解读：

+ 参数1（path）：必选参数，字符串，表示文件的路径。
+ 参数2（options）：可选参数，表示以什么**编码格式**来读取文件。
+ 参数3（callback）：必选参数，文件读取完成后，通过回调函数拿到读取的结果。

### 2.2、示例

可以判断 err 对象是否为 null，从而知晓文件读取的结果：

```js
const fs = require('fs');
fs.readFile('1.txt',"utf-8",function(err,datastr){
    if(err){
        return console.log("文件读取失败"+err.message);
    }
    console.log('文件读取成功，内容是'+datastr)
}
```

err如过文件读取成功，则返回null，如果读取失败，则返回一个错误对象

## 3、fs.writeFile()

### 3.1、语法

```
fs.writeFile(path ,data [,option] ,callback)
```

数解读：

+ 参数1（path）：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。
+ 参数2（data）：必选参数，表示要写入的内容。
+ 参数3（option）：可选参数，表示以什么格式写入文件内容，默认值是 utf8。
+ 参数4（callback）：必选参数，文件写入完成后的回调函数。

## 3.2、示例

```js
fs.writeFile("1.txt","Hello Node.js","utf-8",function(err){
        if(err){
            return console.log("文件写入失败，原因是"+err.message);
        }
        console.log("文件写入成功");
    })
```

## 4、fs路径动态凭借的问题

在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的**相对路径**时，很容易出现路径动态拼接错误的问题。
原因：代码在运行的时候，**会以执行 node 命令时所处的目录**，动态拼接出被操作文件的完整路径。
解决方案：在使用 fs 模块操作文件时，**直接提供完整的路径**，不要提供 ./ 或 ../ 开头的相对路径，从而防止路径动态拼接的问题。

```js
//不要使用 ./ 或 ../ 这样的相对路劲
fs.read('./files/1.txt','utf-8',function(err.datastr){
	if(err) return console.log("读取文件失败"+err.message)
	console.log(data.str)
})

// __dirname 表示执行js文件当前文件所处的目录
fs.readFile(__dirname,'./files/1.txt','utf-8',function(err,datastr){
	if(err) return console.log("读取文件失败"+err.message)
	console.log(data.str)
})
```

## 5、注意点

1. fs.writeFile() 方法只能用来创建文件，不能用来创建路径
2. 重复调用 fs.writeFile() 写入同一个文件，新写入的内容会覆盖之前的旧内容

# 第三章、path路径模块

## 1、什么是path路径模块

path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。
例如：

+ path.join() 方法，用来将多**个路径片段拼接成一个完整的路径字符串**

+ path.basename() 方法，用来从路径字符串中，将文件名解析出来

  如果要在 JavaScript 代码中，使用 path 模块来处理路径，则需要使用如下的方式先导入它：

```js
const path = require('path');
```

## 2、path.join()

### 2.1、语法

使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串，语法格式如下：

```js
path.join([...paths])
```

参数解读：

+ ...paths <string> 路径片段的序列
+ 返回值: <string>

### 2.2、示例

使用 path.join() 方法，可以把多个路径片段拼接为完整的路径字符串：

```js
const pathStr = path.join('/a','/b/c','../','./d','e')
console.log(pathStr)   //输出\a\b\d\e

const pathstr2 = path.join(__dirname,'./files/1.txt')
console.log(parhstr2)   //输出 当前文件所处目录\files\1.txt
```

## 3、path.basename()

### 3.1、语法

使用 path.basename() 方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下：

```js
path.basename(path[,ext])
```

参数解读：

+ path <string> 必选参数，表示一个路径的字符串
+ ext <string> 可选参数，表示文件扩展名
+ 返回: <string> 表示路径中的最后一部分

### 3.2、示例

使用 path.basename() 方法，可以从一个文件路径中，获取到文件的名称部分：

```js
const fpath = 'a/b/c/index.html'

var fullName = path.basename(fpath);
console.log(fullName);    //输出  index.html

var nameWithoutExt = pathname(fpath,'.html')
console.log(nameWithoutExt)    //输出 index
```

## 4、path.extname()

### 4.1、语法

使用 path.extname() 方法，可以获取路径中的扩展名部分，语法格式如下：

```js
path.extname(path)
```

参数解读：

+ path <string>必选参数，表示一个路径的字符串
+ 返回: <string> 返回得到的扩展名字符串

### 4.2、示例

使用 path.extname() 方法，可以获取路径中的扩展名部分：

```js
const fpath = 'a/b/c/index.html';

const fext = path.extname(fpath)
console.log(fext)   //输出 .html
```

# 第四章、http模块

## 1、什么是http模块

http 模块是 Node.js 官方提供的、用来**创建 web 服务器**的模块。通过 http 模块提供的 http.createServer() 方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

```js
const http = require('http')
```

## 2、http模块的作用

服务器和普通电脑的区别在于，服务器上安装了 **web 服务器软件**，例如：IIS、**Apache** 等。通过安装这些服务器软件，就能把一台普通的电脑变成一台 web 服务器。

在 Node.js 中，我们**不需要使用** IIS、Apache 等这些**第三方 web 服务器软件**。因为我们可以基于 Node.js 提供的 http 模块，**通过几行简单的代码，就能轻松的手写一个服务器软件**，从而对外提供 web 服务。

## 3、服务器相关的知识

### 3.1、IP地址

IP 地址就是**互联网上每台计算机的唯一地址**，因此 IP 地址具有唯一性。如果把“个人电脑”比作“一台电话”，那么“IP地址”就相当于“电话号码”，只有在知道对方 IP 地址的前提下，才能与对应的电脑之间进行数据通信。
IP 地址的格式：通常用“**点分十进制**”表示成（a.b.c.d）的形式，其中，a,b,c,d 都是 0~255 之间的十进制整数。例如：用点分十进表示的 IP地址（192.168.1.1）
**注意**：

1. **互联网中每台 Web 服务器，都有自己的 IP 地址**，例如：大家可以在 Windows 的终端中运行 ping www.baidu.com 命令，即可查看到百度服务器的 IP 地址。
2. 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入 127.0.0.1 这个 IP 地址，就能把自己的电脑当做一台服务器进行访问了。

### 3.2、域名和域名服务器

尽管 IP 地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套**字符型的地址方案**，即所谓的**域名（Domain Name）地址。**
IP地址和域名是一一**对应的关系**，这份对应关系存放在一种叫做**域名服务器**(DNS，Domain name server)的电脑中。使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，**域名服务器就是提供 IP 地址和域名之间的转换服务的服务器。**

注意：

1. 单纯使用 IP 地址，互联网中的电脑也能够正常工作。但是有了域名的加持，能让互联网的世界变得更加方便。
2. 在开发测试期间， **127.0.0.1 对应的域名是 localhost**，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。

### 3.3、端口号

计算机中的端口号，就好像是现实生活中的门牌号一样。通过门牌号，外卖小哥可以在整栋大楼众多的房间中，准确把外卖送到你的手中。
同样的道理，在一台电脑中，可以运行成百上千个 web 服务。每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给**对应的 web 服务**进行处理。

![image-20230304143909710](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230304143909710.png)

注意：

1. 每个端口号不能同时被多个 web 服务占用。
2. 在实际应用中，URL 中的 **80 端口可以被省略**。

## 4、创建web服务器的基本步骤

### 4.1、基本步骤

1. 导入 http 模块
2. 创建 web 服务器实例
3. 为服务器实例绑定 request 事件，监听客户端的请求
4. 启动服务器

#### 4.1.1、导入http模板

如果希望在自己的电脑上创建一个 web 服务器，从而对外提供 web 服务，则需要导入 http 模块：

```js
const http = require('http');
```

#### 4.1.2、创建web服务器实例

调用 ==http.createServer()== 方法，即可快速创建一个 web 服务器实例：

```js
const server = http.createServer()
```

#### 4.1.3、为服务器绑定request事件

为服务器实例绑定 request 事件，即可监听客户端发送过来的网络请求：

```js
server.on('request', (req, res) => {
	console.log('Someone visit web server')
}）
```

#### 4.1.4、启动服务器

调用服务器实例的 .listen() 方法，即可启动当前的 web 服务器实例：

```js
server.listen(8080, () => {
  console.log('server running at http://127.0.0.1:8080')
})
```

### 4.2、req请求对象

只要服务器接收到了客户端的请求，就会调用通过 **server.on()** 为服务器绑定的 **request 事件处理函数**。
如果想在事件处理函数中，**访问与客户端相关的数据或属性**，可以使用如下的方式：

```js
server.on('request', (req) => {
	// req 是请求对象，包含了与客户端相关的数据和属性
  // req.url 是客户端请求的 URL 地址
  const url = req.url
  // req.method 是客户端请求的 method 类型
  const method = req.method
  const str = `Your request url is ${url}, and request method is ${method}`
  console.log(str)

}）
```

==注意：浏览器只能发起默认的get请求==

### 4.3、res响应对象

在服务器的 request 事件处理函数中，如果想访问与**服务器相关的数据或属性**，可以使用如下的方式：

```js
/ res 是响应端对象，包含了与服务端相关的数据和属性
server.on('request', (req, res) => {
  //要发送客户端的字符串
  const str = `Your request url is ${url}, and request method is ${method}`
  console.log(str)
  // 调用 res.end() 方法，向客户端响应一些内容，并结束这次请求的处理过程
  res.end(str)
})
```

### 4.4、解决中文乱码问题

当调用 res.end() 方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要**手动设置内容的编码格式**：

```js
server.on('request', (req, res) => {
  // 定义一个字符串，包含中文的内容
  const str = `您请求的 URL 地址是 ${req.url}，请求的 method 类型为 ${req.method}`
  // 调用 res.setHeader() 方法，设置 Content-Type 响应头，解决中文乱码的问题
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  // res.end() 将内容响应给客户端
  res.end(str)
})
```

### 4.5、根据不同的url响应不同的html内容

```js
const http = require('http')
const server = http.createServer()

server.on('request', (req, res) => {
  // 1. 获取请求的 url 地址
  const url = req.url
  // 2. 设置默认的响应内容为 404 Not found
  let content = '<h1>404 Not found!</h1>'
  // 3. 判断用户请求的是否为 / 或 /index.html 首页
  // 4. 判断用户请求的是否为 /about.html 关于页面
  if (url === '/' || url === '/index.html') {
    content = '<h1>首页</h1>'
  } else if (url === '/about.html') {
    content = '<h1>关于页面</h1>'
  }
  // 5. 设置 Content-Type 响应头，防止中文乱码
  res.setHeader('Content-Type', 'text/html; charset=utf-8')
  // 6. 使用 res.end() 把内容响应给客户端
  res.end(content)
})

server.listen(80, () => {
  console.log('server running at http://127.0.0.1')
})
```

![image-20230304145447819](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230304145447819.png)



# 第五章、模块化

## 1、什么是模块化

**模块化**是指解决一个复杂问题时，自顶向下逐层**把系统划分成若干模块的过程**。对于整个系统来说，模块是可组合、分解和更换的单元。

### 编程领域的模块化

编程领域中的模块化，就是**遵守固定的规则**，把一个大文件拆成独立并互相依赖的多个小模块。

把代码进行模块化拆分的好处：

① 提高了代码的复用性

② 提高了代码的可维护性

③ 可以实现按需加载

## 2、模块化规范

**模块化规范**就是对代码进行模块化的拆分与组合时，需要遵守的那些规则。

例如：

+ 使用什么样的语法格式来引用模块
+ 在模块中使用什么样的语法格式向外暴露成员

**模块化规范的好处**：大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己。

## 3、Node.js中模块化

### 3.1、分类

Node.js 中根据模块来源的不同，将模块分为了 3 大类，分别是：

+ ==内置模块==（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）

+ ==自定义模块==（用户创建的每个 .js 文件，都是自定义模块）
+ ==第三方模块==（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）

### 3.2、加载模块

使用强大的 ==require()== 方法，可以加载需要的**内置模块、用户自定义模块、第三方模块进行使用**。例如：

```js
//加载内置模块的fs模块
const fs = require('fs');

//加载用户的自定义模块
const custom = require('./custom.js');

//加载第三方模块
const monent = require('moment');
```

注意：

+ 在使用require加载用户自定义模块可以省略   .js   的后缀名。
+ 使用 require() 方法加载其它模块时，会执行被加载模块中的代码。

### 3.3、模块作用域

#### 3.3.1、什么是模块作用域

和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做**模块作用域**。

![image-20230307134825924](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307134825924.png)

#### 3.3.2、好处

防止了全局变量污染的问题

![image-20230307134921725](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307134921725.png)

### 3.4、向外共享模块作用域中的成员

#### 3.4.1、module对象

在每个 .js 自定义模块中都有一个 module 对象，它里面**存储了和当前模块有关的信息**，打印如下：

![image-20230307140415061](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307140415061.png)

#### 3.4.2、module.exports对象

在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。

外界用 **require()** 方法导入自定义模块时，得到的就是 module.exports 所指向的对象。

#### 3.4.3、共享成员时的注意点

使用 require() 方法导入模块时，导入的结果，**永远以 module.exports 指向的对象为准**。

![image-20230307140820914](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307140820914.png)

#### 3.4.4、exports对象

由于 module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了 exports 对象。默认情况下，==exports 和 module.exports 指向同一个对象==。最终共享的结果，还是以 module.exports 指向的对象为准。

#### 3.4.5、exports和module.exports的使用误区

时刻谨记，require() 模块时，==得到的永远是 module.exports 指向的对象==：

![image-20230307141225461](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307141225461.png)

**注意：**为了防止混乱，建议大家不要在同一个模块中同时使用 exports 和 module.exports

### 3.5、Node.js中的模块化规范

Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了**模块的特性和各模块之间如何相互依赖**。

CommonJS 规定：

① 每个模块内部，**module 变量**代表当前模块。

② module 变量是一个对象，它的 exports 属性（即 **module.exports）是对外的接口**。

③ 加载某个模块，其实是加载该模块的 module.exports 属性。**require() 方法用于加载模块。**

# 第六章、npm与包

## 1、包

### 1.1、什么是包

Node.js 中的$\textcolor{red}{第三方模块}$又叫做包。

就像电脑和计算机指的是相同的东西，第三方模块和包指的是同一个概念，只不过叫法不同。

### 1.2、下载包的网址

国外有一家 IT 公司，叫做 **npm, Inc.** 这家公司旗下有一个非常著名的网站： https://www.npmjs.com/ ，它是**全球最大的包共享平台**，你可以从这个网站上搜索到任何你需要的包，只要你有足够的耐心！

到目前位置，全球约 1100 多万的开发人员，通过这个包共享平台，开发并共享了超过 120 多万个包 供我们使用。

**npm, Inc. 公司**提供了一个地址为 https://registry.npmjs.org/ 的服务器，来对外共享所有的包，我们可以从这个服务器上下载自己所需要的包。

**注意：**

+ 从 https://www.npmjs.com/ 网站上搜索自己所需要的包
+ 从 https://registry.npmjs.org/ 服务器上下载自己需要的包

### 1.3、如何下载包

**npm, Inc. 公司**提供了一个包管理工具，我们可以使用这个包管理工具，从 https://registry.npmjs.org/ 服务器把需要

的包下载到本地使用。

这个包管理工具的名字叫做 Node Package Manager（简称 npm 包管理工具），这个包管理工具随着 Node.js 的安

装包一起被安装到了用户的电脑上。

大家可以在终端中执行$\textcolor{red}{npm -v}$ 命令，来查看自己电脑上所安装的 npm 包管理工具的版本号：

## 2、npm初体验

### 2.1、示例：格式化时间

$\textcolor{red}{① 使用 npm 包管理工具，在项目中安装格式化时间的包 moment}$

② 使用 require() 导入格式化时间的包

③ 参考 moment 的官方 API 文档对时间进行格式化

### 2.2、在项目中安装包

如果想在项目中安装指定名称的包，需要运行如下的命令：

```
npm install 包的完整名臣
```

上述的装包命令，可以简写成如下格式：

```
npm i 包的完整名称
```

### 2.3、初次安装包哪些文件

初次装包完成后，在项目文件夹下多一个叫做 $\textcolor{red}{node\_modules}$的文件夹和 $\textcolor{red}{package-lock.json}$ 的配置文件。

其中：

$\textcolor{blue}{node\_modules}$ 文件夹用来$\textcolor{red}{存放所有已安装到项目中的包}$。require() 导入第三方包时，就是从这个目录中查找并加载包。

$\textcolor{blue}{package-lock.json}$ 配置文件用来$\textcolor{red}{记录 node\_modules 目录下的每一个包的下载信息}$，例如包的名字、版本号、下载地址等。

注意：程序员不要手动修改 node_modules 或 package-lock.json 文件中的任何代码，npm 包管理工具会自动维护它们

### 2.4、安装指定版本

默认情况下，使用 npm install 命令安装包的时候，会自动安装最新版本的包。如果需要安装指定版本的包，可以在包名之后，通过 **@ 符号**指定具体的版本，例如：

```
npm i moment@2.22.2
```

### 2.5、报的语义化版本规范

包的版本号是以“点分十进制”形式进行定义的，总共有三位数字，例如 **2.24.0**

其中每一位数字所代表的的含义如下：

第1位数字：大版本

第2位数字：功能版本

第3位数字：Bug修复版本

**版本号提升的规则**：只要前面的版本号增长了，则后面的版本号归零。

## 3、包管理配置文件

npm 规定，在项目根目录中，**必须**提供一个叫做 package.json 的包管理配置文件。用来记录与项目有关的一些配置

信息。例如：

+ 项目的名称、版本号、描述等
+ 项目中都用到了哪些包
+ 哪些包只在开发期间会用到
+ 那些包在开发和部署时都需要用到

### 3.1、多人协作问题

现实问题：整个项目的体积是 30.4M；第三方包的体积是 28.8M；项目源代码的体积 1.6M

遇到的问题：**第三方包的体积过大**，不

方便团队成员之间共享项目源代码。

解决方案：$\textcolor{red}{共享时剔除node\_modules}$

### 3.2、如何记录项目安装了哪些包

在**项目根目录**中，创建一个叫做 **package.json** 的配置文件，即可用来记录项目中安装了哪些包。从而方便剔除

node_modules 目录之后，在团队成员之间共享项目的源代码。

**注意**：今后在项目开发中，一定要把 node_modules 文件夹，**添加到 .gitignore 忽略文件中。**

### 3.3、快速创建package.json

npm 包管理工具提供了一个快捷命令，可以在**执行命令时所处的目录中**，快速创建 package.json 这个包管理配置文件：

```js
//作用：在执行命令所处的目录中，快速创建package.json文件
npm init -y
```

注意：

① 上述命令$\textcolor{red}{只能在英文的目录下成功运行}$！所以，项目文件夹的名称一定要使用英文命名，$\textcolor{red}{不要使用中文，不能出现空格}$。

② 运行 npm install 命令安装包的时候，npm 包管理工具会自动把包的名称和版本号，记录到 package.json 中。

### 3.4、dependcies节点

package.json 文件中，有一个 dependencies 节点，专门用来记录您使用 **npm install 命令**安装了哪些包。

![image-20230307215145806](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307215145806.png)

### 3.5、一次性安装所有的包

可以运行 **npm install 命令（或 npm i）**一次性安装所有的依赖包：

```js
//执行npm install 命令时，npm包管理工具先读取package,json 中华的dependencies节点
//读取到记录的所有依赖包和版本号之后，npm 包管理工具智慧，npm包管理工具把这些包一次性下载到项目中
npm install
```

### 3.6、卸载包

可以运行 **npm uninstall** 命令，来卸载指定的包

```js
npm uninstall moment
```

注意：npm uninstall 命令执行成功后，会把卸载的包，自动从 package.json 的 dependencies 中移除掉。

### 3.7、 **devDependencies 节点**

如果某些包**只在项目开发阶段**会用到，在**项目上线之后不会用到**，则建议把这些包记录到 devDependencies 节点中。

与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。

您可以使用如下的命令，将包记录到 devDependencies 节点中：

```js
//安装指定的包，并记录到deDependencies节点中
npm i 包名 -D
//注意：上述命令是简写形式，等价于下面的完整写法
npm install 包名 -save-dev
```

## 4、解决下包速度慢的问题

### 4.1、下包速度慢的原因

在使用 npm 下包的时候，默认从国外的 https://registry.npmjs.org/ 服务器进行下载，此时，网络数据的传输需要经过漫长的海底光缆，因此下包速度会很慢。

### 4.2、解决问题

淘宝在国内搭建了一个服务器，专门把国外官方服务器上

的包**同步**到国内的服务器，然后在国内提供下包的服务。

从而极大的提高了下包的速度。

扩展：

**镜像**（Mirroring）是一种文件存储形式，一个磁盘上的

数据在另一个磁盘上存在一个完全相同的副本即为镜像。

![image-20230307220015486](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307220015486.png)

### 4.3、切换npm的下包镜像源

下包的镜像源，指的就是**下包的服务器地址**

```
#查看当前的下包镜像源
npm config get registry
#将下包的镜像源切换到淘宝镜像源
npm config set registry=https://registry.npm.taobao.org/
#检查镜像源是否下载成功
npm config get registry
```

### 4.4、nrm

为了更方便的切换下包的镜像源，我们可以安装 **nrm** 这个小工具，利用 nrm 提供的终端命令，可以快速查看和切换下包的镜像源。

```
#通过npm 包管理器，将nrm安装为全局可用的工具
npm i nrm -g
#查看所有可用的镜像源
nrm ls
#将下包的镜像源切换到taobao镜像
nrm use taobao
```

## 5、包的分类

使用 npm 包管理工具下载的包，共分为两大类，分别是：

+ 项目包
+ 全局包

### 5.1、项目包

那些被安装到项目的 node_modules 目录中的包，都是项目包。

项目包又分为两类，分别是：

+ **开发依赖包**（被记录到 devDependencies 节点中的包，只在开发期间会用到）
+ **核心依赖包**（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）

![image-20230307220742333](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307220742333.png)

### 5.2、全局包

在执行 npm install 命令时，如果提供了 **-g** 参数，则会把包安装为**全局包。**

全局包会被安装到 **C:\Users\用户目录\AppData\Roaming\npm\node_modules** 目录下。

```
npm i 包名 -g      #全局安装指定的包
npm uninstall 包名 -g   #卸载全局安装的包
```

注意：

① 只有**工具性质的包**，才有全局安装的必要性。因为它们提供了好用的终端命令。

② 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可

### 5.3、i5ting_toc

i5ting_toc 是一个可以把 md 文档转为 html 页面的小工具，使用步骤如下:

![image-20230307221158905](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230307221158905.png)

### 5.4、规范的包结构

在清楚了包的概念、以及如何下载和使用包之后，接下来，我们深入了解一下**包的内部结构**。

一个规范的包，它的组成结构，必须符合以下 3 点要求：

① 包必须以**单独的目录**而存在

② 包的顶级目录下要必须包含 **package.json** 这个包管理配置文件

③ package.json 中必须包含 **name，version，main** 这三个属性，分别代表包的名字、版本号、包的入口。

注意：以上 3 点要求是一个规范的包结构必须遵守的格式，关于更多的约束，可以参考如下网址：

https://yarnpkg.com/zh-Hans/docs/package-json

# 第七章、开发属于自己的包

## 1、开发包

### 1.1、包的基本结构

① 新建 itheima-tools 文件夹，作为包的根目录

② 在 itheima-tools 文件夹中，新建如下三个文件：

+ package.json （包管理配置文件）
+ index.js （包的入口文件）
+ README.md （包的说明文档）

### 1.2、初始化package.json

![image-20230309184854068](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230309184854068.png)

关于更多 license 许可协议相关的内容，可参考 https://www.jianshu.com/p/86251523e898

### 1.3、 **将不同的功能进行模块化拆分**

① 将格式化时间的功能，拆分到 src -> dateFormat.js 中

② 将处理 HTML 字符串的功能，拆分到 src -> htmlEscape.js 中

③ 在 index.js 中，导入两个模块，得到需要向外共享的方法

④ 在 index.js 中，使用 module.exports 把对应的方法共享出去

### 1.4、编辑包的说明文档

包根目录中的 README.md 文件，是包的使用说明文档。通过它，我们可以事先把包的使用说明，以 markdown 的格式写出来，方便用户参考。

README 文件中具体写什么内容，没有强制性的要求；只要能够清晰地把包的作用、用法、注意事项等描述清楚即可。

我们所创建的这个包的 README.md 文档中，会包含以下 6 项内容：

安装方式、导入方式、格式化时间、转义 HTML 中的特殊字符、还原 HTML 中的特殊字符、开源协议

## 2、发布包

### 2.1、登入npm账号

npm 账号注册完成后，可以在终端中执行 $\textcolor{red}{npm\       login} $命令，依次输入用户名、密码、邮箱后，即可登录成功。

![image-20230309185252601](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230309185252601.png)

注意：在运行 npm login 命令之前，必须先把下**包的服务器地址切换为 npm 的官方服务器**。否则会导致发布包失败！

### 2.2、发布包

将终端切换到包的根目录之后，运行 $\textcolor{red}{npm\  publish}$ 命令，即可将包发布到 npm 上（注意：**包名不能雷同**）。

![image-20230309185515267](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230309185515267.png)

### 2.3、删除已发布的包

运行 $\textcolor{red}{npm \ unpublish}$ 包名 --force 命令，即可从 npm 删除已发布的包。

注意：

![image-20230309185649670](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230309185649670.png)

① npm unpublish 命令只能删除 72 小时以内发布的包

② npm unpublish 删除的包，在 24 小时内不允许重复发布

③ 发布包的时候要慎重，尽量不要往 npm 上发布没有意义的包！

# 第八章、模块的加载机制

## 1、优先从缓冲中加载

**模块在第一次加载后会被缓存**。 这也意味着多次调用 require() 不会导致模块的代码被执行多次。

注意：不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，**从而提高模块的加载效率**。

## 2、内置模块的加载机制

内置模块是由 Node.js 官方提供的模块，**内置模块的加载优先级最高**。

例如，require('fs') 始终返回内置的 fs 模块，即使在 node_modules 目录下有名字相同的包也叫做 fs。

## 3、自定义模块的加载机制

使用 require() 加载自定义模块时，必须指定以 **./ 或 ../ 开头的路径标识符**。在加载自定义模块时，如果没有指定 ./ 或 ../ 这样的路径标识符，则 node 会把它当作**内置模块或第三方模块**进行加载。

同时，在使用 require() 导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会**按顺序**分别尝试加载以下的文件：

① 按照确切的文件名进行加载

② 补全 .js 扩展名进行加载

③ 补全 .json 扩展名进行加载

④ 补全 .node 扩展名进行加载

⑤ 加载失败，终端报错

## 4、第三方模块的加载机制

如果传递给 require() 的模块标识符不是一个内置模块，**也没有以 ‘./’ 或 ‘../’ 开头**，则 Node.js 会从当前模块的父目录开始，尝试从 **/node_modules 文件夹**中加载第三方模块。

**如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。**

例如，假设在 'C:\Users\itheima\project\foo.js' 文件里调用了 require('tools')，则 Node.js 会按以下顺序查找：

① C:\Users\itheima\project\node_modules\tools

② C:\Users\itheima\node_modules\tools

③ C:\Users\node_modules\tools

④ C:\node_modules\tools

## 5、目录作为模块

当把目录作为模块标识符，传递给 require() 进行加载的时候，有三种加载方式：

① 在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口

② 如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 $\textcolor{red}{index.js}$ 文件。

③ 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'

# 第九章、初始Express

## 1、简介

### 1.1、什么是Express

官方给出的概念：Express 是**基于 Node.js 平台**，快速、开放、极简的 Web 开发框架。
通俗的理解：Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。
**Express 的本质**：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。

Express 的中文官网： http://www.expressjs.com.cn/

### 1.2、Express能做什么

对于前端程序员来说，最常见的两种服务器，分别是：

+ **Web 网站服务器**：专门对外提供 Web 网页资源的服务器。
+  **API 接口服务器**：专门对外提供 API 接口的服务器。

使用 Express，我们可以方便、快速的创建 Web 网站的服务器或 API 接口的服务器。

### 1.3、安装

在项目所处的目录中，运行如下的终端命令，即可将 express 安装到项目中使用：

```
npm i express@4.17.1
```

## 2、基本使用

### 2.1、创建基本的Web服务器

```js
//1.导入express
const express = require('express')
//2、创建应用对象
const app = express();
//4、监听端口启动服务
app.listen(8000,()=>{
    console.log("服务端已经启用，8000端口监听中....");
})
```

### 2.2、监听GET请求

```js
//参数1：客户端请求的URL
//参数2：请求对应的处理函数
//   req：请求对象（包含了与请求相关的属性和方法）
//   res：响应对象（包含了与响应相关的属性和方法）
app.get('请求的URL'，function(req,res){
    /*处理函数*/
})
```

### 2.3、监听POST请求

```
//参数1：客户端请求的URL
//参数2：请求对应的处理函数
//   req：请求对象（包含了与请求相关的属性和方法）
//   res：响应对象（包含了与响应相关的属性和方法）
app.post('请求的URL'，function(req,res){
    /*处理函数*/
})
```

### 2.4、把内容响应给客户端

通过==res.send()== 方法，可以把处理好的内容，发送给客户端：

```js
//4.监听客户端的GET和POST请求，并向客户端响应具体的内容
app.get('/user', (req, res) => {
    //调用express提供的res.send()方法，并向客户端响应一个JSON对象
    res.send({name:'zs',age:20,gender:'男'})
})
app.post('/user',(req,res)=>{
    //调用express提供的res.send()方法，并向客户端响应 文本字符串
    res.send('请求成功');
})
```

### 2.5、获取URL中携带的查询参数

通过 ==req.query== 对象，可以访问到客户端通过**查询字符串**的形式，发送到服务器的参数：

```js
app.get('/',(req,res)=>{
    //通过 req.query 可以获取到客户端发送过俩的查询参数
    //注意：默认情况下，req.query 是一个空对象
    //req.query.name   req.query.age
    console.log(req.query);
    res.send(req.query);
})
```

### 2.6、获取到URL中的动态参数

通过 ==req.params== 对象，可以访问到 URL 中，通过 : 匹配到的**动态参数**：

```js
//URL地址中，可以通过 :参数名 的形式，匹配动态参数值
app.get('/user', (req, res) => {
    //req.params默认是一个空对象
    //里面存放着通过 : 动态匹配到的参数值
   console.log(req.params)
})
```

## 3、托管静态资源

### 3.1、express.static()

express 提供了一个非常好用的函数，叫做 ==express.static()==，通过它，我们可以非常方便地**创建一个静态资源服务器**，例如，通过如下代码就可以将 public 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

```js
app.use(express.static('public'))

//现在，你就可以访问 public 目录中的所有文件了：
http://localhost:3000/images/bg.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/login.js
```

注意：Express 在**指定**的静态目录中查找文件，并对外提供资源的访问路径。
因此，**存放静态文件的目录名不会出现在 URL 中**。

### 3.2、托管多个静态资源目录

如果要托管多个静态资源目录，请多次调用 express.static() 函数：

```js
app.use(express.static('public'))
app.use(express.static('file'))
```

访问静态资源文件时，express.static() 函数会根据目录的**添加顺序查找所需的文件**。

### 3.3、挂载路径前缀

如果希望在托管的**静态资源访问路径**之前，**挂载路径前缀**，则可以使用如下的方式：

```js
app.use('/public',express.static('public'))

//现在，你就可以通过带有 /public 前缀地址来访问 public 目录中的文件了：
http://localhost:3000/public/images/kitten.jpg
http://localhost:3000/public/css/style.css
http://localhost:3000/public/js/app.js
```

## 4、nodemon

### 4.1、为什么要使用nodemon

在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐。
现在，我们可以使用 nodemon（https://www.npmjs.com/package/nodemon） 这个工具，它能够**监听项目文件的变动**，当代码被修改后，nodemon 会**自动帮我们重启项目**，极大方便了开发和调试。

### 4.2、安装nodemon

```
npm install -g nodemon
```

### 4.3、使用nodemon

当基于 Node.js 编写了一个网站应用的时候，传统的方式，是运行 **node app.js** 命令，来启动项目。这样做的坏处是：代码被修改之后，需要手动重启项目。
现在，我们可以将 node 命令替换为 nodemon 命令，使用 **nodemon app.js** 来启动项目。这00样做的好处是：代码被修改之后，会被 nodemon 监听到，从而实现自动重启项目的效果。

```
nodemon app.js
```

# 第十章、Express路由

## 1、路由的概念

### 1.1、Express中的路由

在 Express 中，路由指的是**客户端的请求与服务器处理函数**之间的映射关系。
Express 中的路由分 3 部分组成，分别是**请求的类型、请求的 URL 地址、处理函数**，格式如下：

```JS
app.METHOD(PATH,HANDLER)
```

### 1.2、示例

```JS
//匹配搭配GET请求，且请求URL 为 /
app.get('/',(req,res)=>{
   res.send('Hello World')
})

//匹配搭配POST请求，且请求URL 为 /
app.get('/',(req,res)=>{
   res.send('Got a POST request')
})
```

### 1.3、路由的匹配过程

每当一个请求到达服务器之后，**需要先经过路由的匹配**，只有匹配成功之后，才会调用对应的处理函数。
在匹配时，会按照路由的顺序进行匹配，如果**请求类型和请求的 URL** 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。

![image-20230310112107889](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310112107889.png)

路由匹配的注意点：
① 按照定义的**先后顺序**进行匹配
② **请求类型和请求的URL**同时匹配成功，才会调用对应的处理函数

## 2、路由的使用

### 2.1、最简单的用法

在 Express 中使用路由最简单的方式，就是把路由挂载到 app 上，示例代码如下：

```js
const express = require('express')
const app = express()

// 挂载路由
app.get('/', (req, res) => {
  res.send('hello world.')
})
app.post('/', (req, res) => {
  res.send('Post Request.')
})

app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```

### 2.2、模块化路由

为了**方便对路由进行模块化的管理**，Express **不建议**将路由直接挂载到 app 上，而是**推荐将路由抽离为单独的模块**。
将路由抽离为单独模块的步骤如下：

1. 创建路由模块对应的 .js 文件
2. 调用 **express.Router()** 函数创建路由对象
3. 向路由对象上挂载具体的路由
4. 使用 **module.exports** 向外共享路由对象
5. 使用 **app.use()** 函数注册路由模块

#### 2.2.1、创建路由模块

```js
// 这是路由模块
// 1. 导入 express
const express = require('express')
// 2. 创建路由对象
const router = express.Router()

// 3. 挂载具体的路由
router.get('/user/list', (req, res) => {
  res.send('Get user list.')
})
router.post('/user/add', (req, res) => {
  res.send('Add new user.')
})

// 4. 向外导出路由对象
module.exports = router
```

#### 2.2.2、注册路由模块

```js
// 1. 导入路由模块
const router = require('./03.router')
// 2. 注册路由模块
app.use(router)
```

#### 2.2.3、为路由模块添加前缀

类似于托管静态资源时，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也非常简单：

```js
// 1. 导入路由模块
const router = require('./03.router')
// 2. 注册路由模块
app.use('/api', router)
```

# 第十一章、Express中间件

## 1、中间件的概念

中间件（Middleware ），特指业务流程的**中间处理环节**。

### 1.1、现实中的中间件

在处理污水的时候，一般都要经过**三个处理环节**，从而保证处理过后的废水，达到排放标准。

![image-20230310113037324](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310113037324.png)

处理污水的这三个中间处理环节，就可以叫做中间件。

### 1.2、Express中间件的调用流程

当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行**预处理**。

![image-20230310113202159](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310113202159.png)

### 1.3、Express中间件的格式

Express 的中间件，本质上就是一个 **function 处理函数**，Express 中间件的格式如下：

![image-20230310113254346](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310113254346.png)

注意：中间件函数的形参列表中，必须包含 $\textcolor{red}{next \ 参数}$。而路由处理函数中只包含 req 和 res。

### 1.4、next函数的作用

**next 函数**是实现**多个中间件连续调用**的关键，它表示把流转关系转交给下一个中间件或路由。

![image-20230310113417371](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310113417371.png)

## 2、中间件的初体验

### 2.1、定义中间件

可以通过如下的方式，定义一个最简单的中间件函数：

```js
// 定义一个最简单的中间件函数
const mw = function (req, res, next) {
	console.log('这是最简单的中间件函数')
  // 把流转关系，转交给下一个中间件或路由
	next()
}
```

### 2.2、全局生效的中间件

客户端发起的**任何请求**，到达服务器之后，**都会触发的中间件**，叫做全局生效的中间件。
通过调用 ==app.use(中间件函数)==，即可定义一个**全局生效**的中间件，示例代码如下：

```js
// 常量mw所指向的就是一个中间件函数
const mw = function (req, res, next) {
	console.log('这是最简单的中间件函数')
	next()
}

//全局生效的中间件
app.use(mw)
```

### 2.3、定义全局中间件的简化形式

```js
// 这是定义全局中间件的简化形式
app.use((req, res, next) => {
  console.log('这是最简单的中间件函数')
  next()
})
```

### 2.4、中间件的作用

多个中间件之间，$\textcolor{red}{共享同一份 req 和 res}$。基于这样的特性，我们可以在**上游**的中间件中，**统一**为 req 或 res 对象$\textcolor{red}{添加自定义的属性或方法}$，供下游的中间件或路由进行使用。

![image-20230310124605240](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310124605240.png)

### 2.5、定义多个全局中间件

可以使用 app.use() 连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件**定义的先后顺序依次**进行调用，示例代码如下：

```js
// 定义第一个全局中间件
app.use((req, res, next) => {
  console.log('调用了第1个全局中间件')
  next()
})
// 定义第二个全局中间件
app.use((req, res, next) => {
  console.log('调用了第2个全局中间件')
  next()
})

// 定义一个路由，请求这个路由，会依次触发上诉两个全局中间件
app.get('/user', (req, res) => {
  res.send('User page.')
})
```

### 2.6、局部生效的中间件

$\textcolor{red}{不使用 app.use() 定义的中间件}$，叫做局部生效的中间件，示例代码如下：

```js
// 1. 定义中间件函数
const mw1 = (req, res, next) => {
  console.log('调用了局部生效的中间件')
  next()
}

// 2. 创建路由
//mw1这个中间件只在当前路由中生效
app.get('/', mw1, (req, res) => {
  res.send('Home page.')
})
//mw1这个中间件不会影响下面这个路由
app.get('/user', (req, res) => {
  res.send('User page.')
})
```

### 2.7、定义对各局部中间件

可以在路由中，通过如下两种**等价**的方式，使用多个局部中间件：

```js
app.get('/', mw1, mw2, (req, res) => {
  res.send('Home page.')
})
app.get('/', [mw1, mw2], (req, res) => {
  res.send('Home page.')
})
```

### 2.8、中间件的6个使用事项

1. 一定要在**路由之前**注册中间件

2. 客户端发送过来的请求，**可以连续调用多个**中间件进行处理

3. 执行完中间件的业务代码之后，**不要忘记调用 next() 函数**

4. 为了**防止代码逻辑混乱**，调用 next() 函数后不要再写额外的代码

5. 连续调用多个中间件时，多个中间件之间，**共享** req 和 res 对象

6. $\textcolor{red}{可以发现next()在监听函数on('end',function)外使用了,}$

   $\textcolor{red}{但由于监听函数是异步任务next()被先执行了就会导致req.body = body req.body 无法挂载成功}$

## 3、中间件的分类

为了方便大家理解和记忆中间件的使用，Express 官方把常见的中间件用法，分成了 5 大类，分别是：

+ **应用级别**的中间件
+  **路由级别**的中间件
+ **错误级别**的中间件
+  **Express 内置**的中间件
+  **第三方**的中间件

### 3.1、应用级别的中间件

通过 **app.use() 或 app.get() 或 app.post()** ，绑定到 app 实例上的中间件，叫做**应用级别的中间件**，代码示例如下：

```js
//应用级别的中间件（全局中间件）
app.use((req,res,next)=>{
	next()
})

//应用级别的中间件（局部中间件）
app.get('/',mw1 ,(req,res) => {
	res.send('home page')
})
```

### 3.2、路由级别的中间件

绑定到 **express.Router()** 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过，**应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上**，代码示例如下：

```js
let app = express();
let router = express.Router();

//路由级别的中间件
router.use( (req,res，next) => {
	console.log('Time' + Date.now());
	next();
})

app.use('/',router);
```

### 3.3、错误级别的中间件

错误级别中间件的**作用**：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。
**格式**：错误级别中间件的 function 处理函数中，$\textcolor{red}{必须有 4 个形参}$，形参顺序从前到后，分别是 $\textcolor{red}{(err, req, res, next)}$。

```js
// 1. 定义路由
app.get('/', (req, res) => {
  // 1.1 人为的制造错误
  throw new Error('服务器内部发生了错误！')
  res.send('Home page.')
})

// 2. 定义错误级别的中间件，捕获整个项目的异常错误，从而防止程序的崩溃
app.use((err, req, res, next) => {
  console.log('发生了错误！' + err.message)
  res.send('Error：' + err.message)
})
```

注意：错误级别的中间件，$\textcolor{red}{必须注册在所有路由之后}$！

### 3.4、Express内置的中间件

自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验：

+ **express.static** 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）
+ **express.json** 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
+ **express.urlencoded** 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

```js
// 导入 express 模块
const express = require('express')
// 创建 express 的服务器实例
const app = express()

// 注意：除了错误级别的中间件，其他的中间件，必须在路由之前进行配置
// 通过 express.json() 这个中间件，解析表单中的 JSON 格式的数据
app.use(express.json())
// 通过 express.urlencoded() 这个中间件，来解析 表单中的 url-encoded 格式的数据
app.use(express.urlencoded({ extended: false }))

app.post('/user', (req, res) => {
  // 在服务器，可以使用 req.body 这个属性，来接收客户端发送过来的请求体数据
  // 默认情况下，如果不配置解析表单数据的中间件，则 req.body 默认等于 undefined
  console.log(req.body)
  res.send('ok')
})

app.post('/book', (req, res) => {
  // 在服务器端，可以通过 req,body 来获取 JSON 格式的表单数据和 url-encoded 格式的数据
  console.log(req.body)
  res.send('ok')
})

// 调用 app.listen 方法，指定端口号并启动web服务器
app.listen(80, function () {
  console.log('Express server running at http://127.0.0.1')
})
```

### 3.5、第三方的中间件

非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率。
例如：在 express@4.16.0 之前的版本中，经常使用 body-parser 这个第三方中间件，来解析请求体数据。使用步骤如下：

1. 运行 **npm install body-parser** 安装中间件
2. 使用 **require** 导入中间件
3. 调用 **app.use()** 注册并使用中间件

注意：Express 内置的 express.urlencoded 中间件，就是基于 body-parser 这个第三方中间件进一步封装出来的。用法和Express内置中间类似。

## 4、自定义中间件

### 4.1、需求分析

自己手动模拟一个类似于 express.urlencoded 这样的中间件，来解析 POST 提交到服务器的表单数据。
实现步骤：

1. 定义中间件
2. 监听 req 的 data 事件
3. 监听 req 的 end 事件
4. 使用 querystring 模块解析请求体数据
5. 将解析出来的数据对象挂载为 req.body
6. 将自定义中间件封装为模块

### 4.2、自定义中间件

使用 app.use() 来定义全局生效的中间件，代码如下：

```js
app.use(function(req,res,next){
	//中间件的业务逻辑
})
```

### 4.3、监听req的data事件

在中间件中，需要监听 req 对象的 data 事件，来获取客户端发送到服务器的数据。
如果数据量比较大，无法一次性发送完毕，则客户端会**把数据切割后，分批发送到服务器**。所以 data 事件可能会触发多次，每一次触发 data 事件时，**获取到数据只是完整数据的一部分**，需要手动对接收到的数据进行拼接。

```js
//1.定义变量，专门用来存储客户端发送过来的请求体数据
    let str = '';
    //2.监听req的data时间
    req.on('data',(chunk) =>{
        str +=chunk;
    });
```

### 4.4、监听req 的 end事件

当请求体数据**接收完毕**之后，会自动触发 req 的 end 事件。
因此，我们可以在 req 的 end 事件中，**拿到并处理完整的请求体数据**。示例代码如下：

```js
 //3.监听req的end事件
    req.on('end',()=>{
        //在str存放的是完整的请求体数据
        // console.log(str);
    })
```

### 4.5、使用querystring 模块解析请求体数据

Node.js 内置了一个 **querystring** 模块，**专门用来处理查询字符串**。通过这个模块提供的 **parse()** 函数，可以轻松把查询字符串，解析成对象的格式。示例代码如下：

```js
//导入node.js内置的queryString模块
const qs = require('querystring');

//调用qs.query()方法，把查询自负床解析为对象
const body = qs.parse(str);
```

### 4.6、将解析出来的数据对象挂载为 req.body

上游的中间件和下游的中间件及路由之间，**共享同一份 req 和 res**。因此，我们可以将解析出来的数据，**挂载为 req 的自定义属性，命名为 req.body**，供下游使用。示例代码如下

```js
req.on('end',()=>{
        //在str存放的是完整的请求体数据
        // console.log(str);

        //TODO:把字符串格式的请求体数据，解析成对象格式
        const body = qs.parse(str);
        console.log(body);
        req.body = body;
        next();
})
```

==注意：==

$\textcolor{red}{可以发现next()在监听函数on('end',function)外使用了,}$

$\textcolor{red}{但由于监听函数是异步任务next()被先执行了就会导致req.body = body req.body 无法挂载成功}$

### 4.7、将自定义中间件封装为模块

为了优化代码的结构，我们可以把自定义的中间件函数，**封装为独立的模块**，示例代码如下：

![image-20230310134958057](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310134958057.png)

# 第十二章、使用Express写接口

## 1、创建基本的服务器

```js
//1.导入express
const express = require('express')
//2、创建应用对象
const app = express();
//4、监听端口启动服务
app.listen(8000,()=>{
    console.log("服务端已经启用，8000端口监听中....");
})
```

## 2、创建API路由模块

```js
// apiRouter.js [路由模块]
const express = require('express');
const router = express.Router();

//bind your router here ...

module.exports = router


//-------------------------------------------------
//app.js [导入并注册路由模块]
//导入路由模块
const router = require('./apiRouter');
//把路由模块，注册到app
app.use('/api', router)
```

## 3、编写GET接口

```js
//在这里挂在对应的路由
router.get('/get',(req,res)=>{
    //通过req.query 获取客户端通过查询字符串，发送到服务器的数据
    const query = req.query;
    //调用res.send方法，向客户端响应处理结果
    res.send({
        status: 0,//0表示处理成功，1表示处理失败
        meg: 'GET请求成功',  //状态的描述
        data: query   //需要响应给客户端的数据
    })
})
```

## 4、编写POST接口

```js
//定义POST接口
router.post('/post',(req,res)=>{
    //通过req.body 获取请求体中包含的url-encoded 格式的数据
    const body = req.body;
    //调用res.send方法，向客户端响应处理结果
    res.send({
        status: 0,//0表示处理成功，1表示处理失败
        meg: 'POST请求成功',  //状态的描述
        data: body  //需要响应给客户端的数据
    })
})
```

注意：如果要获取 URL-encoded 格式的请求体数据，==必须配置中间件 app.use(express.urlencoded({ extended: false }))==

## 5、CORS跨域资源共享

### 5.1、接口的跨域问题

刚才编写的 GET 和 POST接口，存在一个很严重的问题：**不支持跨域请求**。
解决接口跨域问题的方案主要有两种：

+ $\textcolor{red}{CORS}$（主流的解决方案，推荐使用）
+  $\textcolor{red}{JSONP}$（有缺陷的解决方案：只支持 GET 请求） 

### 5.2、使用cors中间件解决跨域问题

cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。
使用步骤分为如下 3 步：

+ 运行 **npm install cors 安装中间件**
+ 使用 **const cors = require('cors') 导入中间件**
+ 在路由之前调用 **app.use(cors()) 配置中间件**

```
//一定要在路由之前配置cors这个中间件，从而解决接口跨域的问题
const cors = require('cors')
app.use(cors())
```

### 5.3、什么是cors

CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 **HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源**。
浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器**配置了 CORS 相关的 HTTP 响应**头，就可以**解除浏览器端的跨域访问限制**。

![image-20230310220111084](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310220111084.png)

### 5.4、CORS的注意事项

1. CORS 主要在**服务器端**进行配置。**客户端浏览器无须做任何额外的配置**，即可请求开启了 CORS 的接口。
2. CORS 在浏览器中**有兼容性**。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。

### 5.5、CORS响应头部

#### 5.5.1、Access-Control-Allow-Origin 

响应头部中可以携带一个 $\textcolor{red}{Access-Control-Allow-Origin}$ 字段，其语法如下:

```js
Access-Control-Allow-Origin: <origin> | *
```

其中，origin 参数的值指定了$\textcolor{red}{允许访问该资源的外域 URL}$。
例如，下面的字段值将**只允许**来自 http://itcast.cn 的请求：

```js
res.setHeader('Access-Control-Allow-Origin',' http://itcast.cn')
```

如果指定了 Access-Control-Allow-Origin 字段的值为**通配符 ***，表示允许来自任何域的请求，示例代码如下：

```js
res.setHeader('Access-Control-Allow-Origin','*')
```

#### 5.5.2、Access-Control-Allow-Headers

默认情况下，CORS 仅支持$\textcolor{blue}{客户端向服务器}$发送如下的 9 个**请求头**：
Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）
如果客户端向服务器**发送了额外的请求头信息**，则需要**在服务器端**，通过 Access-Control-Allow-Headers **对额外的请求头进行声明**，否则这次请求会失败！

![image-20230310221048252](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310221048252.png)

#### 5.2.3、Access-Control-Allow-Methods

默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。
如果客户端希望通过 $\textcolor{red}{PUT、DELETE}$ 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来**指明实际请求所允许使用的 HTTP 方法**。
示例代码如下：

![image-20230310221227339](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310221227339.png)

### 5.6、CORS请求的分类

客户端在请求 CORS 接口时，根据==请求方式和请求头==的不同，可以将 CORS 的请求分为两大类，分别是：

+ 简单请求
+ 预检请求

#### 5.6.1、简单请求

同时满足以下两大条件的请求，就属于简单请求：

1. **请求方式**：GET、POST、HEAD 三者之一
2. **HTTP 头部信息**不超过以下几种字段：$\textcolor{blue}{无自定义头部字段}$、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain）

#### 5.6.2、预测监测

只要符合以下任何一个条件的请求，都需要进行预检请求：

1. 请求方式为 $\textcolor{blue}{GET、POST、HEAD 之外的请求 Method 类型}$
2. 请求头中包$\textcolor{blue}{含自定义头部字段}$
3.  向服务器发送了 $\textcolor{blue}{application/json 格式的数据}$

在浏览器与服务器正式通信之前，浏览器**会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求**，所以这一次的 OPTION 请求称为“预检请求”。**服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据**。

#### 5.6.3、简单请求和预检请求的区别

**简单请求的特点**：客户端与服务器之间$\textcolor{blue}{只会发生一次请求}$。
**预检请求的特点**：客户端与服务器之间会发生两次请求，$\textcolor{blue}{OPTION 预检请求成功之后，才会发起真正的请求}$。

## 6、JSONP接口

### 6.1、JSONP的概念和特点

**概念**：浏览器端通过 <script> 标签的 src 属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做 JSONP。
**特点**：

1. JSONP 不属于真正的 Ajax 请求，因为它没有使用 XMLHttpRequest 这个对象。
2. JSONP 仅支持 GET 请求，不支持 POST、PUT、DELETE 等请求。

### 6.2、创建 JSONP 接口的注意事项

如果项目中$\textcolor{red}{已经配置了 CORS 跨域资源共享}$，为了==防止冲突，必须在配置 CORS 中间件之前声明 JSONP 的接口==。否则 JSONP 接口会被处理成开启了 CORS 的接口。示例代码如下：

![image-20230310222206548](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230310222206548.png)

### 6.3、实现JSONP接口的步骤

1. **获取**客户端发送过来的**回调函数的名字**
2. **得到**要通过 JSONP 形式**发送给客户端的数据**
3. 根据前两步得到的数据，**拼接出一个函数调用的字符串**
4. 把上一步拼接得到的字符串，响应给客户端的 <script> 标签进行解析执行

### 6.4、实现 JSONP 接口的具体代码

```js
//必须在配置cors中间件之前，配置JSONP的接口
app.get('/api/jsonp',(req,res)=>{
    //1.得到函数的名称
    const funcName = req.query.callback;
    //2.定义要发送到客户端的数据对象
    const data = {name:'zs',age:20};
    //3.拼接处一个函数的调用
    const scriptStr = `${funcName}(${JSON.stringify(data)})`;
    //4.把拼接的字符串响应给客户端
    res.send(scriptStr);
})
```

### 6.5、在网页中使用 jQuery 发起 JSONP 请求

调用 $.ajax() 函数，**提供 JSONP 的配置选项**，从而发起 JSONP 请求，示例代码如下：

```js
 //测试JSONP接口
$('#btnJSONP').on('click', function () {
       $.ajax({
           type: 'GET',
           dataType:'jsonp',
           url: 'http://127.0.0.1:8080/api/jsonp',
           success: function (res) {
               console.log(res);
       		}
		})
})
```





