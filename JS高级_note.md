# JS高级

## 一、基础深入总结

#### 数据类型

##### 1.分类

​    基本（值）类型
​        String：任意字符串
​        Number：任意的数值
​        Boolean：true/false
​        undefined：undefined
​        null：null
​    对象（引用）类型
​        Object：任意对象
​        Function：函数，一种特别的对象（可以执行）
​        Array：数组，一种特别的对象（数值下标，内部数据是有序的）

##### 2.判断

​    typeof
​        可以判断 undefined 数值 字符串 布尔值 function
​        不能判断 null与object object与array
​    instanceof
​        判断对象的具体类型
​    ===（三个等号不会做数据转换）
​        可以判断undefined null

*实例：实例对象*
*类型：类型对象*

##### 3.undefined与null的区别

​	undefined代表定义未赋值
​	null代表定义并赋值了，只是值为null

##### 4.什么时候给变量赋值为null

​    初始赋值，表明将要赋值为对象
​    结束前赋值，为了让其成为垃圾对象，被垃圾回收器回收

##### 5.严格区别变量类型与数据类型

​    数据的类型
​        基本类型
​        对象类型
​    变量的类型（变量内存值的类型）
​        基本类型：保存的就是基本类型的数据
​        引用类型：保存的是地址值

```
<script>
    //1.基本
    //typeof返回数据类型的字符串表达
    var a;
    console.log(a , typeof a , typeof a === 'undefined' , a === undefined )
    //2.对象
    // 实例：实例对象
    // 类型：类型对象
    function Person(name , age){ //构造函数 类型
        this.name = age;
        this.age = age;
    }
    var p = new Person('admin' , 18) // 根据类型创建的实例对象
    
    var a;
    console.log(a);//undefined
    a = null;
    console.log(a);//null
    //起始
    var b = null;//初始赋值为null，表明将要赋值为对象
    //确定对象就赋值
    b = ['cc' , 22];
    //最后
    b = null;//让b指向的对象成为垃圾对象（被垃圾回收器回收）
    var c = {};
</script>
```

#### 数据、内存与变量

##### 1.什么是数据

​    存储在内存中代表特定信息的'东西'，本质上是电脑二进制数据
​    数据的特点：可传递，可运算
​    一切皆数据，函数也是数据
​    内存中所有操作的目标：数据
​        算术运算
​        逻辑运算
​        赋值
​        运行函数 （形参的本质是变量，实参的实质是数据）

##### 2.什么是内存

​    内存条通电后产生的可存储数据的空间（临时的）
​    内存产生和死亡: 内存条(电路版)==>通电==>产生内存空间==>存储数据==>处理数据==>断电==>内存空间和数据都消失
​    一块小内存的两个数据
​        内部存储的数据
​        地址值数据
​    内存分类
​        栈：全局变量/局部变量
​        堆：对象

##### 3.什么是变量

​    可变化的量，由变量名和变量值组成
​    每个变量都对应一块小内存，变量名用来查找对应的内存，变量值就是内存中保存的数据

##### 4.内存，数据，变量三者之间的关系

​    内存用来存储数据的空间
​    变量是内存的标识

```
<script>
    /*
    问题：var a = xxx , a内存中到底保存的是什么？ 
        xxx是基本数据，保存的就是这个数据
        xxx是对象，保存的是对象的地址值
        xxx是一个变量，保存的是xxx的内存内容（可能是基本数据，也可能是地址值）
    */
    var a = 3;
    var a = function (){
        
    };

    var b = 'abc';
    a = b;
    b = {};
    a = b;

    /*
    关于引用变量赋值问题
        2个引用变量指向同一个对象，通过一个变量修改对象内部数据，另一个变量看到的是修改之后的数据
        2个引用变量指向同一个对象，让其中一个引用变量指向另一个对象，另一个引用变量依然指向前一个对象    
    */
    var obj1 = {name:'cc'};
    var obj2 = obj1;
    obj1.name = 'dd';
    console.log(obj2.name);//'dd'

    /*
    问题：在js调用函数时传递变量参数时，是值传递还是引用传递
        理解1.都是值（基本/地址值）传递
        理解2.可能是值传递，也可能是引用传递（地址值）
    */
    var a = 3;
    function fn(a){
        a = a + 1;
    }
    fn(a);
    console.log(a);
    
    function fn2(obj){
        console.log(obj.name);
    }
    var obj = {name:'ccc'};
    fn2(obj);

    /*
    问题：JS引擎如何管理内存？
    1.内存生命周期
        分配小内存空间，得到它的使用权
        存储数据，可以反复进行操作
        释放小内存空间
    2.释放内存
        局部变量：函数执行完自动释放
        对象：成为垃圾对象==>垃圾回收器回收
    */
    var a = 3;
    var obj = {};
    obj = null;

    function fn(){
        var b = {};
    }

    fn()//b是自动释放，b所指向的对象是在后面的某个时刻由垃圾回收器回收
</script>
```
#### 对象

##### 1.什么是对象？

​    多个数据的封装体
​    用来保存多个数据的容器
​    一个对象代表现实世界中的一个事物，是该事物在编程中的抽象

##### 2.为什么要用对象？

​    统一管理多个数据

##### 3.对象的组成

​    属性：
​        属性名（字符串）和属性值（任意类型）组成
​        代表现实事物的状态数据
​    方法：
​        一种特别的属性（属性值是函数）
​        代表现实事物的行为数据

##### 4.如何访问对象内部数据？

​    .属性名 编码简单，但有时不能用
​    ['属性名']  编码复杂，但能够通用

```
<script>
    var obj = {
        name:'cc',
        age:22,
        setName:function(name){
            this.name = name;
        },
        setAge:function(){
            this.age = age;
        }
    }
    p.setName('Bob');
    p['setAge'](23);
    console.log(p.name , p['age']);
    /*
    问题：什么时候必须使用['属性名']的方式？
        1.属性名包含特殊字符：- 空格
        2.属性名不确定
    */
   var p = {};
   //1.给p对象添加一个属性：conten-type:text/json
   //p.content-type = 'text/json';//不能用
   p['content-type'] = 'text/json';
   //2.变量名不确定
   var propName = 'myAge';
   var value = 18;
   //p.propName = value;//不能用
   p[propName] = value;
   console.log(p[propName]);
</script>
```
#### 函数

##### 1.什么是函数？

​    实现特定功能的n条语句的封装体
​    只有函数是可以执行的，其他类型的数据不能执行

##### 2.为什么要用函数？

​    提高代码复用
​    便于阅读交流

##### 3.如何定义函数？

​    函数声明
​    表达式

##### 4.如何调用（执行）函数？

​    `test()`:直接调用
​    `obj.test()`:通过对象调用
​    `new test()`:new调用
​    `test.call/apply(obj)`:相当于obj.test，但这种是临时让test成为obj的方法进行调用

#### 回调函数

##### 1.什么函数才是回调函数？

​    ①编写者定义的
​    ②编写者没有调用
​    ③但最终它执行了
​    （和事件绑定了，事件发生之后就会执行）

##### 2.常见的回调函数？

​    dom事件回调函数==>发生事件的dom元素（实现与用户的交互）
​    定时器回调函数==>window

ajax请求回调函数（实现与后台的交互）
	生命周期回调函数

```
<script>
    document.getElementById('btn').onclick = function(){//dom事件回调函数
        alert(this.innerHTML);
    };
    //定时器
        //超时定时器
        //循环定时器
    setTimeout(function(){//定时器回调函数
        alert('是时候了')
    },2000);
</script>
```

#### IIFE

##### 1.理解

​    全称：Immediately-Invoked Function Expression 
​    立即执行函数表达式 别名：匿名函数自调用

##### 2.作用

​    隐藏内部实现
​    不会污染外部（全局）命名空间
​    用其来编码js模块

```
<script>
    (function(){//匿名函数自调用，等同于IIFE
        var a = 3;
        console.log(a + 3);
    })();
    (function(){
        var a = 1;
        function test(){
            console.log(++a);
        };
        window.$ = function(){//向外暴露了一个全局函数
            return {
                test: test
            };
        };
    })();
    $().test();//1.$是一个函数 2.$执行后返回的是一个对象
</script>
```

#### 函数中的this

##### 1.this是什么?

​	任何函数本质上都是通过某个对象来调用的,如果没有直接指定就是window
​	所有函数内部都有一个变量this
​	它的值是调用函数的当前对象

##### 2.如何确定this的值?

​	`test()`: window
​	`p.test()`: p
​	`new test()`: 新创建的对象
​	`	p.call(obj)`: obj

```
<script>
    function Person(color) {
        console.log(this)
        this.color = color;
        this.getColor = function () {
          console.log(this)
          return this.color;
        };
        this.setColor = function (color) {
          console.log(this)
          this.color = color;
        };
    }
    
    Person("red"); //this是谁? window
    
    var p = new Person("yellow"); //this是谁? p
    
    p.getColor(); //this是谁? p
    
    var obj = {};
    p.setColor.call(obj, "black"); //this是谁? obj
    
    var test = p.setColor;
    test(); //this是谁? window
    
    function fun1() {
        function fun2() {
          console.log(this);
        }
      
        fun2(); //this是谁? window
    }
    fun1();
</script>
```

## 二、函数高级

### 01 原型与原型链

#### 原型

##### 1.函数的prototype属性

​    每个函数都有一个prototype属性，它默认指向一个Object空对象（即称为：原型对象）
​    原型对象中有一个属性constructor，它指向函数对象

##### 2.给原型对象添加属性（一般都是方法）

​    作用：函数的所有实例对象自动拥有原型中的属性（方法）
​    

```
<script>
    console.log(Date.prototype,typeof Date.prototype);
    function Fun(){

    };
    
    console.log(Fun.prototype);//默认指向一个Object空对象（没有我们的属性）
    fn1.prototype;

    // 原型对象中有一个属性constructor, 它指向函数对象
    console.log(Date.prototype.constructor===Date)
    console.log(Fun.prototype.constructor===Fun)

    //给原型对象添加属性(一般是方法) ===>实例对象可以访问
    Fun.prototype.test = function () {
    console.log('test()')
  }
  var fun = new Fun()
  fun.test()
</script>
```

#### 显式原型与隐式原型

1. 每个函数function都有一个prototype，即显式原型(属性)

2. 每个实例对象都有一个__proto__，可称为隐式原型(属性)

3. 对象的隐式原型的值为其对应构造函数的显式原型的值

4. 内存结构(图)

    ![](C:\Users\阿堆\Desktop\study\typora\img\QQ浏览器截图20210602213956.png)

5. 总结:
    函数的prototype属性: 在定义函数时自动添加的, 默认值是一个空Object对象
    对象的__proto__属性: 创建对象时自动添加的, 默认值为构造函数的prototype属性值
    程序员能直接操作显式原型, 但不能直接操作隐式原型(ES6之前)

```
<script>
    //定义构造函数
    function Fn() {   // 内部语句: this.prototype = {}
  
    }
    // 1. 每个函数function都有一个prototype，即显式原型属性, 默认指向一个空的Object对象
    console.log(Fn.prototype)
    // 2. 每个实例对象都有一个__proto__，可称为隐式原型
    //创建实例对象
    var fn = new Fn()  // 内部语句: this.__proto__ = Fn.prototype
    console.log(fn.__proto__)
    // 3. 对象的隐式原型的值为其对应构造函数的显式原型的值
    console.log(Fn.prototype===fn.__proto__) // true
    //给原型添加方法
    Fn.prototype.test = function () {
      console.log('test()')
    }
    //通过实例调用原型的方法
    fn.test()
</script>
```
#### 原型链

##### 1.原型链（图解）

![](C:\Users\阿堆\Desktop\study\typora\img\QQ浏览器截图20210602203524.png)

访问一个对象的属性时
    先在自身属性中查找，找到返回
    如果没有，再沿着__proto__这条链向上查找，找到返回
    如果最终没找到，返回undefined
别名：隐式原型链
作用：查找对象的属性（方法）

##### 2.构造函数/原型/实体对象的关系（图解）

![](C:\Users\阿堆\Desktop\study\typora\img\构造函数 原型 实体对象的关系（图解）.png)

##### 3.构造函数/原型/实体对象的关系2（图解）

所有函数的__proto__都是一样的

##### 补充

1.函数的显式原型指向的对象：默认是空的Object实例对象（但Object不满足）
2.所有函数都是Function的实例（包含Function自身）
3.Object的原型对象是原型链尽头
4.一个实例的原型链上，可能存在多个原型对象

```
<script>
    function Fn(){
        this.test1 = function(){
            console.log('test1()');
        };
    };

    Fn.prototype.test2 = function(){
        console.log('test2()');
    };

    var fn = new Fn();

    fn.test1();
    fn.test2();
    console.log(fn.toString());
    fn.test3();
</script>
```

#### 原型链属性问题

1.读取对象的属性值时：会自动到原型链中查找
2.设置对象的属性值时：不会查找原型链，如果当前对象中没有此属性，直接添加此属性并设置其值
3.方法一般定义在原型中，属性一般通过构造函数定义在对象本身上

```
<script>
    function Fn(){
    };
    Fn.prototype.a = 'xxx';
    var fn1 = new Fn();
    console.log(fn1.a);
    var fn2 = new Fn();
    fn2.a = 'yyy';
    console.log(fn1.a,fn2.a);
</script>
```
#### 关于instanceof

##### 1.instanceof是如何判断的？

​    表达式：A instanceof B
​    如果B函数的显式原型对象在A对象的原型链上，返回true，否则返回false

##### 2.Function是通过new自己产生的实例

```
<script>
/*
案例1
*/
function Foo(){};
var f1 = new Foo();
console.log(f1 instanceof Foo);//true
console.log(f1 instanceof Object);//true

/*
案例2
*/
console.log(Object instanceof Function);//true
console.log(Object instanceof Object);//false
console.log(Function instanceof Function);//true
console.log(Function instanceof Object);//true

function Foo(){};
console.log(Object instanceof Foo);// 

</script>
```

### 02执行上下文与执行上下文栈

#### 变量提升与函数提升

##### 1.变量声明提升

​    通过var定义（声明）的变量，在定义语句之前就可以访问到
​    值：undefined

##### 2.函数声明提升

​    通过function声明的函数，在之前就可以直接调用
​    值：函数定义（对象）
​    先执行变量提升，再执行函数提升
​    函数提升优先级高于变量提升，且不会被同名变量声明覆盖，但是会被变量赋值后覆盖

```
<script>
/*
面试题：输出undefined
可以看作函数内是先var了一个a，再输出之后才赋值了4，所以输出为undefined
*/
var a = 3;
function fn(){
    console.log(a);
    var a = 4;
};
fn();
console.log(b);//undefined 变量提升
fn2()//可调用 函数提升
fn3()//不能 变量提升
var b = 3;
function fn2(){
    console.log('fn2()');
};
var fn3 = function(){
    console.log('fn3()');
};
</script>
```

#### 执行上下文

##### 1.代码分类（位置）

​    全局代码
​    函数（局部）代码

##### 2.全局执行上下文

​    在执行全局代码前将undefined确定为全局执行上下文
​    对全局数据进行预处理
​        var定义的群居变量==>undefined，添加为window的属性
​        function声明的全局函数==>赋值（fun），添加为window的方法
​        this==>赋值（window）
​    开始执行全局代码

##### 3.函数执行上下文

​    在调用函数，准备执行函数体之前，创建对于的函数执行上下文对象
​    对局部数据进行预处理
​        形参变量==>赋值（实参）==>添加为执行上下文的属性
​        arguments==>赋值（实参列表），添加为执行上下文的属性
​        function声明的函数==>赋值（fun），添加为执行上下文的方法
​        this==>赋值（调用函数的对象）
​    开始执行函数体代码
​    调用完之后会自动销毁，另外调用会是一个新的代码块

```
<script>
    console.log(a1, window.a1);
    window.a2();
    console.log(this);
    var a1 = 3;
    function a2(){
        console.log('a2()');
    };
    console.log(a1);
</script>
```

#### 执行上下文栈

1. 在全局代码执行前, JS引擎就会创建一个栈来存储管理所有的执行上下文对象
2. 在全局执行上下文(window)确定后, 将其添加到栈中(压栈)
3. 在函数执行上下文创建后, 将其添加到栈中(压栈)
4. 在当前函数执行完后,将栈顶的对象移除(出栈)
5. 当所有的代码执行完后, 栈中只剩下window

*栈：后进先出 队列：先进先出*
从设计原理上分析是因为先进的数据参与运算更深，后进的参与程度更浅

```
<script>
    var a = 10;
    var bar = function (x) {
      var b = 5;
      foo(x + b);
    };
    var foo = function (y) {
      var c = 5;
      console.log(a + c + y);
    };
    bar(10);
/*
1. 依次输出什么?
    gb:undefined
    fb:1
    fb:2
    fb:3
    fe:3
    fe:2
    fe:1
    ge:1

2. 整个过程中产生了几个执行上下文? 5
*/
    console.log('gb: '+ i);
    var i = 1;
    foo(1);
    function foo(i) {
      if (i == 4) {
        return;
      };
      console.log('fb:' + i);
      foo(i + 1); //递归调用: 在函数内部调用自己
      console.log('fe:' + i);
    };
    console.log('ge: ' + i);
</script>
```
### 03作用域与作用域链

#### 作用域

##### 1.理解

​    就是一块“地盘”，一个代码段所在的区域
​    它是静态的（相对于上下文对象），在编写代码时就确定了

##### 2.分类

​    全局作用域
​    函数作用域
​    没有块作用域（ES6有了）

##### 3.作用

​    隔离变量，不同作用域下同名变量不会有冲突

```
<script>
    var a = 10, b = 20;
    function fn(x){
        var a = 100, c = 300;
        console.log('fn()', a, b, c, x);
        function bar(x){
            var a = 1000, d = 400;
            console.log('bar()', a, b, c, d, x);
        };

        bar(100);
        bar(200);
    };
    fn(10);
</script>
```
#### 作用域与执行上下文

##### 1.区别1

​    全局作用域之外，每个函数都会创建自己的作用域，作用域在函数定义时就已经确定了。而不是在函数调用时
​    全局执行上下文环境是在全局作用域确定之后，js代码马上执行之前创建
​    函数执行上下文环境是在调用函数时，函数体代码执行之前创建

##### 2.区别2

​    作用域是静态的，只要函数定义好了就一直存在，且不会再变化
​    执行上下文是动态的，调用函数时创建，函数调用结束时就会自动释放

##### 3.联系

​    执行上下文（对象）是从属于所在的作用域
​    全局上下文环境==>全局作用域
​    函数上下文环境==>对于的函数使用域

```
<script>
    var a = 10, b = 20;
    function fn(x){
        var a = 100, c = 300;
        console.log('fn()', a, b, c, x);
        function bar(x){
            var a = 1000, d = 400;
            console.log('bar()', a, b, c, d, x);
        };

        bar(100);
        bar(200);
    };
    fn(10);
</script>
```
#### 作用域链

##### 1.理解

​    多个上下级关系得出作用域形成的链，它的方向是从下向上的（从内到外）
​    查找变量时就是沿着作用域链来查找的

##### 2.查找一个变量的查找规则

​    在当前作用域下的执行上下文中查找对应的属性，如果有直接返回，否则进入2
​    在上一级作用域的执行上下文中查找对应的属性，如果有直接返回，否则进入3
​    再次执行2的相同操作，知道全局作用域，如果还找不到就抛出找不到的异常

```
<script>
    var a = 1;
    function fn1(){
        var b = 2;
        function fn2(){
            var c = 3;
            console.log(c);//3
            console.log(b);//2
            console.log(a);//1
            console.log(d);//报错
        };
        fn2();
    };
    fn1();
</script>
```

### 04闭包

#### 循环遍历与监听

```
<body>
<button>test1</button>
<button>test2</button>
<button>test3</button>
<!-- 需求：点击某个按钮，提示“点击的是哪个按钮” -->
<script>
    var btns = document.getElementsByTagName('button');
    //遍历加监听
    /*for (var i = 0; i < btns.length; i++){
        var btn = btns[i];
        //将btn所对应的下标保存在btn上
        btn.index = i;
        btn.onclick = function(){
            alert('第'+(this.index+1)+'个');
        };
    };*/
    //利用闭包
    for (var i = 0; i < btns.length; i++){
        (function (i){
        var btn = btns[i];
        btn.onclick = function(){
            alert('第'+(i+1)+'个');
        };
    })(i);
    };
</script>
</body>
```
#### 理解闭包

##### 1.如何产生闭包？

​    当一个嵌套的内部（子）函数引用了嵌套的外部（父）函数的变量（函数）时，就产生了闭包

##### 2.闭包到底是什么？

​    使用chrome调试查看
​    理解一：闭包是嵌套的内部函数（绝大部分人）
​    理解二：包含被引用变量（函数）的对象（极少数人）
​    注意：闭包存在于嵌套的内部函数中

##### 3.产生闭包的条件？

​    函数嵌套
​    内部函数引用了外部函数的数据（变量/函数）
​    闭包需要内部函数调用

```
<script>
    function fn1(){
        var a = 2;
        function fn2(){//闭包需要内部函数调用
            console.log(a);
        };
        fn2();
    };
    fn1();
    
</script>
```

#### 常见的闭包

1.将函数作为另一个函数的返回值

2.将函数作为实参传递给另一个函数调用

```
<script>
    //1.将函数作为另一个函数的返回值
    function fn1(){
        var a = 2;
        function fn2(){
            a++;
            console.log(a);
        };
        return fn2;
    };
    var f = fn1();
    f();//3
    f();//4

    // 2.将函数作为实参传递给另一个函数调用
    function showDelay(msg, time){
        setTimeout(function(){
            alert(msg);
        },time);
    };
    showDelay('ccc', 2000);

</script>
```

#### 闭包的作用

1.使用函数内部的变量在函数执行完后，仍然存活在内存中（延长了局部变量的生命周期）
2.让函数外部可以操作（读写）到函数内部的数据（变量/函数）

**问题：**
1.函数执行完后，函数内部声明的局部变量是否还存在？
    *一般情况下是不存在，存在于闭包中的变量才可能存在*
2.在函数外部能直接访问函数内部的局部变量吗？
    *不能，但我们可以通过闭包让外部操作局部变量*

```
<script>
    function fn1(){
        var a = 2;
        function fn2(){
            a++;
            console.log(a);
        };

        function fn3(){
            a--;
            console.log(a);
        };
        return fn3;
    };
    var f = fn1();
    f();//1
    f();//0
</script>
```

#### 闭包的生命周期

1.产生：在嵌套的内部函数定义执行完成时就产生了
2.死亡：在嵌套的内部函数成为垃圾对象时

```
<script>
    function fn1(){
        var a = 2;
        function fn2(){
            a++;
            console.log(a);
        };
        return fn2;
    };
    var f = fn1();
    f();//3
    f();//4
    f = null//闭包死亡（包含闭包的函数对象成为了垃圾对象）
</script>
```

#### 闭包的应用

##### 闭包的应用：定义JS模块

​    具有特定功能的js文件
​    将所有的数据和功能都封装在一个函数内部（私有的）
​    只向外暴露一个包含n个方法的对象或函数
​    模块的使用者，只需要通过模块暴露的对象调用方法来实现对应的功能

```
<script src="myModule.js"></script>
<script>
    var module = myModule();
    module.doSomething();
    module.doOtherthing();
</script>
```

```
<script src="myModule2.js"></script>
<script>
    myModule2.doSomething();
    myModule2.doOtherthing();
</script>
```

#### 闭包的缺点及解决

##### 1.缺点

​    函数执行完后，函数内的局部变量没有释放，占用内存时间会变长
​    容易造成内存泄露（内存被白白占用）

##### 2.解决

​    能不用闭包就不用
​    及时释放

```
<script>
    function fn(){
        var arr = new Array[100000];
        function fn2(){
            console.log(arr.length);
        };
        return fn2;
    };
    var f = fn1();
    f();

    f = null//让内部函数成为垃圾对象-->回收闭包
</script>
```

## 三、面向对象高级

### 01对象创建模式

#### 方式一：Object构造函数模式

​    套路：先创建空Object对象，再动态添加属性/方法
​    适用场景：起始时不确定对象内部数据
​    问题：语句太多

```
<script>
    /*
    一个人：name:"Tom", age: 12
    */
    // 先创建空Object对象
    var p = new Object();
    p = {} //此时内部数据是不确定的
    // 再动态添加属性/方法
    p.name = 'Tom';
    p.age = 12;
    p.setName = function (name) {
    this.name = name;
    };

    //测试
    console.log(p.name, p.age);
    p.setName('Bob');
    console.log(p.name, p.age);
</script>
```
#### 方式二：对象字面量模式

​    套路：使用{}创建对象，同时指定属性/方法
​    适用场景：起始时对象内部数据是确定的
​    问题：如果创建多个对象，有重复代码

```
<script>
    var p = {
      name: 'Tom',
      age: 12,
      setName: function (name) {
        this.name = name;
      }
    }

    //测试
    console.log(p.name, p.age);
    p.setName('JACK');
    console.log(p.name, p.age);

    var p2 = {  //如果创建多个对象代码很重复
      name: 'Bob',
      age: 13,
      setName: function (name) {
        this.name = name;
      }
    }
</script>
```
#### 方式三：工厂模式

​    套路：通过工厂函数动态创建对象并返回
​    适用场景：需要创建多个对象
​    问题：对象没有一个具体的类型，都是Object类型

```
<script>
    function createPerson(name, age) { //返回一个对象的函数===>工厂函数
    var obj = {
    name: name,
    age: age,
    setName: function (name) {
      this.name = name;
    }
  }
  return obj;
}
// 创建2个人
var p1 = createPerson('Tom', 12);
var p2 = createPerson('Bob', 13);

// p1/p2是Object类型

function createStudent(name, price) {
  var obj = {
    name: name,
    price: price
  }
  return obj;
}
var s = createStudent('张三', 12000);
// s也是Object

</script>
```
#### 方式四：自定义构造函数模式

​    套路：自定义构造函数，通过new创建对象
​    适用场景：需要创建多个类型确定的对象
​    问题：每个对象都有相同的数据，浪费内存

```
<script>
    //定义类型
    function Person(name, age){
        this.name = name;
        this.age = age;
        this.setName = function (name){
            this.name = name;
        };
    };
    var p1 = new Person('Tom', 12);
    p1.setName('Jack');
    console.log(p1.name, p1.age);

    function Student (name, price){
        this.name = name;
        this.price = price;
    };
    var s = new Student('Bob', 13000);

    var p2 = new Person('JACK', 23);
    console.log(p1, p2);
</script>
```
#### 方式五：构造函数+原型的组合模式

​    套路：自定义构造函数，属性在函数中初始化，方法添加到原型上
​    适用场景：需要创建多个类型确定的对象

```
<script>
    function Person(name, age){//在构造函数中只初始化一般函数
        this.name = name;
        this.age = age;
    };
    Person.prototype.setName = function(name){
        this.name = name;
    };

    var p1 = new Person('Tom', 23);
    var p2 = new Person('Jack', 24);
    console.log(p1, p2);
</script>
```
### 02继承模式

#### 原型链继承

##### 方式1：原型链继承

1.套路
    1.定义父类型构造函数
    2.给父类型的原型添加方法
    3.定义子类型的构造函数
    4.创建父类型的对象赋值给子类型的原型
    5.将子类型原型的构造属性设置为子类型
    6.给子类型原型添加方法
    7.创建子类型的对象：可以调用父类型的方法
2.关键
    1.子类型的原型为父类型的一个实例对象

![](C:\Users\阿堆\Desktop\study\typora\img\原型链继承.png)

```
<script>
    //父类型
    function Supper(){
        this.supProp = 'Supper property';
    };
    Supper.prototype.showSupperProp = function(){
        console.log(this.supProp);
    };

    //子类型
    function Sub(){
        this.subProp = 'Sub property'
    };
    Sub.prototype.showSubProp = function(){
        console.log(this.subProp);
    };

    var sub = new Sub();
    sub.showSupperProp();
    //sub.toString();
    sub.showSubProp();

    console.log(sub.constructor);
    
</script>
```
借用构造函数继承

##### 方式2：借用构造函数继承（假的）

1.套路：
    1.定义父类型构造函数
    2.定义子类型构造函数
    3.在子类型构造函数中调用父类型构造
2.关键：
    1.在子类型构造函数中通用super()调用父类型构造函数

```
<script>
    function Person(name, age){
        this.name = name;
        this.age = age;
    };
    function Student(name, age, price){
        Person.call(this, name, age);//相当于：this.Person(name, age)
        this.price = price;
    };

    var s = new Student('Tom', 20, 14000);
    console.log(s.name, s.age, s.price);
</script>
```
组合继承

##### 方式3：原型链+借用构造函数的组合继承

1.利用原型链实现对父类型对象的方法继承
2.利用super()借用父类型构建函数初始化相同属性

```
<script>
    function Person(name, age){
        this.name = name;
        this.age = age;
    };
    Person.prototype.setName = function(name){
        this.name = name;
    };

    function Student(name, age, price){
        Person.call(this, name, age);//为了得到属性
        this.price = price;
    };
    Student.prototype = new Person();//为了能看到父类型的方法
    Student.prototype.constructor = Student;//修正constructor属性
    Student.prototype.setPrice = function(price){
        this.price = price;
    };

    var s = new Student('Tom', 24, 15000);
    s.setName('Bob');
    s.setPrice(16000);
    console.log(s.name, s.age, s.price);
</script>
```

## 四、线程机制与事件机制

#### 进程与线程

##### 1.进程

  程序的一次执行, 它占有一片独有的内存空间

##### 2.线程

CPU的基本（最小）调度单位, 是程序执行的一个完整流程，进程内的相互独立的执行单元

##### 3.进程与线程

​    应用程序必须运行在某个进程的某个线程上
​    一个进程中一般至少有一个运行的线程: 主线程，进程启动后自动创建
​    一个进程中也可以同时运行多个线程, 我们会说程序是多线程运行的
​    一个进程内的数据可以供其中的多个线程直接共享
​    多个进程之间的数据是不能直接共享的
​    线程池（thread pool）：保存多个线程对象的容器，实现线程对象的反复利用

##### 4.多进程与多线程

​    多线程运行：一个应用程序可以同时启动多个实例运行
​    多线程：在一个进程内，同时有多个线程运行
​    优点：有效提升CPU利用率
​    缺点：创建多线程开销，线程间切换开销，死锁与状态同步问题    
​    单线程：一个应用程序只能启动一个实例运行
​    优点：顺序编程简单易懂
​    缺点：效率低
​    JS是单线程运行的，但使用H5中的Web Workers可以多线程运行

##### 5.浏览器运行是单进程还是多进程?

​    有的是单进程
​    老版IE
​    有的是多进程
​    chrome
​    firefox
​    新版IE

##### 6.如何查看浏览器是否是多进程运行的呢?

​    任务管理器==>进程

##### 7.浏览器运行是单线程还是多线程?

​    都是多线程运行的

#### 浏览器内核

##### 1.什么是浏览器内核?

​    支持浏览器运行的最核心的程序

##### 2.不同的浏览器可能不太一样

​    Chrome: blink
​    Safari: webkit
​    firefox: Gecko
​    IE: Trident
​    360,搜狗等国内浏览器: Trident(有关安全性的就用它) + webkit

##### 3.内核由很多模块组成

​    js引擎模块 ：负责js程序的编译与运行
​    html,css文档解析模块 : 负责页面文本的解析
​    DOM/CSS模块 : 负责dom/css在内存中的相关处理
​    布局和渲染模块 : 负责页面的布局和效果的绘制
​						↑↑↑主线程

 	定时器模块 : 负责定时器的管理
	 网络请求模块 : 负责服务器请求(常规/Ajax)
 	DOM事件模块 : 负责事件的管理
						↑↑↑分线程

#### 定时器引发的思考

##### 1.定时器真是定时执行的吗?

​    定时器并不能保证真正定时执行
​    一般会延迟一丁点(可以接受), 也有可能延迟很长时间(不能接受)

##### 2.定时器回调函数是在分线程执行的吗?

​    在主线程执行的, js是单线程的

##### 3.定时器是如何实现的?

​    事件循环模型(后面讲)

```
<script>

  document.getElementById('btn').onclick = function () {
    var start = Date.now()
    console.log('启动定时器前...')
    setTimeout(function () {
      console.log('定时器执行了', Date.now()-start)
    }, 200)
    console.log('启动定时器后...')

    // 做一个长时间的工作
    for (var i = 0; i < 1000000000; i++) {

    }
  }
</script>
```

#### JS是单线程的

##### 1.如何证明js执行是单线程的?

​    setTimeout()的回调函数是在主线程执行的
​    定时器回调函数只有在运行栈中的代码全部执行完后才有可能执行

##### 2.为什么js要用单线程模式, 而不用多线程模式?

​    JavaScript的单线程，与它的用途有关。
​    作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。
​    这决定了它只能是单线程，否则会带来很复杂的同步问题

##### 3.代码的分类

​    初始化代码
​    回调代码

##### 4.JS引擎执行代码的基本流程

​    先执行初始化代码: 包含一些特别的代码   回调函数(异步执行)
​    设置定时器
​    绑定事件监听
​    发送ajax请求
​    后面在某个时刻才会执行回调代码

```
<script>
  setTimeout(function () {
    console.log('timeout 2222')
    alert('22222222')
  }, 2000)
  setTimeout(function () {
    console.log('timeout 1111')
    alert('1111111')
  }, 1000)
  setTimeout(function () {
    console.log('timeout() 00000')
  }, 0)
  function fn() {
    console.log('fn()')
  }
  fn()

  console.log('alert()之前')
  alert('------') //暂停当前主线程的执行, 同时暂停计时, 点击确定后, 恢复程序执行和计时
  console.log('alert()之后')
</script>
```

#### 事件循环模型

##### 1.所有代码分类

​    初始化执行代码(同步代码): 包含绑定dom事件监听, 设置定时器, 发送ajax请求的代码
​    回调执行代码(异步代码): 处理回调逻辑

##### 2.js引擎执行代码的基本流程:

​    初始化代码===>回调代码

##### 3.模型的2个重要组成部分

​    事件(定时器/DOM事件/Ajax)管理模块
​    回调队列

##### 4.模型的运转流程

​    执行初始化代码, 将事件回调函数交给对应模块管理
​    当事件发生时, 管理模块会将回调函数及其数据添加到回调列队中
​    只有当初始化代码执行完后(可能要一定时间), 才会遍历读取回调队列中的回调函数执行

![](C:\Users\阿堆\Desktop\study\typora\img\事件循环模型.png)

```
<script>
  function fn1() {
    console.log('fn1()')
  }
  fn1()
  document.getElementById('btn').onclick = function () {
    console.log('点击了btn')
  }
  setTimeout(function () {
    console.log('定时器执行了')
  }, 2000)
  function fn2() {
    console.log('fn2()')
  }
  fn2()
</script>
```
#### Web Workers

##### 1.H5规范提供了js分线程的实现, 取名为: Web Workers

​    我们可以将一些大计算量的代码交由web Worker运行而不冻结用户界面
​    **使用**：创建在分线程执行的js文件，在主线程中的js中发消息并设置回调

##### 2.相关API

​    Worker: 构造函数, 加载分线程执行的js文件
​    Worker.prototype.onmessage: 用于接收另一个线程的回调函数
​    Worker.prototype.postM0essage: 向另一个线程发送消息

##### 3.不足

​    子线程完全受主线程控制，worker内代码不能操作DOM(更新UI)，所以这个新标准并没有改变JS单线程的本质
​    不能跨域加载JS
​    不是每个浏览器都支持这个新特性

![](C:\Users\阿堆\Desktop\study\typora\img\H5 Web Workers(多线程).png)

```
<input type="text" placeholder="数值" id="number">
<button id="btn">计算</button>
<script>
  // 1 1 2 3 5 8    f(n) = f(n-1) + f(n-2)
  function fibonacci(n) {
    return n<=2 ? 1 : fibonacci(n-1) + fibonacci(n-2)  //递归调用
  }
  // console.log(fibonacci(7))
  var input = document.getElementById('number')
  document.getElementById('btn').onclick = function () {
    var number = input.value
    var result = fibonacci(number)
    alert(result)
  }

</script>
```

```
<input type="text" placeholder="数值" id="number">
<button id="btn">计算</button>
<script>
  var input = document.getElementById('number')
  document.getElementById('btn').onclick = function () {
    var number = input.value

    //创建一个Worker对象
    var worker = new Worker('worker.js')
    // 绑定接收消息的监听
    worker.onmessage = function (event) {
      console.log('主线程接收分线程返回的数据: '+event.data)
      alert(event.data)//event.date是固定的属性，获得发送来的数据
    }

    // 向分线程发送消息
    worker.postMessage(number)
    console.log('主线程向分线程发送数据: '+number)
  }
  // console.log(this) // window

</script>
```

//worker.js
```
function fibonacci(n) {
  return n<=2 ? 1 : fibonacci(n-1) + fibonacci(n-2)  //递归调用
}

console.log(this)
this.onmessage = function (event) {
  var number = event.data
  console.log('分线程接收到主线程发送的数据: '+number)
  //计算
  var result = fibonacci(number)
  postMessage(result)
  console.log('分线程向主线程返回数据: '+result)
  // alert(result)  alert是window的方法, 在分线程不能调用
  // 分线程中的全局对象不再是window, 所以在分线程中不可能更新界面
}
```

### 五、补充

#### 内存溢出与内存泄漏

##### 1.内存溢出

​    一种程序运行出现的错误
​    当程序运行需要的内存超过了剩余的内存时, 就抛出内存溢出的错误

##### 2.内存泄露

​    占用的内存没有及时释放
​    内存泄露积累多了就容易导致内存溢出
​    常见的内存泄露:
​        意外的全局变量
​        没有及时清理的计时器或回调函数
​        闭包

```
<script>
    // 1. 内存溢出
    var obj = {}
    for (var i = 0; i < 10000; i++) {
      obj[i] = new Array(10000000)
      console.log('-----')
    }
  
    // 2. 内存泄露
      // 意外的全局变量
    function fn() {
      a = new Array(10000000)
      console.log(a)
    }
    fn()
  
     // 没有及时清理的计时器或回调函数
    var intervalId = setInterval(function () { //启动循环定时器后不清理
      console.log('----')
    }, 1000)
  
    // clearInterval(intervalId)
  
      // 闭包
    function fn1() {
      var a = 4
      function fn2() {
        console.log(++a)
      }
      return fn2
    }
    var f = fn1()
    f()
  
    // f = null
  
</script>
```