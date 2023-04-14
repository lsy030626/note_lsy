# 一、函数

## 1、函数的使用

### ①声明函数（两种）

1、自定义函数方式(命名函数)

```js
//声明函数
function 函数名(形参1, 形参2 , 形参3...){
     //函数体代码
}
函数名();
```

2.函数表达式方式(匿名函数)

```js
// 这是函数表达式写法，匿名函数后面跟分号结束
var fn = function(){...};

// 调用的方式，函数调用必须写到函数体下面
fn();
```



### ②调用函数

```js
//调用函数
函数名(实参1，实参2，实参3...); //通过调用函数名来执行函数体代码
```

| 参数个数             | 说明                               |
| -------------------- | ---------------------------------- |
| 实参个数等于形参个数 | 输出正确结果                       |
| 实参个数多于形参个数 | 只取到形参的个数                   |
| 实参个数小于形参个数 | 多的形参定义为undefined，结果为NaN |

## 2、arguments变量

当我们不确定有多少个参数传递的时候，可以用 arguments 来获取。在 JavaScript 中，arguments 实际上它是当前函数的一个内置对象。所有函数都内置了一个 arguments 对象，arguments 对象中存储了传递的所有实参。

+ arguments存放的是传递过来的实参

+ arguments展示形式是一个伪数组，因此可以进行遍历。伪数组具有以下特点

 ①：具有 length 属性

 ②：按索引方式储存数据

 ③：不具有数组的 push , pop 等方法

## 3、三元表达式

- 语法结构 : 表达式1 ? 表达式2 : 表达式3

==说明：==如果表达式1为true，则返回表达式2的值,如果表达式1为false，则返回表达式3的值

## 4、作用域

==全局作用域：==作用于所有代码执行的环境(整个 script 标签内部)或者一个独立的 js 文件

==局部（函数）作用域：==作用于函数内的代码环境，就是局部作用域。 因为跟函数有关系，所以也称为函数作用域

**重点**

JS 没有块级作用域🔥

在其它语言中，例如Java

```js
if(true){
    int num = 123;
    System.out.println(num);	// 123
}
System.out.println(num);		// 报错
```

es6之前js没有块级作用域（es6中let有）

```js
if(true){
    int num = 123;
    System.out.println(num);	// 123
}
System.out.println(num);		// 123
```

## 5、局部变量和全局变量

- 全局变量：在任何一个地方都可以使用，只有在浏览器关闭时才会被销毁，因此比较占内存
- 局部变量：只在函数内部使用，当其所在的代码块被执行时，会被初始化；当代码块运行结束后，就会被销毁，因此更节省内存空间

## 6、预解析

- **预解析**：js引擎会把js里面所有的 **var** 还有 **function** 提升到当前作用域的最前面

### 6.1、变量预解析（变量提升）

变量提升: 变量的声明会被提升到**当前作用域**的最上面，变量的赋值不会提升

```js
console.log(num);  // 结果是多少？
var num = 10;   
// undefined


//相当于执行了以下代码
var num;		// 变量声明提升到当前作用域最上面
console.log(num);
num = 10;		// 变量的赋值不会提升
```

### 6.2、函数预解析（函数提升）

```js
// 匿名函数(函数表达式方式):若我们把函数调用放在函数声明上面
fn();
var  fn = function() {
    console.log('22'); // 报错
}


//相当于执行了以下代码
var fn;
fn();      //fn没赋值，没这个，报错
var  fn = function() {
    console.log('22'); //报错
}
```

# 二、对象

## 1、创建对象

### 1.1、利用字面量创建对象

对象字面量：就是花括号 `{ }` 里面包含了表达这个具体事物（对象）的属性和方法

`{ }` 里面采取键值对的形式表示

```js
var star = {
    name : 'pink',
    age : 18,
    sex : '男',
    sayHi : function(){
        alert('大家好啊~');
    }
};
// 多个属性或者方法中间用逗号隔开
// 方法冒号后面跟的是一个匿名函数
```

### 1.2、利用new Object创建对象

```js
var obj = new Object(); //创建了一个空的对象
obj.name = '张三丰';
obj.age = 18;
obj.sex = '男';
obj.sayHi = function() {
    console.log('hi~');
}

//1.我们是利用等号赋值的方法添加对象
//2.每个属性和方法之间用分号结束
console.log(obj.name);
console.log(obj['sex']);
obj.sayHi();
```

### 1.3、利用构造函数创建对象

```js
//构造函数的语法格式
function 构造函数名() {
    this.属性 = 值;
    this.方法 = function() {}
}
new 构造函数名();
```

```js
//1. 构造函数名字首字母要大写
//2. 构造函数不需要return就可以返回结果
//3. 调用构造函数必须使用 new
//4. 我们只要new Star() 调用函数就创建了一个对象
//5. 我们的属性和方法前面必须加this
function Star(uname,age,sex) {
    this.name = uname;
    this.age = age;
    this.sex = sex;
    this.sing = function(sang){
        console.log(sang);
    }
}
var ldh = new Star('刘德华',18,'男');
console.log(typeof ldh) // object对象，调用函数返回的是对象

console.log(ldh.name);
console.log(ldh['sex']);
ldh.sing('冰雨');
//把冰雨传给了sang

var zxy = new Star('张学友',19,'男');

```

- 构造函数名字==首字母要大写==
- 函数内的属性和方法前面需要添加==this== ，表示当前对象的属性和方法。
- 构造函数中不需要 return 返回结果。
- 当我们创建对象的时候，必须用 new 来调用构造函数。

## 2、new关键字

new 在执行时会做四件事:

1. 在内存中创建一个新的空对象。
2. 让 this 指向这个新的对象。
3. 执行构造函数里面的代码，给这个新对象添加属性和方法
4. 返回这个新对象（所以构造函数里面不需要return）

## 3、遍历对象的属性

- `for...in` 语句用于对数组或者对象的属性进行循环操作

```js
for(变量 in 对象名字){
    // 在此执行代码
}
```

```js
var obj = {
    name: '秦sir',
    age: 18,
    sex: '男',
    fn:function() {};
};
console.log(obj.name);
console.log(obj.age);
console.log(obj.sex);

//for in 遍历我们的对象
//for (变量 in 对象){}
//我们使用for in 里面的变量 我们喜欢写k 或者key
for(var k in obj){
    console.log(k); // k 变量 输出得到的是属性名
    console.log(obj[k]); // obj[k] 得到的是属性值
}
```

# 二、内置对象

查文档：

MDN: https://developer.mozilla.org/zh-CN/

## 1、数学对象Math

```js
// Math数学对象，不是一个构造函数，所以我们不需要new 来调用，而是直接使用里面的属性和方法即可

Math.PI		 			// 圆周率
Math.floor() 	 		// 向下取整
Math.ceil()             // 向上取整
Math.round()            // 四舍五入版 就近取整   注意 -3.5   结果是  -3 
Math.abs()		 		// 绝对值
Math.max()/Math.min()	// 求最大和最小值 
Math.random()			//随机返回一个小数，其取值范围是 [0，1)，左闭右开 0 <= x < 1
```

## 2、时间对象Date

**注意：**获取当前时间必须要实例化

==var now = new Date()==

### 2.1、Date()构造函数的参数

如果括号里面有时间，就返回参数里面的时间。例如日期格式字符串为 `‘2019-5-1’`，可以写成`new Date('2019-5-1')` 或者 `new Date('2019/5/1')`

- 如果Date()不写参数，就返回当前时间
- 如果Date()里面写参数，就返回括号里面输入的时间

```js
// 1.如果没有参数，返回当前系统的当前时间
var now = new Date();
console.log(now);

// 2.参数常用的写法 数字型 2019,10,1  字符串型 '2019-10-1 8:8:8' 时分秒
// 如果Date()里面写参数，就返回括号里面输入的时间 
var data = new Date(2019,10,1);
console.log(data);  // 返回的是11月不是10月

var data2 = new Date('2019-10-1 8:8:8');
console.log(data2);
```

| 方法名        | 说明                     |
| ------------- | ------------------------ |
| getFullYear() | 获取当年                 |
| getMonth()    | 获取当月（0-11）         |
| getDate()     | 获取日期（1-31）         |
| getDay()      | 获取星期几(周日0到周六6) |
| getHours()    | 获取当前小时（0-23）     |
| getMinutes()  | 获取当前分钟（0-59）     |
| getSeconds()  | 获取当前秒数（0-59）     |

### 2.2、获取日期的总的毫秒形式

- `date.valueOf()` ：得到现在时间距离1970.1.1总的毫秒数
- `date.getTime()` ：得到现在时间距离1970.1.1总的毫秒数

```js
// 获取Date总的毫秒数 不是当前时间的毫秒数 而是距离1970年1月1号过了多少毫秒数

// 实例化Date对象
var date = new Date();

// 1 .通过 valueOf()  getTime() 用于获取对象的原始值
console.log(date.valueOf());  //得到现在时间距离1970.1.1总的毫秒数
console.log(date.getTime());

// 2.简单的写法
var date1 = +new Date();  // +new Date()返回的就是总的毫秒数，
console.log(date1);

// 3. HTML5中提供的方法 获得总的毫秒数 有兼容性问题
console.log(Date.now());
```

## 3、数组对象

### 3.1、创建的两种方法

- 字面量方式
- new Array()

### 3.2、检测是否为数组

- instanceof 运算符，可以判断一个对象是否属于某种类型
- `Array.isArray()` 用于判断一个对象是否为数组，isArray() 是 HTML5 中提供的方法

### 3.3、添加删除数组（重点）

| 方法名          | 说明                                                  | 返回值               |
| --------------- | ----------------------------------------------------- | -------------------- |
| push(参数1....) | 末尾添加一个或多个元素，注意修改原数组                | 并返回新的长度       |
| pop()           | 删除数组最后一个元素                                  | 返回它删除的元素的值 |
| unshift(参数1…) | 向数组的开头添加一个或更多元素，注意修改原数组        | 并返回新的长度       |
| shift()         | 删除数组的第一个元素，数组长度减1，无参数，修改原数组 | 并返回第一个元素     |

### 3.4、数组排序

| 方法名    | 说明                         | 是否修改原数组                     |
| --------- | ---------------------------- | ---------------------------------- |
| reverse() | 颠倒数组中元素的顺序，无参数 | 该方法会改变原来的数组，返回新数组 |
| sort()    | 对数组的元素进行排序         | 该方法会改变原来的数组，返回新数组 |

### 3.5、数组索引

| 方法名        | 说明                               | 返回值                                   |
| ------------- | ---------------------------------- | ---------------------------------------- |
| indexOf()     | 数组中查找给定元素的第一个索引     | 如果存在返回索引号，如果不存在，则返回-1 |
| lastIndexOf() | 在数组的最后一个索引，从后向前索引 | 如果存在返回索引号，如果不存在，则返回-1 |

### 3.6、数组转化为字符串

| 方法名         | 说明                                       | 返回值         |
| -------------- | ------------------------------------------ | -------------- |
| toString()     | 把数组转换成字符串，逗号分隔每一项         | 返回一个字符串 |
| join(‘分隔符’) | 方法用于把数组中的所有元素转换为一个字符串 | 返回一个字符串 |

### 3.7、其他方法

| 方法名   | 说明                                   | 返回值                                   |
| -------- | -------------------------------------- | ---------------------------------------- |
| concat() | 连接两个或多个数组 不影响原数组        | 返回一个新的数组                         |
| slice()  | 数组截取slice(begin,end)               | 返回被截取项目的新数组                   |
| splice() | 数组删除splice(第几个开始要删除的个数) | 返回被删除项目的新数组，这个会影响原数组 |

## 4、字符串对象

### 4.1、字符串的不可变

指的是里面的值不可变，虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间。

```js
var str = 'abc';
str = 'hello';
// 当重新给 str 赋值的时候，常量'abc'不会被修改，依然在内存中
// 重新给字符串赋值，会重新在内存中开辟空间，这个特点就是字符串的不可变
// 由于字符串的不可变，在大量拼接字符串的时候会有效率问题
var str = '';
for(var i = 0; i < 10000;  i++){
    str += i;
}
console.log(str);
// 这个结果需要花费大量时间来显示，因为需要不断的开辟新的空间

```

### 4.2、根据字符返回位置

| 方法名                              | 说明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| indexOf(‘要查找的字符’，开始的位置) | 返回指定内容在元字符串中的位置，如果找不到就返回-1，开始的位置是index索引号 |
| lastIndexOf()                       | 从后往前找，只找第一个匹配的                                 |

### 4.3、根据位置返回字符

| 方法名            | 说明                                     | 使用                        |
| ----------------- | ---------------------------------------- | --------------------------- |
| charAt(index)     | 返回指定位置的字符(index字符串的索引号)  | str.charAt(0)               |
| charCodeAt(index) | 获取指定位置处字符的ASCII码(index索引号) | str.charCodeAt(0)           |
| str[index]        | 获取指定位置处字符                       | HTML,IE8+支持和charAt()等效 |

### 4.4、字符串操作方法

| 方法名                  | 说明                                                         |
| ----------------------- | ------------------------------------------------------------ |
| concat(str1,str2,str3…) | concat() 方法用于连接两个或对各字符串。拼接字符串            |
| substr(start,length)    | 从 start 位置开始(索引号), length 取的个数。                 |
| slice(start,end)        | 从 start 位置开始，截取到 end 位置 ，end 取不到 (两个都是索引号) |
| substring(start,end)    | 从 start 位置开始，截取到 end 位置 ，end 取不到 (基本和 slice 相同，但是不接受负) |

### 4.5、replace()方法

replace() 方法用于在字符串中用一些字符替换另一些字符

其使用格式：`replace(被替换的字符,要替换为的字符串)`

```js
// 1. 替换字符 replace('被替换的字符', '替换为的字符')  它只会替换第一个字符
    var str = 'andyandy';
    console.log(str.replace('a', 'b'));
    // 有一个字符串 'abcoefoxyozzopp'  要求把里面所有的 o 替换为 *
    var str1 = 'abcoefoxyozzopp';
    while (str1.indexOf('o') !== -1) {
        str1 = str1.replace('o', '*');
    }
    console.log(str1);
```

### 4.6、split()方法

split() 方法用于切分字符串，它可以将字符串切分为数组。在切分完毕之后，返回的是一个新数组。

例如下面代码：

```js
var str = 'a,b,c,d';
console.log(str.split(','));
// 返回的是一个数组 ['a', 'b', 'c', 'd']
```

### 4.7、大小写转化

- `toUpperCase()` 转换大写
- `toLowerCase()` 转换小写

# 三、DOM

## 1、获取元素

### 1.1、根据ID属性获取元素

使用 `getElementByld()` 方法可以获取带ID的元素对象

### 1.2、根据标签名获取

①根据**标签名**获取，使用 `getElementByTagName()` 方法可以返回带有指定标签名的**对象的集合**

- 因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历
- 得到元素对象是动态的
- 返回的是获取过来元素对象的集合，以伪数组的形式存储
- 如果获取不到元素，则返回为空的伪数组(因为获取不到对象)

②还可以根据标签名获取某个元素（父元素）内部所有指定标签名的子元素,获取的时候不包括父元素自己

```js
element.getElementsByTagName('标签名')

ol.getElementsByTagName('li');
```

### 1.3、通过H5新增方法获取

**①getElementsByClassName**

根据类名返回元素对象合集

**②document.querySelector**

根据指定选择器返回第一个元素对象

**③document.querySelectorAll**

根据指定选择器返回所有元素对象

### 1.4、获取特殊元素

**①获取body元素**

返回body元素对象

```js
document.body;
```

**②获取html元素**

返回html元素对象

```js
document.documentElement;
```

## 2、操作元素

### 2.1、改变元素属性

```js
// img.属性
img.src = "xxx";

input.value = "xxx";
input.type = "xxx";
input.checked = "xxx";
input.selected = true / false;
input.disabled = true / false;
```

**样式**

```js
// element.style
div.style.backgroundColor = 'pink';
div.style.width = '250px';

//直接修改类名
element.className
```

+ JS里面的样式采取驼峰命名法，比如 fontSize ，backgroundColor
+ JS 修改 style 样式操作 ，产生的是行内样式，CSS权重比较高
+ 如果样式修改较多，可以采取操作类名方式更改元素样式
+ class 因为是个保留字，因此使用className来操作元素类名属性
+ className 会直接更改元素的类名，会覆盖原先的类名

### 2.2、自定义属性

#### 2.2.1、获取属性值

**①获取属性值**

element.属性;

**②获取自定义属性**

element.getAttribute('属性');

#### 2.2.2、设置属性值

**①设置内置属性值**

element.属性 = '值';

**②设置自定义属性**

element.setAttribute('属性','值');

#### 2.2.3、移除属性

```js
element.removeAttribute('属性');
```

### 2.3、H5自定义属性

自定义属性目的：

- 保存并保存数据，有些数据可以保存到页面中而不用保存到数据库中
- 有些自定义属性很容易引起歧义，不容易判断到底是内置属性还是自定义的，所以H5有了规定

#### 2.3.1、设置H5自定义属性

H5规定自定义属性 `data-`开头作为属性名并赋值

```js
<div data-index = "1"></>
// 或者使用JavaScript设置
div.setAttribute('data-index',1);
```

#### 2.3.2 获取H5自定义属性

- 兼容性获取 `element.getAttribute('data-index')`
- H5新增的：`element.dataset.index` 或`element.dataset['index']` IE11才开始支持

## 3、节点操作

![img](https://img-blog.csdnimg.cn/f176c025b5ff43468d53ed4d49259812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

### 3.1、父级节点

```js
node.parentNode
```

- `parentNode`属性可以返回某节点的父结点，注意是最近的一个父结点
- 如果指定的节点没有父结点则返回null

### 3.2、子节点

**①parentNode.childNodes(标准)**

- `parentNode.childNodes` 返回包含指定节点的子节点的集合，该集合为即时更新的集合
- 返回值包含了所有的子节点，包括元素节点，文本节点等
- 如果只想要获得里面的元素节点，则需要专门处理。所以我们一般不提倡使用`childNodes`

**②parentNode.children(非标准)**

- `parentNode.children` 是一个只读属性，返回所有的子元素节点
- 它只返回子元素节点，其余节点不返回 （**这个是我们重点掌握的**）
- 虽然 children 是一个非标准，但是得到了各个浏览器的支持，因此我们可以放心使用

#### 3.2.1、第一个子节点

**①parentNode.firstChild**

- `firstChild` 返回第一个子节点，找不到则返回null
- 同样，也是包含所有的节点

**②parentNode.firstElementChild**

- `firstElementChild` 返回第一个子节点，找不到则返回null（元素）
- 有兼容性问题，IE9以上才支持

#### 3.2.2、最后一个子节点

**①parentNode.lastChild**

- `lastChild` 返回最后一个子节点，找不到则返回null
- 同样，也是包含所有的节点

**②parentNode.lastElementChild**

- `lastElementChild` 返回最后一个子节点，找不到则返回null（元素）
- 有兼容性问题，IE9以上才支持

#### 3.2.3、解决兼容性问题

实际开发中，firstChild 和 lastChild 包含其他节点，操作不方便，而 firstElementChild 和 lastElementChild 又有兼容性问题，那么我们如何获取第一个子元素节点或最后一个子元素节点呢？

- 如果想要第一个子元素节点，可以使用 `parentNode.chilren[0]`

- 如果想要最后一个子元素节点，可以使用

  ```js
  // 数组元素个数减1 就是最后一个元素的索引号
  parentNode.chilren[parentNode.chilren.length - 1]
  ```

### 3.3、兄弟节点

#### 3.3.1、下一个兄弟节点

```
node.nextSibling
```

+ nextSibling 返回当前元素的下一个兄弟元素节点，找不到则返回null
+ 同样，也是包含所有的节点

#### 3.3.2、上一个兄弟节点

```js
node.previousSibling
```

- `previousSibling` 返回当前元素上一个兄弟元素节点，找不到则返回null
- 同样，也是包含所有的节点

#### 3.3.3、下一个兄弟节点(兼容性)

```js
node.nextElementSibling
```

- `nextElementSibling` 返回当前元素下一个兄弟元素节点，找不到则返回null（元素）
- 有兼容性问题，IE9才支持

#### 3.3.4、上一个兄弟节点(兼容性)

```js
node.previousElementSibling
```

- `previousElementSibling` 返回当前元素上一个兄弟元素节点，找不到则返回null（元素）
- 有兼容性问题，IE9才支持

#### 3.3.5、解决兼容性

```js
function getNextElementSibling(element) {
    var el = element;
    while(el = el.nextSibling) {
        if(el.nodeType === 1){
            return el;
        }
    }
    return null;
}
```

### 4、创建节点

```js
document.createElement('tagName');
```

- `document.createElement()` 方法创建由 tagName 指定的HTML 元素
- 因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为**动态创建元素节点**

### 5、添加节点

**①node.appendChild(child)**

- `node.appendChild()` 方法将一个节点添加到指定父节点的子节点列表**末尾**。类似于 CSS 里面的 after 伪元素。

**②node.insertBefore(child,指定元素)**

- `node.insertBefore()` 方法将一个节点添加到父节点的指定子节点**前面**。类似于 CSS 里面的 before 伪元素。

### 6、删除节点

```js
node.removeChild(child)
```

- `node.removeChild()`方法从 DOM 中删除一个子节点，返回删除的节点

### 7、复制节点（克隆节点）

```js
node.cloneNode()
```

- `node.cloneNode()`方法返回调用该方法的节点的一个副本。 也称为克隆节点/拷贝节点
- 如果括号参数为空或者为 false ，则是浅拷贝，即只克隆复制节点本身，不克隆里面的子节点
- 如果括号参数为 true ，则是深度拷贝，会复制节点本身以及里面所有的子节点

### 8、三者创建元素的区别

- doucument.write()
- element.innerHTML
- document.createElement()

**==区别==**

- `document.write()` 是直接将内容写入页面的内容流，但是文档流执行完毕，则它会导致页面全部重绘
- `innerHTML` 是将内容写入某个 DOM 节点，不会导致页面全部重绘
- `innerHTML` 创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂

- `createElement()`创建多个元素效率稍低一点点，但是结构更清晰

## 5、事件高级

### 5.1、注册事件

给元素添加事件，称为==注册事件==或者==绑定事件==。

注册事件有两种方式：==传统方式==和==方法监听注册方式==

| 传统注册方式                                                 | 方法监听注册方式                                      |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| 利用 on 开头的事件 onclick                                   | w3c 标准推荐方式                                      |
| `<button onclick = "alert("hi")"></button>`                  | addEventListener() 它是一个方法                       |
| btn.onclick = function() {}                                  | IE9 之前的 IE 不支持此方法，可使用 attachEvent() 代替 |
| 特点：注册事件的唯一性                                       | 特点：同一个元素同一个事件可以注册多个监听器          |
| 同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面注册的处理函数 | 按注册顺序依次执行                                    |

#### ①addEventListener事件监听方式

- `eventTarget.addEventListener()`方法将指定的监听器注册到 eventTarget（目标对象）上
- 当该对象触发指定的事件时，就会执行事件处理函数

```js
eventTarget.addEventListener(type,listener[,useCapture])
```

该方法接收三个参数：

- `type`:事件类型字符串，比如click,mouseover,注意这里不要带on
- `listener`：事件处理函数，事件发生时，会调用该监听函数
- `useCapture`：可选参数，是一个布尔值，默认是 false。学完 DOM 事件流后，我们再进一步学习

#### ②attachEvent事件监听方式(兼容)

- `eventTarget.attachEvent()`方法将指定的监听器注册到 eventTarget（目标对象） 上
- 当该对象触发指定的事件时，指定的回调函数就会被执行

```js
eventTarget.attachEvent(eventNameWithOn,callback)
```

该方法接收两个参数：

- `eventNameWithOn`：事件类型字符串，比如 onclick 、onmouseover ，==这里要带 on==
- `callback`： 事件处理函数，当目标触发事件时回调函数被调用
- ie9以前的版本支持

#### ③注册事件兼容性解决方案

兼容性处理的原则：==首先照顾大多数浏览器，再处理特殊浏览器==

```js
 function addEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 addEventListener 方法
      if (element.addEventListener) {
        element.addEventListener(eventName, fn);  // 第三个参数 默认是false
      } else if (element.attachEvent) {
        element.attachEvent('on' + eventName, fn);
      } else {
        // 相当于 element.onclick = fn;
        element['on' + eventName] = fn;
 } 
```

### 5.2、删除事件

#### ①removeEventListener删除事件方式

```
eventTarget.removeEventListener(type,listener[,useCapture]);
```

该方法接收三个参数：

- `type`:事件类型字符串，比如click,mouseover,注意这里不要带on
- `listener`：事件处理函数，事件发生时，会调用该监听函数
- `useCapture`：可选参数，是一个布尔值，默认是 false。学完 DOM 事件流后，我们再进一步学习

#### **②detachEvent删除事件方式(兼容)**

该方法接收两个参数：

- `eventNameWithOn`：事件类型字符串，比如 onclick 、onmouseover ，这里要带 on
- `callback`： 事件处理函数，当目标触发事件时回调函数被调用
- ie9以前的版本支持

#### ③传统事件删除方式

```js
eventTarget.onclick = null;
```

#### ④兼容性解决方案

```js
 function removeEventListener(element, eventName, fn) {
      // 判断当前浏览器是否支持 removeEventListener 方法
      if (element.removeEventListener) {
        element.removeEventListener(eventName, fn);  // 第三个参数 默认是false
      } else if (element.detachEvent) {
        element.detachEvent('on' + eventName, fn);
      } else {
        element['on' + eventName] = null;
 } 
```

## 6、DOM事件流

- 事件流描述的是从页面中接收事件的顺序
- 事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流

![img](https://img-blog.csdnimg.cn/063297f2336f43dfb246930ae877a9ad.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

- ==事件冒泡==： IE 最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到 DOM 最顶层节点的过程。
- ==事件捕获==： 网景最早提出，由 DOM 最顶层节点开始，然后逐级向下传播到到最具体的元素接收的过程。

![img](https://img-blog.csdnimg.cn/51f0146f0e334813b35d9b7075382a33.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

**小结**

+ JS 代码中只能执行捕获或者冒泡其中的一个阶段

+ onclick 和 attachEvent只能得到冒泡阶段

+ addEventListener(type,listener[,useCapture])第三个参数如果是 true，表示在事件捕获阶段调用事件处理程序；如果是 false (不写默认就是false),表示在事件冒泡阶段调用事件处理程序

+ 实际开发中我们很少使用事件捕获，我们更关注事件冒泡。
+ 有些事件是没有冒泡的，比如 onblur、onfocus、onmouseenter、onmouseleave

## 7、事件对象

```js
eventTarget.onclick = function(event) {
   // 这个 event 就是事件对象，我们还喜欢的写成 e 或者 evt 
} 
eventTarget.addEventListener('click', function(event) {
   // 这个 event 就是事件对象，我们还喜欢的写成 e 或者 evt  
})

```

- 官方解释：event 对象代表事件的状态，比如键盘按键的状态、鼠标的位置、鼠标按钮的状态

- 简单理解：
  - 事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面
  - 这个对象就是事件对象 event，它有很多属性和方法，比如“
    - 谁绑定了这个事件
    - 鼠标触发事件的话，会得到鼠标的相关信息，如鼠标位置
    - 键盘触发事件的话，会得到键盘的相关信息，如按了哪个键

- 这个 event 是个形参，系统帮我们设定为事件对象，不需要传递实参过去
- 当我们注册事件时， event 对象就会被系统自动创建，并依次传递给事件监听器（事件处理函数）

```js
<body>
    <div>123</div>
    <script>
        // 事件对象
        var div = document.querySelector('div');
        div.onclick = function(e) {
                // console.log(e);
                // console.log(window.event);
                // e = e || window.event;
                console.log(e);


            }
        // 1. event 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看
        // 2. 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数
        // 3. 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键
        // 4. 这个事件对象我们可以自己命名 比如 event 、 evt、 e
        // 5. 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法  e = e || window.event;
    </script>
</body>
```

### 7.1、事件对象的兼容性方案

事件对象本身的获取存在兼容问题：

1. 标准浏览器中是浏览器给方法传递的参数，只需要定义形参 e 就可以获取到。
2. 在 IE6~8 中，浏览器不会给方法传递参数，如果需要的话，需要到 window.event 中获取查找

解决：

```js
e = e || window.event;
```

### 7.2、事件对象的常见属性和方法

| 事件对象属性方法    | 说明                                          |
| ------------------- | --------------------------------------------- |
| e.target            | 返回触发事件的对象 标准                       |
| e.srcElement        | 返回触发事件的对象 非标准 ie6-8使用           |
| e.type              | 返回事件的类型 比如`click` `mouseover` 不带on |
| e.cancelBubble      | 该属性阻止冒泡，非标准，ie6-8使用             |
| e.returnValue       | 该属性阻止默认行为 非标准，ie6-8使用          |
| e.preventDefault()  | 该方法阻止默认行为 标准 比如不让链接跳转      |
| e.stopPropagation() | 阻止冒泡 标准                                 |

e.target 和 this 的区别：

- this 是事件绑定的元素， 这个函数的调用者（绑定这个事件的元素）
- e.target 是事件触发的元素。

```js
<body>
    <div>123</div>
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
    <script>
        // 常见事件对象的属性和方法
        // 1. e.target 返回的是触发事件的对象（元素）  this 返回的是绑定事件的对象（元素）
        // 区别 ： e.target 点击了那个元素，就返回那个元素 this 那个元素绑定了这个点击事件，那么就返回谁
        var div = document.querySelector('div');
        div.addEventListener('click', function(e) {
            console.log(e.target);
            console.log(this);

        })
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
                // 我们给ul 绑定了事件  那么this 就指向ul  
                console.log(this);
                console.log(e.currentTarget);

                // e.target 指向我们点击的那个对象 谁触发了这个事件 我们点击的是li e.target 指向的就是li
                console.log(e.target);

            })
        // 2. 了解 跟 this 有个非常相似的属性 currentTarget  ie678不认识
    </script>
</body>

```



### 7.3、事件对象阻止默认行为

```js
<body>
    <div>123</div>
    <a href="http://www.baidu.com">百度</a>
    <form action="http://www.baidu.com">
        <input type="submit" value="提交" name="sub">
    </form>
    <script>
        // 常见事件对象的属性和方法
        // 1. 返回事件类型
        var div = document.querySelector('div');
        div.addEventListener('click', fn);
        div.addEventListener('mouseover', fn);
        div.addEventListener('mouseout', fn);

        function fn(e) {
            console.log(e.type);

        }
        // 2. 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
        var a = document.querySelector('a');
        a.addEventListener('click', function(e) {
                e.preventDefault(); //  dom 标准写法
            })
            // 3. 传统的注册方式
        a.onclick = function(e) {
            // 普通浏览器 e.preventDefault();  方法
            // e.preventDefault();
            // 低版本浏览器 ie678  returnValue  属性
            // e.returnValue;
            // 我们可以利用return false 也能阻止默认行为 没有兼容性问题 特点： return 后面的代码不执行了， 而且只限于传统的注册方式
            return false;
            alert(11);
        }
    </script>
</body>
```

### 7.4、阻止事件冒泡

**标准写法**

```js
e.stopPropagation();
```

**非标准写法：IE6-8利用对象事件cancelBubble属性**

```js
e.cancelBubble = true;
```

### 7.5、阻止事件冒泡兼容性写法

```js
if(e && e.stopPropagation){
      e.stopPropagation();
  }else{
      window.event.cancelBubble = true;
  }
```

### 7.6、事件委托

- 事件委托也称为事件代理，在 jQuery 里面称为事件委派
- 事件委托的原理
  - **不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点**

```js
<body>
    <ul>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
        <li>知否知否，点我应有弹框在手！</li>
    </ul>
    <script>
        // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // alert('知否知否，点我应有弹框在手！');
            // e.target 这个可以得到我们点击的对象
            e.target.style.backgroundColor = 'pink';
            // 点了谁，就让谁的style里面的backgroundColor颜色变为pink
        })
    </script>
</body>
```

### 7.7、常见的鼠标事件

| 鼠标事件    | 触发条件         |
| ----------- | ---------------- |
| onclick     | 鼠标点击左键触发 |
| onmouseover | 鼠标经过触发     |
| onmouseout  | 鼠标离开触发     |
| onfocus     | 获得鼠标焦点触发 |
| onblur      | 失去鼠标焦点触发 |
| onmousemove | 鼠标移动触发     |
| onmouseup   | 鼠标弹起触发     |
| onmousedown | 鼠标按下触发     |

#### 7.7.1、禁止鼠标右键与鼠标选中

- `contextmenu`主要控制应该何时显示上下文菜单，主要用于程序员取消默认的上下文菜单
- `selectstart` 禁止鼠标选中

#### 7.7.2、鼠标事件对象

| 鼠标事件对象    | 说明                                      |
| --------------- | ----------------------------------------- |
| e.clientX       | 返回鼠标相对于浏览器窗口**可视区**的X坐标 |
| e.clientY       | 返回鼠标相对于浏览器窗口**可视区**的Y坐标 |
| e.pageX（重点） | 返回鼠标相对于文档页面的X坐标 IE9+ 支持   |
| e.pageY（重点） | 返回鼠标相对于文档页面的Y坐标 IE9+ 支持   |
| e.screenX       | 返回鼠标相对于电脑屏幕的X坐标             |
| e.screenY       | 返回鼠标相对于电脑屏幕的Y坐标             |

### 7.8、常见的键盘事件对象

| 键盘事件   | 触发条件                                                     |
| ---------- | ------------------------------------------------------------ |
| onkeyup    | 某个键盘按键被松开时触发                                     |
| onkeydown  | 某个键盘按键被按下时触发                                     |
| onkeypress | 某个键盘按键被按下时触发，但是它不识别功能键，比如 ctrl shift 箭头等 |

- **如果使用addEventListener 不需要加 on**
- `onkeypress` 和前面2个的区别是，它不识别功能键，比如左右箭头，shift 等
- 三个事件的执行顺序是： keydown – keypress — keyup

#### 7.8.1、键盘对象属性

| 键盘事件对象 **属性** | 说明                    |
| --------------------- | ----------------------- |
| keyCode               | 返回该**键**值的ASCII值 |

- `onkeydown`和 `onkeyup` 不区分字母大小写，`onkeypress` 区分字母大小写。
- 在我们实际开发中，我们更多的使用keydown和keyup， 它能识别所有的键（包括功能键）
- `Keypress` 不识别功能键，但是`keyCode`属性能区分大小写，返回不同的ASCII值

# 四、BOM

## 1、概述

| DOM                                | BOM                                              |
| ---------------------------------- | ------------------------------------------------ |
| 文档对象模型                       | 浏览器对象模型                                   |
| DOM 就是把 文档 当作一个对象来看待 | 把 浏览器当作一个对象来看待                      |
| DOM 的顶级对象是 document          | BOM 的顶级对象是 window                          |
| DOM 主要学习的是操作页面元素       | BOM 学习的是浏览器窗口交互的一些对象             |
| DOM 是 W3C 标准规范                | BOM 是浏览器厂商在各自浏览器上定义的，兼容性较差 |

![img](https://img-blog.csdnimg.cn/5c83bf307ec9486687a5f52312943ecb.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

+ ==window 对象是浏览器的顶级对象，它具有双重角色==

+ 它是 JS 访问浏览器窗口的一个接口
+ 它是一个全局对象。定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法

+ 在调用的时候可以省略 window，前面学习的对话框都属于 window 对象方法，如 alert()、prompt()等。
  

## 2、Windows对象的常见事件

### 2.1、窗口加载事件

**①onload**

`window.onload`是窗口（页面）加载事件，当文档内容完全加载完成会触发该事件（包括图像，脚本文件，CSS文件等），就调用的处理函数。

==注意==

- 有了`window.onload`就可以把JS代码写到页面元素的上方
- 因为`onload`是等页面内容全部加载完毕，再去执行处理函数
- `window.onload` 传统注册事件方式，只能写一次
- 如果有多个，会以最后一个`window.onload`为准
- **如果使用addEventListener 则没有限制**

```js
window.onload = function(){
    
};

// 或者
window.addEventListener("load",function(){});
```

**②DOMCountLoaded**

```js
document.addEventListener('DOMContentLoaded',function(){})
```

- DOMCountentLoaded事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等等
- 如果页面的图片很多的话, 从用户访问到onload触发可能需要较长的时间
- 交互效果就不能实现，必然影响用户的体验，此时用 `DOMContentLoaded`事件比较合适。

**③两者区别**

- `load`等页面内容全部加载完毕，包括页面dom元素，图片，flash，css等
- `DOMContentLoaded` 是DOM加载完毕，不包含图片 flash css 等就可以执行，加载速度比load更快一些

### 2.2、调整窗口大小事件

`window.onresize` 是调整窗口大小加载事件，当触发时就调用的处理函数

```js
window.onresize = function() {}

// 或者
window.addEventListener('resize',function(){});
```

- 只要窗口大小发生像素变化，就会触发这个事件
- 我们经常利用这个事件完成响应式布局。`window.innerWidth` 当前屏幕的宽度

## 3、定时器

### 3.1、setTimeout()定时器

`setTimeout()`方法用于设置一个定时器，该定时器在定时器到期后执行调用函数。（只执行一次）

```js
window.setTimeout(调用函数,[延迟的毫秒数]);
```

**停止定时器**

- `clearTimeout()`方法取消了先前通过调用 `setTimeout()`建立的定时器

```js
window.clearTimeout(timeoutID)
```

### 3.2、setInterval()定时器

- `setInterval()`方法重复调用一个函数，每隔这个时间，就去调用一次回调函数。（执行n次）

```js
window.setInterval(回调函数,[间隔的毫秒数]);
```

- 第一次执行也是间隔毫秒数之后执行，之后每隔毫秒数就执行一次

**停止定时器**

- `clearInterval ( )` 方法取消了先前通过调用 `setInterval()` 建立的定时器

```js
window.clearInterval(timeoutID)
```

### 3.3、this指向

+ this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁
  现阶段，我们先了解一下几个this指向

+ 全局作用域或者普通函数中this指向全局对象window(注意定时器里面的this指向window)
+ 方法调用中谁调用this指向谁
+ 构造函数中this指向构造函数实例

```js
<body>
    <button>点击</button>
    <script>
        // this 指向问题 一般情况下this的最终指向的是那个调用它的对象

        // 1. 全局作用域或者普通函数中this指向全局对象window（ 注意定时器里面的this指向window）
        console.log(this);

        function fn() {
            console.log(this);

        }
        window.fn();
        window.setTimeout(function() {
            console.log(this);

        }, 1000);
        // 2. 方法调用中谁调用this指向谁
        var o = {
            sayHi: function() {
                console.log(this); // this指向的是 o 这个对象

            }
        }
        o.sayHi();
        var btn = document.querySelector('button');
        // btn.onclick = function() {
        //     console.log(this); // this指向的是btn这个按钮对象

        // }
        btn.addEventListener('click', function() {
                console.log(this); // this指向的是btn这个按钮对象

            })
            // 3. 构造函数中this指向构造函数的实例
        function Fun() {
            console.log(this); // this 指向的是fun 实例对象

        }
        var fun = new Fun();
    </script>
</body>

```

## 4、js执行机制

### 4.1、同步与异步

- 同步
  - 前一个任务结束后再执行后一个任务
- 异步
  - 在做这件事的同时，你还可以去处理其他事情

**同步任务**

同步任务都在主线程上执行，形成一个 执行栈

**异步任务**

- JS中的异步是通过回调函数实现的
- 异步任务有以下三种类型
  - 普通事件，如`click`,`resize`等
  - 资源加载，如`load`,`error`等
  - 定时器，包括`setInterval`,`setTimeout`等
- 异步任务相关回调函数添加到任务队列中

**执行过程**

1. 先执行执行栈中的同步任务
2. 异步任务(回调函数)放入任务队列中
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行

**事件循环**

<img src="https://img-blog.csdnimg.cn/eaabe7880146428fb68e6e64f23db40c.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center" alt="img" style="zoom:150%;" />

## 5、location对象

### 5.1、url

==统一资源定位符（uniform resouce locator）==是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的 URL，它包含的信息指出文件的位置以及浏览器应该怎么处理它。

**一般语法**

```js
protocol://host[:port]/path/[?query]#fragment
//例子
http://www.itcast.cn/index.html?name=andy&age=18#link
```

| 组成     | 说明                                     |
| -------- | ---------------------------------------- |
| protocol | 通信协议 常用的http,ftp,maito等          |
| host     | 主机(域名) www.itheima.com               |
| port     | 端口号，可选                             |
| path     | 路径 由零或多个`'/'`符号隔开的字符串     |
| query    | 参数 以键值对的形式，通过`&`符号分隔开来 |
| fragment | 片段 `#`后面内容 常见于链接 锚点         |

### 5.2、location对象属性

| location对象属性    | 返回值                            |
| ------------------- | --------------------------------- |
| ==location.href==   | 获取或者设置整个URL               |
| location.host       | 返回主机（域名）www.baidu.com     |
| location.port       | 返回端口号，如果未写返回空字符串  |
| location.pathname   | 返回路径                          |
| ==location.search== | 返回参数                          |
| location.hash       | 返回片段 #后面内容常见于链接 锚点 |

### 5.3、location对象方法

| location对象方法   | 返回值                                                       |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 跟href一样，可以跳转页面（也称为重定向页面）                 |
| location.replace() | 替换当前页面，因为不记录历史，所以不能后退页面               |
| location.reload()  | 重新加载页面，相当于刷新按钮或者 f5 ，如果参数为true 强制刷新 ctrl+f5 |

### 5.4、获取URL案例

**登录页面**

```js
<body>
    <form action="index.html">
        用户名： <input type="text" name="uname">
        <input type="submit" value="登录">
    </form>
</body>
```

**主页**

```js
<body>
    <div></div>
    <script>
        console.log(location.search); // ?uname=andy
        // 1.先去掉？  substr('起始的位置'，截取几个字符);
        var params = location.search.substr(1); // uname=andy
        console.log(params);
        // 2. 利用=把字符串分割为数组 split('=');
        var arr = params.split('=');
        console.log(arr); // ["uname", "ANDY"]
        var div = document.querySelector('div');
        // 3.把数据写入div中
        div.innerHTML = arr[1] + '欢迎您';
    </script>
</body>
```

## 6、navigator对象

+ navigator 对象包含有关浏览器的信息，它有很多属性
+ 我们常用的是userAgent,该属性可以返回由客户机发送服务器的user-agent头部的值

下面前端代码可以判断用户是用哪个终端打开页面的，如果是用 PC 打开的，我们就跳转到 PC 端的页面，如果是用手机打开的，就跳转到手机端页面

```js
if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    window.location.href = "";     //手机
 } else {
    window.location.href = "";     //电脑
 }
```

## 7、history对象

- window 对象给我们提供了一个 history 对象，与浏览器历史记录进行交互
- 该对象包含用户（在浏览器窗口中）访问过的 URL。

| history对象方法 | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| back()          | 可以后退功能                                                 |
| forward()       | 前进功能                                                     |
| go(参数)        | 前进后退功能，参数如果是 1 前进1个页面 如果是 -1 后退1个页面 |

# 五、pc端网页特效

## 1、元素偏移量offest

### 1.1 offset 概述

`offset` 翻译过来就是偏移量，我们使用 `offset` 系列相关属性可以==动态的==得到该元素的位置（偏移）、大小等。

- 获得元素距离==带有定位父元素==的位置(如果没有父亲或者父亲没有定位，则以body为准)
- 获得元素自身的大小（宽度高度）
- 注意：返回的数值都==不带单位==

| offest系列属性       | 作用                                                       |
| -------------------- | ---------------------------------------------------------- |
| element.offestParent | 返回该元素带有定位的父级元素，如果父级都没有定位则返回body |
| element.offestTop    | 返回元素相对带有定位父元素上方的偏移                       |
| element.offestLeft   | 返回元素相对带有定位父元素左边框的偏移                     |
| element.offestWidth  | 返回自身包括padding,边框,内容区的宽度，返回值不带单位      |
| element.offestHeight | 返回自身包括padding,边框,内容区的高度，返回值不带单位      |

### 1.2 offset 与 style 区别

#### 1.2.1 offset

- `offset` 可以得到任意样式表中的样式值
- `offset` 系列获得的数值是没有单位的
- `offsetWidth` 包含 `padding+border+width`
- `offsetWidth` 等属性是只读属性，只能获取不能赋值
- **所以，我们想要获取元素大小位置，用 `offset`更合适**

#### 1.2.2 style

- `style` 只能得到行内样式表中的样式值
- `style.width` 获得的是带有单位的字符串
- `style.width` 获得不包含 `padding` 和 `border` 的值
- `style.width` 是可读写属性，可以获取也可以赋值
- **所以，我们想要给元素更改值，则需要用 `style` 改变**

### 1.3、案例

**获取鼠标在盒子里的坐标**

```js
<body>
    <!-- 1.我们在盒子内点击，想要得到鼠标距离盒子左右的距离。
    2.首先得到鼠标在页面中的坐标（e.pageX, e.pageY）
    3.其次得到盒子在页面中的距离( box.offsetLeft, box.offsetTop)
    4.用鼠标距离页面的坐标减去盒子在页面中的距离，得到鼠标在盒子内的坐标
    5.如果想要移动一下鼠标，就要获取最新的坐标，使用鼠标移动事件mousemove-->
    <div class="box"></div>
    <script>
        var box=document.querySelector(".box");
        box.addEventListener('mousemove',function(e){
            var x = e.pageX - this.offsetLeft;
            var y = e.pageY - this.offsetTop;
            this.innerHTML = 'x坐标是' + x + 'y坐标是' + y;
        })
    </script>
</body>
```

## 2、元素可视区client

### 2.1 定义

`client` 翻译过来就是客户端，我们使用 `client` 系列的相关属性来获取元素可视区的相关信息。通过`client` 系列的相关属性可以动态的得到该元素的边框大小、元素大小等。

| client系列属性         | 作用                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `element.clientTop`    | 返回元素==上边框==的大小                                     |
| `element.clientLeft`   | 返回元素==左边框==的大小                                     |
| `element.clientWidth`  | 返回自身包括 `padding`、内容区的宽度，不含边框，返回数值不带单位 |
| `element.clientHeight` | 返回自身包括 `padding`、内容区的高度，不含边框，返回数值不带单位 |

### 2.2、立即执行函数

立即执行函数是指函数定义好后，不需要调用直接执行。即一引入 JS 文件，则该函数自动执行。

语法：`(function() {})()` 或者 `(function(){}())`

主要作用：

- 创建一个独立的作用域
- 避免了命名冲突问题

可以传参数：

```
(function (a) {console.log(a);})(10); // 10
```

### 2.3、pageShow 事件

下面三种情况都会刷新页面都会触发load 事件。

1. a标签的超链接
2. F5或者刷新按钮（强制刷新）
3. 前进后退按钮

但是火狐中，有个特点，有个“往返缓存”，这个缓存中不仅保存着页面数据，还保存了 DOM 和 JavaScript 的状态；实际上是将整个页面都保存在了内存里。

所以此时后退按钮不能刷新页面。

此时可以使用 `pageshow` 事件来触发。，这个事件在页面显示时触发，无论页面是否来自缓存。在重新加载页 面中，`pageshow` 会在 `load` 事件触发后触发；根据事件对象中的 `persisted` 来判断是否是缓存中的页面触发的`pageshow` 事件，注意这个事件给 `window` 添加。

## 3、元素滚动 scroll 系列

`scroll` 翻译过来就是滚动的，我们使用 `scroll` 系列的相关属性可以动态的得到该元素的大小、滚动距离等。

| scroll系列属性         | 作用                                         |
| ---------------------- | -------------------------------------------- |
| `element.scrollTop`    | 返回被卷上去的上侧距离，返回数值不带单位     |
| `element.scrollLeft`   | 返回被卷上去的左侧距离，返回数值不带单位     |
| `element.scrollWidth`  | 返回自身实际宽度，不含边框，返回数值不带单位 |
| `element.scrollHeight` | 返回自身实际高度，不含边框，返回数值不带单位 |

### 3.1、 页面被卷去的头部

如果浏览器的高（或宽）度不足以显示整个页面时，会自动出现滚动条。当滚动条向下滚动时，页面上面被隐藏 掉的高度，我们就称为页面被卷去的头部。滚动条在滚动时会触发 `onscroll` 事件。

**获取页面被卷去的头部**：

- **页面** 被卷去的头部：可以通过 `window.pageYOffset` 获得，如果是被卷去的左侧 `window.pageXOffset`
- 注意，元素被卷去的头部是 `element.scrollTop`，左侧 `element.scrollLeft`

## 4、总结

| 三大系列大小对比      | 作用                                                         |
| --------------------- | ------------------------------------------------------------ |
| `element.offsetWidth` | 返回自身包括 `padding`、边框、内容区的宽度，返回数值不带单位 |
| `element.clientWidth` | 返回自身包括 `padding`、内容区的宽度，不含边框，返回数值不带单位 |
| `element.scrollWidth` | 返回自身实际的宽度，不含边框，返回数值不带单位               |

### 4.1、主要用法

1. `offset` 系列经常用于获得元素位置 `offsetLeft`、`offsetTop`
2. `client` 经常用于获取元素大小 `clientWidth` 、`clientHeight`
3. `scroll` 经常用于获取滚动距离 `scrollTop`、`scrollLeft`
4. 注意页面滚动的距离通过 `window.pageXOffset` 获得

### 4.2、mouseenter和mouseover区别

- 当鼠标移动到元素上时就会触发 `mouseenter` 事件
- 类似 `mouseover`，它们两者之间的差别是
- `mouseover` 鼠标经过自身盒子会触发，经过子盒子还会触发。`mouseenter` 只会经过自身盒子触发
- 之所以这样，就是因为 `mouseenter` 不会冒泡
- 跟 `mouseenter` 搭配鼠标离开 `mouseleave` 同样不会冒泡

### 4.3、animate封装

```js
 //封装动画函数
 function animate(obj, target, callback) {
    clearInterval(obj.timer);
    obj.timer = setInterval(function () {
        var step = (target - obj.offsetLeft) / 10;
        // 当往回走时，调用floor
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        if (obj.offsetLeft == target) {
            clearInterval(obj.timer);
            //回调函数写在定时器结束里面
            if(callback){
                callback();
            }
            return;
        }
        //匀速动画就是+常量值，缓动动画就是+（目标值 - 现在的位置）/10 作为每次移动的步长
        obj.style.left = obj.offsetLeft + step + 'px';
    }, 30)
}
```

# 六、移动端网页特效

## 1、触屏事件

`touch` 对象代表一个触摸点。触摸点可能是一根手指，也可能是一根触摸笔。触屏事件可响应用户手指（或触控 笔）对屏幕或者触控板操作。

常见的触屏事件如下：

| 触屏         | touch 事件说明                  |
| ------------ | ------------------------------- |
| `touchstart` | 手指触摸到一个 DOM 元素时触发   |
| `touchmove`  | 手指在一个 DOM 元素上滑动时触发 |
| `touchend`   | 手指从一个 DOM 元素上移开时触发 |

## 2、触摸事件对象

TouchEvent 是一类描述手指在触摸平面（触摸屏、触摸板等）的状态变化的事件。这类事件用于描述一个或多个触点，使开发者可以检测触点的移动，触点的增加和减少，等等

`touchstart`、`touchmove`、`touchend` 三个事件都会各自有事件对象。

触摸事件对象重点我们看三个常见对象列表：

| 触摸列表         | 说明                                             |
| ---------------- | ------------------------------------------------ |
| `touches`        | 正在触摸屏幕的所有手指的一个列表                 |
| `targetTouches`  | 正在触摸当前 DOM 元素上的手指的一个列表          |
| `changedTouches` | 手指状态发生了改变的列表，从无到有，从有到无变化 |

==因为平时我们都是给元素注册触摸事件，所以重点记住 targetTocuhes==

## 3、移动端拖动元素

1. `touchstart、touchmove、touchend` 可以实现拖动元素
2. 但是拖动元素需要当前手指的坐标值我们可以使用 `targetTouches[0]` 里面的 `pageX` 和 `pageY`
3. 移动端拖动的原理：手指移动中，计算出手指移动的距离。然后用盒子原来的位置+ 手指移动的距离
4. 手指移动的距离：手指滑动中的位置减去手指刚开始触摸的位置

拖动元素三步曲：

- （1）触摸元素 `touchstart` ：获取手指初始坐标，同时获得盒子原来的位置
- （2）移动手指 `touchmove` ：计算手指的滑动距离，并且移动盒子
- （3）离开手指 `touchend` :

注意：手指移动也会触发滚动屏幕所以这里要阻止默认的屏幕滚动 `e.preventDefault();`

## 4、classList

`classList` 属性是 HTML5 新增的一个属性，返回元素的类名。但是 ie10 以上版本支持。 该属性用于在元素中添加，移除及切换 CSS 类。有以下方法

添加类：

```js
focus.classList.add('current');Copy to clipboardErrorCopied
```

移除类：

```js
focus.classList.remove('current');Copy to clipboardErrorCopied
```

切换类：

```js
focus.classList.toggle('current');Copy to clipboardErrorCopied
```

注意以上方法里面，所有类名都不带点

## 5、click延时解决方案

移动端 `click` 事件会有 `300ms` 的延时，原因是移动端屏幕双击会缩放（double tap to zoom）页面。 解决方案：

### （1）禁用缩放

浏览器禁用默认的双击缩放行为并且去掉300ms 的点击延迟。

```js
<meta name="viewport" content="user-scalable=no">Copy to clipboardErrorCopied
```

### （2）利用touch事件自己封装这个事件解决 `300ms` 延迟。

原理就是：

1. 当我们手指触摸屏幕，记录当前触摸时间
2. 当我们手指离开屏幕，用离开的时间减去触摸的时间
3. 如果时间小于 `150ms`，并且没有滑动过屏幕，那么我们就定义为点击

代码实现：

```js
//封装tap，解决click 300ms 延时
function tap(obj, callback) {
  var isMove = false;
  var startTime = 0; // 记录触摸时候的时间变量
  obj.addEventListener('touchstart', function(e) {
    startTime = Date.now(); // 记录触摸时间
  });
  obj.addEventListener('touchmove', function(e) {
    isMove = true; // 看看是否有滑动，有滑动算拖拽，不算点击
  });
  obj.addEventListener('touchend', function(e) {
    // 如果手指触摸和离开时间小于150ms 算点击
    if (!isMove && (Date.now() - startTime) < 150) { 
      callback && callback(); // 执行回调函数
    }
    isMove = false; // 取反重置
    startTime = 0;
  });
}
//调用
tap(div, function() { // 执行代码});Copy to clipboardErrorCopied
```

### （3）使用插件 fastclick

使用 fastclick 插件解决300ms 延迟。官网：https://github.com/ftlabs/fastclick

1. 引入
2. 按照文档说明使用

例如，在原生 JS 中：

```js
if ('addEventListener' in document) {
  document.addEventListener('DOMContentLoaded', function() {
    FastClick.attach(document.body);
  }, false);
}
```

## 6、插件的使用

常用的插件

+ superslide : http://www.superslide2.com
+ iscroll:  https://github.com/cubiq/iscroll
+ Swiper:   https://swiper.com.cn/

流程：

1. 确认插件实现的功能
2. 去官网查看使用说明
3. 下载插件
4. 打开demo 示例文件，查看需要引入的文件，并且引入
5. 复制demo示例文件中的HTML，样式css以及js代码

# 七、本地存储

## 1. 本地存储概述

### 1.1 背景

随着互联网的快速发展，基于网页的应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经 常性在本地存储大量的数据，HTML5 规范提出了相关解决方案。

### 1.2 本地存储特性

- 数据存储在用户浏览器中
- 设置、读取方便、甚至页面刷新不丢失数据
- 容量较大，`sessionStorage` 约5M、`localStorage` 约20M
- ==只能存储字符串，可以将对象 `JSON.stringify()` 编码后存储==
- 获取数据可以把字符串数据转换为对象格式，`JSON.parse()`

## 2. window.sessionStorage

### 2.1 特点

- 生命周期为 **关闭浏览器窗口**
- 在同一个窗口（页面）下数据可以共享
- 以键值对的形式存储使用

### 2.2 相关操作

1. 存储数据：

   ```js
   sessionStorage.setItem(key, value)Copy to clipboardErrorCopied
   ```

2. 获取数据：

   ```js
   sessionStorage.getItem(key)Copy to clipboardErrorCopied
   ```

3. 删除数据：

   ```js
   sessionStorage.removeItem(key)Copy to clipboardErrorCopied
   ```

4. 删除所有数据：

   ```js
   sessionStorage.clear()Copy to clipboardErrorCopied
   ```

## 3. window.localStorage

### 3.1 特点

- 生命周期 **永久生效**，除非手动删除否则关闭页面也会存在
- 可以多窗口（页面）共享（同一浏览器可以共享）
- 以键值对的形式存储使用

### 3.2 相关操作

1. 存储数据：

   ```js
   localStorage.setItem(key, value)Copy to clipboardErrorCopied
   ```

2. 获取数据：

   ```js
   localStorage.getItem(key)Copy to clipboardErrorCopied
   ```

3. 删除数据：

   ```js
   loaclStorage.removeItem(key)Copy to clipboardErrorCopied
   ```

4. 删除所有数据：

   ```js
   localStorage.clear()
   ```
