<u>一切符合W3C规范</u>

**HTML**

**CSS**

**JavaScript**

# **HTML**

## HTML基本格式

```
<!-- 文档声明 -->
<!doctype html>
<html>
	<head>
		<!-- 通过meta标签设置网页的字符集，避免乱码 -->
		<meta charset="utf-8">
		<title>标题</title>
	</head>
<body>
	<!-- font标签：设置字体颜色和大小 注意：不建议使用 -->
	<h1>网页<font color="red" size="16">一级</font>标题</h1>
	<h2>二级标题</h2>
	<h3>三级标题</h3>
	<p>段落</p>
</body>
</html>
```

文档查看网站：www.w3cschool.cn.com

## *注释*

```
<!-- 注释内容 -->
```

注释不可嵌套



## *属性*

在标签（开始或自结束标签）中可以设置属性
	属性是一个名值对（x=y）
	属性用来设置标签中的内容如何显示
	属性和标签名或其他属性应该使用空格隔开
	属性不能瞎写，应按照文档中的规定来写
		有些属性有属性值，有些没有，属性值应该使用引号(单双引号都可)括起来

## *实体*

在网页中编写的多个空格默认情况会自动被浏览器解析为一个空格

​    在HTML中有些时候，我们不能直接书写一些特殊符号

​      比如：多个连续的空格，比如字母两侧的大于和小于号

如果需要在网页中书写一些特殊的字符，需要使用html中的实体（转义字符）
    实体的语法：&实体名字;
		例：

```
	&nbsp; 空格
	&gt; 大于号
	&lt; 小于号
	&copy; 版权符号 
```

```
<p>
    今天&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;天气真不错！
</p>
```

## *标签*

在网页中html只是专门用来负责网页结构的

	所以在使用html标签时，应关注标签语义而非样式

### 1.meta标签

（写在head标签里面,自结束标签）
meta主要用于设置网页中的一些元数据，元数据不是给用户看的
	`charset` 指定网页的字符集
	`name` 指定的数据名称
	`content` 指定数据的内容
		`keywords` 表示网站关键字，可同时指定多个关键字，关键字间用“,”隔开
		`description` 用于指定网站的描述
		`title` 标签内容将会作为搜索结果的超链接文字显示

	<meta name="keywords" content="HTML5,前端,CSS3">
	     <meta name="description" content="这是一个非常不错的网站">
	
	<meta http-equiv="refresh" content="3,www.baidu.com">
	<!--表示将页面重定向到另一个网站 数字3表示三秒后转向-->

### 2.标题标签

​	h1 ~ h6 一共有六级标题
​	从h1~h6重要性依次递减
​	h1在网页中的重要性仅次于title标签，一般情况下一个网页中只有一个h1标题
​	一般只会使用到h1~h3，h4~h6很少用

		<h1>一级标题</h1>
		<h2>二级标题</h2>
		<h3>三级标题</h3>
		<h4>四级标题</h4>
		<h5>五级标题</h5>
		<h6>六级标题</h6>

标题标签都是块元素

#### 块元素

在页面中独占一行的元素称为**块元素**（block element）

### 3.hgroup标签

​	hgroup标签用来为标题分组，可将一组相关的标题同时放入到hgroup

```
	<hgroup>
		<h1>一级标题</h1>
		<h2>二级标题</h2>
	</hgroup>
```

### 4.p标签

​	p标签表示页面中的一个段落
​	p标签也是一个块元素
​	p元素里面不能放块元素

```
	<p>在p标签中的内容就表示一个段落</p>
```

### 5.em标签

​	em标签表示语音语调的一个加重

```
	<p>今天天气<em>真</em>不错！</p>
```

### 6.strong标签

​	strong标签表示强调重要内容

```
	<p>你今天必须要<strong>完成作业</strong>！</p>
```

### 7.blockquote标签

​	blockquote标签表示一个长引用

```
鲁迅说：
	<blockquote>
		这句话我没有说过
	</blockquote>
```

### 8.q标签

​	q标签表示一个短引用

```
子曰<q>学而时习之，不亦乐乎</q>
```

```
em标签、strong标签等都是行内元素
```
#### 行内元素

在页面中不会独占一行的元素称为行内元素/内联元素（inline element）

### 9.br标签

​	br标签表示页面中的换行

### 10.布局标签（结构化标签）

​	`header` 表示网页的头部
​	`main` 表示网页的主体部分（一个网页中只会有一个main）
​	`footer` 表示网页的底部
​	`nav` 表示网页中的导航
​	`aside` 和主体相关的其他内容（侧边栏）
​	`article` 表示一个独立的文章
​	`section` 表示一个独立的区块，上边的标签都不能表示时使用section
​	`div` 没有语义，就用来表示一个区块，div是目前使用得到主要布局元素
​	`span` 行内元素，没有任何意义，一般用于在网页中选中文字

```
	<header></header>
	<main></main>
	<footer></footer>

	<nav></nav>
	<aside></aside>
	<article></article>

	<section></section>

	<div></div>

	<span></span>
```

### 11.图片标签

​	图片标签勇于向当前页面中引入一个外部图片
​	使用img标签来引入外部图片，img标签是一个自结束标签
​	img这种元素属于替换元素（块和行内元素之间，具有两种元素的特点）
​	属性：
​		`src` 属性指定的是外部图片的路径（路径规则和超链接一样）
​		`alt` 图片的描述，这个描述默认情况下不会显示，有些浏览器会在图片无法加载时显示。搜索引擎会根据alt中的内容来识别图片，如果不写alt属性则图片不会被搜索引擎所容纳
​		`width` 图片的宽度
​		`height` 图片的高度（单位都是像素）
​			宽度和高度中如果只修改了一个，则另一个会等比例缩放

```
	<img width="200" height="100" src="./xxx/xxx.gif(这里也可以填写外部图片路径和图片的base64格式)" alt="图片描述">
```

​	注意：
​		一般情况在pc端，不建议修改图片的大小，图片大小根据需求裁剪
​		但是在移动端，经常需要对图片进行缩放（大图缩小）


	图片的格式
		jpeg（jpg）
			支持的颜色丰富，不支持透明效果，不支持动图
			一般用来显示照片
		gif
			支持的颜色少，支持简单透明效果，支持动图
			颜色单一的图片，动图
		png
			支持的颜色丰富，支持复杂透明效果，不支持动图
			颜色丰富，复杂透明图片（专为网页而生）
		webp
			这是谷歌推出的专门用来表示网页中图片的一种格式
			它具备其他图片所有优点，文件还小
			缺点：兼容性不好
		base64
			将图片使用base64编码，这样可以将图片转换为字符，通过字符的形式来引入图片
			一般都是一些需要和网页一起加载的图片才会使用base64
	选图原则：
		效果一样，用小的
		在保证图片不过大的前提下，效果不一样，用效果好的
`更多标签可自行查找`

```
块元素（block element）
	- 在网页中一般通过块元素来对页面进行布局
行内元素/内联元素（（inline element）
	- 行内元素用来包裹文字，让文字产生特殊效果
	
	- 一般情况下会在块元素中放行内元素，而不会在行内元素中放块元素
	- 块元素中基本上什么都能放
	- p元素中不能放任何的块元素
	
浏览器在解析网页时，会自动对网页中不合规范的内容进行修正
	如：
		标签写在根元素外部
		p元素中嵌套了块元素
		根元素中出现了除head和body以外的子元素
		... ...
```

## *列表*

### 1.有序列表

有序列表，使用`ol`标签来创建有序列表
	使用li表示列表项

### 2.无序列表

无序列表，使用`ul`标签来创建无序列表
	使用li表示列表项
`ul是块元素`

### 3.定义列表

定义列表，使用`dl`标签来创建一个定义列表
	使用`dt`来表示定义的内容
	使用`dd`来对内容进行解释说明

```
 <ul>
        <li>结构</li>
        <li>表现</li>
        <li>行为</li>
    </ul>

    <ol>
        <li>结构</li>
        <li>表现</li>
        <li>行为</li>
    </ol>


    <dl>
        <dt>结构</dt>
        <dd>结构表示网页的结构，结构用来规定网页中哪里是标题，哪里是段落</dd>
        <dd>结构表示网页的结构，结构用来规定网页中哪里是标题，哪里是段落</dd>
        <dd>结构表示网页的结构，结构用来规定网页中哪里是标题，哪里是段落</dd>
    </dl>
```

**列表之间可以互相嵌套**

```
    <ul>
        <li>
            aa
            <ul>
                <li>aa-1</li>
                <li>aa-2
                    <ul>
                        <li>aa-1</li>
                        <li>aa-2</li>
                    </ul>
                </li>
            </ul>
        </li>
    </ul>
```

## *超链接*

超链接可以让我们从一个页面跳转到其他页面，或者是当前页面的其他位置

使用a标签来定义超链接
属性：
	`href` 指定跳转的目标路径

值可以是一个外部网站的地址
也可以写一个内部页面的地址
可以直接将超链接的href属性设置为#，这样点击超链接以后页面不会发生跳转，而是转到当前页面的顶部位置

```
	<a href="#">去页面顶部位置</a>
```

可以跳转到页面的指定位置，只需将href属性设置为 `#目标元素的id属性`

```
	<a href="#bottom">去底部</a>
	<a href="#p3">去第三个自然段</a>
	
	<p id="p3">第三个自然段</p>
	<p id="bottom">页面底部</p>
```

### id属性（唯一不重复的）

​	每一个标签都可以添加一个id属性
​		id属性就是元素的唯一标识，同一个页面中不能出现重复的id属性
​		id都是字母开头，不能使用数字开头
​		在开发中可以将#作为超链接的路径的占位符使用
​		也可以使用 `Javascript:;` 来作为href的属性，此时点击这个超链接什么也不会发生

超链接也是一个行内元素，在a标签中可以嵌套除它自身之外的任何元素

```
	<a href="https://www.baidu.com">超链接</a>
```

## *相对路径*

​	当我们需要跳转到一个服务器内部的页面时，一般我们都会使用相对路径
​		相对路径都会使用./跟../开头
​	./可以省略不写，如果./和../都不写，则默认写了./
​	./表示当前文件所在的目录
​	../表示当前文件所在目录的上一级目录

```
	<a href="./xxx.html">超链接1</a> 

	<a href="../xxxx.html">超链接2</a>

	<a href="./xxx1/xxx.html">超链接3</a>

	<a href="../xxx2/xxxx.html">超链接4</a>
```

### target属性

用来指定超链接打开的位置
	可选值：
		`_self` 默认值 在当前页面中打开超链接
		`_blank` 在一个新的页面中打开超链接

```
	<a href="xxx" target="_blank">超链接</a>
```

## *内联框架*

​	`iframe` 内联框架，用于向当前页面中引入一个其他页面
​		`src` 指定要引入的网页的路径
​		`frameborder` 指定内联框架的边框（1为有边框 0为无边框）
​		也有 `width` 和 `height` 来调整高宽

```
	<iframe src="https://www.qq.com" width="800" height="600" frameborder="0"></iframe>
```

## *音视频播放*

### audio标签

用来向页面中引入一个外部的音频文件
	音频文件引入时，默认情况下不允许用户自己控制播放停止
		属性：
			controls 是否允许用户控制播放
			autoplay 音频文件是否自动播放
		如果设置了 autopaly 则音乐在打开页面时会自动播放
		但是目前来讲大部分浏览器都不会自动对音乐进行播放
			loop 音乐是否循环播放

```
	<audio src="./xxx/xxx.mp3" controls autoplay loop></audio>
```

除了通过src来指定外部文件得到路径以外，还可以通过source来指定文件

```
	<audio controls>
		<source src="./xxx/xxx.mp3">
		<!-- 以下embed标签是为了确保所有浏览器都可以兼容运行 type 是音频的名字和格式 -->
		<embed src="./xxx/xxx.mp3" type="xxx/mp3" width="xxx" height="xxx">
	</audio>
```

### video标签

用来向网页中引入一个视频
使用方式和audio基本上是一样的

```
	<vedio controls>
		<source src="./xxx/xxx.mp4">
		<!-- 以下embed标签是为了确保所有浏览器都可以兼容运行 type 是视频的名字和格式 -->
		<embed src="./xxx/xxx.mp3" type="xxx/mp4" width="xxx" height="xxx">
	</vedio>

	<!-- 以下是可以通过iframe标签将其他视频网站的视频直接引入到自己的网页中观看 同样可以通过 width height 设置宽高 省下了服务器的费用 不过这是没办法的办法 -->
	<iframe frameborder="0" src+"https:xxxx.com(网页的分享通用代码)">
```

## *表格*

在现实生活中，我们经常需要使用表格来表示一些格式化数据：
	课程表、人名单、成绩单....

同样在网页中我们也需要使用表格，我们通过table标签来创建一个表格

在table中使用tr表示表格中的一行，有几个tr就有几行
在tr中使用td表示一个单元格，有几个td就有几个单元格

`rowspan` 纵向的合并单元格

`colspan` 横向的合并单元格

```
<table border="1" width='50%' align="center">
        <tr>
            <td>A1</td>
            <td>B1</td>
            <td>C1</td>
            <td>D1</td>
        </tr>
        <tr>
            <td>A2</td>
            <td>B2</td>
            <td>C2</td>
            <td rowspan="2">D2</td>
        </tr>
        <tr>
            <td>A3</td>
            <td>B3</td>
            <td>C3</td>
        </tr>
        <tr>
            <td>A4</td>
            <td>B4</td>
            <td colspan="2">C4</td>
        </tr>
    </table>
```

### 长表格

可以将一个表格分成三个部分：
	头部 thead
	主体 tbody
	底部 tfoot

th 表示头部的单元格

三个部分在编写代码时，编写顺序不会影响其显示效果
```
<table border="1" width='50%' align="center">
        <thead>
            <tr>
                <th>日期</th>
                <th>收入</th>
                <th>支出</th>
                <th>合计</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>2000.1.1</td>
                <td>500</td>
                <td>200</td>
                <td>300</td>
            </tr>
            <tr>
                <td>2000.1.1</td>
                <td>500</td>
                <td>200</td>
                <td>300</td>
            </tr>
            <tr>
                <td>2000.1.1</td>
                <td>500</td>
                <td>200</td>
                <td>300</td>
            </tr>
            <tr>
                <td>2000.1.1</td>
                <td>500</td>
                <td>200</td>
                <td>300</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td></td>
                <td></td>
                <td>合计</td>
                <td>300</td>
            </tr>
        </tfoot>

    </table>
```

### 表格的样式

`border-spacing`: 指定边框之间的距离

```
border-spacing: 0px;
```
`border-collapse`: collapse; 设置边框的合并

```
border-collapse: collapse;
```
默认情况下元素在td中是垂直居中的 可以通过 `vertical-align` 来修改
```
vertical-align:middle;
text-align: center; 
```

如果表格中没有使用tbody而是直接使用tr，那么浏览器会自动创建一个tbody，并且将tr全都放到tbody中
	tr不是table的子元素

将元素设置为单元格 td

```
display: table-cell;
```

## 表单

表单：
	在现实生活中表单用于提交数据
	在网页中也可以使用表单，网页中的表单用于将本地的数据提交给远程的服务器
	使用form标签来创建一个表单
	

### form的属性

​	action为 表单要提交的服务器的地址

```
<form action="target.html">
```
#### input标签

文本框
​		注意：数据要提交到服务器中，必须要为元素指定一个name属性值

```
文本框 <input type="text" name="username">
```
密码框
```
密码框 <input type="password" name="password">
```
单选按钮
像这种选择框，必须要指定一个value属性，value属性最终会作为用户的填写的值传递给服务器
checked 可以将单选按钮设置为默认选中
```
单选按钮 <input type="radio" name="hello" value="a">
        <input type="radio" name="hello" value="b" checked>
```
多选框
```
多选框 <input type="checkbox" name="test" value="1">
        <input type="checkbox" name="test" value="2">
        <input type="checkbox" name="test" value="3" checked>
```
下拉列表
```
<select name="hello">
            <option value="i">选项一</option>
            <option selected value="ii">选项二</option>
            <option value="iii">选项三</option>
</select>
```
提交按钮
```
<input type="submit" value="注册">
```
autocomplete="off" 关闭自动补全
readonly 将表单项设置为只读，数据会提交
disabled 将表单项设置为禁用，数据不会提交
autofocus 设置表单项自动获取焦点
```
<input type="text" name="username" value="hello" readonly>

<input type="text" name="username" autofocus>

<input type="text" name="b">
```
颜色选择器
```
<input type="color">
```
邮件框
```
<input type="email">
```
重置按钮
```
<input type="reset">
```
普通的按钮（可通过JS设置更多属性，看似无用，实则很有用）

```
<input type="button" value="按钮">
```

#### button标签

​	button标签和input标签类似，不过input标签是自结束标签，这代表了button标签内可添加更多样式

```
<button type="submit">提交</button>
<button type="reset">重置</button>
<button type="button">按钮</button>
```

##### *获取搜索栏焦点的方法

即当鼠标点击了搜索栏状态

`:focus`  设置方法与hover一样

```
.search-wrapper .search-inp:focus
```

