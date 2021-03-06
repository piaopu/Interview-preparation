# ES6

### ES6新特性
- Default Parameters（默认参数） in ES6
- Template Literals （模板文本）in ES6
- Multi-line Strings （多行字符串）in ES6
- Destructuring Assignment （解构赋值）in ES6
- Enhanced Object Literals （增强的对象文本）in ES6
- Arrow Functions （箭头函数）in ES6
- Promises in ES6
- Block-Scoped Constructs Let and Const（块作用域构造Let and Const）
- Classes（类） in ES6
- Modules（模块） in ES6


### let命令
#### 不存在变量提升
在未声明变量时使用变量，会报错

#### 暂时性死区
如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。
在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）
“暂时性死区”也意味着typeof不再是一个百分之百安全的操作。不再是undefined，而是报错ReferenceError
##### ES6增加暂时性死区这一特性，主要是为了减少运行时错误，防止声明之前就使用

#### 不允许重复声明
let不允许在相同作用域内，重复声明同一个变量。


------------



### 箭头函数
#### 箭头函数适用场景
箭头函数适合于无复杂逻辑或者无副作用的纯函数场景下，例如：用在 map、reduce、filter 的回调函数定义中

#### 箭头函数使用注意点
1. 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
2. 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
3. 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
4. 不可以使用yield命令，因此箭头函数不能用作 Generator 函数。
5. 上面四点中，第一点尤其值得注意。this对象的指向是可变的，但是在箭头函数中，它是固定的。

#### 不适用场合
第一个场合是定义对象的方法，且该方法内部包括this。
第二个场合是需要动态this的时候，也不应使用箭头函数。

#### 回调函数
我们先来看看回调的英文定义：A callback is a function that is passed as an argument to another function and is executed after its parent function has completed。

字面上的理解，回调函数就是一个参数，将这个函数作为参数传到另一个函数里面，当那个函数执行完之后，再执行传进去的这个函数。这个过程就叫做回调。

### 线程与进程
### 进程
- 程序的一次执行, 它占有一片独有的内存空间
- 可以通过windows任务管理器查看进程
#### 线程
- 是进程内的一个独立执行单元
- 是程序执行的一个完整流程
- 是CPU的最小的调度单元
#### 关系
- 一个进程至少有一个线程(主)
- 一个进程中也可以同时运行多个线程, 我们会说程序是多线程运行的
- 一个进程内的数据可以供其中的多个线程直接共享
- 多个进程之间的数据是不能直接共享的
- 程序是在某个进程中的某个线程执行的



### 同步与异步
#### 同步任务
同步任务是指在主线程上排队执行的任务，只有前一个任务执行完毕，才能继续执行下一个任务，当我们打开网站时，网站的渲染过程，比如元素的渲染，其实就是一个同步任务

#### 异步任务
异步任务是指不进入主线程，而进入任务队列的任务，只有任务队列通知主线程，某个异步任务可以执行了，该任务才会进入主线程，当我们打开网站时，像图片的加载，音乐的加载，其实就是一个异步任务


### 异步编程
JS引擎是基于单线程事件循环的概念构建的，同一时刻只允许一个代码块在执行。

异步编程的六种方案：
1. 回调函数
2. 事件监听
3. 发布订阅
4. Promise对象
5. 生成器Generators/ yield
6. async + await

详细 https://blog.csdn.net/howgod/article/details/93978297

### Promise
所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。
三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）

Promise对象有以下两个特点
（1）对象的状态不受外界影响。
（2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。

Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。
- resolve函数的作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；
- reject函数的作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

Promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数。










