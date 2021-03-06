# JS

### JS的特性
+ 解释性语言：解释型语言是对代码进行一句一句的直接运行，在程序运行期间，使用解释器动态将代码解释为机器码，再运行。
+ 单线程：JS 是单线程的，但是却能执行异步任务，这主要是因为 JS 中存在事件循环（Event Loop）和任务队列（Task Queue）

#### 解释性语言和编译性语言的定义：
计算机不能直接理解高级语言，只能直接理解机器语言，所以必须要把高级语言翻译成机器语言，计算机才能执行高级语言编写的程序。
翻译的方式有两种，一个是编译，一个是解释。两种方式只是翻译的时间不同。

+ 解释性语言的定义
解释性语言的程序不需要编译，在运行程序的时候才翻译，每个语句都是执行的时候才翻译。这样解释性语言每执行一次就需要逐行翻译一次，效率比较低。
现代解释性语言通常把源程序编译成中间代码，然后用解释器把中间代码一条条翻译成目标机器代码，一条条执行。

+ 编译性语言的定义
编译性语言写的程序在被执行之前，需要一个专门的编译过程，把程序编译成为机器语言的文件，比如exe文件，以后要运行的话就不用重新翻译了，直接使用编译的结果就行了（exe文件），因为翻译只做了一次，运行时不需要翻译，所以编译型语言的程序执行效率高。

#### 为什么JS是单线程
JavaScript语言最大的特点就是单线程。它是浏览器的脚本语言。在同一时间只能做一件事。用于操作DOM。如果JS是多线程的，当我在给一个DOM添加内容时，又删除了这个DOM，那么JS该怎么做。
所谓单线程，是指JS引擎中负责解释和执行JavaScript代码的线程只有一个，也就是一次只能完成一项任务，这个任务执行完后才能执行下一个，它会「阻塞」其他任务。这个任务可称为主线程。
详细 https://www.jianshu.com/p/d22d5f53194b

------------

### JS变量
+ 原始值
Number、Boolean、String、Undefined、Null、symbol
原始变量及他们的值储存在栈中
+ 引用值
Array、Object、Function、Date、RegExp
引用变量的名称储存在栈中，但是把其实际对象储存在堆中

#### 堆和栈
栈(stack)：栈会自动分配内存空间，会自动释放，存放基本类型，简单的数据段，占据固定大小的空间。

堆(heap)：动态分配的内存，大小不定也不会自动释放，存放引用类型，指那些可能由多个值构成的对象，保存在堆内存中，包含引用类型的变量，实际上保存的不是变量本身，而是指向该对象的指针。

#### 深拷贝、浅拷贝
浅拷贝和深拷贝都只针对于引用数据类型
- 浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存；
- 深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象

区别：浅拷贝只复制对象的第一层属性、深拷贝可以对对象的属性进行递归复制

------------

### JS运行三步骤
语法分析
预编译
解释执行

#### 预编译
预编译发生在代码执行的前一刻
步骤：
1. 创建GO/AO对象  AO Activation Object 执行期上下文 函数预编译，在函数执行前一刻 GO Global Object 在整个代码运行前一刻
2. 找形参和变量声明，将变量和形参名作为AO属性名，值为undefined
3. 将实参值和形参统一
4. 在函数体里面找函数声明，值赋予函数体 （注：没有函数表达式 function () {} ）


#### js中函数执行
1. 确定“this”的值 (确切的来说，this在JS里面不是一个变量名而是一个关键字)
2. 创建一个新的作用域
3. 处理形参/实参（没有定义过才声明，无论如何都重新赋值，没有对应实参则赋值为"undefined"）
4. 处理函数定义（没有定义过才声明，无论如何都重新赋值）
5. 处理 "arguments"（没有定义过才声明和赋值）
6. 处理变量声明（没有定义过才声明，不赋值）


#### call 与 apply 与 bind
在JavaScript里，call(),apply(),bind()都是Function内置的三个方法， 它们的作用都是显示的绑定this的指向，三个方法的第一个参数都是this指向的对象，也就是函数在运行时执行的上下文。

bind：bind()方法创建一个新的函数，在bind()被调用时，这个新函数的this被bind的第一个参数指定，其余的参数将作为新函数的参数供调用时使用，第一个thisArg在setTimeout中创建一个函数时传递的原始值都会转化成object，如果bind参数列表为空，thisArg赋值当前当前运行环境this。

特点:
- apply，call，bind三个方法第一个参数都是函数在调用时this指向的对象,也就是运行时的上下文（this显示绑定的原理）
- apply，call第一个参数为空，null，undefined，this指向的是window
- apply，call两个方法只是参数形式有所不同，apply参数是一个数组，call则是参数列表版本
- apply，call 则是立即调用，bind 是则返回对应函数

------------


### 闭包
定义在一个函数内部的函数，内部函数持有外部函数内变量的引用
闭包会导致原有作用域链不释放，造成内存泄漏。


#### 闭包的作用
1. 实现公有变量
2. 可以做缓存（存储结构）
3. 可以实现封装，属性私有化。
4. 模块化开发，防止污染全局变量


------------

### 对象的创建方法
1. var obj = { …… } plainObject  对象字面量/对象直接量
2. 构造函数
- 系统自带的构造函数 new Object ( )
- 自定义   外部添加属性和对象
3. 工厂模式

### new一个对象的过程中发生了什么
1. 创建空对象；
`var obj = {};`
2. 设置新对象的constructor属性为构造函数的名称，设置新对象的`__proto__`属性指向构造函数的prototype对象；
`obj.__proto__ = ClassA.prototype;`
3. 使用新对象调用函数，函数中的this被指向新实例对象：
`ClassA.call(obj);//{}.构造函数();`
4. 将初始化完毕的新对象地址，保存到等号左边的变量中

### 继承
1. 传统形式 --> 原型链
	过多的继承了没用的属性
2. 借用构造函数
	不能继承借用的构造函数的原型
	每次构造函数都要多走一个函数
3. 共享原型
	不能随便改动自己的原型,因为指向同一个空间。
4. 圣杯模式（原型链继承）
	基于共享原型的基础上增加一个中间层

### 原型及原型链
`prototype`与`__proto__`的关系详解
每个函数都有一个prototype属性，它是一个指向原型对象的指针，原型对象在定义函数时同时被创建，原型对象的用途是包含所有实例共享的属性和方法
当调用构造函数创建一个新实例后，该实例的内部将包含一个指针[[Prototype]]，该指针指向创建它的构造函数的原型，在脚本上没有标准的方法来访问[[Prototype]]，但大多数浏览器都支持通过`__proto__`来访问。
`__proto__`是对象实例中用来访问创建它的构造函数的原型



------------



### JS定时器
+ `window.setTimeout(code,millisec);`
	可以使一段代码在指定时间后运行
+ `window.setInterval(code,millisec);`
	可以使一段代码每过指定时间就运行一次
	millisec设置后不可更改
	//此函数非常不准
	有返回值，唯一标识符
+ 定时器清除的方法：clearTimeout(obj)和clearInterval(obj)


------------


### DOM事件的级别
DOM0 element.onclick = function(){}  
DOM2 element.addEventListener(‘click’, funttion(){}, false)  
DOM3 element.addEventListener(‘keyup’, funttion(){}, false) 事件增加了，如键盘时间等    


### 事件触发三阶段（事件流）
1. window 往事件触发处传播，遇到注册的捕获事件会触发  
window -- document -- html -- body -- ……  目标元素  
2. 传播到事件触发处时触发注册的事件
3. 从事件触发处往 window 传播，遇到注册的冒泡事件会触发

事件触发一般来说会按照上面的顺序进行，但是也有特例，如果给一个目标节点同时注册冒泡和捕获事件，事件触发会按照注册的顺序执行。

### 事件处理模型—冒泡、捕获
#### 事件冒泡
代码结构上（非视觉上）嵌套关系的元素，会存在事件冒泡的功能，即同一事件，自子元素冒泡向父元素。（自底向上）  
addEventListener(type, fn, false) 冒泡  
focus聚焦 blur change submit reset select 等事件没有冒泡  

#### 事件捕获
结构上（非视觉上）嵌套关系的元素，会存在事件捕获的功能，即同一事件，自父元素捕获至子元素（事件源元素）。（自顶向下）  
addEventListener(type, fn, true) 捕获  
IE没有捕获事件  

##### 冒泡、捕获都是指的对父级元素的处理，不包括触发事件的那个元素

#### 阻止事件冒泡
W3C标准 event.stopPropagation(); 但不支持ie9以下版本  
IE独有event.cancelBubble = true;  
封装取消冒泡的函数 stopBubble(event)  

#### 阻止默认事件
默认事件 — 表单提交，a标签跳转，右键菜单等  
1. return false;  以对象属性的方式注册的事件才生效  
句柄 div.onclick = function(){};  
2. event.preventDefault(); W3C标准，IE9以下不兼容  
3. event.returnValue = false; 兼容IE 


### 事件委托
将本来需要 A 处理的事情，委托给 B 来处理。  
利用事件冒泡，和事件源对象进行事件处理  
优点：  
- 性能 不需要循环所有的元素一个个绑定事件
- 灵活 当有新的子元素时不需要重新绑定事件


event.target 当5个子元素 都要绑定一个行为，为了优化我们利用事件委托，可以在其父元素上绑定该行为，并通过event.target寻找触发事件的父元素的子元素  
event.currentTarget 仍是4的例子，可以找到当前绑定事件的对象，就是4步骤的父元素，而非子元素

### 自定义事件
    var eve = new Event（'custome'）
    element(dom节点).addEventListen('custome', function(){})
    element(dom节点).dispatchEvent(eve)
    
    **注意** Event 可以替换为 CustomEvent，区别在于CustomEvent可以接受一个对象参数  



------------



### JS加载时间线
在js加载开始的时候，浏览器会记录js执行的这段过程。
1. 创建Document对象，开始解析web页面，解析HTML元素和他们的文本内容后添加Element对象和Text节点到文档中。这个阶段document.readyState = "loading"。
2. 遇到link外部css，创建线程加载，并继续解析文档。
3. 遇到script外部js，并且没有设置async，defer，浏览器加载，并阻塞，等待js加载完成并执行该脚本，然后继续解析文档
4. 遇到script外部js，并且设置有async，defer 浏览器创建线程加载，并继续解析文档，对于async属性的脚本，脚本加载完成后立即执行（异步禁止使用docuemnt.write（）会消除文档流）
5. 遇到img标签等，先正常解析dom结构，然后浏览器异步加载src，并继续解析文档
6. 当文档解析完成，document.readyState = "interactive"；
7. 文档解析完成后，所有设置有defer的脚本会按照顺序执行。
8. 当文档解析完成之后，document对象触发DOMContentLoaded事件,这也标志着程序执行从同步脚本执行阶段，转化为事件驱动阶段
9. 当所有saync的脚本加载完成并执行后，img等加载完成后，document.readyState = "complete"，window对象触发load事件
10. 从此，页面以异步响应方式处理用户输入，网络事件等。


------------



### Promise
所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。
三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败)
Promise对象有以下两个特点。
- 对象的状态不受外界影响。
- 一旦状态改变，就不会再变，任何时候都可以得到这个结果。

Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。
- resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；
- reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

Promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。


### JS文件的异步加载
1. defer 异步加载，但要等到dom文档全部解析完才会被执行。只有IE能用。
`<script type="text/javascript" src="tools.js" defer="defer"></script>`
js代码可以写在标签中或者外部脚本
2. async 异步加载，加载完就执行
`<script src="demo.js" aysnc="aysnc"></script>`
async只能加载外部脚本，不能把js写在script 标签里。

 **1和2 执行时也不阻塞页面**

3. 创建script，插入到DOM中，加载完毕后callBack


### 对象深克隆
1. 判断是不是原始值  typeof()、instanceof、toString、constructor
	万无一失用 toString
	是原始值就直接拷贝
	是引用值进行下一步
2. 判断是数组还是对象
	把引用值当作新的拷贝对象
3. 建立相应的数组或对象

### this 指向问题
this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，实际上this的最终指向的是那个调用它的对象。
如果一个函数中有this，这个函数中包含多个对象，尽管这个函数是被最外层的对象所调用，this指向的也只是它上一级的对象。
详细 https://www.cnblogs.com/pssp/p/5216085.html


### 区分 [ ]数组和{ }对象，本身是不知道的一个变量
1. 利用constructor
	[ ].constructor ->Array     { }.constructor ->Object
2. 利用 instanceof
	[ ] instanceof Array  -> true的是数组
	{ } instanceof Array  -> false的是对象
3. 利用toString
	Object.prototype.toString.call ( [ ] )； ->  Array
	Object.prototype.toString.call ( { } )； ->  Object
	

------------

### 跨域资源共享CORS
暂放
https://www.cnblogs.com/john-hwd/p/10509480.html
http://www.ruanyifeng.com/blog/2016/04/cors.html



### mouseover和mouseenter两个事件的区别
- mouseover(鼠标覆盖)
- mouseenter(鼠标进入)
- 二者的本质区别在于，mouseenter不会冒泡，简单的说，它不会被它本身的子元素的状态影响到。但是mouseover就会被它的子元素影响到，在触发子元素的时候，mouseover会冒泡触发它的父元素，(想要阻止mouseover的冒泡事件就用mouseenter)
- 共同点：当二者都没有子元素时，二者的行为是一致的，但是二者内部都包含子元素时，行为就不同了。

### 数组合并push和从concat的区别
1. push()是在原数组的基础上修改的，执行push()方法后原数组的值也会变；
concat()是先把原数组复制到一个新的数组，然后在新数组上进行操作，所以不会改变原数组的值。
2. 如果参数不是数组，不管参数个数有多少个，push()和concat()都会直接把参数添加到数组后；
如果参数是一个数组，push()就会直接把数组添加到原数组后，而concat()会把数组里的值取出来添加到原数组后。



