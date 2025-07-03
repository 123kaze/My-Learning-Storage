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

```
//颜色有多种方式
color:red  //颜色名方式
color:rgb or hex  //rgb或者hex表示颜色
rgb：(0,0,0,0//可选)//0到255的红绿蓝三原色，后面是透明度
hex：rgb换成16进制
opacity(透明度属性)//对整个元素及其所有子元素
颜色可以赋值给所有样式，像文字，边框，底色等
<div class="background-color">HEllo World</div>
```



## 3.文本TEXT

```
font-family  //定义字体的属性
font-family:MaShanZhen,'sans-serif';//越前优先级越高
//大小和间距
font-size and line-height后面跟px
font-weight 可以调节粗细
font-style  实现斜体（跟italic）
text-decoration  实现字体装饰，诸如underline，overline，line-strough
```

通过这些，就可以做字体效果

## 4.盒子模型box

```
//按下F12，点击任何一个元素，看下面的计算样式就能看到一个box
从外到内是margin边距，border边框，padding填充和body本体（构建类的时候，本体把他们其他包起来）四个部分
前三个都有上下左右之分，即top，bottom，right，left后缀
margin: 6px 12px,第一个表示上下，第二个表示左右
也可以写四个，用上右下左的顺序
边框略有不同
border: 2px soild black;//指定像素之后还要指定边框是虚线，实线还是点线等，还要标注颜色
soild，实线dotted，点线，dashed，虚线
对于body
我们可以直接写weight:80px,height:120px
```

## 5.布局

```
//布局的属性为display
可选值：block，inline，inline-block，none（隐藏块级元素），flex（灵活布局），grid（网格布局）
block：独占一行，从上至下排列，有些默认块级，参考html文档
inline：不会独占一行，会和其他内联元素链接同一行
inline-block：类似内联元素，但是可以像上面的盒子一样设置margin等样式
none：设置后完全不可见
```

## 6.flex布局

flex很强大，所以单拎出来讲，

```
//flex需要一个父容器，即先将一个普通元素设置为flex，此后里面所有子元素都会成为弹性
<div class="flex">
  <div class="item">项目<div>//子元素
<div>//flex默认是水平的，通过flex-direction：colum可以把它变成纵向排列
其中，每一个弹性子元素占据的空间是可以调整的
.item {
  flex:1;//与其他flex比起来，占用的相对空间大小
}
排列时，如果不希望紧挨着，可以用gap属性
.gap {
  gap:12px;
}
//在弹性布局里面，我们可以沿主轴或交叉轴以不同方式对齐
.flex {
  display:flex;
  justify-content：flex-end//横向自动对齐,以末尾位置flex-end，center中心
  align-items： flex-start //如果为row，纵向排列，那么开始，此外，它还有两个常用的值space-between和space-around
  //space-between会把多余的空间压缩到两侧，space-around会在弹性项目周围均匀分布空白空间，使空白空间是项目空白空间之间的一半
  height：12px；
}
```

还有position，之后学

## 7.网格布局

以行和列的形式划分容器，也需要一个父容器

```
 .grid {
   display:"grid";
   grid-tamplete-rows:100px 200px 300px;//指的是指定三行，第一行100，第二行200，第三行300
   grid-tamplete-colums:1fr 2fr ;//指的是指定两列，第一列占据的空间是第二列的一半（理解为flex）
   //如果不想主动指定，可以自动
   grid-auto-rows: 100px;//每行100px
   grid-auto-colums: 1fr;//自适应每列等宽
   
   grid-gap:12px；//同样，可以调节gap空隙，让他们不要紧挨着
 }
```

## 8.position定位

它可以让位置脱离文档流

```
可选：relative，相对定位，absolute，绝对定位，fixed，固定位置，static，静态定位，也是默认
不同定位参考系不同，相对定位按照自身位置进行定位，绝对定位相对与最近的static静态定位定位（需要一个父元素），固定为fixed则参考浏览器窗口

如果你想相对谁（参考）进行定位，那就把相对的（参考）设置为relative
<div class="relative">
  <div class="absolute">图片</div>   //相对父元素
</div>
这时候，就可以用top，bottom，rigth等让“图片”相对于父元素进行位移了
.absolute {
  position: absolute;
  top:50%;
  left:50%;
  transform: translate(-50%,-50%);//向左上移动
}
固定fixed因为相对于浏览器窗口，所以经常用来做导航栏侧边栏等。
```

















