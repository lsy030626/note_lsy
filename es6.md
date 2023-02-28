# 前言

https://es6.ruanyifeng.com/#docs/symbol

# 一、let、const

## 1、let

+ ==变量不能重复声明==

  `let star='罗志祥'; `

  `let star='小猪'  *//error*`

+ ==let有块级作用域==

  `{    `

  `		let girl='周扬青'`		

  ` } ` 

  `console.log(girl)  //error`

+ ==不存在变量提升==

  `console.log(song)   *//error*` 

  `let song='恋爱达人    //如果是var则输出undefined`

+ ==不影响作用域链==

​	`let school='abc' `

​     `	function fn(){    `

​	`	console.log(school) //abc `

​	`	}`



经典例题

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div>
        <div class="item" style="width: 50px;height: 50px;background-color: red"></div>
        <div class="item" style="width: 50px;height: 50px;background-color: red"></div>
        <div class="item" style="width: 50px;height: 50px;background-color: red"></div>
    </div>
    <script>
        let items=document.getElementsByClassName("item");
        for (var i=0;i<items.length;i++){
            items[i].onclick=function (){
                items[i].style.backgroundColor='pink';
            }
        }
        console.log(windows.i)  //3 
        // 当var=3的时候，点击事件开始向外层作用域找，找不到，就是windows.i，此时是3，如果是let i，具有块级作用域，所以每一次触碰事件的i都是不同的。
    </script>
</body> 
</html>


## 2、const(声明常量)

+ ==一定赋初始值==

+ ==一般常量使用大写（潜规则）==

+ ==常量的值不能修改==

+ ==也具有块级作用域==

+ ==对于数组和对象的元素修改，不算作对常量的修改==

  `const team = ['uzi','MXLG','Ming','Letme'];
  team.push('Meiko'); //不报错，常量地址没有发生变化`

## 3、三者区别

+ let和var 声明变量，const声明常量
+ var允许重复声明，但let、const只能声明一次
+ var存在变量提升（预解析），不存在块级作用域，但是let和const有块级作用域

# 二、解析结构（方便程序员）

## 1、数组的解析

`const F4 = ['小沈阳'，'刘能','赵四','宋小宝']` 

`let [xiao,liu,zhao,song] = F4;`  

`console.log(xiao)   //小沈阳`

`console.log(liu)   //刘能`

`console.log(zhao)   //赵四`

`console.log(song)   //宋小宝`

## 2、对象的解析

`const zhao = {
    name : '赵本山'，
    age: '不详',
    xiaopin: function(){
        console.log("我可以演小品")
    }
}
let {name,age,xiaopin} = zhao;
console.log(name);
console.log(age);
console.log(xiaopin);`

# 三、模板字符串（内容可出现换行符）

+ ==声明(用``标识)==（由于热键占用，所以用  ‘  代替）

`let str = ’我也是一个字符串‘`
`console.log(str,typeof str);`

+ 内容中可以直接出现换行符

`let str = ’<ul>
			<li>RHF</li>
			<li>RHF</li>
		   </ul>‘；`

+ 变量拼接

`let lovest = 'RHF';`
`let out =’ ${lovest}是最帅的‘;`
`console.log(out)  //RHF是最帅的`

# 四、对象的简单写法

ES6允许在大括号里面，直接写入变量和函数，作为对象的属性和方法,这样的书写更加简洁

`let name = 'aaa';`
`let change = function(){`
    `console.log('aaa');`
`}`

`const school = {`
    `name,`
    `change,`
    `improve(){`
        `consolg.log('bbb');`
    `}`
`}`

# ==五、箭头函数（重点）==

ES6允许使用箭头（=>）定义函数

## 1、this指向

this是静态的，this始终指向函数声明时所在作用域下的this的值

`function A(){`
    `console.log(this.name)`
`}`

`let B = () => {`
    `console.log(this.name);`
`}`

`window.name = '尚硅谷';`
`const school = {`
    `name: 'ATGUIGU'`
`}`

`//直接调用`
`A()   //尚硅谷`
`B()  //尚硅谷`

`//call`
`A.call(school); //ATGUIGU`
`B.cal(school);  //尚硅谷`

## 2、不能作为构造实例化对象

`let A(name,age) => {`   

​		`this.name=name;`    

​		`this.age=age;` 

`}` 

`let me = new A('xiao',123);`

`console.log(me)  //error`

## 3、不能使用arguments变量

`let fn = () => {    `

​		`console.log(arguments)； `

`} `

`fn(1,2,3)  *//error*`

## 4、简写

+ 省略小括号，当形参有且只有一个

  `let add = n => {`    

  `return n + 1; }`

+ 略花括号，当代码体只有一条语句的时候，此时return也必须省略

  `let add = n => n+1;`

  

# 六、函数参数默认值

## 1、赋初始值

可以给形参赋初始值，一般位置要靠后（潜规则）

`function add(a,b,c=12){`
    `return a+b+c;` 
`}`
`let result = add (1,2);`
`console.log(result) // 15`

## 2、与解构赋值结合

`function A({host='127.0.0.1',username,password,port}){`
    `console.log(host+username+password+port)`
`}`
`A({`
    `username:'ran',`
    `password:'123456',`
    `port:3306`
`})`



# 七、rest参数

ES6引入rest参数，用于获取函数的实参，用来代替arguments

`function date(...args){   `

​			`		 console.log(args); `		 

`} `

`date('aaa','bbb','ccc')；`

# 八、扩展运算符

扩展运算符是能将数组转换为逗号分隔的参数序列

## 1、特性

`const tfboys=['AA','BB','CC']` 

`function chunwan(){`    

​		`console.log(arguments); }` 

`chunwan(...tfboys);   //0:'AA' 1:'BB' 2:'CC'`

## 2、数组的合并

`const A = ['aa','bb'];` 

`const B = ['cc','dd'];` 

`const C = [...A,...B];` 

`console.log(C)   //[aa,bb,cc,dd]`

## 3、数组的克隆

`const A = ['a','b','c'];` 

`const B = [...A];` 

`console.log(B)   //[a,b,c]`

## 4、将伪数组转换为真正的数组

`const A = documents.querySelectorAll('div');`
`const B = [...A];`
`console.log(B) // [div,div,div]`



# 九、Symbol



## 1、简介

一种原始数据类型

作用：对象属性名都是字符串，这容易造成属性名的冲突，symbol表示独一无二的值，保证每个属性的名字都是独一无二的就好了，这样就从根本上防止属性名的冲突

## 2、内容

https://es6.ruanyifeng.com/#docs/symbol



for in 打印键名
