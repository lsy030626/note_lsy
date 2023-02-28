# 一、选择器

## 1、基础选择器

### 1.1、标签选择器

直接用 HTML 标签名作为选择器，按标签名称分类，**为页面某一类标签指定统一的 CSS 样式。**

==语法==

```HTML
标签名 {
    属性1： 属性值1;
    属性2： 属性值2;
    属性3： 属性值3;
}
```

优点 标签选择器可以把某一标签全部选择出来，快速为同类型标签设置统一样式。

缺点 不能设置差异化样式，只能选择全部当前标签。

### 1.2、类选择器

==语法==

使用 `class` 属性来调用 class 类，样式点定义，结构类调用，一个或多个，开发最常用。

类选择器用 `.` 号显示。

==注意==

1. 类选择器用 `.` 标识，紧跟类名。
2. 小写，使用 `-` 连接单词。
3. 不要用纯数字、中文。
4. 命名有意义。

### 1.3、id选择器

id 选择器可以为标有特定 id 的 HTML 元素指定特定的样式。

HTML 元素以 id 属性来设置 id 选择器，用 `#` 来定义。

```HTML
#id名 {
    属性1: 属性值1;
    ...
}
```

样式 `#` 定义，结构 id 调用，别人切勿使用。

==id 选择器与类选择器的区别==

1. 类选择器可以被多个元素调用。
2. id 选择器只能允许一个标签调用。
3. 类选择器使用的较多，id 选择器用于唯一特性的标签。

### 1.4、通配符选择器

==语法==

```HTML
* {
    属性1: 属性值1;
    ...
}
```

- 用 `*` 定义通配符选择器，选取页面中所有标签。
- 不需要调用，自动给所有标签。
- 特殊情况使用

```HTML
* {
    margin: 0;
    padding: 0;
}
```



### 1.5、总结

| 基础选择器   | 作用                 | 特点                             | 使用情况         | 用法                 |
| ------------ | -------------------- | -------------------------------- | ---------------- | -------------------- |
| 标签选择器   | 选中所有相同标签     | 不能差异化选择                   | 较多             | `p{color:red;}`      |
| 类选择器     | 选出一个或多个标签   | 可以根据需求选择                 | 较多             | `.nav {color: red;}` |
| id 选择器    | 一次只能选出一个标签 | 一个 id 属性在页面中只能出现一次 | 一般配合 js 使用 | `#nav {color: red;}` |
| 通配符选择器 | 选择所有标签元素     | 选择的太多，有部分不需要         | 特殊情况使用     | `* {color: red; }`   |

## 2、复合选择器

### 2.1、后代选择器

后代选择器又称为包含选择器，可以选择父元素里的子元素。写法是将外层标签写在前面，内层标签写在后面，中间空格分开。 **语法**

```CSS
元素1 元素2 { 样式声明; }
```

- 上述语法表示选择元素 1 里面所有的元素 2
- 可以连续嵌套，比如可以是孙子等
- 元素 1、2 可以是任何基础标签

### 2.2、子代选择器

子元素选择器（子选择器）只能选择作为元素作为元素的最近一级子元素。简单理解就是选亲儿子。

==**语法**==

```CSS
元素1 > 元素2 { 样式声明; }
```

- 元素之间用大于号 `>` 隔开
- 1 为父级。二为子级，最终选择的是元素 2
- 元素 2 必须是亲儿子。

### 2.3、并集选择器

并集选择器可以选择多组标签，同时为他们定义相同的样式。通常用于集体声明。

并集选择器是各选择器通过英文逗号 `,` 连接而成，任何形式的选择器都可以作为并集选择器的一部分。

==**语法**==

```css
元素1, 元素2 { 样式声明; }
```

### 2.4、伪类选择器

伪类选择器用于向某些选择器添加特殊的效果。 伪类选择器书写最大特点是用冒号 `:` 表示。 伪类选择器种类多，比如链接伪类选择器、结构选择器等。

#### 2.4.1、链接伪类

```css
a:link /*选择所有未被访问的链接*/
a:visited /*选择所有已被访问的链接*/
a:hover /*选择鼠标指针位于其上的链接*/
a:active /*选择活动链接（鼠标按下未弹起的链接）*/
```

**注意事项**

1. 确保样式生效，要按照 LVHA 的顺序声明：link,visited,hover, active。
2. a 链接在浏览器中有默认样式，所以实际开发都需要给链接单独指定样式。

#### 2.4.2、focus伪类选择器

`:focus` 伪类选择器用于获取焦点的表单元素。 焦点就是光标，一般情况 `<input>` 类表单元素才能获取，因此这个选择器也主要针对表单元素来说。

```css
input:focus {
  background-color: yellow;
}
```

### 2.5、总结

| 选择器         | 作用                   | 特征             | 使用情况 | 隔开符号及用法             |
| -------------- | ---------------------- | ---------------- | -------- | -------------------------- |
| 后代选择器     | 用来选择后代元素       | 可以是子孙后代   | 较多     | 符号是空格 `.nav a`        |
| 子代选择器     | 选择最近一级元素       | 只能选亲儿子     | 较少     | 符号是大于 `.nav>p`        |
| 并集选择器     | 选择某些相同样式的元素 | 可以用于集体声明 | 较多     | 符号是逗号，`.nav, a`      |
| 链接伪类选择器 | 选择不同状态的链接     | 跟链接相关       | 较多     | 重点记住`a{}`和`a:hover{}` |
| :focus 选择器  | 选择获得光标的表单     | 跟表单相关       | 较少     | 记住`input:focus`用法      |

## 3、css3新增选择器

### 3.1、属性选择器

属性选择器可以根据元素特定属性的来选择元素。这样就可以不用借助于类或者id选择器。

| 简介          | 选择                                  |
| ------------- | ------------------------------------- |
| `E[att]`      | 选择具有att属性的E元素                |
| `E[att:val`   | 选择具有att属性且属性值等于val的E元素 |
| `E[att^=val]` | 匹配具有att属性且值以val开头的E元素   |
| `E[att$=val]` | 匹配具有att属性且值以val结尾的E元素   |
| `E[att*=val]` | 匹配具有att属性且值中含有val的E元素   |

```
input[type=text] {
    color: green;
}
<input type="password">
<input type="text">
```

类选择器、属性选择器、伪类选择器的权重都为 10

### 3.2、 结构伪类选择器

结构伪类选择器主要根据文档结构来选择器元素，常用于根据父级选择器里面的子元素。

| 选择符              | 简介                        |
| ------------------- | --------------------------- |
| `E: first-child`    | 匹配父元素中的第一个子元素E |
| `E: last-child`     | 匹配父元素中最后一个E元素   |
| `E: nth-child(n)`   | 匹配父元素中的第n个子元素E  |
| `E: first-of-type`  | 指定类型E的第一个           |
| `E: last-of-type`   | 指定类型E的最后一个         |
| `E: nth-of-type(n)` | 指定类型E的第n个            |

```
ul li:first-child {
    background-color: pink;
}
ul li:last-child {
    background-color: pink;
}
ul li:nth-child(5) {
    background-color: skyblue;
}
```

重点：`E: nth-child(key)`

- `key` 可以是整数、关键字（`even/odd`）、公式（`n/2n/2n+1`）

| 公式 | 取值        |
| ---- | ----------- |
| 2n   | 偶数        |
| 2n-1 | 奇数        |
| 5n   | 5 10 15 ... |
| n+   | 5 6 7 8 ... |
| -n+5 | 前五个      |

关于 `nth-of-type` 与 `nth-of-child`

1. `div: nth-child` 会把所有的盒子都排列序号 执行的时候首先看 `:nth-child(1)` 之后回去看 前面 `div`
2. `div: nth-of-type` 会把指定元素的盒子排列序号 执行的时候首先看 div指定的元素 之后回去看 `:nth-of-type(1)` 第几个孩子

区别：

1. nth—child对父元素里面所有孩子排序选择（序号是固定的）先找到第n个孩子，然后看看是否和E匹配
2. nth—of—type对父元素里面指定子元素进行排序选择。先去匹配E ，然后再根据E找第n个孩子

### 3.3、 伪元素选择器

伪元素选择器可以帮助我们利用CSS创建新标签元素，而不需要HTML标签，从而简化HTML结构。

| 选择符     | 简介                     |
| ---------- | ------------------------ |
| `::before` | 在元素内部的前面插入内容 |
| `::after`  | 在元素内部的后面插入内容 |

注意：

- before 和 after 创建一个元素，但是属于行内元素
- 新创建的这个元素在文档树中是找不到的，所以我们称为伪元素
- 语法：`element：before{}`
- before 和 after 必须有 content 属性
- before 在父元素内容的前面创建元素， after 在父元素内容的后面插入元素
- 伪元素选择器和标签选择器一样，权重为 1

#### 2.4.1 案例一：伪元素字体图标

```
 div::after {
    position: absolute;
    top: 10px;
    right: 10px;
    font-family: 'icomoon';
    content: '\e91b';
    color: red;
    font-size: 18px;
}
```

#### 2.4.2 案例二：伪元素遮罩层

```
.tudou::before {
    content: '';
    display: none;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .3) url(images/arr.png) no-repeat center;
}
```



#### 2.4.3 案例三：伪元素清除浮动

```
.clearfix::after {
    content: '';
    display: block; 
    height: 0;
    clear: both;
    visibility: hidden;
}
```

双伪元素清除浮动

```
.clearfix::before,
.clearfix::after {
    content: '';
    display: block;
}
.clearfix::after {
    clear: both;
}
```

# 二、浮动

## 1、清除浮动

### 1.1额外标签法

也成为隔墙法，是 W3C 推荐的方法。

额外标签法是在最后一个浮动元素末尾添加一个 **空块级元素**，给其赋以属性 `clear:both;`。

```html
<style>
  clear: both;
</style>
<div class="clear"></div>
```

- 优点：通俗易懂，书写方便
- 缺点：添加许多无意义的标签，结构化差

总结

1. 清除浮动的本质

   清除浮动的本质是清除浮动元素脱离标准流造成的影响

2. 清除浮动的策略

   **闭合浮动**，只让浮动在父盒子内部影响，不影响父盒子外面的其他盒子。

3. 使用场景

   实际开发中可能会遇到，但是不常用。

### 1.2父级添加 overflow

可以给父级添加 `overflow` 属性，将其属性设置为 `hidden`、`auto`或`scroll`。

注意是给父元素添加代码：

- 优点：代码简洁
- 缺点：无法显示溢出部分

### 1.3、:after 伪元素法

实际上也是额外标签法的一种。

```css
.clearfix {
  content: "";
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
.clearfix {
  /*IE6、7专有*/
  *zoom: 1;
}
```

### 1.4、双伪元素法

语法

```css
.clearfix::before,
.clearfix::after {
  content: "";
  display: table;
}
.clearfix::after {
  clear: both;
}
.clearfix {
  *zoom: 1;
}
```

- 优点：代码更简洁
- 缺点：照顾低版本浏览器
- 代表网站：小米、腾讯

### 1.5、清除浮动总结

为什么需要清除浮动？

1. 父级没高度
2. 子盒子浮动了
3. 影响下面布局了，应该清除浮动。

# 三、定位

## 1、静态定位 staic

静态定位是元素的默认定位方式，无定位的意思。语法：

```css
选择器 {
  position: static;
}
```

静态定位按照标准流特性摆放位置，它没有边偏移静态定位在布局时很少用到。

## 2、相对定位 relative

相对定位是元素在移动位置的时候，是相对于它原来的位置来说的（自恋型）。

语法：

```css
选择器 {
  position: relative;
}
```

**相对定位的特点：（务必记住）**

1. 它是相对于自己原来的位置来移动的（移动位置的时候参照点是自己原来的位置）。
2. 原来在标准流的位置继续占有，后面的盒子仍然以标准流的方式对待它。（不脱标，继续保留原来位置因此，相对定位并没有脱标。它最典型的应用是给绝对定位当爹的。

## 3、绝对定位 absolute

绝对定位是元素在移动位置的时候，是相对于它祖先元素来说的（拼爹型）。

语法：

```css
选择器 {
  position: absolute;
}
```

绝对定位的特点： （务必记住）

1. 如果 **没有祖先元素** 或者 **祖先元素没有定位**，则以 **浏览器** 为准定位（ Document 文档）。
2. 如果祖先元素有定位（相对、绝对、固定定位） ，则以最近一级的有定位祖先元素为参考点移动位置。
3. 绝对定位不再占有原先的位置。（脱标）

## 4. 子绝父相的由来

弄清楚这个口诀，就明白了绝对定位和相对定位的使用场景。

这个“子绝父相”太重要了，是我们学习定位的口诀，是定位中最常用的一种方式这句话的意思是：子级是绝对定位的话，父级要用相对定位

- 子级绝对定位，不会占有位置，可以放到父盒子里面的任何一个地方，不会影响其他的兄弟盒子。

- 父盒子需要加定位限制子盒子在父盒子内显示。

- 父盒子布局时，需要占有位置，因此父亲只能是相对定位。

  这就是子绝父相的由来，所以相对定位经常用来作为绝对定位的父级。 总结：因为父级需要占有位置，因此是相对定位，子盒子不需要占有位置，则是绝对定位

## 5、 固定定位 fixed （重要）

固定定位是元素固定于浏览器可视区的位置。主要使用场景：可以在浏览器页面滚动时元素的位置不会改变。

语法：

```css
选择器 {
  position: fixed;
}
```

固定定位的特点： （务必记住）

1. 以浏览器的可视窗口为参照点移动元素。
   - 跟父元素没有任何关系
   - 不随滚动条滚动
2. 固定定位不 占有原先的位置。 固定定位也是脱标的，其实固定定位也可以看做是一种特殊的绝对定位。

固定定位小技巧：固定在版心右侧位置。

1. 让固定定位的盒子 left： 50%，走到浏览器可视区（也可以看做版心）的一半位置。
2. 让固定定位的盒子 margin—left）板心宽度的一半距离。多走版心宽度的一半位置就可以让固定定位的盒子贴着版心右侧对弃了

## 6、粘性定位 sticky

粘性定位可以被认为是相对定位和固定定位的混合。Sticky 粘性的 语法：

```css
选择器 {
  position: sticky;
  top: 10px;
}
```

粘性定位的特点：

1. 以浏览器的可视窗口为参照点移动元素（固定定位特点）
2. 粘性定位占有原先的位置（相对定位特点）
3. 必须添加 top， left， right， bottom 其中一个才有效跟页面滚动搭配使用。兼容性较差， IE 不支持。

## 7、定位的扩展

### 7.1、绝对定位的盒子居中

加了绝对定位的盒子不能通过 margin：0auto 水平居中，但是可以通过以下计算方法实现水平和垂直居中。

- left： 50% ：让盒子的左侧移动到父级元素的水平中心位置。
- margin—left：—100px； ：让盒子向左移动自身宽度的一半。

# 四、元素的显示与隐藏

### 1、display 属性

- `display` 属性用于设置一个元素应如何显示。
- `display： none;` 隐藏对象
- `display ： block;` 除了转换为块级元素之外，同时还有显示元素的意思 display 隐藏元素后，不再占有原来的位置。

后面应用及其广泛，搭配 JS 可以做很多的网页特效。

### 2、 visibility 可见性

- visibility 属性用于指定一个元素应可见还是隐藏。- - visibility : visible;元素可视
- visibility : hidden;元素隐藏
- visibility 隐藏元素后，继续占有原来的位置

如果隐藏元素想要原来位置，就用 `visibility ： hidden` 如果隐藏元素不想要原来位置，就用 `display ： none` （用处更多重点）

### 3、overflow 溢出

overflow 属性指定了如果内容溢出一个元素的框（超过其指定高度及宽度）时，会发生什么。

| 属性值  | 描述                                           |
| ------- | ---------------------------------------------- |
| visible | 不剪切内容也不添加滚动条                       |
| hidden  | 不显示超过对象尺寸的内容                       |
| scroll  | 超出的部分隐藏掉不管超出内容否，总是显示滚动条 |
| auto    | 超出自动显示滚动条，不超出不显示滚动条         |

一般情况下，我们都不想让溢出的内容显示出来，因为溢出的部分会影响布局。但是如果有定位的盒子，请慎用`overflowhidden` 因为它会隐藏多余的部分。

### 4、应用（处理文字溢出）

```css
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
```

效果图

![](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230204163816204.png)

# 五、css高级

## 1、精灵图

### 1. 1、精灵图

一个网页中往往会应用很多小的背景图像作为修饰，当网页中的图像过多时，服务器就会频繁地接收和发送请求图片，造成服务器请求压力过大，这将大大降低页面的加载速度。

因此，为了有效地减少服务器接收和发送请求的次数，提高页面的加载速度，出现了 CSS 精灵技术（也称 CSS Sprites. CSS 雪碧）。

### 1.2、精灵图的使用

使用精灵图核心总结：

1. 精灵图主要针对于小的背景图片使用。
2. 主要借助于背景位置来实现———background—position.
3. 一般情况下精灵图都是负值。（千万注意网页中的坐标： x 轴右边走是正值，左边走是负值， y 轴同理。）

## 2、css三角图形

```css
.box1 {
  width: 0;
  height: 0;
  border: 10px solid transparent;
  border-left-color: black;
  /* 照顾兼容性 */
  line-height: 0;
  font-size: 0;
}
```

## 3、取消表单轮廓和文本域缩放

```css
input {
  outline: none;
}
textarea {
  outline: none;
  resize: none;
}
```

## 4、vertical-align

`vertical-align` 指定行内/行内块元素的元素的垂直对齐方式。

### 4.1、图片、表单和文字对齐 vertical-align

```css
img {
  vertical-align: middle;
}
li {
  disaplay: inline-block;
  vertical-align: middle;
}Copy to clipboardErrorCopied
```

### 4.2、解决图片底部默认空白缝隙问题

bug ：图片底侧会有一个空白缝隙，原因是行内块元素会和文字的基线对齐。主要解决方法有两种：

1. 给图片添加 `vertical—align: middle topl bottom;` 等。（提倡使用的）
2. 把图片转换为块级元素 `display: block；`

## 5、溢出文字省略号显示

### 5.1、单行文本

```css
/*1·先强制一行内显示文本*/
white-space: nowrap;
默认normal 自动换行）
/*2·超出的部分隐藏*/
overflow: hidden;
/*3.文字用省略号替代超出的部分*/
text-overflow: ellipsis;
```

### 5.2、多行文本

```css
overflow:hidden
text-overflow:ellipsis
/*弹性收缩盒子模型显示*/
display:-webkit-box
/*限制在一个块元素显示文本的行数*/
-weikit-line-clamp:2
/*设置或检索伸缩盒对象的子元素的排列方式*/
-webkit-box-orient:vertical;
```

## 6、margin负值巧妙利用

1. 解决并排盒子之间的边框宽度加倍问题。 原理：让每个盒子压住前面的盒子，边框叠加。
2. 鼠标移动边框颜色变化效果。

```css
/*如果盒子没有定位，则鼠标经过添加相对定位即可*/
ul li:hover {
  position: relative;
  border: 1px solid orange;
}
/*若li都有定位，则使用 z-index 提高层级*/
ul li {
  z-index: 1;
  border: 1px solid orange;
}
```

## 7、行内块元素巧妙运用

行内块元素布局当前页码和 `pre`，`next`盒子，使用 `text-align: center` 居中。

# 六、html新特性

## 1、HTML5新增语义化标签

- `<header>`：头部标签
- `<nav>`：导航标签
- `<article>`：内容标签
- `<section>`：定义文档某个区域
- `<asider>`：侧边栏标签
- `<footer>`：尾部标签

注意：

+ 主要针对搜索引擎的
+ 这些新标签可以使用多次
+ 在IE9中，需要把这些元素改成块级元素
+ 移动端更加喜欢这些标签‘

## 2、HTML5新增多媒体标签

### 2.1、视频 <vedio>

所有浏览器支持 mp4 格式。

- `autoplay="autoplay"`
- `controls="controls"` 显示控件
- `width` 设置宽度
- `height` 设置高度
- `loop=loop` 设置循环播放
- `preload="auto/none"` 是否预加载
- `src=url` 视频地址
- `poster=url` 封面图片
- `muted=muted` 静音播放

#### 2.2、 音频 <audio>

所有浏览器支持 mp3 格式。

- `controls`：显示控件
- `autoplay`：（谷歌禁用）
- `loop=loop` 设置循环播放

## 3、input新增

### 3.1、类型

| 属性值          | 说明                    |
| --------------- | ----------------------- |
| `type="email"`  | 限制用户输入为Email类型 |
| `type="url"`    | 限制用户输入为URL类型   |
| `type="date"`   | 限制用户输入为日期类型  |
| `type="time"`   | 限制用户输入为时间类型  |
| `type="month"`  | 限制用户输入为月类型    |
| `type="week"`   | 限制用户输入为周类型    |
| `type="number"` | 限制用户输入为数字类型  |
| `type="tel"`    | 手机号码                |
| `type="search"` | 搜索框                  |
| `type="color"`  | 生成一个颜色表单        |

### 3.2、表单属性

| 属性         | 值        | 说明                                                         |
| ------------ | --------- | ------------------------------------------------------------ |
| required     | required  | 表单拥有该属性表示其内容不能为空，必填                       |
| placeholder  | 提示文本  | 表单的提示信息                                               |
| autofocus    | autofocus | 自动聚焦属性，页面加载完成自动聚焦到指定表单                 |
| autocomplete | off/on    | 当用户在字段开始键入时，浏览器基于之前键入过的值，应该显示出在字段中填写的选项默认已经打开,如autocomplete="on",关闭autocomplete ="off" 需要放在表单内，同时加上name属性，同时成功提交 |
| multiple     | multiple  | 可以多选文件                                                 |

可以通过以下设置方式修改placeholder里面的字体颜色：

```css
input::placeholder {
    color: pink;
}
```

# 七、css新特性

## 1、盒子模型

CSS3中可以通过 box-sizing 来指定盒模型，有2个值：即可指定为 content-box，border-box ，这样我们计算盒子大小的方式就发生了改变。

可以分成两种情况：

1. `box-sizing：content-box` 盒子大小为 width + padding + border （以前默认的）
2. `box-sizing: border-box` 盒子大小为 width 如果盒子模型我们改为了 box-sizing： border-box ，那padding 和 border就不会撑大盒子了（前提 padding 和 border 不会超过 width 宽度）

## 2、颜色渐变

CSS 渐变是 CSS3 图像模块中添加的新类型的图像。CSS 渐变允许您在 **两个或多个指定颜色之间显示平滑过渡**。 浏览器支持两种类型的渐变：

- 线性渐变（Linear Gradients）：向下/向上/向左/向右/对角方向，用 `linear-gradient()` 函数定义
- 径向渐变（Radial Gradients）：由它们的中心定义，用 `radial-gradient()` 函数定义

### 2.1、线性渐变

语法

```css
background: linear-gradient(direction, color1, color2, ...);
```

参数

- `direction`：指定了颜色过度的方向，不写默认为从上到下，值可以为 `to bottom`、`to top`、`to right`、`to left`、`to bottom right` 等。
- `color1`：可以有多个 `color` 值，指定了颜色变化的范围。

## 3、transition过渡

```css
transition: 要过渡的属性 花费时间 运动曲线 何时开始;
```

1. 属性：想要变化的css属性，宽度高度背景颜色内外边距都可以。如果想要所有的属性都变化过渡，写一个all就可以。
2. 花费时间：单位是秒（必须写单位）比如 0.5s
3. 运动曲线：默认是ease （可以省略）
4. 何时开始：单位是秒（必须写单位）可以设置延迟触发时间默认是Os （可以省略）

```css
div {
    width: 200px;
    height: 100px;
    background-color: pink;
    /* transition: width .5s, height .5s; */
    transition: all .5s;
}
div:hover {
    width: 400px;
    height: 200px;
    background-color: skyblue;
}
```

## 4、私有前缀

浏览器私有前缀是为了兼容老版本的写法，比较新版本的浏览器无须添加。

### 4.1、私有前缀

- `-moz-`: 代表firefox浏览器私有属性
- `-ms-`: 代表ie浏览器私有属性
- `-webkit-`: 代表safari、chrome私有属性-o-∶代表Opera私有属性

### 4.2、提倡的写法

```css
-moz-border-radius: 10px;
-webkit-border-radius: 10px;
-o-border-radius: 10px;
border-radius: 10px;
```

## 5、其他特性

### 5.1、滤镜fiter

filter CSS属性将模糊或颜色偏移等图形效果应用于元素。

```css
filter: 函数();
```

例如： `filter： blur(5px);` blur 模糊处理数值越大越模糊

### 5.2、CSS3 calc函数

此 CSS 函数让你在声明CSS属性值时执行一些计算。

```css
width: calc(100%-30px);
/* 子盒子永远比父盒子小30px */
```

括号里面可以使用 `+ - * /` 来进行计算。

# 八、2D转换

## 1、移动translate

==语法==

```css
transform: translate(x, y);
transform: translateX(x);
transform: translateY(y);
```

- 参数 `x, y` 可以是百分数，为盒子自身的宽度或高度。

重点

- 定义 2D 转换中的移动，沿着X和Y轴移动元素
- translate 最大的优点：不会影响到其他元素的位置
- translate 中的百分比单位是相对于 自身元素 的 `trainslate:(50%，50%)`
- 对行内标签没有效果

### 1.1 让盒子实现水平和垂直居中

```css
/*子绝父相*/
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
```

## 2、旋转 rotate

值为正数则顺时针旋转，为负数则逆时针旋转。

```css
transform: rotate(45deg);
```

## 3、2D 转换中心点 transform-origin

我们可以通过设置 `transform-origin` 设置元素转换的中心点。

```css
transform-origin: x y;
```

==重点==

- 注意后面的参数 x 和 y 用空格隔开
- x y 默认转换的中心点是元素的中心点（50% 50%）
- 还可以给 x y 设置像素或者方位名词（top bottom left right center）

## 4、2D 转换之缩放 scale

```css
 transform: scale(x, y);
```

`x, y` 不跟单位的话，是指缩放的倍数。

```css
transform: scale(2,1);
```

- 参数大于 `1` 则放大，小于 `1` 则缩小。
- 可以配合 `transform-origin` 使用，改变缩放中心。
- `scale` 的优势：不占空间

## 5、2D 转换综合写法

1. 同时使用多个转换，其格式为： `transform: translate(), rotate() scale()`
2. 其顺序会影转换的效果。（先旋转会改变坐标轴方向）
3. 当我们同时有位移和其他属性的时候，记得要将位移放到最前.

# 九、动画

动画( animation ) 是 CSS3 中具有颠覆性的特征之一，可通过设置多个节点来精确控制一个或一组动画，常用来实现复杂的动画效果。 相比较过渡，动画可以实现更多变化，更多控制，连续自动播放等效果。

## 1、动画的基本使用

分为两步：

1. 定义动画
2. 使用动画

```css
 /* 1. 定义动画 */
@keyframes move {
    /*开始状态*/
    0% {
        transform: translateX(0px);
    }
    /*结束状态*/
    100% {
        transform: translateX(1000px);
    }
}
div {
    width: 200px;
    height: 200px;
    background-color: pink;
    /* 2. 调用动画 */
    /* 动画名称 */
    animation-name: move;
    /* 持续时间 */
    animation-duration: 5s;
}
```

**动画序列**

- 0% 是动画的开始，100% 是动画的完成。这样的规则就是动画序列。
- 在 @keyframes 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果。
- 动画是使元素从一种样式逐渐变化为另一种样式的效果。您可以改变任意多的样式任意多的次数。
- 请用百分比来规定变化发生的时间，或用关键词"from"和“to”，等同于0%和100%。

注意:

1. 可以做多个状态的变化 `keyframes` 关键帧
2. 百分比必须是整数
3. 百分比是总时间 `animation-duration` 的划分

## 2、动画常用属性

| 属性                        | 描述                                                         |
| --------------------------- | ------------------------------------------------------------ |
| `keyframes`                 | 规定动画。                                                   |
| `animation`                 | 所有动画属性的简写属性,除了animation-play-state属性。        |
| `animation-name`            | 规定@keyframes动画的名称。(必须的)                           |
| `animation-duration`        | 规定动画完成一个周期所花费的秒或毫秒，默认是0。（必须的)     |
| `animation-timing-function` | 规定动画的速度曲线，默认是“ease” .                           |
| `animation-delay`           | 规定动画何时开始，默认是0.                                   |
| `animation-iteration-count` | 规定动画被播放的次数，默认是1，还有infinite                  |
| `animation-direction`       | 规定动画是否在下一周期逆向播放，默认是 "normal",alternate逆播放 |
| `animation-play-state`      | 规定动画是否正在运行或暂停。默认是"running",还有"paused".    |
| `animation-fill-mode`       | 规定动画结束后状态,保持forwards回到起始backwards             |

## 3、动画简写属性

```css
animation: 动画名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 动画起始或者结束的状态;
animation: myfirst 5s linear 2s infinite alternate;
```

- 简写属性里面不包含 `animation-play-state`
- 暂停动画: `animation-play-state: puased;`
- 经常和鼠标经过等其他配合使用想要动画走回来，而不是直接跳回来: `animation-direction: alternate`
- 盒子动画结束后，停在结束位置: ` animation-fill-mode: forwards`

## 4、速度曲线细节

animation-timing-function：规定动画的速度曲线

| 值          | 描述                                         |
| ----------- | -------------------------------------------- |
| linear      | 动画从头到尾的速度都是相同的。匀速           |
| ease        | 默认。动画以低速开始，然后加快，在结束前变慢 |
| ease-in     | 动画以低速开始                               |
| ease-out    | 动画以低速结束                               |
| ease-in-out | 动画以低速开始和结束                         |
| steps()     | 指定了时间函数中的间隔数量（步长）           |

# 十、3D转换

## 1、三维坐标系

x轴：水平向右   注意：x右边是正值，左边是负值

y轴：垂直向下   注意：y下面是正值，上面是负值

z轴：屏幕垂直   注意：往外面是正值，往里面是负值

## 2、tranlate3D

```css
transform: translate(x, y ,z);
transform: translateX(x);
transform: translateY(y);
transform: translateZ(Z);
```

注意：

+ 简写x,y,z不能省略，如果没有就写0

+ 父盒子没有加透视，z轴translateZ()没有变化

## 3、透视perspective

**透视**：在2D平面产生近大远小视觉立体，但是只是效果二维的

+ 如果想要在网页产生3D效果需要透视（理解成3D物体投影在2D平面内）
+ 模拟人类的视觉位置，可认为安排一只眼睛去看
+ 透视我们也称为视距：视距就是人的眼睛到屏幕的距离
+ 距离视觉点越近的在电脑平面成像越大，越远成像越小
+ 透视的单位是像素

==透视写在被观察元素的父盒子上面的==

![img](https://img-blog.csdnimg.cn/07b834ed67b14d038613fdb993b161e3.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

d：就是视距，视距就是一个距离人的眼睛到屏幕的距离。

z：就是 z轴，物体距离屏幕的距离，z轴越大（正值） 我们看到的物体就越大

### 透视的作用

有了透视，就能看到translateZ 引起的变化了

- translateZ：近大远小
- translateZ：往外是正值
- translateZ：往里是负值

![img](https://img-blog.csdnimg.cn/fc804561fd5d4f6f892404c3df05dde6.gif#pic_center)

## 4、3D旋转rotate3d

3D旋转：3D旋转指可以让元素在三维平面内沿着 x轴，y轴，z轴或者自定义轴进行旋转。

+ transform: rotateX(45deg) ：沿着X轴正方向旋转45度
+ transform: rotateY(45deg) ：沿着Y轴正方向旋转45度
+ transform: rotateZ(45deg) ：沿着Z轴正方向旋转45度
+ transform: rotate3d(x,y,z,deg) ：沿着自定义轴旋转 deg为角度(了解即可)

xyz是表示旋转轴的矢量，是标示你是否希望沿着该轴旋转，最后一个标示旋转的角度。

```css
/*沿着X轴旋转45deg*/
transform: rotate3d(1,0,0,45deg) 
/*沿着对角线旋转45deg*/
transform: rotate3d(1,1,0,45deg) 
```

**左手准则**

translateX

- 左手的手拇指指向 x轴的正方向
- 其余手指的弯曲方向就是该元素沿着x轴旋转的方向

![img](https://img-blog.csdnimg.cn/6eccd83b5b2e48adbeadb673c96ed0fc.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0F1Z2Vuc3Rlcm5fUVhM,size_16,color_FFFFFF,t_70#pic_center)

translateY

- 左手的手拇指指向 y轴的正方向
- 其余手指的弯曲方向就是该元素沿着y轴旋转的方向（正值）

![img](https://img-blog.csdnimg.cn/70b7feb515b24793a832060719ed33d6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_16,color_FFFFFF,t_70,g_se,x_16)

translateZ

+ 旋转模式和2D相类似

## 5、3D呈现transform-style

1. 控制子元素是否开启三维立体环境
2. `transform-style: flat` 子元素不开启3d立体空间 默认的
3. `transform-style: preserve-3d` 子元素开启立体空间
4. **代码写给父级**，但是影响的是子盒子
5. 这个属性很重要



# 十一、移动端web

国内的 UC 和 QQ，百度等手机浏览器都是根据 Webkit 修改过来的内核，国内尚无自主研发的内核。

> 总结：兼容移动端主流浏览器，处理 Webkit 内核浏览器即可。

## 1、视口

- 视口（viewport）就是浏览器显示页面内容的屏幕区域。 视口可以分为**布局视口、视觉视口和理想视口**
- 我们只需要关注理想视口

①布局视口layout viewport

②视觉视口 visual viewport

③理想视口 ideal viewport

- 需要手动添写meta视口标签通知浏览器操作
- meta视口标签的主要目的：布局视口的宽度应该与理想视口的宽度一致，简单理解就是设备有多宽，我们布局的视口就多宽(乔布斯提出的哟)

## 2、meta视口标签

```css
<meta name="viewport" content="width=device-width, user-scalable=no,initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

| 属性          | 解释说明                                                     |
| ------------- | ------------------------------------------------------------ |
| width         | 宽度设置的是viewport宽度，可以设置device-width特殊值(宽度是设备宽度) |
| initial-scale | 初始缩放比，大于0的数字                                      |
| maximum-scale | 最大缩放比，大于0的数字                                      |
| minimum-scale | 最小缩放比，大于0的数字                                      |
| user-scalable | 用户是否可以缩放，yes或no（1或0）                            |

**标准的viewport设置**

- 视口宽度和设备保持一致
- 视口的默认缩放比例1.0
- 不允许用户自行缩放
- 最大允许的缩放比例1.0
- 最小允许的缩放比例1.0

## 3、二倍图

### 3.1物理像素和物理像素比

+ 物理像素点指的是屏幕显示的最小颗粒，是物理真实存在的，我们开发时候的1px 不是一定等于1个物理像素的

- PC端页面，1个px 等于1个物理像素的，但是移动端就不尽相同

我们准备的图片，比我们实际需要的大小大2倍，这种方式就是二倍图

### 3.2、背景缩放

```css
background-size: 背景图片宽度 背景图片高度;
```

- 单位： 长度|百分比|cover|contain
- cover把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。
- contain把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域

##  4、移动端开发选择

1. 单独制作移动端页面(主流)，通常情况下，网址域名前面加 m(mobile) 可以打开移动端。
   - m.taobao.com
   - m.jd.com
   - m.suning.com
   - 通过判断设备，如果是移动设备打开，则跳到移动端页面。
2. 响应式页面兼容移动端(其次)

## 5、css初始化 normalize.css

移动端 CSS 初始化推荐使用 normalize.css

官网地址：http://necolas.github.io/normalize.css/

## 6、CSS3盒子模型 box-sizing

传统模式宽度计算：盒子的宽度 = CSS中设置的width + border + padding
CSS3盒子模型： 盒子的宽度 = CSS中设置的宽度width，里面包含了 border 和 padding
也就是说，我们的CSS3中的盒子模型， padding 和 border 不会撑大盒子了

```css
/*CSS3盒子模型*/
box-sizing: border-box;
/*传统盒子模型*/
box-sizing: content-box;
```

移动端可以全部CSS3 盒子模型
PC端如果完全需要兼容，我们就用传统模式，如果不考虑兼容性，我们就选择 CSS3 盒子模型

## 7、特殊样式

```css
/*CSS3盒子模型*/
box-sizing: border-box;
-webkit-box-sizing: border-box;

/*点击高亮我们需要清除 设置为transparent 完成透明*/
-webkit-tap-highlight-color: transparent;

/*在移动端浏览器默认的外观在iOS上加上这个属性才能给按钮和输入框自定义样式*/
-webkit-appearance: none;

/*禁用长按页面时的弹出菜单*/
img,a { 
    -webkit-touch-callout: none;
}
```

# 十二、单独制作移动端页面

## 1、流式布局

- 流式布局，就是百分比布局，也称非固定像素布局。
- 通过盒子的宽度设置成百分比来根据屏幕的宽度来进行伸缩，不受固定像素的限制，内容向两侧填充。

## 2、flex布局

| 传统布局                       | flex弹性布局                             |
| ------------------------------ | ---------------------------------------- |
| 兼容性好                       | 操作方便，布局极为简单，移动端应用很广泛 |
| 布局繁琐                       | PC 端浏览器支持情况较差                  |
| 局限性，不能再移动端很好的布局 | IE 11或更低版本，不支持或仅部分支持      |

建议：

1. 如果是PC端页面布局，我们还是传统布局。
2. 如果是移动端或者不考虑兼容性问题的PC端页面布局，我们还是使用flex弹性布局

### 2.1、flex布局原理

- 当我们为父盒子设为 flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效。
- 伸缩布局 = 弹性布局 = 伸缩盒布局 = 弹性盒布局 =flex布局

![在这里插入图片描述](https://img-blog.csdnimg.cn/d27de399dbd64e5db668e9d20c8b48bd.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 2.2、flex布局常见父项属性

+ flex-direction：设置主轴的方向
+ justify-content：设置主轴上的子元素排列方式
+ flex-wrap：设置子元素是否换行
+ align-content：设置侧轴上的子元素的排列方式（多行）
+ align-items：设置侧轴上的子元素排列方式（单行）
+ flex-flow：复合属性，相当于同时设置了 flex-direction 和 flex-wrap

#### 2.2.1、flex-direction设置主轴方向

主轴和侧轴：在 flex 布局中，是分为主轴和侧轴两个方向，同样的叫法有：行和列、x轴和y轴

- 默认主轴方向就是 x 轴方向，水平向右
- 默认侧轴方向就是 y 轴方向，水平向下

- flex-direction 属性决定主轴的方向（即项目的排列方向）
- 注意： 主轴和侧轴是会变化的，就看 flex-direction 设置谁为主轴，剩下的就是侧轴。而我们的子元素是跟着主轴来排列的

| 属性值         | 说明               |
| -------------- | ------------------ |
| **row**        | **默认值从左到右** |
| row-reverse    | 从右到左           |
| **column**     | **从上到下**       |
| column-reverse | 从下到上           |

#### 2.2.2、justify-content 设置主轴上的子元素排列方式

stify-content 属性定义了项目在主轴上的对齐方式
注意： 使用这个属性之前一定要确定好主轴是哪个

| 属性值            | 说明                                            |
| ----------------- | ----------------------------------------------- |
| **flex-start**    | **默认值从头部开始，如果主轴是x轴，则从左到右** |
| flex-end          | 从尾部开始排列                                  |
| **center**        | **在主轴居中对齐(如果主轴是 x 轴则水平居中)**   |
| **space-around**  | **平分剩余空间**                                |
| **space-between** | **先两边贴边，再平分剩余空间🔥**                 |

#### 2.2.3、flex-wrap 设置子元素是否换行

默认情况下，项目都排在一条线（又称”轴线”）上。flex-wrap属性定义，flex布局中默认是不换行的。

意思就是如果按照我们设置的盒子大小，一行只能装 3 个盒子，但是我们有 5 个盒子，那么 flex 布局默认会给我们塞上去，自动缩小盒子大小。

| 属性值   | 说明           |
| -------- | -------------- |
| nowrap   | 默认值，不换行 |
| **wrap** | **换行**       |

#### 2.2.4、align-items 设置侧轴上的子元素排列方式(单行)

该属性是控制子项在侧轴（默认是y轴）上的排列方式 在子项为单项（**单行**）的时候使用

| 属性值         | 说明                       |
| -------------- | -------------------------- |
| **flex-start** | **从上到下**               |
| flex-end       | 从下到上                   |
| **center**     | **挤在一起居中(垂直居中)** |
| **stretch**    | **拉伸(默认值)**           |

#### 2.2.5、align-content 设置侧轴上的子元素的排列方式(多行)

设置子项在侧轴上的排列方式 并且只能用于子项出现 **换行** 的情况（多行），在单行下是没有效果的。

| 属性值            | 说明                                       |
| ----------------- | ------------------------------------------ |
| **flex-start**    | **默认值在侧轴的头部开始排列**             |
| flex-end          | 在侧轴的尾部开始排列                       |
| **center**        | **在侧轴中间显示**                         |
| **space-around**  | **子项在侧轴平分剩余空间**                 |
| **space-between** | **子项在侧轴先分布在两头，再平分剩余空间** |
| **stretch**       | **设置子项元素高度平分父元素高度**         |

#### 2.2.6、align-content 和 align-items 区别

+ align-items 适用于单行情况下， 只有上对齐、下对齐、居中和 拉伸
+ align-content 适应于换行（多行）的情况下（单行情况下无效）， 可以设置 上对齐、 下对齐、居中、拉伸以及平均分配剩余空间等属性值。
+ 总结就是单行找 align-items 多行找 align-content

#### 2.2.7、flex-flow

flex-flow 属性是 flex-direction 和 flex-wrap 属性的复合属性

```css
flex-flow: row wrap;
```



### 2.3、flex布局子项常见属性

- flex 子项目占的份数
- align-self 控制子项自己在侧轴的排列方式
- order属性定义子项的排列顺序（前后顺序）

#### 2.3.1、flex属性

flex 属性定义子项目**分配剩余空间**，用flex来表示占多少份数。

#### 2.3.2、align-self 控制子项自己在侧轴上的排列方式

+ align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性。
+ 默认值为 auto，表示继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch。

#### 2.3.3、order属性定义项目的排列顺序

数值越小，排列越靠前，默认为0。

注意：和 z-index 不一样。

## 3、背景颜色渐变

```css
/* 背景渐变必须添加浏览器私有前缀 */
/* background: -webkit-linear-gradient(left, red, blue); */
/* background: -webkit-linear-gradient(red, blue); */
background: -webkit-linear-gradient(top left, red, blue);

```

## 4、rem适配布局

流式布局和flex布局主要针对于宽度布局，rem解决高度自适应

+ rem (root em)是一个相对单位，类似于em，em是父元素字体大小。
+ 不同的是rem的基准是相对于html元素的字体大小。
  + 比如，根元素（html）设置font-size=12px; 非根元素设置width:2rem; 则换成px表示就是24px
  + rem的优势：父元素文字大小可能不一致， 但是整个页面只有一个html，可以很好来控制整个页面的元素大小

## 5、媒体查询

媒体查询（Media Query）是CSS3新语法。

+ 使用 @media 查询，可以针对不同的媒体类型定义不同的样式
+ @media 可以针对不同的屏幕尺寸设置不同的样式
+ 当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面
+ 目前针对很多苹果手机、Android手机，平板等设备都用得到多媒体查询

**语法**

```css
@media mediatype and|not|only(media feature){
    CSS-code
}
//例如
 @media screen and (max-width: 800px) {
     body {
         background-color: pink;
     }
  }
```

- 用 @media 开头 注意@符号
- mediatype 媒体类型
- 关键字 and not only
- media feature 媒体特性 必须有小括号包含

### 5.1、mediatype查询类型

| 值         | 解释说明                               |
| ---------- | -------------------------------------- |
| all        | 用于所有设备                           |
| print      | 用于打印机和打印预览                   |
| **screen** | **用于电脑屏幕、平板电脑、智能手机等** |

### 5.2、关键词

| 值   | 解释说明                                       |
| ---- | ---------------------------------------------- |
| and  | 可以将多个媒体特性连接到一起，相当于“且”的意思 |
| not  | 排除某个媒体类型，相当于“非”的意思，可以省略   |
| only | 指定某个特定的媒体类型，可以省略               |

### 5.3、媒体特性

| 值        | 解释                               |
| --------- | ---------------------------------- |
| width     | 定义输出设备中页面可见区域的宽度   |
| min-width | 定义输出设备中页面最小可见区域宽度 |
| max-width | 定义输出设备中页面最大可见区域宽度 |

### 5.4、媒体查询+rem实现元素动态大小变化

- rem单位是跟着html来走的，有了rem页面元素可以设置不同大小尺寸
- 媒体查询可以根据不同设备宽度来修改样式
- 媒体查询+rem 就可以实现不同设备宽度，实现页面元素大小的动态变化

```css
  @media screen and (min-width: 320px) {
            html {
                font-size: 50px;
            }
        }
        
   @media screen and (min-width: 640px) {
            html {
                font-size: 100px;
            }
        }
        
    .top {
            height: 1rem;
            font-size: .5rem;
            background-color: green;
            color: #fff;
            text-align: center;
            line-height: 1rem;
        }

```

## 6、引入资源

- 当样式比较繁多的时候，我们可以针对不同的媒体使用不同 stylesheets（样式表）。
- 原理，就是直接在link中判断设备的尺寸，然后引用不同的css文件。

**语法**

```css
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">
```

**示例**

```css
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css">
```

## 7、less(重点)

Less （Leaner Style Sheets 的缩写） 是一门 CSS 扩展语言，也成为CSS预处理器。

+ 做为 CSS 的一种形式的扩展，它并没有减少 CSS 的功能，而是在现有的 CSS 语法上，为CSS加入程序式语言的特性。
+ 它在 CSS 的语法基础之上，引入了变量，Mixin（混入），运算以及函数等功能，大大简化了 CSS 的编写，并且降低了 CSS 的维护成本，就像它的名称所说的那样，Less 可以让我们用更少的代码做更多的事情
+ Less中文网址： http://lesscss.cn/

+ Less 是一门 CSS 预处理语言，它扩展了CSS的动态特性。

### 7.1、less安装

```
npm install -g less     //如果使用vscode无需安装less
```

查看版本

```
lessc -v
```

### 7.2、less变量

```less
@变量名: 值;
```

变量命名规范

- 必须有@为前缀
- 不能包含特殊字符
- 不能以数字开头
- 大小写敏感

例：

```less
@color: pink;
```

变量是指没有固定的值，可以改变的。因为我们CSS中的一些颜色和数值等经常使用。

### 7.3、编译

我们需要把我们的 less文件，编译生成为css文件，这样我们的html页面才能使用。

我们可以在 vscode 安装 `Easy LESS` 插件来把 less 文件编译为 css。安装完毕插件，重新加载下 vscode。只要保存一下Less文件，会自动生成CSS文件。

### 7.4、Less嵌套

```less
#header .logo {
	width: 300px;
}

#header {
    .logo{
        width: 300px;
    }
}
```

如果遇见 （交集|伪类|伪元素选择器）

- 内层选择器的前面没有 & 符号，则它被解析为父选择器的后代
- 如果有 & 符号，它就被解析为父元素自身或父元素的伪类

```less

a{
    &:hover{
        color: red;
    }
}
```

### 7.5、less运算

任何数字、颜色或者变量都可以参与运算。就是Less提供了加（+）、减（-）、乘（*）、除（/）算术运算。

```less
@width: 10px + 5;
div {
    border: @width solid red;
}

/* 生成的css */
div {
    border: 15px solid red;
}

/* Less甚至还可以这样 */
width: (@width + 5) * 2;
```

注意：

- 乘号（*）和除号（/）的写法
- 运算符中间左右有个空格隔开 1px + 5
- 对于两个不同的单位的值之间的运算，运算结果的值取第一个值的单位
- 如果两个值之间只有一个值有单位，则运算结果就取该单位

### 7.6、导入less文件

```less
//在index.less导入common.less文件
@import "common"
```



## 8、rem适配方案

实际开发中适配方案：

1. 按照设计稿与设备宽度的比例，动态计算并设置 html 根标签的 font-size 大小；（媒体查询）
2. CSS 中，设计稿元素的宽、高、相对位置等取值，按照同等比例换算为 rem 为单位的值；

![img](https://img-blog.csdnimg.cn/a0b6ea5dab89442096a4d3595c121dc7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

### 8.1、技术方案1

rem + 媒体查询 + less 技术

![img](https://img-blog.csdnimg.cn/2f0494ce7c554a6985ac4f0d0db421e4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA55Sf5ZG95piv5pyJ5YWJ55qE,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

一般情况下，我们以一套或两套效果图适应大部分的屏幕，放弃极端屏或对其优雅降级，牺牲一些效果。现在基本以750为准。

> 动态设置 html 标签 font-size 大小

+ 假设设计稿是750px
+ 假设我们把整个屏幕划分为15等份（划分标准不一可以是20份也可以是10等份）
+ 每一份作为html字体大小，这里就是50px
+ 那么在320px设备的时候，字体大小为320/15 就是 21.33px
+ 用我们页面元素的大小 除以不同的 html 字体大小会发现他们比例还是相同的
+ 比如我们以 750为标准设计稿
+ 一个100*100像素的页面元素 在 750屏幕下， 就是 100 / 50 转换为rem 是 2rem * 2 rem 比例是 1比1
+ 320屏幕下， html 字体大小为 21.33 则 2rem = 42.66px 此时宽和高都是 42.66 但是 宽和高的比例还是 1比1
+ 但是已经能实现不同屏幕下 页面元素盒子等比例缩放的效果

**元素的取值公式**

1. 最后的公式： 页面元素的rem值 = 页面元素值（px） / （屏幕宽度 / 划分的份数）
2. 屏幕宽度/划分的份数 就是 html font-size 的大小
3. 或者： 页面元素的rem值 = 页面元素值（px） / html font-size 字体大小

**body的设置代码**

```ss
body {
    min-width: 320px;
    /* 因为划分十五等分 */
    width: 15rem;
    margin: 0 auto;
    line-height: 1.5;
    font-family: Arial, Helvetica;
    background-color: #f2f2f2;
}
```

### 8.2、技术方案2

设计图：本设计图采用750px设计尺寸

它的原理是将当前设备**十等分**，但是在不同设备下，比例还是一样的。

github地址：[https://github.com/amfe/lib-flexible](https://github.com/amfe/lib-flexible)

**body的设置代码**

```css
body {
    min-width: 320px;
    max-width: 750px;
    /* 因为划分十等分 */
    width: 10rem;
    margin: 0 auto;
    line-height: 1.5;
    font-family: Arial, Helvetica;
    background-color: #f2f2f2;
}
```

#### 8.2.1、vscode插件cssrem

自动将px转化为rem

修改默认rem的html字体大小

![image-20230207122218600](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230207122218600.png)

#### 8.2.2、修改flexible默认的html字体大小

```css
@media screen and (min-width: 750px) {
      html {
          font-size: 75px!important;
      }
}
```

# 十三、响应式开发移动web

## 1、原理

响应式开发原理：就是使用媒体查询针对不同宽度的设备来进行布局和样式的设置，从而适配不同的设备

| 设备划分                 | 尺寸区间            |
| ------------------------ | ------------------- |
| 超小屏幕（手机）         | <768px              |
| 小屏设备（平板）         | >= 768px ~ < 992px  |
| 中等屏幕（桌面显示器）   | >= 992px ~ < 1200px |
| 宽屏屏幕（大桌面显示器） | >= 1200px           |

## 2、响应式布局容器

响应式开发需要一个父级容器，来配合子元素实现变化效果。

原理就是在不同屏幕下，通过媒体查询，来改变这个布局容器的大小，在改变里面子元素的排列方式和大小，从而实现在不同屏幕下，看到不同的页面布局和样式变化。

**平时响应式尺寸划分大小**

+ 超小屏幕：设置宽度为100%
+ 小屏幕：设置宽度为750px
+ 中等屏幕：设置宽度为970px
+ 大屏幕：设置宽度为1170px

## 3、bootstrap前端开发框架

+ 中国官网：[http://www.bootcss.com/](http://www.bootcss.com/)
+ 官网：[http://getbootstrap.com/](http://getbootstrap.com/)
+ 推荐使用：[http://bootstrap.css88.com/](http://bootstrap.css88.com/)

### 3.1、Bootstrap使用

使用四部曲：1.创建文件夹  2.创建HTML骨架结构   3.引入相关的样式   4.书写内容

​	1. 创建文件夹

![image-20230207161523963](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230207161523963.png)

2. 创建HTML骨架结构

![image-20230207162120444](C:\Users\lsy\AppData\Roaming\Typora\typora-user-images\image-20230207162120444.png)

3. 引入相关的样式

```css
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
```

4. 书写内容
   + 修改Bootstrap原来的样式，注意权重问题
   + 学好Bootstrap关键在于它定义了哪些样式，以及这些样式能实现怎么样的效果

### 3.2、布局容器

Bootstrap预先定义好了布局容器

#### 1.container类

+ 超小屏幕：设置宽度为100%
+ 小屏幕：设置宽度为750px
+ 中等屏幕：设置宽度为970px
+ 大屏幕：设置宽度为1170px

#### 2.container-fluid类

+ 流式布局容器 百分之百宽度
+ 占据全部视口（viewport）的容器
+ 适合于单独做移动端开发

### 3.3、Bootstrap栅格系统

Bootstrap提供一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为12列。

Bootstrap里面container宽度是固定的，但是不同屏幕下，container的宽度不同，我们再把container划分为12等分

|                       | 超小屏幕 手机 (<768px) | 小屏幕 平板 (≥768px)                                | 中等屏幕 桌面显示器 (≥992px) | 大屏幕 大桌面显示器 (≥1200px) |
| :-------------------- | :--------------------- | :-------------------------------------------------- | :--------------------------- | ----------------------------- |
| 栅格系统行为          | 总是水平排列           | 开始是堆叠在一起的，当大于这些阈值时将变为水平排列C |                              |                               |
| `.container` 最大宽度 | None （自动）          | 750px                                               | 970px                        | 1170px                        |
| 类前缀                | `.col-xs-`             | `.col-sm-`                                          | `.col-md-`                   | `.col-lg-`                    |
| 列（column）数        | 12                     | 12                                                  | 12                           | 12                            |

+ 可以给一个列指定多个设备的列名，以划分不同的份数，例如class="col-md-4 col-lg-2"

+ 列大于12，则最后一个元素另起一行，小于12则会留白

#### 3.3.1、列嵌套

```html
 <div class="container">
       <div class="row">
            <div class="col-md-4">
                我们列嵌套最好加一个行row，这样可以取消父元素的padding值，而且高度自动和父级一样高
                <div class="row">
                    <div class="col-md-6">a</div>
                    <div class="col-md-6">b</div>
                </div>
            </div>
            <div class="col-md-4">2</div>
            <div class="col-md-4">3</div>
       </div>
    </div>
```

#### 3.3.2、列偏移

```html
<div class="container">
       <div class="row">
            <div class="col-md-4">左侧</div>
            <div class="col-md-4 col-md-offset-4">右侧</div>
       </div>
		//如果只有一个盒子，那么偏移 = 12 -8 /2
    	<div class="row">
            <div class="col-md-8 col-md-offset-2">右侧</div>
       </div>
</div>
```

#### 3.3.3、列排序

通过.col-md-push-* 和.col-md-pull- *类就很容易的改变列的顺序。

```html
<div class="row">
            <div class="col-md-4" colmd-push-8>左侧</div>
            <div class="col-md-8 col-md-pull-4">右侧</div>
</div>
```

#### 3.3.4、响应式工具

利用媒体查询，针对不同设备显示与隐藏页面内容

| 类名       | 超小屏 | 小屏 | 中屏 | 大屏 |
| ---------- | ------ | ---- | ---- | ---- |
| .hidden-xs | 隐藏   | 显示 | 显示 | 显示 |
| .hidden-sm | 显示   | 隐藏 | 显示 | 显示 |
| .hidden-md | 显示   | 显示 | 隐藏 | 显示 |
| .hidden-lg | 显示   | 显示 | 显示 | 隐藏 |

与之相反的是，==visivle-xs  visivle-sm   visivle-md  visivle-lg== 是显示某个页面的内容

# 十四、vw和vh

## 1、vw和vh

+ vw，vh是一个相对单位（类似于em和rem）

vw: viewport width(视口宽度单位)

vh: viewport height(视口长度单位)

+ 相对视口单位的尺寸计算结果：

1vw=1/100视口宽度

1vh=1/100视口高度

例如：当前屏幕视口是375px，1vw就是3.75px

**注意事项**

==和百分比有区别，百分比是相对父元素来说的，而vw和vh总是针对于当前视口来说的==

## 2、使用

设计稿视口宽度375px

1. 1vw是多少像素		375px/100=3.75px
2. 目标是多少像素？     50px*50px
3. 那么50*50是多少个vw      50/3.75=13.3333vw

# 十五、css代码规范

1. 类名语义化，尽量简短，必须以字母开头命名，且全部字母为小写，单词之间统一使用下划线"_"连接
2. 类名嵌套层次尽量不超过三层
3. 尽量避免直接使用元素选择器
4. 属性书写顺序
   + 布局定位属性：display / position / float / clear / visibility / overflow
   + 尺寸属性：width / height / margin / padding / border / background
   + 文本属性：color / font / text-decoration / text-align / vertical-align
   + 其他属性（css3）:content / cursor / border-radius / box-shadow / text-shadow

5. 避免使用id选择器
6. 避免使用通配符和!important
