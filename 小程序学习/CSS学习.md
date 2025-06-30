# CSS学习初步





[TOC]

css是层叠样式表，可以做前端字体，样式，动画等，为方便，本文中“//”后均为注释。

## 1.选择器

在html的<head>里面用<link rel="stylesheet" herf="xxxx">把css文件引入

```
index.html
//元素选择器，类选择器，ID选择器
<h1>元素选择器</h1>//元素选择器是对语法标签改动，所有语法不变
<p class="class1">类选择器</p>//类选择器是指定class参数类变量，而id选择器是设置id为变量
<p id="id1">类选择器</p>//类选择器是指定class参数类变量，而id选择器是设置id为变量
//快捷输入方式p.(类名/id名)
```

```
index.css
h1 {
  color:red;//对标签的语法
}
.class1 {
  color:blue;//类语法，最常见，用它
}
#id1 {
  color：green;//id语法
}
//指定类的父子关系，层级
.child {
  color:brown;
}
.parent .child {
  color:gery;
}
或者
.parent {
  .child {
  color:brown;
}
}//这样就可以指定只有该父类中的子类可以使用该样式

//如果想分配不同样式到同一个元素上，那就加空格隔开类名
```

## 2.颜色