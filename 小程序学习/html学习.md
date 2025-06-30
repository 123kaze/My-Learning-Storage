# HTML学习







[TOC]



## 1.HTML页面结构

为方便，本文中“//”后均为注释。

```
//vscode里面按下！+Tab就可以自动生成
<!DOCTYPE html>//表示声明这个文件是html
<html lang="en">
  <head>//head头表示浏览器页面上面看到的东西，定义标题，连接工程类的css或者js文件等，定义搜索引擎可以搜到的网站描述，关键词
	<meta charset="UTF-8">//设置为UTF-8显示模式
	<title>Document</title>
  </head>
  <body>//表示内部显示的东西
	.................
  </body>
</html>
```

这就是一个html文件应该有的各种结构

## 2.注释与标签

```
<!DOCTYPE html>
<html>
  <head>html tutorial</title>
  <body>
	<!--这样的结构表示一个注释-->//vscode快捷键是/+ctrl
	<h1>Heading 1</h1>//标题标签，h1会让文字变得更大，加上空白填充，同理，还有h2，h3，它会让文本换行显示，可以用css改变
	
	<!--段落标签-->//块级元素
	<p>
	  Hello World
	</p>
  </body>
</html>
```

## 3.行级元素与块级元素

```
<!DOCTYPE html>
<html>
  <head>html tutorial</title>
  <body>
	<!--这样的结构表示一个注释-->//vscode快捷键是/+ctrl
	<h1>Heading 1</h1>//标题标签，h1会让文字变得更大，加上空白填充，同理，还有h2，h3，它会让文本换行显示，可以用css改变
	
	<!--段落标签-->//块级元素
	<p>
	  Hello World
	</p>
  </body>
</html>
```

标签可以是行级元素，也可以是块级元素。行级元素不会提行，所占空间和自身所占空间有关。块级元素则不同，会新起一段，占据给定一行的100%宽度

```
//块级元素 div h p form ...
//行级元素 span image a strong em vedio ...
<strong> 对内容进行加粗 <em> 将某些内容改为斜体 <a> 链接标签，可以去其他页面或者其他网站，a一般需要属性，如href

<a href="http:xxxx.com">repudiandae?</a>  //用法例子
<a href="http:xxxx.com" target="_blank">repudiandae?</a>  //如果希望在新标签中打开页面，则加一个target属性
```

## 4.标签属性

所有标签都可以有属性，且可以不只有一个属性。属性的意义在于提供某个元素的更多信息 例如刚刚的href target

```
href  //打开某个标签的地址
target  //在新标签页面中被打开
属性通常写在标签头里面，且以键值对的形式 可以写那些属性？去w3school可以查询
```

[w3school](https://www.w3school.com.cn/)

```
<h1 align="center"> 拥有关于对齐方式的附加信息
<body bgcolor="yellow"> 拥有关于背景颜色的附加信息。
<table border="1"> 拥有关于表格边框的附加信息。table定义表格
class	规定元素的类名（classname）
id		规定元素的唯一id
style	规定元素的行内样式（inline style）规定元素的行内 CSS 样式，后面一般加类。
title	规定元素的额外信息（可在工具提示中显示）
```

[完整的标签名](https://www.w3school.com.cn/tags/index.asp)

[HTML 全局属性](https://www.w3school.com.cn/tags/html_ref_standardattributes.asp)

```
Type的属性表
1. input 输入标签的 type 属性
1.1 input 标签的 type类型 属性的常用属性值
⑴ 单行文本框: type="text"
⑵ 密码框: type="password"
⑶ 复选框: type="checkbox"
⑷ 隐藏值: type="hidden"
♣ 6 种 按钮类型
⑸ 文件上传: type="file"
⑹ 图片提交按钮: type="image"
⑺ 按钮: type="button"
⑻ 单选按钮: type="radio"
⑼ 重置清空表单: type="reset"
⑽ 提交按钮: type="submit"
1.2 input 标签的 type 属性的 html5 新增类型值
⑴ 颜色: type="color" （颜色选择器 / 颜色文本框）
⑵ 年月日: type="date"( yyyy-MM-dd )
⑶ 年月日 小时分钟: type="datetime-local"( yyyy-MM-ddThh:mm )
⑷ 年月: type="month" ( YYYY-MM )
⑸ 年份 周号: type="week" ( yyyy-Www )
⑹ 小时 分钟,可选的秒: type="time"( hh:mm, hh:mm:ss)
⑺ 输入数字: type="number"
⑻ 不精确数值 (范围数值): type="range"
⑼ 搜索文本框: type="search"
⑽ 输入电话号码: type="tel"
⑾ 输入url: type="url"
⑿ 邮箱: type="email"
```

[【input 标签的 type 属性详解】_input type属性-CSDN博客](https://blog.csdn.net/VickyTsai/article/details/94839889)

## 5.列表标签与表格标签

```
//列表有有序列表和无序列表
<ul>//无序列表
  <li>//列表项标签名字</li>
  <li>//列表项标签名字</li>
  <li>//列表项标签名字</li>
</ul>
<ol>//有序标签
  <li>//列表项标签名字</li>
  <li>//列表项标签名字</li>
  <li>//列表项标签名字</li>
</ol>
```

无序列表默认样式大概如下：

- 1
- 2
- 3

```
<table>//表格标签,表格分为两个标签，一个表头，一个表体<tr>表示行，<th>表示列名，<td>表示值
  <thead>
    <tr>
    <th>name</th>
    </tr>
  </thead>//t(able)head标签表示表头
  <tbody>
    <tr>
    <td>name</td>
    </tr>//复制以产生多行
    <tr>
    <td>name</td>
    </tr>
  </tbody>
</table>         //tips：以前的时候是这样完成web开发的，现在要求越来越高，必须用css完成
```



## 6.表单标签与输入标签

表单  form

```
//表单非常常见，如登陆表单，注册表单，我们只能用html构建表单外观，不能做功能
<form action="">//action可以指定我们把表单数据提交到哪里，但是我们一般用其他方法处理
  <label>name:</label>
  <input type="text">//type的值可以有非常多种
</form>

<br>// 水平的空白行
<hr>// 水平的分割线  这两个都不用闭包

如果你希望让他们纵向排列，可以使用div分割他们，变成这样：
<form action="">
  <div><label>name:</label><input type="text"></div>
  <div><label>name:</label><input type="text"></div>//  对其中的type值进行变化，可以得到不同的输入框
  <div><label>password:</label><textarea></textarea></div>//textarea相比起input更大，而且大小可以在页面改变
  <div><select><option value=""></option></select></div>//select选项框，option选项，代表的值写在value，显示内容写在中间
</form>
```

## 7.按钮与图片

```
<button>点我</button>//没有绑定事件
<img src="" alt="" width="" hight="">//自闭合，在src里面写图片的路径，链接与本地都可以，在alt里是图片备选文本，加载不出图片则显示，他也是一个行级元素。
```

