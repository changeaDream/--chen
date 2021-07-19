# less

## less简介

less是一门css的预处理语言，less是一个css的增强版，通过less可以编写更少的代码实现更强大的样式，在less中添加了许多的新特性：像对变量的支持、对mixin的支持... ...less的语法大体上和css语法一致，但是less中增添了许多对css的扩展，所以浏览器无法直接执行less代码，要执行必须向将less转换为css，然后再由浏览器执行。

#### css原生也支持变量的设置
即可在css中编写less代码，不过由于兼容性问题，一般不推荐使用
	语法：
		在html中：
		--名称:属性值；
		引用：
		属性名：var（--名称）；

```
 html{
	--color:#ff0;
	--length:200px;
}

.box1{
	/* calc()计算函数 */
	width: calc(200px*2);
	height: var(--length);
	background-color: var(--color);
}

.box2{
	width: var(--length);
	height: var(--length);
	color: var(--color);
}
```
#### less中的注释

`//` less中的**单行注释**，注释中的内容不会被解析到css中
注意：css中的注释`/* */`，内容会被解析到css文件中

#### 变量

变量，在变量中可以存储一个任意的值
并且我们可以在需要时，任意的修改变量中的值
变量的语法： @变量名

```
@a:200px;
@b:#bfa;
@c:box6;
```

使用变量时，如果是直接使用则以 @变量名 的形式使用即可

```
.box5{
    width: @a;
    color:@b;
}
```
--->css

```
.box5 {
  width: 200px;
  color: #bfa;
}
```

作为类名，或者一部分值使用时必须以 @{变量名} 的形式使用

```
.@{c}{
    width: @a;
    background-image: url("@{c}/1.png");
}
```

--->css

```
.box6 {
  width: 200px;
  background-image: url("box6/1.png");
}
```

变量发生重名时，下面的变量会覆盖上面的变量

```
@d:200px;
@d:300px;

div{
    width: @d;
}
```

--->css

```
div {
  width: 300px;
}
```

可以在变量声明前就使用变量

```
div{
	width:115px;
    height: @e;
}
@e:335px;
```

--->css

```
div {
  width: 115px;
  height: 335px;
}
```

#### 混合函数

混合函数 在混合函数中可以直接设置变量

调用混合函数，按顺序传递参数

:extend() 对当前选择器扩展指定选择器的样式（选择器分组）

直接对指定的样式进行引用，这里就相当于将p1的样式在这里进行了复制

使用类选择器时可以在选择器后边添加一个括号，这时我们实际上就创建了一个mixins

为box1设置一个hover
& 就表示外层的父元素

```
div{
	&:hover{
		color: orange;
	}
}
```

