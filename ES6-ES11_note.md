#### 什么是ECMA

​	ECMA（European Computer Manufacturers Association）中文名称为欧洲计算机制造商协会，这个组织的目标是评估、开发和认可电信和计算机标准。1994 年后该组织改名为 Ecma 国际。

#### 什么是 ECMAScript

​	ECMAScript 是由 Ecma 国际通过 ECMA-262 标准化的脚本程序设计语言。
什么是 ECMA-262
​	Ecma 国际制定了许多标准，而 ECMA-262 只是其中的一个，所有标准列表查看
http://www.ecma-international.org/publications/standards/Standard.htm

### ES6

#### let

let 关键字用来声明变量，使用 let 声明的变量有几个特点：
	1) 不允许重复声明
	2) 块儿级作用域
	3) 不存在变量提升
	4) 不影响作用域链
*应用场景：以后声明变量使用 let 就对了*

```
<script>
    //声明变量
    let a;
    let b,c,d;
    let e = 100;
    let f = 500, g = 'ccc', h = [];

    //1.变量不能重复声明
    let star = 'chenchen';
    let star = '丢堆';//报错，显示已被定义

    /*
    2.块级作用域
    ES5中有三种作用域：全局，函数，eval(ES5严格模式)
    ES6中引入了块级作用域，let声明的变量就是块级作用域，变量只在代码块内有效
    块级作用域还包括if else while for这些{}代码块
    */
    {
        let boy = 'xiaochen';
    }
    console.log(boy);//报错，未定义
    /*
    3.不存在变量提升
    */
    console.log(you);//不会报错，但会返回undefined
    var you = 'baby';

    console.log(me);//直接报错，不允许在变量声明之前使用这个变量
    let me = 'baby';
    /*
    4.不影响作用域链
    */
    {
        let boy = 'xiaochen';
        function fn(){
                console.log(boy);
            }
            fn();
    }
</script>
```

##### let实践练习：

```
<body>
    <div class="container">
        <h2 class="page-header">点击切换颜色</h2>
        <div class="item"></div>
        <div class="item"></div>
        <div class="item"></div>
    </div>
<script>
    let items = document.getElementsByClassName('item');

    for(let i = 0; i<items.length; i++){
        items[i].onclick = function(){
            //修改当前元素的背景颜色
            // this.style.background = 'pink';
            items[i].style.background = 'pink';
        }
    }
</script>
</body>
```

#### const

const 关键字用来声明常量，const 声明有以下特点
	1) 声明必须赋初始值
	2) 标识符一般为大写
	3) 不允许重复声明
	4) 值不允许修改
	5) 块儿级作用域

**注意: 对象属性修改和数组元素变化不会出发 const 错误**
*应用场景：声明对象类型使用 const ，非对象类型声明选择 let*
*声明数组和对象时，用const声明比较稳妥，避免误操作修改数据里面的值*

#### 解构赋值

ES6 允许按照一定模式从数组和对象中提取值，对变量进行赋值
这被成为解构赋值，方便我们写代码，简化书写量

*属性解构用得比较少，方法解构用得比较多*

```
<script>
    //1.数组的解构
    const XI = ['唐僧','孙悟空','猪八戒','沙和尚'];
    let [tang,sun,zhu,sha] = XI;
    console.log(tang);
    console.log(sun);
    console.log(zhu);
    console.log(sha);

    //2.对象的解构
    const SUN = {
        name:'孙悟空',
        age:'18',
        zhanji:function(){
            console.log("三打白骨精");
        }
    };

    // let {name, age, zhanji} = SUN;
    // console.log(name);
    // console.log(age);
    // console.log(zhanji);

    let {zhanji} = SUN;
    zhanji();//这样解构可以避免重复性代码
</script>
```

#### 模板字符串

模板字符串（template string）是增强版的字符串，用反引号 ` 标识，特点：
	1) 字符串中可以出现换行符
	2) 可以使用 ``${xxx}`` 形式输出变量

```
<script>
    //ES6 引入新的什么字符串的方式 ``
    //1.声明
    // let str = `我也是字符串`;

    //2.内容中可以直接出现换行符
    let str =`<ul>
            <li>唐僧</li>
            <li>孙悟空</li>
            <li>猪八戒</li>
            <li>沙和尚</li>
            </ul>`;
    //3.变量拼接
    //${}是拼接的固定格式
    let shiFu = '唐僧';
    let out = `${shiFu}是取经四人组里面最厉害的`;
    console.log(out);
</script>
```

#### 简化对象写法

ES6 允许在大括号里面直接写入变量和函数，作为对象的属性和方法。
这样的书写更加简洁

```
<script>
    let name = 'chenchen';
    let change = function(){
        console.log('你真的很不错！');
    };

    const BOY = {
        name,
        change,
        improve(){
            console.log("真的真的很不错！")
        }
    };

    console.log(BOY);
</script>
```

#### 箭头函数

ES6 允许使用 箭头（`=>`）定义函数
    特性
    1.this 是静态的
        this 始终指向函数声明时所在作用域下的 this 的值
    2.不能作为构造函数实例化对象
    3.不能使用arguments变量
    4.箭头函数的简写
        ①省略小括号 当形参有且只有一个的时候
        ②省略花括号 当代码体只有一条语句的时候，此时 return 必须省略，而且语句的执行结果就是函数的返回值

*箭头函数适合与 this 无关的回调，定时器，数组的方法回调*
*箭头函数不适合与 this 有关的回调，DOM元素的事件回调，对象的方法*

```
<script>
    let fn1 = function(){

    }
    //箭头函数声明
    let fn2 = (a,b) => {
        return a + b;
    }
    //调用函数
    let result = fn2(1,2);
    console.log(result);//3

    //1.this是静态的
    function getName(){
        console.log(this.name);
    }
    let getName2 = () => {
        console.log(this.name);
    }

    //设置 window 对象的 name 属性
    window.name = 'chenchen';
    const BOY = {
        name:"丢堆"
    }

    //直接调用
    getName();//chenchen
    getName2();//chenchen

    //call方法调用
    getName.call(BOY);//丢堆
    getName2.call(BOY);//chenchen

    //2.不能作为构造函数实例化对象
    let Person = (name, age) => {
        this.name = name;
        this.age = age;
    }

    let me = new Person('sun', 18);
    console.log(me);//报错 Person并不是一个构造器

    //3.不能使用 arguments 变量
    let fn3 = () => {
        console.log(arguments);
    }
    fn3(1, 2, 3);//报错 这个变量没有定义

    //4.箭头函数的简写
        //省略小括号
        let add = (n) => {
            return n + n;
        }
        console.log(add(9));//18
        //省略花括号
        let pow = (n) => n * n;

        console.log(pow(9));//81
</script>
```

##### 箭头函数实践：

```
<script>
    //需求1 点击 div 2s 后颜色变成粉色
    let ad = document.getElementById('ad');

    ad.addEventListener("click",function(){
        //保存 this 的值
        //let _this = this;
        //定时器
        setTimeout(() => {
            //修改背景颜色 this
            //_this.style.background = 'pink';
            this.style.background = 'pink';
        },2000);
    });
    
    //需求2 从数组中返回偶数的元素
    const ARR = [1,6,9,10,100,25];
    // const RESULT = ARR.filter(function(item){
    //     if(item % 2 === 0){
    //         return true;
    //     }else{
    //         return false;
    //     }
    // });
    // console.log(RESULT);

    const RESULT = ARR.filter(item => item % 2 === 0);
    
    console.log(RESULT);
    
</script>
```

#### 函数参数默认值

ES6 允许给函数参数赋值初始值
    1.形参初始值 具有默认值的参数，一般位置要靠后（潜规则）
    2.与解构赋值结合 如果参数未传，则会用默认值

```
<script>
    //1.形参初始值
    function add(a,b,c=10){
        return a + b + c;
    }
    let result = add(1,2);
    console.log(result);
    //2.与解构赋值结合
    function connect({host="127.0.0.1", username, password, port}){
       console.log(host)
       console.log(username)
       console.log(password)
       console.log(port)
    }
    connect({
        host: 'localhost',
        username: 'root',
        password: 'root',
        port: 3306
    });
</script>
```

#### rest参数

ES6引入 rest 参数，用于获取函数的实参，用来代替 arguments，是ES6获取实参的方式
	*rest参数必须要放到参数最后（语法限制）*

```
<script>
    //ES5的获取方式
    function data(){
        console.log(arguments);
    }
    data('孙悟空','唐僧','猪八戒');
    
    //ES6的rest参数
    function data(...args){
        console.log(args);
    }
    data('孙悟空','唐僧','猪八戒');

</script>
```

#### 扩展运算符

​    `...` 扩展运算符能将 数组 转换为逗号分隔的 参数序列
​    声明一个数组 `...`

```
<script>
    const XI = ['孙悟空','唐僧','猪八戒'];// => '孙悟空','唐僧','猪八戒'
    
    //声明一个函数
    function xiyouji(){
        console.log(arguments);
    }

    xiyouji(...XI);//等于 xiyouji('孙悟空','唐僧','猪八戒')
    
</script>
```

##### 扩展运算符应用

​    1.数组的合并
​    2.数组的克隆
​        如果拷贝的元素中有引用类型数据的话，那也是一个浅拷贝
​        浅拷贝：即拷贝变量所存的值，如果是引用变量，那拷贝的就是它里面的地址
​    3.将伪数组转化为真正的数组

```
<script>
    const XI = ['孙悟空','唐僧'];
    const YAO = ['白骨精','黑风怪'];
    //数组合并
    const SAN = [...XI, ...YAO];
    console.log(SAN);

    //数组克隆
    const XI1 = [...XI];
    console.log(XI1);
    //数组转换
    const DIVS = document.querySelectorAll('div');
    const DIVARR = [...DIVS];
    console.log(DIVARR);

</script>
```

#### symbol

ES6 引入了一种新的原始数据类型 Symbol，表示独一无二的值。是一种描述字符串，可以更好地解数据作用。
它是JavaScript 语言的第七种数据类型，是一种类似于字符串的数据类型。
Symbol 特点
    1) Symbol 的值是唯一的，用来解决命名冲突的问题
    2) Symbol 值不能与其他数据进行运算
    3) Symbol 定义的对象属性不能使用 `for…in` 循环遍历，但是可以使用`Reflect.ownKeys` 来获取对象的所有键名

```
<script>
    //创建Symbol
    let s = Symbol();
    let s2 = Symbol('丢堆'); //此时为函数
    //Symbol.for 创建
    let s3 = Symbol.for('丢堆');//此时为对象

    //不能与其他数据进行运算
    let result = s + 100;//报错
    let result = s > 100;//报错
    let result = s + s;//报错
</script>
```

##### Symbol 创建对象属性

```
<script>
    //向对象中添加方法 up down
    let game = {
        name:'俄罗斯方块',
        up: function(){},
        down: function(){}
    }

    //声明一个对象
    //第一种添加方式
    let methods = {
        up: Symbol(),
        down: Symbol()
    }

    game[methods.up] = function(){
        console.log("我可以改变形状");
    }

    game[methods.down] = function(){
        console.log("我可以快速下降");
    }

    console.log(game);

    //第二种添加方式
    let youxi = {
            name:"狼人杀",
            [Symbol('say')]: function(){
                console.log("我可以发言");
            },
            [Symbol('zibao')]: function(){
                console.log('我可以自爆');
            }
        }

    console.log(youxi);
</script>
```

##### Symbol内置属性

除了定义自己使用的 Symbol 值以外，ES6 还提供了11个内置的Symbol值，
指向语言内部使用的方法。可以称这些方法为魔术方法，因为它们会在特定的场景下自动执行。

`Symbol.hasInstance` 
    当其他对象使用 instanceof 运算符，判断是否为该对象的实例时，会调用这个方法
`Symbol.isConcatSpreadable`
    对象的 Symbol.isConcatSpreadable 属性等于的是一个布尔值，
    表示该对象用于 Array.prototype.concat()时，是否可以展开。
`Symbol.species` 
    创建衍生对象时，会使用该属性
`Symbol.match`
    当执行 str.match(myObject) 时，如果该属性存在，会调用它，返回该方法的返回值。
`Symbol.replace`
    当该对象被 str.replace(myObject)方法调用时，会返回该方法的返回值。
`Symbol.search`
    当该对象被 str. search (myObject)方法调用时，会返回该方法的返回值。
`Symbol.split`
    当该对象被 str. split (myObject)方法调用时，会返回该方法的返回值。
`Symbol.iterator`
    对象进行 for...of 循环时，会调用 Symbol.iterator 方法，返回该对象的默认遍历器
`Symbol.toPrimitive`
    该对象被转为原始类型的值时，会调用这个方法，返回该对象对应的原始类型值。
Symbol. `toStringTag`
    在该对象上面调用 toString 方法时，返回该方法的返回值
`Symbol.unscopables` 
    该对象指定了使用 with 关键字时，哪些属性会被 with环境排除。

```
<script>
    class Person{
        static [Symbol.hasInstance](param){
            console.log(param);
            console.log("我被用来检测类型了");
        }
    }

    let o = {};

    console.log(o instanceof Person);
</script>
```

#### 迭代器

迭代器又称遍历器（Iterator），就是一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。
任何数据结构只要部署 Iterator 接口（对象里面的一个属性，属性名字为Symbol.iterator），就可以完成遍历操作。

1) ES6 创造了一种新的遍历命令 `for...of` 循环，Iterator 接口主要供 `for...of` 消费
2) 原生具备 iterator 接口的数据(可用 `for of` 遍历)
    a) Array
    b) Arguments
    c) Set
    d) Map
    e) String
    f) TypedArray
    g) NodeList
3) 工作原理
    a) 创建一个指针对象，指向当前数据结构的起始位置
    b) 第一次调用对象的 next 方法，指针自动指向数据结构的第一个成员
    c) 接下来不断调用 next 方法，指针一直往后移动，直到指向最后一个成员
    d) 每调用 next 方法返回一个包含 value 和 done 属性的对象
注：需要自定义遍历数据的时候，要想到迭代器

```
<script>
    //声明一个数组
    const XI = ['孙悟空','唐僧','猪八戒','沙和尚'];

    /*
    使用 for...of 遍历数组
    for...of 语句创建一个循环来迭代可迭代的对象。在 ES6 中引入的 for...of 循环，以替代 for...in 和 forEach() ，
    并支持新的迭代协议。for...of 允许你遍历 Arrays（数组）, Strings（字符串）, Maps（映射）, Sets（集合）等可迭代的数据结构等。
    for in 保存的是键名，for of 保存的是键值
    */
    for(let v of XI){
        console.log(v);
    }

    let iterator = XI[Symbol.iterator]();

    //调用对象的next方法
    console.log(iterator.next());
    console.log(iterator.next());
    console.log(iterator.next());
    console.log(iterator.next());
    console.log(iterator.next());
</script>
```

##### 迭代器应用

```
<script>
    //声明一个对象
    const XI = {
        name:"师徒四人",
        person:[
            '孙悟空',
            '唐僧',
            '猪八戒',
            '沙和尚'
        ],
        [Symbol.iterator](){
            //索引变量
            let index = 0;
            let _this = this;
            return{
                next:function(){
                    if(index < _this.person.length){
                        const result = {value:_this.person[index], done:false};
                        //让下标自增
                        index++;
                        return result;
                    }else{
                        return {value: undefined, done: true};
                    }
                }
            };
        }
    }

    //遍历这个对象
    for(let v of XI){
        console.log(v);
    }
</script>
```

#### 生成器函数

生成器函数是ES6提供的一种异步编程解决方案，语法行为与传统函数完全不同
生成器其实就是一个特殊的函数，用于进行异步编程（之前用的是纯回调函数 node fs ajax mongodb）

```
<script>
    //特殊的声明方式
    //yield 函数代码的分隔符，把函数代码切分成了几块
    function * gen(){
        
        yield '孙悟空';
        
        yield '唐僧';
        
        yield '猪八戒';
        
    }

    // let iterator = gen();
    //特殊的执行方式
    // iterator.next();

    //遍历
    for(let v of gen()){
        console.log(v);
    }
</script>
```

##### 生成器函数参数

```
<script>
    function * gen(arg){
        console.log(arg);
        let one = yield 111;
        console.log(one);
        let two = yield 222;
        console.log(two);
        let three = yield 333;
        console.log(three);
    }

    //执行获取迭代器对象
    let iterator = gen('AAA');
    console.log(iterator.next());
    //next方法可以传入实参 这个实参会作为上一个yield语句的返回结果
    console.log(iterator.next('BBB'));
    console.log(iterator.next('CCC'));
    console.log(iterator.next('DDD'));
</script>
```

##### 生成器函数实例1

```
<script>
    /*
    异步编程 JS本身是单线程的，所以很多操作都是异步编程完成的，如文件操作、网络操作（ajax，request）、数据库操作
    需求：1s 后控制台输出 111  2s后输出 222  3s后输出 333
    */
    //回调地狱
    // setTimeout(() => {
    //     console.log(111);
    //     setTimeout(() => {
    //         console.log(222);
    //         setTimeout(() => {
    //             console.log(333);
    //         }, 3000);
    //     }, 2000);
    // }, 1000);

    function one(){
        setTimeout(() => {
            console.log(111);
            iterator.next();
        }, 1000);
    }

    function two(){
        setTimeout(() => {
            console.log(222);
            iterator.next();
        }, 2000);
    }

    function three(){
        setTimeout(() => {
            console.log(333);
            iterator.next();
        }, 3000);
    }

    function * gen(){
        yield one();
        yield two();
        yield three();
    }

    //调用生成器函数
    let iterator = gen();
    iterator.next();
</script>
```

##### 生成器函数实例2

```
<script>
    //模拟获取：用户数据 订单数据 商品数据
    function getUsers(){
        setTimeout(() => {
            let data = '用户数据';
            //调用next方法，并且将数据传入
            iterator.next(data);
        }, 1000);
    }
    
    function getOrders(){
        setTimeout(() => {
            let data = '订单数据';
            iterator.next(data);
        }, 1000);
    }

    function getGoods(){
        setTimeout(() => {
            let data = '商品数据';
            iterator.next(data);
        }, 1000);
    }

    function * gen(){
        let users = yield getUsers();
        console.log(users);
        let orders = yield getOrders();
        console.log(orders);
        let goods = yield getGoods();
        console.log(goods);
    }

    //调用生成器函数
    let iterator = gen();
    iterator.next();
</script>
```

#### Promise基本语法

Promise 是 ES6 引入的异步编程的新解决方案。语法上 Promise 是一个构造函数，
用来封装异步操作并可以获取其成功或失败的结果。
	1) Promise 构造函数: Promise (excutor) {}
	2) Promise.prototype.then 方法
	3) Promise.prototype.catch 方法

```
<script>
    //实例化 Promise 对象
    const P = new Promise(function(resolve, reject){
        setTimeout(function(){
            // let data = '数据库中的用户数据';
            // //调用resolve
            // resolve(data);

            let err = '数据读取失败';
            reject(err);
        },1000);
    });

    /*
    调用 promise 对象的then方法
    当异步代码内调用了resolve，则表示成功了，则P.then 会自动调用第一个回调函数
    当异步代码内调用了reject，则表示失败了，则P.then 会自动调用第二个回调函数
    通过这种方式将异步任务封装在了一个Promise对象里面，且通过resolve和reject这两个函数来改变他的状态，之后再调用then方法中的回调
    */
    P.then(function(value){
        console.log(value);
    },function(reason){
        console.error(reason);
    })
</script>
```
##### Promise读取文件.js

```
//1.引入 fs模块
const fs = require('fs');

//2.调用方法读取文件
// fs.readFile('./resources/为学.md',(err, data)=>{
//     //如果失败，则抛出错误
//     if(err) throw err;
//     //如果没出错，则输出内容
//     console.log(data.toString());
// });

//3.使用 Promise 封装
const P = new Promise(function(resolve, reject){
    fs.readFile("./resources/为学.md",(err, data)=>{
        //判断如果失败
        if(err) reject(err);
        //如果成功
        resolve(data);
    });
});

P.then(function(value){
    console.log(value.toString());
}, function(reason){
    console.log("读取失败！");
});
```

##### Promise封装AJAX

```
    <script>
        //接口地址： https://api.apiopen.top/getJoke

        const P = new Promise((resolve, reject) => {
            //1.创建对象
            const XHR = new XMLHttpRequest();

            //2.初始化
            XHR.open("GET", "https://api.apiopen.top/getJoke");

            //3.发送
            XHR.send();

            //4.绑定事件，处理响应结果
            XHR.onreadystatechange = function () {
                //判断
                if (XHR.readyState === 4) {
                    //判断响应状态码 200-299
                    if (XHR.status >= 200 && XHR.status < 300) {
                        //表示成功
                        resolve(XHR.response);
                    } else {
                        //如果失败
                        reject(XHR.status);
                    }
                }
            }
        })
    
        //指定回调
        P.then(function(value){
            console.log(value);
        }, function(reason){
            console.error(reason);
        })
    </script>
```

##### Promise then方法

调用 then 方法  then方法的返回结果是 Promise 对象，对象状态由回调函数的执行结果决定
	1.如果回调函数返回的结果是 非promise类型的属性，状态为成功，返回值为对象的成功值
	2.如果回调函数返回的结果是 promise对象，内部promise返回的状态决定then方法返回promise的对象状态
	3.如果抛出错误，也是失败的promise状态，错误的值就是抛出的值

*由于then方法的这个特性，使得它可以链式调用*

```
<script>
    //创建 promise 对象
    const P = new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve('用户数据');
        }, 1000)
    });

    const result = P.then(value =>{
        console.log(value);
        //1.非promise类型的属性
        //return 'ccc';
        //2.是promise对象
        // return new Promise((resolve, reject)=>{
        //     resolve('ok');
        // });
        //3.抛出错误
        //throw new Error('出错！');
    }, reason =>{
        console.error(reason);
    });

    //链式调用 可以回避回调地狱的问题
    p.then(value=>{

    },reason=>{

    }).then(value=>{

    },reason=>{

    });
    console.log(result);//"resolved"
    
</script>
```

##### Promise catch方法

```
<script>
    const P = new Promise((resolve, reject)=>{
        setTimeout(()=>{
            //设置 p 对象的状态为失败，并设置失败的值
            reject("出错！");
        }, 1000);
    });

    // p.then(function(value){}, function(reason){
    //     console.error(reason);
    // });
        
    p.catch(function(reason){
        console.warn(reason);
    });
</script>
```

##### Promise实践 读取多个文件.js

```
//引入 fs 模块
const fs = require("fs");

// fs.readFile('./resources/为学.md', (err, data1)=>{
//     fs.readFile('./resources/插秧诗.md', (err, data2)=>{
//         fs.readFile('./resources/观书有感.md', (err, data3)=>{
//             let result = data1 + '\r\n' +data2  +'\r\n'+ data3;
//             console.log(result);
//         });
//     });
// });

//使用 promise 实现
const p = new Promise((resolve, reject) => {
    fs.readFile("./resources/为学.md", (err, data) => {
        resolve(data);
    });
});

p.then(value => {
    return new Promise((resolve, reject) => {
        fs.readFile("./resources/插秧诗.md", (err, data) => {
            resolve([value, data]);
        });
    });
}).then(value => {
    return new Promise((resolve, reject) => {
        fs.readFile("./resources/观书有感.md", (err, data) => {
            //压入
            value.push(data);
            resolve(value);
        });
    })
}).then(value => {
    console.log(value.join('\r\n'));
});
```

#### set

ES6 提供了新的数据结构 Set（集合）。它类似于数组，但成员的值都是唯一的，
集合实现了 iterator 接口，所以可以使用『扩展运算符』和『for…of…』进行遍历，
集合的属性和方法：
	1) size 返回集合的元素个数
	2) add 增加一个新元素，返回当前集合
	3) delete 删除元素，返回 boolean 值
	4) has 检测集合中是否包含某个元素，返回 boolean 值
	5) clear 清空集合，返回 undefined

```
<script>
    //声明一个set
    let s = new Set();
    let s2 = new Set(['壹','贰','叁','肆','壹']);
    
    //元素个数
    console.log(s2.size);
    //添加新的元素
    s2.add('伍');
    //删除元素
    s2.delete('肆');
    //检测
    console.log(s2.has('壹'));
    //清空
    s2.clear();
    // console.log(s2, typeof s);

    for(let v of s2){
        console.log(v);
    }

</script>
```

##### set实践

```
<script>
    let arr = [1,2,3,4,5,4,3,2,1];
    //1.数组去重
    // let result = [...new Set(arr)];
    // console.log(result);
    //2.交集
    let arr2 = [4,5,6,5,6];
    // let result = [...new Set(arr)].filter(item =>{
    //     let s2 = new Set(arr2);// 4 5 6
    //     if(s2.has(item)){
    //         return true;
    //     }else{
    //         return false;
    //     }
    // });
    // console.log(result);
    
    // let result = [...new Set(arr)].filter(item => new Set(arr2).has(item));
    // console.log(result);
    //3.并集
    // let union = [...new Set([...arr, ...arr2])];
    // console.log(union);
    //4.差集
    let diff = [...new Set(arr)].filter(item => !(new Set(arr2).has(item)));
    console.log(diff);
</script>
```

#### Map的介绍与API

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。
但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。
Map 也实现了iterator 接口，所以可以使用『扩展运算符』和『for…of…』进行遍历。
Map 的属性和方法：
	1) size 返回 Map 的元素个数
	2) set 增加一个新元素，返回当前 Map
	3) get 返回键名对象的键值
	4) has 检测 Map 中是否包含某个元素，返回 boolean 值
	5) clear 清空集合，返回 undefined

```
<script>
    //声明 Map
    let m = new Map();

    //添加元素
    m.set('name','陈丢堆');
    m.set('saying',function(){
        console.log("欲速则不达");
    });
    let key = {
        num : 'number'
    };
    m.set(key, ['壹','贰','叁']);

    //返回元素个数
    console.log(m.size);

    //删除
    m.delete('name');

    //获取
    console.log(m.get('saying'));
    console.log(m.get(key));

    //遍历
    for(let v of m){
        console.log(v);
    }

    //清空
    m.clear();

    //console.log(m);

</script>
```

#### class类

ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。
基本上，ES6 的 class 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，
新的 class 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
知识点：
	1) class 声明类
	2) constructor 定义构造函数初始化
	3) extends 继承父类
	4) super 调用父级构造方法
	5) static 定义静态方法和属性
	6) 父类方法可以重写

```
<script>
    //ES5通过构造函数实例化对象
    //手机
    // function Phone(brand, price){
    //     this.brand = brand;
    //     this.price = price;
    // }

    // //添加方法
    // Phone.prototype.call = function(){
    //     console.log("我可以打电话");
    // }

    // //实例化对象
    // let Huawei = new Phone('华为', 5999);
    // Huawei.call();
    // console.log(Huawei);

    //class语法实例化对象
    class Phone{
        //构造方法 名字不能修改
        constructor(brand, price){
            this.brand = brand;
            this.price = price;
        }
        
        //方法必须使用该语法， 不能使用ES5的对象完整形式
        call(){
            console.log("我可以打电话");
        }
    }

    let onePlus = new Phone("1+", 1999);

    console.log(onePlus);
</script>
```

##### class静态成员

```
<script>
    // function Phone(){

    // }

    // Phone.name = '手机';
    // Phone.change = function(){
    //     console.log("为发烧而生");
    // }
    // Phone.prototype.size = '5.5inch';

    // let mi = new Phone();

    // console.log(mi.name);
    // // mi.change();
    // console.log(mi.size);

    class Phone{
        //静态属性
        static name = '手机';
        static change(){
            console.log("为发烧而生");
        }
    }

    let mi = new Phone();
    console.log(nokia.name);
    console.log(Phone.name);
</script>
```

##### class的类继承

```
<script>
    //ES5的构造函数继承
    //手机
    function Phone(brand, price){
        this.brand = brand;
        this.price = price;
    }

    Phone.prototype.call = function(){
        console.log("我可以打电话")
    }

    //智能手机
    function SmartPhone(brand, price, color, size){
        Phone.call(this, brand, price);
        this.color = color;
        this.size = size;
    }

    //设置了级构造函数的原型
    SmartPhone.prototype = new Phone;
    SmartPhone.prototype.constructor = SmartPhone;

    //声明了类的方法
    SmartPhone.prototype.photo = function(){
        console.log("我可以拍照");
    }

    SmartPhone.prototype.game = function(){
        console.log("我可以玩游戏");
    }

    const mi = new SmartPhone('xiaomi', 1999, '黑色', '5.5inch');

    console.log(mi);

    //ES6 calss类继承
    class Phone{
        //构造方法
        constructor(brand, price){
            this.brand = brand;
            this.price = price;
        }

        //父类的成员属性
        call(){
            console.log("打电话");
        }
    }

    class SmartPhone extends phone{
        //构造方法
        constructor(brand, price, color, size){
            super(brand, price);//等于 Phone.call(this, brand, price);
            this.color = color;
            this.size = size;
        }

        photo(){
            console.log("拍照");
        }

        game(){
            console.log("玩游戏");
        }
    }

    const mi = new SmartPhone('小米', 1999, '黑色', '5.5inch');
    console.log(mi);
</script>
```

##### class子类对父类方法的重写

```
<script>
    //ES6 calss类继承
    class Phone{
        //构造方法
        constructor(brand, price){
            this.brand = brand;
            this.price = price;
        }

        //父类的成员属性
        call(){
            console.log("打电话");
        }
    }

    class SmartPhone extends phone{
        //构造方法
        constructor(brand, price, color, size){
            super(brand, price);//等于 Phone.call(this, brand, price);
            this.color = color;
            this.size = size;
        }

        photo(){
            console.log("拍照");
        }

        game(){
            console.log("玩游戏");
        }

        //子类重写父类方法
        call(){
            console.log("视频通话");
        }
    }

    const mi = new SmartPhone('小米', 1999, '黑色', '5.5inch');
    console.log(mi);
</script>
```

##### calss中的get和set

```
<script>
    /*
    get 和 set
    get 通常对动态属性做一个封装，set 可以添加更多的控制和判断
    */
    class Phone{
        get price(){
            console.log("价格属性被读取了");
            return 'ccc';
        }

        set price(newVal){
            console.log('价格属性被修改了');
            
        }
    }

    //实例化对象
    let s = new Phone();

    // console.log(s.price);
    s.price = 'free';
</script>
```

#### 数值扩展

```
<script>
    
    //0. Number.EPSILON 是 JavaScript 表示的最小精度
    //EPSILON 属性的值接近于 2.2204460492503130808472633361816E-16
     function equal(a, b){
         if(Math.abs(a-b) < Number.EPSILON){
             return true;
         }else{
             return false;
         }
     }
     console.log(0.1 + 0.2 === 0.3);
     console.log(equal(0.1 + 0.2, 0.3))

    //1. 二进制和八进制
     let b = 0b1010; //二进制
     let o = 0o777; //八进制
     let d = 100; //十进制
     let x = 0xff; //十六进制
     console.log(x);

    //2. Number.isFinite  检测一个数值是否为有限数
     console.log(Number.isFinite(100));
     console.log(Number.isFinite(100/0));
     console.log(Number.isFinite(Infinity));
        
    //3. Number.isNaN 检测一个数值是否为 NaN 
     console.log(Number.isNaN(123)); 

    //4. Number.parseInt Number.parseFloat字符串转整数
     console.log(Number.parseInt('5211314love'));
     console.log(Number.parseFloat('3.1415926神奇'));

    //5. Number.isInteger 判断一个数是否为整数
     console.log(Number.isInteger(5));
     console.log(Number.isInteger(2.5));

    //6. Math.trunc 将数字的小数部分抹掉  
     console.log(Math.trunc(3.5));

    //7. Math.sign 判断一个数到底为正数 负数 还是零 ，返回1 -1 0
     console.log(Math.sign(100));
     console.log(Math.sign(0));
     console.log(Math.sign(-20000));
    

</script>
```

#### 对象方法扩展

```
<script>
    //1. Object.is 判断两个值是否完全相等 类似于 === ，但不完全一样 
    console.log(Object.is(120, 120));// true
    console.log(Object.is(NaN, NaN));// true
    console.log(NaN === NaN);// false

    //2. Object.assign 对象的合并 后面参数的属性会把前面参数的属性覆盖（同名属性）
    const config1 = {
        host: 'localhost',
        port: 3306,
        name: 'root',
        pass: 'root',
        test: 'test'
    };
    const config2 = {
        host: 'http://atguigu.com',
        port: 33060,
        name: 'atguigu.com',
        pass: 'iloveyou',
        test2: 'test2'
    }
    console.log(Object.assign(config1, config2));//

    //3. Object.setPrototypeOf 设置原型对象  Object.getPrototypeof(参数1， 参数2) 把后面的当成前面的原型
    const BOY = {
        name: 'ccc'
    }
    const NUM = {
        num: ['壹','贰','叁']
    }
    Object.setPrototypeOf(BOY, NUM);
    console.log(Object.getPrototypeOf(BOY));
    console.log(BOY);      
</script>
```

#### 模块化

模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来。

模块化的优势有以下几点：
	1) 防止命名冲突
	2) 代码复用
	3) 高维护性

在ES6中暴露模块的方式
	1.通用的导入方式
		import * as m1 from "./src/js/m1.js";
	2.解构赋值形式
	3.简便形式（只能针对默认暴露）

```
<script type="module">
    //1.通用的导入方式
    //引入 m1.js 模块内容
    import * as m1 from "./src/js/m1.js";
    console.log(m1);
    //引入 m2.js 模块内容
    import * as m2 from "./src/js/m2.js"
    console.log(m2);
    //引入 m3.js 模块内容
    import * as m3 from "./src/js/m3.js"
    // console.log(m3);
    //若想使用里面的属性和方法 就得多加一层default
    m3.default.saying();

    //2.解构赋值形式
    import {name, saying} from "./src/js/m1.js";
    import {name as boy, saying} from "./src/js/m2.js";
    import {default as m3} from "./src/js/m3.js";
    // console.log(name);
    // console.log(saying);
    console.log(boy, saying);
    console.log(m3);

    //3.简便形式
    import m3 from "./src/js/m3.js";
    console.log(m3);
</script>
```

##### 模块化引入2

```
<script src="./src/js/app.js" type="module"></script>
```

### ES7

#### ES7新特性

##### 1.Array.prototype.includes
  Includes 方法用来检测数组中是否包含某个元素，返回布尔类型值
##### 2.指数操作符
  在 ES7 中引入指数运算符「**」，用来实现幂运算，功能与 Math.pow 结果相同
```
<script>
    //includes indexOf
    const mingzhu = ['西游记','红楼梦','三国演义','水浒传'];

    //判断
    console.log(mingzhu.includes('西游记'));//true
    console.log(mingzhu.includes('金瓶梅'));//false

    // **
    console.log(2 ** 10);//1024
    console.log(Math.pow(2, 10));//1024
</script>
```

### ES8

#### async 和 和 await

​    async 和 await 两种语法结合可以让异步代码像同步代码一样

##### 1.async 函数

​    1. async 函数的返回值为 promise 对象，
​    2. promise 对象的结果由 async 函数执行的返回值决定

##### 2.await 表达式

​    1. await 必须写在 async 函数中
​    2. await 右侧的表达式一般为 promise 对象
​    3. await 返回的是 promise 成功的值
​    4. await 的 promise 失败了, 就会抛出异常, 需要通过 try...catch 捕获处理

##### async函数

```
<script>
    //async函数
    async function fn(){
        //返回一个字符串
        return '陈同学';
        //返回的结果不是一个 Promise 类型的对象，返回的结果就是成功 Promise 对象
        return;
        //抛出错误，返回的结果是一个失败的 Promise
        throw new Error('出错啦！');
        //返回的结果如果是一个 Promise 对象，返回的是成功就是成功的值，返回的失败就是失败的值
        return new Promise((resolve, reject)=>{
            // resolve('成功的数据');
            reject("失败的错误");
        });
    }

    const result = fn();

    //调用then方法
    result.then(value => {
        console.log(value);
    }, reason => {
        console.warn(reason);
    })
</script>
```

##### await函数

```
<script>
    //创建 promise 对象
    const p = new Promise((resolve, reject) => {
        resolve("用户数据");
        reject("失败");
    })

    //await 必须要放在 async 函数中
    async function main() {
        try {
            let result = await p;
            console.log(result);
        } catch (e) {
            console.log(e);
        }
    }
    
    //调用函数
    main();
</script>
```

##### async和await结合.js

```
//1.引入 fs 模块
const fs = require("fs");

//读取『为学』
function readWeiXue() {
    return new Promise((resolve, reject) => {
        fs.readFile("./resources/为学.md", (err, data) => {
            //如果失败
            if (err) reject(err);
            //如果成功
            resolve(data);
        })
    })
}

function readChaYangShi() {
    return new Promise((resolve, reject) => {
        fs.readFile("./resources/插秧诗.md", (err, data) => {
            //如果失败
            if (err) reject(err);
            //如果成功
            resolve(data);
        })
    })
}

function readGuanShu() {
    return new Promise((resolve, reject) => {
        fs.readFile("./resources/观书有感.md", (err, data) => {
            //如果失败
            if (err) reject(err);
            //如果成功
            resolve(data);
        })
    })
}

//声明一个 async 函数
async function main(){
    //获取为学内容
    let weixue = await readWeiXue();
    //获取插秧诗内容
    let chayang = await readChaYangShi();
    // 获取观书有感
    let guanshu = await readGuanShu();

    console.log(weixue.toString());
    console.log(chayang.toString());
    console.log(guanshu.toString());
}

main();
```

#### 发送ajax请求

```
<script>
    //发送 AJAX 请求，返回的结果是 Promise 对象
    
    function sendAJAX(url) {
        return new Promise((resolve, reject) => {
            
            //1.创建对象
            const x = new XMLHttpRequest();
            
            //2.初始化
            x.open('GET', url);
            
            //3.发送
            x.send();
            
            //4.事件绑定
            x.onreadystatechange = function () {
                if (x.readyState === 4) {
                    if (x.status >= 200 && x.status < 300) {
                        //成功
                        resolve(x.response);
                    }else{
                        //如果失败
                        reject(x.status);
                    }
                }
            }
        })
    }
    
    //promise then 方法测试
    // sendAJAX("https://api.apiopen.top/getJoke").then(value=>{
    //     console.log(value);
    // }, reason=>{})

    // async 与 await 测试  axios
    async function main(){
        //发送 AJAX 请求
        let result = await sendAJAX("https://api.apiopen.top/getJoke");
        //再次测试
        let tianqi = await sendAJAX('https://www.tianqiapi.com/api/?version=v1&city=%E5%8C%97%E4%BA%AC&appid=23941491&appsecret=TXoD5e8P')
        console.log(tianqi);
    }
    main();
</script>
```

#### 对象扩展方法

##### Object.values 和 和 Object.entries

​	1.Object.values()方法
​        返回一个给定对象的所有可枚举属性值的数组
​	2.Object.entries()方法
​        返回一个给定对象自身可遍历属性 [key,value] 的数组
​	3.Object.getOwnPropertyDescriptors
​        该方法返回指定对象所有自身属性的描述对象

```
<script>
    //声明对象
    const boy = {
        name:"陈同学",
        num:['一','二','三'],
        numpro:['壹','贰','叁']
    };

    //获取对象所有的键
    console.log(Object.keys(name));
    //获取对象所有的值
    console.log(Object.values(name));
    //entries
    console.log(Object.entries(name));
    //创建 Map
    const m = new Map(Object.entries(name));
    console.log(m.get('num'));

    //对象属性的描述对象
    console.log(Object.getOwnPropertyDescriptors(name));

    const obj = Object.create(null, {
        name:{
            //设置值
            value:'陈同学',
            //属性特性
            writable: true,
            configurable: true,
            enumerable: true
        }
    })
</script>
```

### ES9

#### 对象展开

Rest 参数与 spread 扩展运算符在 ES6 中已经引入，不过 ES6 中只针对于数组，
在 ES9 中为对象提供了像数组一样的 rest 参数和扩展运算符

```
<script>
    //rest 参数
    function connect({host, port, ...user}){
        console.log(host);
        console.log(port);
        console.log(user);
    }

    connect({
        host: '127.0.0.1',
        port: 3306,
        username: 'root',
        password: 'root',
        type: 'master'
    });

    //对象合并
    const skillOne = {
        q: '天音波'
    }

    const skillTwo = {
        w: '金钟罩'
    }

    const skillThree = {
        e: '天雷破'
    }

    const skillFour = {
        r: '猛龙摆尾'
    }
    
    const mangseng = {...skillOne, ...skillTwo, ...skillThree, ...skillFour};
    
    console.log(mangseng);
    
    // ...skillOne   =>  q: '天音波', w: '金钟罩'
</script>
```

#### 正则扩展=命名捕获分组

ES9 允许命名捕获组使用符号『`?<name>`』,这样获取捕获结果可读性更强

```
<script>
    //声明一个字符串
    //let str = '<a href="http://www.baidu.com">百度</a>';

    //提取 url 与 标签文本
    //const reg = /<a href="(.*)">(.*)<\/a>/;

    //执行
    //const result = reg.exec(str);

    //console.log(result[1]);
    //console.log(result[2]);

    let str = '<a href="http://www.baidu.com">百度</a>';
    
    const reg = /<a href="(?<url>.*)">(?<text>.*)<\/a>/;

    const result = reg.exec(str);

    console.log(result);
</script>
```

#### 反向断言

ES9 支持反向断言，
通过对匹配结果前面的内容进行判断，对匹配进行筛选。

```
<script>
    //声明字符串
    let str = 'TT5201314你你你520哈哈哈';
    //正向断言
    // const reg = /\d+(?=哈)/;

    // const result = reg.exec(str);

    //反向断言
    const reg = /(?<=你)\d+/;

    const result = reg.exec(str);
    
    console.log(result);
</script>
```

#### dotAll模式

正则表达式中点.匹配除回车外的任何单字符，
标记『s』改变这种行为，允许行终止符出现

```
<script>
    //dot . 元字符  除换行符以外的任意单个字符
    let str = `
        <ul>
            <li>
                <a>肖申克的救赎</a>
                <p>上映日期: 1994-09-10</p>
            </li>
            <li>
                <a>阿甘正传</a>
                <p>上映日期: 1994-07-06</p>
            </li>
        </ul>`;
        //声明正则
        // const reg = /<li>\s+<a>(.*?)<\/a>\s+<p>(.*?)<\/p>/;
        const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/gs;
        //执行匹配
        // const result = reg.exec(str);
        let result;
        let data = [];
        while(result = reg.exec(str)){
            data.push({title: result[1], time: result[2]});
        }
        //输出结果
        console.log(data);
</script>
```

### ES10

#### Object.fromEntries

```
<script>
    //二维数组
    // const result = Object.fromEntries([
    //     ['name', '陈同学'],
    //     ['num', '壹,贰,叁,肆']
    // ]);

    //Map
    const m = new Map();
    m.set('name','陈同学');

    const result = Object.fromEntries(m);

    //Object.entries ES8
    const arr = Object.entries({
        name:"陈同学"
    })

    console.log(result);
</script>
```

#### trimStart 与 trimEnd

```
<script>    
    // trim  清除字符串左右侧的空白
    let str = '   iloveyou   ';
    
    console.log(str);
    console.log(str.trimStart());
    console.log(str.trimEnd());
</script>
```

#### flat 与 flatMap

```
<script>
    //flat 将多维数组转化为低维数组
    // const arr = [1,2,3,4,[5,6]];
    // const arr = [1,2,3,4,[5,6,[7,8,9]]];
    //参数为深度，是一个数字，默认值为1
    // console.log(arr.flat(2));  
    
    //flatMap 和Map相似，不过是把Map的结果做一个维度降低
    const arr = [1,2,3,4];
    const result = arr.flatMap(item => [item * 10]);
    console.log(result);
</script>
```

#### Symbol.prototype.description

```
<script>
    //创建 Symbol
    let s = Symbol('尚硅谷');
    //description 用来获取Symbol的字符串描述
    console.log(s.description);
</script>
```

### ES11

#### 私有属性

```
    <script>
        class Person{
            //公有属性
            name;
            //私有属性
            #age;
            #weight;
            //构造方法
            constructor(name, age, weight){
                this.name = name;
                this.#age = age;
                this.#weight = weight;
            }

            intro(){
                console.log(this.name);
                console.log(this.#age);
                console.log(this.#weight);
            }
        }

        //实例化
        const girl = new Person('晓红', 18, '45kg');

        // console.log(girl.name);
        // console.log(girl.#age);
        // console.log(girl.#weight);

        girl.intro();
    </script>
```

#### Promise.allSettled

```
    <script>
        //声明两个promise对象
        const p1 = new Promise((resolve, reject)=>{
            setTimeout(()=>{
                resolve('商品数据 - 1');
            },1000)
        });

        const p2 = new Promise((resolve, reject)=>{
            setTimeout(()=>{
                resolve('商品数据 - 2');
                // reject('出错啦!');
            },1000)
        });

        //调用 allsettled 方法
        // const result = Promise.allSettled([p1, p2]);
        
        // const res = Promise.all([p1, p2]);

        console.log(res);

    </script>
```

#### String.prototype.matchAll

```
    <script>
        let str = `<ul>
            <li>
                <a>肖生克的救赎</a>
                <p>上映日期: 1994-09-10</p>
            </li>
            <li>
                <a>阿甘正传</a>
                <p>上映日期: 1994-07-06</p>
            </li>
        </ul>`;

        //声明正则
        const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/sg

        //调用方法 matchAll 用来得到正则批量匹配的结果
        const result = str.matchAll(reg);

        // for(let v of result){
        //     console.log(v);
        // }

        const arr = [...result];

        console.log(arr);
    </script>
```

#### 可选链操作符

```
    <script>
        // ?.
        function main(config){
            // const dbHost = config && config.db && config.db.host;
            const dbHost = config?.db?.host;

            console.log(dbHost);
        }

        main({
            db: {
                host:'192.168.1.100',
                username: 'root'
            },
            cache: {
                host: '192.168.1.200',
                username:'admin'
            }
        })
    </script>
```

#### 动态 import

```
<body>
    <button id="btn">点击</button>
    <script src="./js/app.js" type="module"></script>
</body>
```

#### BigInt

```
    <script>
        //大整形
        // let n = 521n;
        // console.log(n, typeof(n));

        //函数 可以将普通字符串转换成大整形
        // let n = 123;
        // console.log(BigInt(n));
        //不能用浮点数来转换
        // console.log(BigInt(1.2));

        //大数值运算
        let max = Number.MAX_SAFE_INTEGER;
        console.log(max);
        console.log(max + 1);
        console.log(max + 2);

        console.log(BigInt(max))
        console.log(BigInt(max) + BigInt(1))
        console.log(BigInt(max) + BigInt(2))
    </script>
```

#### globalThis

```
    <script>
        console.log(globalThis);
    </script>
```

