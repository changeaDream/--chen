#  CSS简介

网页分成三个部分：
	结构(HTML)
	表现(CSS)
	行为(JavaScript)

## CSS（层叠样式表）

​	网页实际上是一个多层的结构，通过CSS可以分别为网页的每一个层来设置样式
​	而最终我们能看到只是网页的最上边一层
​	总之一句话，CSS用来设置网页中元素的样式
​	html中，<head>标签内的<style>标签部分就属于CSS，语法规则与CSS一样

## *使用CSS来修改元素的样式*

### 第一种方式(内联样式，行内样式)：

​	在标签内部通过style属性来设置元素的样式
​		问题：
​			使用内联样式，样式只能对一个标签生效，
​			如果希望影响到多个元素必须在每一个元素中都复制一遍
​			并且当样式发生变化时，我们必须要一个一个的修改，非常的不方便

```
<p style="color:red; font-size: 60px;">文字内容</p>
```

`注意：开发时绝对不要使用内联样式`

### 第二种方式（内部样式表）

		- 将样式编写到head中的style标签里，然后通过CSS的选择器来选中元素并为其设置各种样式
​		可以同时为多个标签设置样式，并且修改时只需要修改一处即可全部应用
​		内部样式表更加方便对样式进行复用
​		问题：
​			我们的内部样式表只能对一个网页起作用，
​			它里边的样式不能跨页面进行复用

```
<head>
<style>

	p{
		color: green;
		font-size: 50px;
	}

</style>
</head>
```

### 第三种方式 （外部样式表） 最佳实践

​		可以将CSS样式编写到一个外部的CSS文件中,然后通过link标签来引入外部的CSS文件
​		外部样式表需要通过link标签进行引入，意味着只要想使用这些样式的网页都可以对其进行引用,使样式可以在不同页面之间进行复用
​		将样式编写到外部的CSS文件中，可以使用到浏览器的缓存机制，从而加快网页的加载速度，提高用户的体验。

```
<head>
	<link rel="stylesheet" href="./style.css(外部CSS文件)">
</head>

```

### *CSS中的注释*

```
/* 注释内容 */
```

注释内容会被浏览器自动忽略

## *CSS的基本语法*

### 声明块 

通过声明块来指定要为元素设置的样式
		声明块由一个一个的声明组成
		声明是一个名值对结构
	一个样式名对应一个样式值，名和值之间以:连接，以;结尾 

### 选择器

通过选择器可以选中页面中的指定元素
		比如 p 的作用就是选中页面中所有的p元素

```
<head>
	<style>

	p{
		color: red;
		font-size: 40px;
	}

	h1{
		color: green;
	}

	</style>
</head>
```

#### 常用选择器

##### 1.元素选择器

​	作用：根据标签名来选中指定的元素
​	语法：标签名{}
​	例子：p{}  h1{}  div{}

```
<head>
	<style>
		p{
			color: red;
		}

		h1{
			color: green;
		}
	</style>
</head>
```

##### 2.id选择器

​	作用：根据元素的id属性值选中一个元素
​	语法：#id属性值{}
​	例子：#box{} #red{}

```
<head>
	<style>
		#red{
			color: red;
		}
	</style>
</head>
```

##### 3.类选择器

​	作用：根据元素的class属性值选中一组元素
​	语法：.class属性值

```
<head>
	<style>
		.blue{
			color: blue;
		}

		.abc{
			font-size: 20px;
		}
	</style>
</head>
```

``class 是一个标签的属性，它和id类似，不同的是class可以重复使用`
	`可以通过class属性来为元素分组`
	`可以同时为一个元素指定多个class属性``

##### 4.通配选择器

​	作用：选中页面中的所有元素
​	语法: *

```
<head>
	<style>
		*{
			color: red;
		}
	</style>
</head>
```

#### 复合选择器

##### 5.交集选择器

​	作用：选中同时复合多个条件的元素
​	语法：选择器1选择器2选择器3选择器n{}
​	注意点：交集选择器中如果有元素选择器，必须使用元素选择器开头

```
<head>
	<style>
		div.red{
			font-size: 30px;
		}

		.a.b.c{
			color: blue
		}
	</style>
</head>
```

##### 6.并集选择器（选择器分组）

​	作用：同时选择多个选择器对应的元素
​	语法：选择器1,选择器2,选择器3,选择器n{}

```
<head>
	<style>
		h1, span{
			color: green
		}
	</style>
</head>
```

#### 关系选择器

```
父元素
	直接包含子元素的元素叫做父元素
子元素
	直接被父元素包含的元素是子元素
祖先元素
	直接或间接包含后代元素的元素叫做祖先元素
	一个元素的父元素也是它的祖先元素
后代元素
	直接或间接被祖先元素包含的元素叫做后代元素
	子元素也是后代元素
兄弟元素
	拥有相同父元素的元素是兄弟元素
```

##### 7.子元素选择器

​	作用：选中指定父元素的指定子元素
​	语法：父元素 > 子元素

```
<head>
	<style>
		div.box > span{
			color: orange;
		}
	</style>
</head>
```

##### 8.后代元素选择器

​	作用：选中指定元素内的指定后代元素
​	语法：祖先 后代

```
<head>
	<style>
		div span{
			color: skyblue
		}
	</style>
</head>
```

##### 9.兄弟选择器

​	选择下一个兄弟
​	语法：前一个 + 下一个
​	选择下边所有的兄弟
​	语法：兄 ~ 弟

```
<head>
	<style>
	<!-- 这个语法只能选择相邻的下一个兄弟元素，如例子中，若p的下一个元素不是span，则无法被选中。 -->
		p + span{
			color: red;
		}

		p ~ span{
			color: red;
		}
	</style>
</head>
```

#### 10.属性选择器

​	[属性名] 选择含有指定属性的元素
​	[属性名=属性值] 选择含有指定属性和属性值的元素
​	[属性名^=属性值] 选择属性值以指定值开头的元素
​	[属性名$=属性值] 选择属性值以指定值结尾的元素
​	[属性名*=属性值] 选择属性值中含有某值的元素的元素

```
<head>
	<style>
	p[title]{ 
		color: orange;
	}
	p[title=abc]{ 
		color: orange;
	}
	p[title^=abc]{
		color: orange;
	}
	p[title$=abc]{ 
		color: orange;
	}
	p[title*=e]{
		color: orange;
	}
	</style>
</head>
```

#### 11.伪类选择器

### *伪类*

（不存在的类，特殊的类）
	伪类用来描述一个元素的特殊状态
	比如：第一个子元素、被点击的元素、鼠标移入的元素...
	伪类一般情况下都是使用 : 开头
		`:first-child` 选中第一个子元素
		`:last-child` 选中最后一个子元素
		`:only-child` 选中唯一的一个子元素（可以选那些只有一个子元素的父元素）
		`:nth-child()` 选中第n个子元素
	特殊值（放在`:nth-child()`括号内的）：
		n 第n个 n的范围0到正无穷
		2n 或 even 表示选中偶数位的元素
		2n+1 或 odd 表示选中奇数位的元素

以上这些伪类都是根据所有的子元素进行排序
		`:first-of-type`选中同类型第一个子元素
		`:last-of-type`选中同类型最后一个子元素
		`:nth-of-type()`选中同类型第n个子元素
		`:only-of-type`选中同类型中唯一的一个子元素（可以选那些只有一个子元素的父元素）
这几个伪类的功能和上述的类似，不同点是他们是在同类型元素中进行排序
		`:not()` 否定伪类
		`:empty`选中无子元素的父元素
		将符合条件的元素从选择器中去除

```
<html>
<head>
	<style>
	ul > li:first-child{
		color: red;
	} 
    
	ul > li:last-child{
		color: red;
	} 

	ul > li:only-child{
		color: red;
	} 

	ul > li:nth-child(2n+1){
		color: red;
	} 

	ul > li:nth-child(even){
		color: red;
	} 

	ul > li:first-of-type{
		color: red;
	} 

	ul > li:not(:nth-of-type(3)){
		color: yellowgreen;
	}
	</style>
</head>
<body>

	<ul>
		<span>我是一个span</span>
		<li>第〇个</li>
		<li>第一个</li>
		<li>第二个</li>
		<li>第三个</li>
		<li>第四个</li>
		<li>第五个</li>
	</ul>


</body>
</html>
```

#### *超链接的伪类*

`:link` 用来表示没访问过的链接（正常的链接）
`:visited` 用来表示访问过的链接
	由于隐私的原因，所以visited这个伪类只能修改链接的颜色
`:hover` 用来表示鼠标移入的状态
`:active` 用来表示鼠标点击

```
<head>
	<style>
		a:link{
			color: red;
		}

		a:visited{
			color: orange;
			/* font-size: 50px;由于隐私原因，字体大小不可设置*/
		}

		a:hover{
			color: aqua;
			font-size: 50px;
		}

		a:active{
			color: yellowgreen;
		}
	</style>
</head>
```

#### 12.伪元素选择器

伪元素，表示页面中一些特殊的并不真实的存在的元素（特殊的位置）
伪元素使用 :: 开头

`::first-letter` 表示第一个字母
`::first-line` 表示页面的第一行
`::selection` 表示鼠标选中的内容
`::before` 元素的开始 
`::after` 元素的最后
	**before 和 after 必须结合content属性来使用**

```
<head>
	<style>
		p::first-letter{
			font-size: 50px;
		}

		p::first-line{
			ground-color: yellow; 
		}

		p::selection{
			background-color: greenyellow;
		}

		div::before{
			content: 'aaa';
			color: red;
		}

		div::after{
			content: 'bbb';
			color: blue;
		}

	</style>
</head>
```

### *继承*

样式的继承，我们为一个元素设置的样式同时也会应用到它的后代元素上

继承是发生在祖先后后代之间的

继承的设计是为了方便我们的开发，
利用继承我们可以将一些通用的样式统一设置到共同的祖先元素上，
这样只需设置一次即可让所有的元素都具有该样式

注意：并不是所有的样式都会被继承：
比如 背景相关的，布局相关等的这些样式都不会被继承。

### *选择器的权重*

样式的冲突
当我们通过不同的选择器，选中相同的元素，并且为相同的样式设置不同的值时，此时就发生了样式的冲突。

发生样式冲突时，应用哪个样式由选择器的权重（优先级）决定
	选择器的权重
		内联样式              1,0,0,0
		id选择器               0,1,0,0
		类和伪类选择器   0,0,1,0
		元素选择器           0,0,0,1
		通配选择器           0,0,0,0
		继承的样式           没有优先级

​	比较优先级时，需要将所有的选择器的优先级进行相加计算，最后优先级越高，则越优先显示（分组选择器是单独计算的）,选择器的累加不会超过其最大的数量级，类选择器再高也不会超过id选择器，如果优先级计算后相同，此时则优先使用靠下的样式

​	可以在某一个样式的后边添加 !important ，则此时该样式会获取到最高的优先级，甚至超过内联样式，
​	**注意：在开发中这个玩意一定要慎用！**

### *单位*

长度单位：
	像素
		屏幕（显示器）实际上是由一个一个的小点点构成的
		不同屏幕的像素大小是不同的，像素越小的屏幕显示的效果越清晰
		所以同样的200px在不同的设备下显示效果不一样

​	百分比
​		也可以将属性值设置为相对于其父元素属性的百分比
​		设置百分比可以使子元素跟随父元素的改变而改变

​	em
​		em是相对于元素的字体大小来计算的
​		1em = 1font-size
​		em会根据字体大小的改变而改变

​	rem
​		rem是相对于根元素的字体大小来计算

### *颜色*

​	颜色单位：
​		在CSS中可以直接使用颜色名来设置各种颜色
​		比如：red、orange、yellow、blue、green ... ...
​		但是在css中直接使用颜色名是非常的不方便

​	RGB值：
​		RGB通过三种颜色的不同浓度来调配出不同的颜色
​		R red，G green ，B blue
​		每一种颜色的范围在 0 - 255 (0% - 100%) 之间
​		语法：RGB(红色,绿色,蓝色)

​	RGBA:
​		就是在rgb的基础上增加了一个a表示不透明度
​		需要四个值，前三个和rgb一样，第四个表示不透明度
​		1表示完全不透明   0表示完全透明  .5半透明

​	十六进制的RGB值：
​		语法：#红色绿色蓝色
​		颜色浓度通过 00-ff
​		如果颜色两位两位重复可以进行简写  
​		#aabbcc --> #abc
​                    
​	HSL值 HSLA值（这个在CSS中很少用到）
​		H 色相(0 - 360)
​		S 饱和度，颜色的浓度 0% - 100%
​		L 亮度，颜色的亮度 0% - 100%

```
background-color: red;

background-color: rgb(255, 0, 0);

background-color: rgba(106,153,85,.5);

background-color: #ffff00;
background-color: #ff0;

background-color: hsl(98, 48%, 40%);
background-color: hsla(98, 48%, 40%, 0.658);
```

## layout(布局)

### *文档流*

文档流（normal flow）
	网页是一个多层的结构，一层摞着一层
	通过CSS可以分别为每一层来设置样式
	作为用户来讲只能看到最顶上一层
	这些层中，最底下的一层称为文档流，文档流是网页的基础
	我们所创建的元素默认都是在文档流中进行排列
	对于我们来元素主要有两个状态：
		在文档流中
		不在文档流中（脱离文档流）
	元素在文档流中有什么特点：

#### 		块元素

​			块元素会在页面中独占一行(自上向下垂直排列)
​			默认宽度是父元素的全部（会把父元素撑满）
​			默认高度是被内容撑开（子元素）
​	

#### 		行内元素

​			行内元素不会独占页面的一行，只占自身的大小
​			行内元素在页面中左向右水平排列，如果一行之中不能容纳下所有的行内元素，则元素会换到第二行继续自左向右排列（书写习惯一致）
​			行内元素的默认宽度和高度都是被内容撑开

`这里的块元素和行内元素内容可以和HTML互相补充`

### *盒模型（box model）*

盒模型、框模型、盒子模型（box model）
	CSS将页面中的所有元素都设置为了一个矩形的盒子
	将元素设置为矩形的盒子后，对页面的布局就变成将不同的盒子摆放到不同的位置
	每一个盒子都由一下几个部分组成：
		内容区（content）
		内边距（padding）
		边框（border）
		外边距（margin）

#### 内容区（content）

​	元素中的所有的子元素和文本内容都在内容区中排列 
​	内容区的大小由width 和 height两个属性来设置
​		width 设置内容区的宽度
​		height 设置内容区的高度

```
<head>
	<style>
		.box1{
			width: 200px;
			height: 200px;
			background-color: #bfa;
		}
		}
	</style>
</head>
```

#### 边框（border）

​	边框属于盒子边缘，边框里边属于盒子内部，出了边框都是盒子的外部
​	边框的大小会影响到整个盒子的大小
​	要设置边框，需要至少设置三个样式：
​		**边框的宽度 border-width**
​			默认值一般都是 3个像素
​			border-width可以用来指定四个方向的边框的宽度
​				值的情况
​					四个值：上 右 下 左
​					三个值：上 左右 下
​					两个值：上下 左右
​					一个值：上下左右

​	除了border-width还有一组 border-xxx-width
​		xxx可以是 top right bottom left，用来单独指定某一个边的宽度

​		**边框的颜色 border-color**
​		border-color用来指定边框的颜色，同样可以分别指定四个边的边框
​		规则和border-width一样

​		border-color也可以省略不写，如果省略了则自动使用color的颜色值

​		**边框的样式 border-style**
​			border-style 指定边框的样式，边框样式同样可以指定四个不同的边
​			
​			solid 表示实线
​			dotted 点状虚线
​			dashed 虚线
​			double 双线
​			transparent 透明的

​			border-style的默认值是none 表示没有边框

```
<head>
	<style>
		.box1{
			border-width: 10px;
			border-color: red;
			border-style: solid;
		}
		}
	</style>
</head>
```

​	**border简写属性**

​	通过该属性可以同时设置边框所有的相关样式，并且没有顺序要求

​			除了border以外还有四个 border-xxx
​				border-top
​				border-right
​				border-bottom
​				border-left

```
			border: 10px red solid;
```

#### 内边距（padding）

​	内容区和边框之间的距离是内边距
​	一共有四个方向的内边距：
​		padding-top
​		padding-right
​		padding-bottom
​		padding-left

​	内边距的设置会影响到盒子的大小，背景颜色会延伸到内边距上

​	**内边距的简写属性**
​	可以同时指定四个方向的内边距，规则和border-width 一样

```
			padding: 10px 20px 30px 40px;
			padding: 10px 20px 30px ;
			padding: 10px 20px ;
			padding: 10px ;
```

`一个盒子的可见框的大小，由内容区、内边距和边框共同决定，所以在计算盒子大小时，需要将这三个区域加到一起计算`

#### 外边距（margin）

​	外边距不会影响盒子可见框的大小
​	但是外边距会影响盒子的位置
​	一共有四个方向的外边距：
​		margin-top
​			上外边距，设置一个正值，元素会向下移动
​		margin-right
​			默认情况下设置margin-right不会产生任何效果
​		margin-bottom
​			下外边距，设置一个正值，其下边的元素会向下移动
​		margin-left
​			左外边距，设置一个正值，元素会向右移动

​	margin也可以设置负值，如果是负值则元素会向相反的方向移动

​	元素在页面中是按照自左向右的顺序排列的，所以默认情况下如果我们设置的左和上外边距则会移动元素自身，而设置下和右外边距会移动其他元素

​	**margin的简写属性**
​	margin 可以同时设置四个方向的外边距 ，用法和padding一样

```
			margin：100px;
			margin-bottom: 100px;
			margin-top: -100px;
			margin-left: -100px;
			margin-bottom: -100px;
```

##### 垂直外边距的重叠（折叠）

相邻的垂直方向外边距会发生重叠现象
	兄弟元素
	兄弟元素间的相邻垂直外边距会取两者之间的较大值（两者都是正值）
	特殊情况：
		如果相邻的外边距一正一负，则取两者的和
		如果相邻的外边距都是负值，则取两者中绝对值较大的

​	兄弟元素之间的外边距的重叠，对于开发是有利的，所以我们不需要进行处理

​	父子元素
​	父子元素间相邻外边距，子元素的会**传递**给父元素（上外边距）
​	父子外边距的折叠会影响到页面的布局，必须要进行处理

<u>margin会影响到盒子实际占用空间</u>

#### 盒子的水平布局

元素的水平方向的布局：
元素在其父元素中水平方向的位置由以下几个属性共同决定：
		`margin-left`
		`border-left`
		`padding-left`
		`width`
		`padding-right`
		`border-right`
		`margin-right`

​	一个元素在其父元素中，水平布局必须要满足以下的等式
margin-left + border-left + padding-left + width + padding-right + border-right + margin-right = 其父元素内容区的宽度 （必须满足）

​	以上等式必须满足，如果相加结果使等式不成立，则称为过度约束，等式会自动调整
​	调整的情况：
​	如果这七个值中没有为 auto 的情况，则浏览器会自动调整margin-right值以使等式满足

​		这七个值中有**三个值**可设置为auto：
​			`width`
​			`margin-left`
​			`maring-right`

​	如果某个值为auto，则会自动调整为auto的那个值以使等式成立

​	如果将一个宽度和一个外边距设置为auto，则宽度会调整到最大，设置为auto的外边距会自动为0
​	如果将三个值都设置为auto，则外边距都是0，宽度最大
​	如果将两个外边距设置为auto，宽度固定值，则会将外边距设置为相同的值
​	所以我们经常利用这个特点来使一个元素在其父元素中水平居中
​	示例：
​		`width:xxxpx;`
​		`margin:0 auto;`

#### 盒子的垂直布局

​	子元素是在父元素的内容区中排列的，
​	如果子元素的大小超过了父元素，则子元素会从父元素中溢出

`默认情况下父元素的高度被内容撑开`

​	使用 overflow 属性来设置父元素如何处理溢出的子元素

​	可选值：
​		`visible` 默认值 子元素会从父元素中溢出，在父元素外部的位置显示
​		`hidden` 溢出内容将会被裁剪不会显示
​		`scroll` 生成两个滚动条，通过滚动条来查看完整的内容
​		`auto` 根据需要生成滚动条

​			`overflow-x:` （设置横轴）
​			`overflow-y:` （设置纵轴）

#### 行内元素的盒模型

​	行内元素不支持设置宽度和高度
​	行内元素可以设置padding，但是垂直方向padding不会影响页面的布局
​	行内元素可以设置border，垂直方向的border不会影响页面的布局
​	行内元素可以设置margin，垂直方向的margin不会影响布局

​	`display` 用来设置元素显示的类型
​		可选值：
​			`inline` 将元素设置为行内元素
​			`block` 将元素设置为块元素
​			`inline-block` 将元素设置为行内块元素 
​					行内块，既可以设置宽度和高度又不会独占一行
​			`table` 将元素设置为一个表格
​			`none` 元素不在页面中显示

​	`visibility` 用来设置元素的显示状态
​		可选值：
​			`visible` 默认值，元素在页面中正常显示
​			`hidden` 元素在页面中隐藏 不显示，但是依然占据页面的位置

```
<head>
	<style>
		a{
			width: 200px;
			height: 200px;
			background-color: #bfa;
			
			display: block;
			visibility: hidden;
		}
	</style>
</head>
```

#### 盒子的尺寸

默认情况下，盒子可见框的大小由内容区、内边距和边框共同决定

`box-sizing` 用来设置盒子尺寸的计算方式（设置width和height的作用）
可选值：
`content-box` 默认值，宽度和高度用来设置内容区的大小
`border-box` 宽度和高度用来设置整个盒子可见框的大小
`width` 和 `height` 指的是内容区 和 内边距 和 边框的总大小

```
<style>
	.box1{
		width: 100px;
		height: 100px;
		background-color: #bfa;
		padding: 10px;
		border: 10px red solid;

		box-sizing: border-box ;
	}
</style>
```

#### 默认样式

默认样式：
	通常情况，浏览器都会为元素设置一些默认样式
	默认样式的存在会影响到页面的布局，
	通常情况下编写网页时必须要去除浏览器的默认样式（PC端的页面，移动端大部分都是统一的）



重置样式表：专门用来对浏览器的样式进行重置的
	reset.css 直接去除了浏览器的默认样式
	normalize.css 对默认样式进行了统一

```
<head>
    <meta charset="UTF-8">
	<title>Document</title>
	<link rel="stylesheet" href="./css/reset.css">
	<link rel="stylesheet" href="./css/normalize.css">
</head>
```

#### 轮廓、阴影和圆角

`outline` 用来设置元素的轮廓线，用法和border一模一样
	轮廓和边框不同的点，就是轮廓不会影响到可见框的大小

```
	.box1{
		outline: 10px red solid;
	}
```

`box-shadow` 用来设置元素的阴影效果，阴影不会影响页面布局 
	第一个值 水平偏移量 设置阴影的水平位置 正值向右移动 负值向左移动
	第二个值 垂直偏移量 设置阴影的水平位置 正值向下移动 负值向上移动
	第三个值 阴影的模糊半径
	第四个值 阴影的颜色

```
box-shadow: 0px 0px 50px rgba(0, 0, 0, .3) ; 
```

`border-radius` 用来设置圆角 圆角设置的圆的半径大小

```
border-top-left-radius:  
border-top-right-radius: 
border-bottom-left-radius: 
border-bottom-right-radius: 
border-top-left-radius:50px 100px; 
```
border-radius 可以分别指定四个角的圆角
		四个值 左上 右上 右下 左下
		三个值 左上 右上/左下 右下 
		两个值 左上/右下 右上/左下

```
border-radius:40px 30px 20px 10px
```

​	border-radius xxpx / xxpx 表示四角设置椭圆角

```
border-radius: 20px / 40px;
```

​	将元素设置为一个圆形

```
border-radius: 50%;
```

## float(浮动)

### *浮动的简介*

通过浮动可以使一个元素向其父元素的左侧或右侧移动
使用 float 属性来设置于元素的浮动
	可选值：
		none 默认值 ，元素不浮动
		left 元素向左浮动
		right 元素向右浮动

`line-height:父元素高度px`  使文字在父元素中垂直居中

注意：元素设置浮动以后，水平布局的等式便不需要强制成立。元素设置浮动以后，会完全从文档流中脱离，不再占用文档流的位置，所以元素下边的还在文档流中的元素会自动向上移动

#### 浮动的特点

​	1、浮动元素会完全脱离文档流，不再占据文档流中的位置
​	2、设置浮动以后元素会向父元素的左侧或右侧移动，
​	3、浮动元素默认不会从父元素中移出
​	4、浮动元素向左或向右移动时，不会超过它前边的其他浮动元素
​	5、如果浮动元素的上边是一个没有浮动的块元素，则浮动元素无法上移
​	6、浮动元素不会超过它上边的浮动的兄弟元素，最多最多就是和它一样高
​	7、浮动元素不会盖住文字，文字会自动环绕在浮动元素的周围，所以我们可以利用浮动来设置文字环绕图片的效果

元素设置浮动以后，将会从文档流中脱离，从文档流中脱离后，元素的一些特点也会发生变化

#### 脱离文档流的特点

​		块元素：
​			1、块元素不在独占页面的一行
​			2、脱离文档流以后，块元素的宽度和高度默认都被内容撑开

​		行内元素：
​			行内元素脱离文档流以后会变成块元素，特点和块元素一样

​		脱离文档流以后，不需要再区分块和行内了

**简单总结**：
	浮动目前来讲它的主要作用就是让页面中的元素可以水平排列，
	通过浮动可以制作一些水平方向的布局

```
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .box1{
            width: 400px;
            height: 200px;
            background-color: #bfa;
            float: left;
        }

        .box2{
            width: 400px;
            height: 200px;
            background-color: orange;
            float: left;
        }

        .box3{
            width: 200px;
            height: 200px;
            background-color: yellow;
            float: right;
        }
    </style>
</head>
```

### *高度塌陷*

高度塌陷的问题：
	在浮动布局中，父元素的高度默认是被子元素撑开的，
		当子元素浮动后，其会完全脱离文档流，子元素从文档流中脱离
		将会无法撑起父元素的高度，导致父元素的高度丢失

​	父元素高度丢失以后，其下的元素会自动上移，导致页面的布局混乱

​	所以高度塌陷是浮动布局中比较常见的一个问题，这个问题我们必须要进行处理！

### *BFC(Block Formatting Context) 块级格式化环境*

​	BFC是一个CSS中的一个隐含的属性，可以为一个元素开启BFC
​		开启BFC该元素会变成一个独立的布局区域
​	元素开启BFC后的特点：
​		1.开启BFC的元素不会被浮动元素所覆盖
​		2.开启BFC的元素子元素和父元素外边距不会重叠
​		3.开启BFC的元素可以包含浮动的子元素

​	可以通过一些特殊方式来开启元素的BFC：
​		1、设置元素的浮动（不推荐）
​		2、将元素设置为行内块元素（不推荐）
​		3、将元素的overflow设置为一个非visible的值
​		常用的方式
​			为元素设置 `overflow:hidden` 开启其BFC 以使其可以包含浮动元素

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>高度塌陷的解决方案测试</title>
    <style>
        .box1{
            border:10px solid red;
        }

        .box1::after{
            display: block;
            content: "";
            clear:both
        }
        .box2{
            width: 100px;
            height: 100px;
            background-color: #bfa;
            float: left;
        }
    </style>
</head>
<body>
    <div class="box1">
        <div class="box2"></div>
    </div>
</body>
</html>
```

### *clear*

​	作用：清除浮动元素对当前元素所产生的影响
​	可选值：
​		`left` 清除左侧浮动元素对当前元素的影响
​		`right` 清除右侧浮动元素对当前元素的影响
​		`both` 清除两侧中最大影响的那侧

```
clear:left;
clear:right;
clear:both;
```

​	原理：
​		设置清除浮动以后，浏览器会自动为元素添加一个上外边距，以使其位置不受其他元素的影响
​		如果我们不希望某个元素因为其他元素浮动的影响而改变位置，可以通过clear属性来清除浮动元素对当前元素所产生的影响

#### 高度塌陷解决方案

使用伪元素`::after`为盒子设置一个最底部元素，为其设置clear属性，再使用display将其设置为块元素
```
	.box::after{
		content: '';
		display: block;
		clear: both;
	}
```

**高度塌陷最终解决方案**
​	`clearfix` 这个样式可以同时解决高度塌陷和外边距重叠的问题，在遇到这些问题时，直接使用clearfix这个类即可

```
	.clearfix::before,
	.clearfix::after{
		content: '';
		display: table;
		clear: both;
	}
```

## position(定位)

定位是一种更加高级的布局手段
通过定位可以将元素摆放到页面的任意位置
	使用`position`属性来设置定位
		可选值：
			`static` 默认值，元素是静止的没有开启定位
			`relative` 开启元素的**相对定位**(relative)
			`absolute` 开启元素的**绝对定位**(absolute)
			`fixed` 开启元素的**固定定位**(fixed)
			`sticky` 开启元素的**粘滞定位**(sticky)

### *偏移量（offset）*

​		当元素开启了定位以后，可以通过偏移量来设置元素的位置
​		`top`  定位元素和定位位置上边的距离
​		`bottom`  定位元素和定位位置下边的距离

​		定位元素垂直方向的位置由top和bottom两个属性来控制
​	通常情况下只会使用其中之一
​		top值越大，定位元素越向下移动
​		bottom值越大，定位元素越向上移动

​		

​		`left`  定位元素和定位位置的左侧距离
​		`right`  定位元素和定位位置的右侧距离

​		定位元素水平方向的位置由left和right两个属性控制
​	通常情况下只会使用其中之一
​		left越大元素越靠右
​		right越大元素越靠左

### *相对定位*

当元素的position属性值设置为relative时则开启了元素的相对定位
	相对定位的特点：
		1.元素开启相对定位以后，如果不设置偏移量元素不会发生任何的变化
		2.相对定位是参照于元素在文档流中的位置进行定位的
		3.相对定位会提升元素的层级
		4.相对定位不会使元素脱离文档流
		5.相对定位不会改变元素的性质，块还是块，行内还是行内

### *绝对定位*

当元素的position属性值设置为absolute时，则开启了元素的绝对定位
	绝对定位的特点：
		1.开启绝对定位后，如果不设置偏移量元素的位置不会发生变化
		2.开启绝对定位后，元素会从文档流中脱离
		3.绝对定位会改变元素的性质，行内变成块，块的宽高被内容撑开
		4.绝对定位会使元素提升一个层级
		5.绝对定位元素是相对于其包含块进行定位的

#### 	*包含块( containing block )*

​	正常情况下,包含块就是离当前元素最近的祖先**块元素**
​	如果祖先元素有定位（相对、绝对、固定定位），则以最近一级的有定位的祖先元素为参考点移动位置。

​	**绝对定位的包含块**
​		包含块就是离它最近的开启了定位的祖先元素，
​		如果所有的祖先元素都没有开启定位则根元素就是它的包含块

​	**html（根元素、初始包含块）**

### *固定定位*

将元素的position属性设置为fixed则开启了元素的固定定位
	固定定位也是一种绝对定位，所以固定定位的大部分特点都和绝对定位一样
	唯一不同的是固定定位永远参照于浏览器的视口进行定位
	固定定位的元素不会随网页的滚动条滚动

### *粘滞定位*

当元素的position属性设置为sticky时则开启了元素的粘滞定位
	粘滞定位和相对定位的特点基本一致，
	不同的是粘滞定位可以在元素到达某个位置时将其固定

### 绝对定位元素的布局

水平方向布局
	left + margin-left + border-left + padding-left + width + padding-right + border-right + margin-right + right = 包含块的内容区的宽度

​	当我们开启了绝对定位后:
​		水平方向的布局等式就需要添加left 和 right 两个值，此时规则和之前一样只是多添加了两个值
​	当发生过度约束：
​		如果9个值中没有 auto 则自动调整right值以使等式满足，如果有auto，则自动调整auto的值以使等式满足

​	可设置auto的值
​		`margin` `width` `left` `right`  

​	因为left 和 right的值默认是auto，所以如果不指定left和right，则等式不满足时，会自动调整这两个值

垂直方向布局
	top + margin-top/bottom + padding-top/bottom + border-top/bottom + height = 包含块的高度

​	**只要是定位 层级就一样**

### 元素的层级

对于开启了定位的元素，可以通过z-index属性来指定元素的层级
	z-index需要一个<u>整数</u>作为参数，值越大元素的层级越高
	元素的层级越高越优先显示

​		如果元素的层级一样，则优先显示靠下的元素

​		祖先的元素的层级再高也不会盖住后代元素

```
	position: absolute;
	z-index: 3; 
```

​	**大局上用浮动 细节上用定位**

## font&background(字体和背景)

### *字体*

字体相关的样式 
	`color` 用来设置字体颜色
	`font-size` 字体的大小
		和font-size相关的单位
			`em` 相当于当前元素的一个font-size
			`rem` 相对于根元素的一个font-size
	font-family 字体族（字体的格式）
		可选值：
			`serif`  衬线字体
			`sans-serif` 非衬线字体
			`monospace` 等宽字体
				指定字体的类别，浏览器会自动使用该类别下的字体

​		`font-family` 可以同时指定多个字体，多个字体间使用 , 隔开
​			字体生效时优先使用第一个，第一个无法使用则使用第二个 以此类推
​			字体示例：
​			Microsoft YaHei,Heiti SC,tahoma,arial,Hiragino Sans GB,"\5B8B\4F53",sans-serif

​		font-family指定字体格式时如果字体名有空格最好加上引号

```
p{
	color: blue;
	font-size: 40px;
	font-family: 'Courier New', Courier, monospace;
}
```

​		`font-face`可以将服务器中的字体直接提供给用户去使用 
​			问题：
​				1.加载速度
​				2.版权
​				3.字体格式

```
@font-face {
	/* 指定字体的名字 */
	font-family:'myfont' ;
	/* 服务器中字体的路径 */
	src: url('./font/ZCOOLKuaiLe-Regular.ttf') format("truetype");
}
```

#### 图标字体

图标字体（iconfont）
	在网页中经常需要使用一些图标，可以通过图片来引入图标，但是图片大小本身比较大，并且非常的不灵活
	所以在使用图标时，我们还可以将图标直接设置为字体，然后通过font-face的形式来对字体进行引入
	这样我们就可以通过使用字体的形式来使用图标

##### fontawesome 使用步骤

​	1.下载 https://fontawesome.com/
​	2.解压
​	3.将css和webfonts移动到项目中
​	4.将all.css引入到网页中
​	5.使用图标字体
​		直接通过类名来使用图标字体
​			class="fas fa-bell"
​			class="fab fa-accessible-icon"

```
<head>
<!-- 将all.css引入到网页中 -->
<link rel="stylesheet" href="./fa/css/all.css">
</head>

<body>
	<i class="fas fa-bell" style="font-size:80px; color:red;"></i>
	<i class="fas fa-bell-slash"></i>
	<i class="fab fa-accessible-icon"></i>
	<i class="fas fa-otter" style="font-size: 160px; color:green;"></i>
</body>
```

##### 通过伪元素来设置图标字体

​	1.找到要设置图标的元素通过before或after选中
​	2.在content中设置字体的编码
​	3.设置字体的样式
​		fab
​			font-family: 'Font Awesome 5 Brands';

​		fas
​			font-family: 'Font Awesome 5 Free';
​			font-weight: 900; 

```
li::before{
	content: '\f1b0';
	/* font-family: 'Font Awesome 5 Brands'; */
	font-family: 'Font Awesome 5 Free';
	font-weight: 900; 
	color: blue;
	margin-right: 10px;
}
```

##### 通过实体来使用图标字体

​	&#x图标的编码;
​	`重要的是class="fas"/class="fab"`

```
	<span class="fas">&#xf0f3;</span>
```

#### 行高

行高（line height）
	行高指的是文字占有的实际高度
	可以通过line-height来设置行高
		行高可以直接指定一个大小（px em）
		也可以直接为行高设置一个整数
			如果是一个整数的话，行高将会是字体的指定的倍数
		行高经常还用来设置文字的行间距
			行间距 = 行高 - 字体大小

```
	line-height: 200px;
	line-height: 1.33; 
	line-height: 2; 
```

<u>可以将行高设置为和高度一样的值，使单行文字在一个元素中垂直居中</u>
（实际上line-heigh设置的高度会直接将父元素撑开，所以有些情况下可以不写父元素高度）

##### 字体框

​	字体框就是字体存在的格子，设置font-size实际上就是在设置字体框的高度

行高会在字体框的上下平均分配

#### 字体的简写属性

font 可以设置字体相关的所有属性
	语法：
		font: 字体大小/行高 字体族
		行高可以省略不写，如果不写则使用默认值（不写不代表没有设置，会覆盖前面设置的属性的）
		前面还可以加两个值作为自重和字体风格（顺序没有规定），同样不写则使用默认值，不写不代表没有设置

```
	font: bold italic 50px/2  微软雅黑, 'Times New Roman', Times, serif;
```

`font-weight` 字重 字体的加粗 
	可选值：
		normal 默认值 不加粗
		bold 加粗
		100-900 九个级别（没什么用）

`font-style` 字体的风格
		normal 正常的
		italic 斜体

```
	font-weight: bold; 
	font-weight: 500;
	font-style: italic;
```

### 文本的样式

#### 文本的水平对齐

​	`text-align` 文本的水平对齐
​		可选值：
​			`left` 左侧对齐
​			`right` 右对齐
​			`center` 居中对齐
​			`justify` 两端对齐

```
	text-align: justify;
```
#### 文本的垂直对齐

​	`vertical-align` 设置元素垂直对齐的方式
​		可选值：
​			`baseline` 默认值 基线对齐
​			`top` 顶部对齐
​			`bottom` 底部对齐
​			`middle` 居中对齐

```
	vertical-align:baseline;
```

在遇到图片需要消除边框间隔的时候
也需要使用`vertical-align:bottom/vertical-align:top`来消除

#### 设置文本修饰

`text-decoration` 设置文本修饰
	可选值：
		`none` 什么都没有
		`underline` 下划线
		`line-through` 删除线
		`overline` 上划线

`text-decoration:` 可以设置样式、颜色与风格，不过老浏览器（ie）不支持

```
text-decoration: overline;

text-decoration: underline red dotted;
```



#### 设置网页处理留白

`white-space` 设置网页如何处理空白
	可选值：
		`normal` 正常
		`nowrap` 不换行
		`pre` 保留空白

如果想要显示多余内容为省略号：
**三个值缺一不可！**

```
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```

### *背景*

#### backgrou-color  设置背景颜色

```
background-color: #bfa;
```

#### background-image 设置背景图片 

​	可以同时设置背景图片和背景颜色，这样背景颜色将会成为图片的背景色
​	如果背景的图片小于元素，则背景图片会自动在元素中平铺将元素铺满
​	如果背景的图片大于元素，将会一个部分背景无法完全显示
​	如果背景图片和元素一样大，则会直接正常显示

```
background-image: url("./img/1.png");
```

#### background-repeat 用来设置背景的重复方式

可选值：
	repeat 默认值 ， 背景会沿着x轴 y轴双方向重复
	repeat-x 沿着x轴方向重复
	repeat-y 沿着y轴方向重复
	no-repeat 背景图片不重复

```
background-repeat: no-repeat;
```

#### background-position 用来设置背景图片的位置

设置方式：
	通过 top left right bottom center 几个表示方位的词来设置背景图片的位置
		使用方位词时必须要同时指定两个值，如果只写一个则第二个默认就是center

```
background-position: center;
```

​	通过偏移量来指定背景图片的位置：
​		水平方向的偏移量 垂直方向变量

```
background-position: -50px 300px;
```

#### 设置背景的范围 

​	background-clip 
​		可选值：
​			border-box 默认值，背景会出现在边框的下边
​			padding-box 背景不会出现在边框，只出现在内容区和内边距
​			content-box 背景只会出现在内容区

​	background-origin 背景图片的偏移量计算的原点
​			padding-box 默认值，background-position从内边距处开始计算
​			content-box 背景图片的偏移量从内容区处计算
​			border-box 背景图片的变量从边框处开始计算

```
background-origin: border-box;
background-clip: content-box;
```

#### background-size 设置背景图片的大小

​	第一个值表示宽度 
​	第二个值表示高度
​		如果只写一个，则第二个值默认是 auto

​	cover 图片的比例不变，将元素铺满
​	contain 图片比例不变，将图片在元素中完整显示

```
 background-size: contain;
```

#### background-attachment 背景图片是否跟随元素移动

可选值：
	scroll 默认值 背景图片会跟随元素移动
	fixed 背景会固定在页面中，不会随元素移动

```
background-attachment: fixed;
```

#### backgound 背景相关的简写属性

​	所有背景相关的样式都可以通过该样式来设置
​	并且该样式没有顺序要求，也没有哪个属性是必须写的

​	注意：
​		background-size必须写在background-position的后边，并且使用/隔开
​		background-position/background-size
​		background-origin background-clip 两个样式 ，orgin要在clip的前边

```
background: url('./img/2.jpg') #bfa  center center/contain border-box content-box no-repeat ;
```

### *渐变*

​	通过渐变可以设置一些复杂的背景颜色，可以实现从一个颜色向其他颜色过渡的效果

**注意：渐变是图片，需要通过background-image来设置**

#### 线性渐变

​	linear-gradient() 线性渐变，颜色沿着一条直线发生变化

​		`linear-gradient(red,yellow);` 红色在开头，黄色在结尾，中间是过渡区域
​	线性渐变的开头，我们可以指定一个渐变的方向
​		to left
​		to right
​		to bottom
​		to top
​		deg deg表示度数
​		turn 表示圈 （360deg等于一圈）

​	渐变可以同时指定多个颜色，多个颜色默认情况下平均分布，也可以手动指定渐变的分布情况

​	repeating-linear-gradient() 可以平铺的线性渐变
```
background-image: linear-gradient(red,yellow,#bfa,orange); 
background-image: linear-gradient(red 50px,yellow 100px, green 120px, orange 200px); 
background-image: repeating-linear-gradient(to right ,red, yellow 50px);
```

#### 径向渐变

​	radial-gradient()  径向渐变(放射性的效果)

​	默认情况下径向渐变的形状根据元素的形状来计算的
​		正方形 --> 圆形
​		长方形 --> 椭圆形
​	我们也可以手动指定径向渐变的大小
​		circle 圆形
​		ellipse 椭圆

​	也可以指定渐变的位置
​		语法：
​			radial-gradient(大小 at 位置, 颜色 位置 ,颜色 位置 ,颜色 位置)
​		大小：
​			circle 圆形
​			ellipse 椭圆
​			closest-side 近边	
​			closest-corner 近角
​			farthest-side 远边
​			farthest-corner 远角

​		位置：
​			top right left center bottom

##### *用CSS设置小三角的方法

设置方向向上的小三角

如果要设置其他方向的，则只需调整border的哪个方向需要设置为none

```
.box1{
            width: 0px;
            height: 0px;
            
            border: 10px solid transparent;
            border-top: none;
            border-bottom-color: #fff;
        }
```

## animation（动画效果）

### 过渡（transition）

通过过渡可以指定一个属性发生变化时的切换方式
通过过渡可以创建一些非常好的效果，提升用户的体验

#### transition-property: 指定要执行过渡的属性

多个属性间使用 , 隔开 
如果所有属性都需要过渡，则使用all关键字
大部分属性都支持过渡效果，注意过渡时必须是从一个有效数值向另外一个有效数值进行过渡

```
transition-property: height , width;
transition-property: all;
```

#### transition-duration: 指定过渡效果的持续时间

时间单位：s 和 ms  1s = 1000ms

```
transition-duration: 100ms, 2s;
transition-duration: 2s;
```

#### transition-timing-function: 过渡的时序函数

指定过渡的执行的方式  
可选值： 
ease 默认值，慢速开始，先加速，再减速
linear 匀速运动
ease-in 加速运动
ease-out 减速运动
ease-in-out 先加速 后减速
cubic-bezier() 来指定时序函数
https://cubic-bezier.com（贝塞尔函数的网站）
steps() 分步执行过渡效果
可以设置一个第二个值：
end ， 在时间结束时执行过渡(默认值)
start ， 在时间开始时执行过渡

```
transition-timing-function: cubic-bezier(.24,.95,.82,-0.88);
transition-timing-function: steps(2, start);
```

#### transition-delay: 过渡效果的延迟，等待一段时间后在执行过渡

```
transition-delay: 2s;
```

**transition 可以同时设置过渡相关的所有属性**，只有一个要求，如果要写延迟，则两个时间中第一个是持续时间，第二个是延迟

```
transition:2s margin-left 1s cubic-bezier(.24,.95,.82,-0.88);
```

### 动画

动画和过渡类似，都是可以实现一些动态的效果，不同的是过渡需要在某个属性发生变化时才会触发，而动画可以自动触发动态效果
设置动画效果，必须先要设置一个关键帧，关键帧设置了动画执行每一个步骤

​	关键帧
```
@keyframes test {
            /* from表示动画的开始位置 也可以使用 0% */
            from{
                margin-left: 0;
                background-color: orange;
            } 

            /* to动画的结束位置 也可以使用100%*/
            to{
                background-color: red;
                margin-left: 700px;
            }
        }
```
#### animation-name: 要对当前元素生效的关键帧的名字

```
animation-name: test;
```

#### animation-duration: 动画的执行时间

```
animation-duration: 4s;
```

#### animation-delay:动画的延时

```
animation-delay: 2s;
```

#### animation-timing-function:动画的时序函数，和过渡类似

```
animation-timing-function: ease-in-out;
```

#### animation-iteration-count：动画执行的次数

可选值：
次数
infinite 无限执行

```
animation-iteration-count: infinite;
```

#### animation-direction：指定动画运行的方向

可选值：
normal 默认值  从 from 向 to运行 每次都是这样 
reverse 从 to 向 from 运行 每次都是这样 
alternate 从 from 向 to运行 重复执行动画时反向执行
alternate-reverse 从 to 向 from运行 重复执行动画时反向执行

```
animation-direction: alternate-reverse;
```

#### animation-play-state: 设置动画的执行状态 

可选值：
	running 默认值 动画执行
	paused 动画暂停

```
animation-play-state: paused;
```

#### animation-fill-mode: 动画的填充模式

可选值：
	none 默认值 动画执行完毕元素回到原来位置
	forwards 动画执行完毕元素会停止在动画结束的位置
	backwards 动画延时等待时，元素就会处于开始位置
	both 结合了forwards 和 backwards

```
animation-fill-mode: both;
```

**animation和过渡transition一样，可以设置为简写属性**，同样，如果要写延迟，则两个时间中第一个是持续时间，第二个是延迟

### 变形

变形就是指通过CSS来改变元素的形状或位置
变形不会影响到页面的布局
	transform 用来设置元素的变形效果
平移：
	translateX() 沿着x轴方向平移
	translateY() 沿着y轴方向平移
	translateZ() 沿着z轴方向平移
平移元素，百分比是相对于自身计算的

```
transform: translateX(100%);
```

#### 变形的原点

transform-origin:变形的原点 默认值 center
```
transform-origin:20px 20px;
```
#### z轴平移

z轴平移，调整元素在z轴的位置，正常情况就是调整元素和人眼之间的距离，
距离越大，元素离人越近

z轴平移属于立体效果（近大远小），默认情况下网页是不支持透视，如果需要看见效果必须要设置网页的视距

```
html{
            /* 设置当前网页的视距为800px，人眼距离网页的距离 */
            perspective: 800px;
        }
```

#### 旋转

通过旋转可以使元素沿着x y 或 z旋转指定的角度
	rotateX()
	rotateY()
	rotateZ()

```
transform: rotateZ(.25turn); 
transform: rotateY(180deg) translateZ(400px); 
transform: translateZ(400px) rotateY(180deg) ; 
transform: rotateY(180deg);
```
##### 是否显示元素的背面

​	hidden 不显示
​	visible 显示

```
backface-visibility: hidden;
```

##### *关于元素的居中

```
这种居中方式，只适用于元素的大小确定
top: 0;
left: 0;
bottom: 0;
right: 0;
margin: auto; 

这种居中方式，才可以让元素真正在页面中央
left: 50%;
top: 50%;
transform: translateX(-50%) translateY(-50%);
```

#### 缩放

对元素进行缩放的函数：
	`scaleX()` 水平方向缩放
	`scaleY()` 垂直方向缩放
	`scale()` 双方向的缩放

```
transform:scale(2);
```

## flex(弹性盒)

### 弹性盒

#### flex(弹性盒、伸缩盒)

​	是CSS中的又一种布局手段，它主要用来代替浮动来完成页面的布局
​	flex可以使元素具有弹性，让元素可以跟随页面的大小的改变而改变

#### 弹性容器

​	要使用弹性盒，必须先将一个元素设置为弹性容器
​	我们通过 display 来设置弹性容器
​		`display:flex`  设置为块级弹性容器
​		`display:inline-flex` 设置为行内的弹性容器

#### 弹性元素

​	弹性容器的子元素是弹性元素（弹性项）
​	弹性元素可以同时是弹性容器

##### 	弹性元素的属性

​		`flex-grow` 指定弹性元素的伸展的系数
​			当父元素有多余的空间时，子元素如何伸展。父元素的剩余空间，会按照比例进行分配
​		`flex-shrink` 指定弹性元素的收缩系数
​			当父元素中的空间不足以容纳所有的子元素时，可以对子元素进行收缩

​		`flex-direction` 指定容器中弹性元素的排列方式
​			可选值：
​				row 默认值，弹性元素在容器中水平排列（左向右）
​				主轴 自左向右
​				row-reverse 弹性元素在容器中方向水平排列（右向左）
​				主轴 自右向左
​				column 弹性元素纵向排列（自上向下）
​				column-reverse 弹性元素方向纵向排列（自下向上）

​	**主轴**
​		弹性元素的排列方向称为主轴
​	**辅轴**
​		与主轴垂直方向的称为辅轴

#### 弹性容器的样式

##### flex-wrap设置弹性元素是否在弹性容器中自动换行

​	可选值：
​		nowrap 默认值，元素不会自动换行
​		wrap 元素沿着辅轴方向自动换行
​		wrap-reverse 元素沿着辅轴反方向换行

##### flex-flow:  wrap 和 direction 的简写属性

##### justify-content 如何分配主轴上的空白空间（主轴上的元素如何排列）

​	可选值：
​		flex-start 元素沿着主轴起边排列
​		flex-end 元素沿着主轴终边排列
​		center 元素居中排列
​		space-around 空白分布到元素两侧
​		space-between 空白均匀分布到元素间
​		space-evenly 空白分布到元素的单侧

##### align-items: 元素在辅轴上如何对齐

元素间的关系
	可选值：
			stretch 默认值，将元素的长度设置为相同的值
			flex-start 元素不会拉伸，沿着辅轴起边对齐
			flex-end 沿着辅轴的终边对齐
			center 居中对齐
			baseline 基线对齐

##### align-content: 辅轴空白空间的分布

和justify-content类似

#### 弹性元素的样式

##### 弹性的增长系数

```
flex-grow: 1;
```

##### 弹性元素的缩减系数

​	缩减系数的计算方式比较复杂
​	缩减多少是根据 缩减系数 和 元素大小来计算

```
flex-shrink: 1;
```

##### 元素基础长度

​	flex-basis 指定的是元素在主轴上的基础长度
​		如果主轴是 横向的 则 该值指定的就是元素的宽度
​		如果主轴是 纵向的 则 该值指定的是就是元素的高度
​		默认值是 auto，表示参考元素自身的高度或宽度
​		如果传递了一个具体的数值，则以该值为准

```
flex-basis: auto;
```

##### flex 可以设置弹性元素所有的三个样式

flex 增长 缩减 基础（得按照顺序来）
	initial "flex: 0 1 auto"
	auto  "flex: 1 1 auto"
	none "flex: 0 0 auto" 弹性元素没有弹性

##### order: 决定弹性元素的排列顺序

##### align-self: 用来覆盖当前弹性元素上的align-items

## *其他

### 像素
屏幕是由一个一个发光的小点构成，这一个个的小点就是像素
	分辨率：1920 x 1080 说的就是屏幕中小点的数量
在前端开发中像素要分成两种情况讨论：CSS像素 和 物理像素
	物理像素，上述所说的小点点就属于物理像素
	CSS像素，编写网页时，我们所用像素都是CSS像素
浏览器在显示网页时，需要将CSS像素转换为物理像素然后再呈现
	一个css像素最终由几个物理像素显示，由浏览器决定：
	默认情况下在pc端，一个css像素 = 一个物理像素

### 视口（viewport）

视口就是屏幕中用来显示网页的区域
可以通过查看视口的大小，来观察CSS像素和物理像素的比值
	默认情况下：
		视口宽度 1920px（CSS像素）
		1920px（物理像素）
			此时，css像素和物理像素的比是 1:1

​	放大两倍的情况：
​		视口宽度 960px（CSS像素）
​		1920px（物理像素）
​			此时，css像素和物理像素的比是1:2

我们可以通过改变视口的大小，来改变CSS像素和物理像素的比值

### 移动端

在不同的屏幕，单位像素的大小是不同的，像素越小屏幕会越清晰
	24寸 1920x1080
	iphone6 4.7寸 750 x 1334

智能手机的像素点 远远小于 计算机的像素点

问题：一个宽度为900px的网页在iphone6中要如何显示呢？

​	默认情况下，移动端的网页都会将视口设置为980像素（css像素），以确保pc端网页可以在移动端正常访问，但是如果网页的宽度超过了980，移动端的浏览器会自动对网页缩放以完整显示网页

​		https://material.io/resources/devices/（各种移动端的尺寸大小）

​	所以基本大部分的pc端网站都可以在移动端中正常浏览，但是往往都不会有一个好的体验，为了解决这个问题，大部分网站都会专门为移动端设计网页

#### 完美视口

​	移动端默认的视口大小是980px(css像素)，
​	默认情况下，移动端的像素比就是  980/移动端宽度
​	如果我们直接在网页中编写移动端代码，这样在980的视口下，像素比会非常不好，导致网页中的内容非常非常的小
​		所以编写移动页面时，必须要确保有一个比较合理的像素比：
​			1css像素 对应 2个物理像素
​			1css像素 对应 3个物理像素

​	我们可以通过meta标签来设置视口大小

每一款移动设备设计时，都会有一个最佳的像素比，
一般我们只需要将像素比设置为该值即可得到一个最佳效果
将像素比设置为最佳像素比的视口大小我们称其为完美视口

```
<!-- 设置视口大小 device-width表示设备的宽度（完美视口）-->
<meta name="viewport" content="width=device-width">
```

**结论：以后再写移动端的页面，就把上边这个玩意先写上**

#### vw（视口宽度）

不同的设备完美视口的大小是不一样的
	iphone6 -- 375
	iphone6plus -- 414

由于不同设备视口和像素比不同，所以同样的375个像素在不同的设备下意义是不一样，
	比如在iphone6中 375就是全屏，而到了plus中375就会缺一块

​	所以在移动端开发时，就不能再使用px来进行布局了

​		`vw` 表示的是视口的宽度（viewport width）
​			100vw = 一个视口的宽度
​			1vw = 1%视口宽度

​	vw这个单位永远相当于视口宽度进行计算

设计图的宽度
	750px 1125px（通常的宽度大小）

举例：
```
设计图 
750px  

使用vw作为单位
100vw

创建一个 48px x 35px 大小的元素

100vw = 750px(设计图的像素) 0.1333333333333333vw = 1px
6.4vw = 48px(设计图像素)
4.667vw = 35px
```

#### vw的适配

网页中字体大小最小是12px，不能设置一个比12像素还小的字体
如果我们设置了一个小于12px的字体，则字体自动设置为12

​	0.1333333vw = 1px
​	5.3333vw = 40px

完美可以利用rem进行适配，rem对应的是html的字体像素大小
	1 rem = 1 html的字体大小
	1 rem = 40 px(设计图)

#### 响应式布局

网页可以根据不同的设备或窗口大小呈现出不同的效果
	使用响应式布局，可以使一个网页适用于所有设备
	响应布局的关键就是 媒体查询
	通过媒体查询，可以为不通的设备，或设备不同状态来分别设置样式

#### 媒体查询

使用媒体查询 
	语法： `@media` 查询规则{}
媒体类型：
	`all` 所有设备
	`print` 打印设备
	`screen` 带屏幕的设备
	`speech` 屏幕阅读器
可以使用 **,** 连接多个媒体类型，这样它们之间就是一个**或**的关系

可以在媒体类型前添加一个`only`，表示只有。
`only`的使用主要是为了兼容一些老版本浏览器

​	媒体特性：
​		width 视口的宽度
​		height 视口的高度

​		min-width 视口的最小宽度（视口大于指定宽度时生效）
​		max-width 视口的最大宽度（视口小于指定宽度时生效）

```
@media only screen and (min-width: 500px) and (max-width:700px){
	body{
		background-color: #bfa;
	}
}
```

#### 断点

样式切换的分界点，我们称其为断点，也就是网页的样式会在这个点时发生变化
一般比较常用的断点

​	小于768 超小屏幕 max-width=768px
​	大于768 小屏幕   min-width=768px
​	大于992 中型屏幕 min-width=992px
​	大于1200 大屏幕  min-width=1200px