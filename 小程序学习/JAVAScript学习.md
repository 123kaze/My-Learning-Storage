# JS学习





[TOC]





## 13.对象数组与json

### 13.1  对象数组类比c\cpp里面的结构体

```
const todos=[
	{
		id:1,//这里用的逗号，不是分号，要特别留意
		text:"Take out trash"，
		isCompleted:True，
	},
	{
		id:2，
		text:"Take out trash"，
		isCompleted:False，
	},//逗号不要忘了！！！
	{
		id:3，
		text:"Take out trash"，
		isCompleted:True，
	}//对象里面还能嵌套对象
]//这样就是一个对象数组，每一个代表储存的对象
console.log(todos);//会得到一个和上面一模一样的输出结果，与c，cpp不同，它不用循环遍历就能直接输出
console.log(todos[1].txt);//下标是从零开始，所以这里打印的是id2的内容


//把对象数组变成Json，记一下
const todoJSON = JSON.stringify(todos);
//这样就把todos变成了JSon格式
```

### 13.2  Json文件

​	类比python里边的字典，cpp的结构体，和对象数组非常类似

```
const todos=[
	{
		"id":1，
		"text":"Take out trash"，
		"isCompleted":True，
	},
	{
		"id":2，
		"text":"Take out trash"，
		"isCompleted":True，
	},//逗号不要忘了！！！
	{
		"id":3，
		"text":"Take out trash"，
		"isCompleted":True，
	}
]//和对象数组不同的是，前面的名字一定要有""隔起来。
```



## 14.if与else条件判断

```
const x="10";（string类型）
if (x==10“number类型”){
	console.log("x is 10");
}//三等号，则要判断数据类型，双等号，则只判断数值。
elseif(条件){
    console.log(xxxx);
}
else{
	xxxxxxxxx;
}
```

## 15.三目运算符

表示判断x是否大于10，如果大于则red，如果小于则蓝色

```
const x=10;
const color =x > 10? "red":"blue";
console.log(color);
```

## 16.switch语句

也是条件语句，类似cpp，case匹配值。**c的case不能用字符串**

```
const x=10;
const color =x > 10? "red":"blue";
switch(color){
	case"red"://如果是红色，就输入xxxx
	  console.log("color is red");
	  break;
	case"blue":
	  console.log("color is blue");
	  break;
	defaulet://表示不是上述任何情况
	  console.log("color is not red or blue.");
	  break;//如果不写break，就会执行后面的所有语句而无视case条件，直到遇到break。
}
```

## 17.for与while

类比cpp

```
//For
for(let i = 0;i<10;i++){
	console.log(i);
    console.log('For loop number: ${i}');//模板字符串用法，${变量名}
}
//while要在外部声明循环变量
let i=0;
while(i<10){
	console.log(i);
    console.log('For loop number: ${i}');
    i++;//一定要在while里面改变循环变量
}


//对象数组也能进行循环
for(let i=0; i < todos.length; i++){
	console.log(todos[i].text);
}
for(let todo(换成i也一样，只是个变量名字) of todos)//表示遍历todos数组中的每一项{
	console.log(todo);//得到的数组中的每一项
	console.log(todo.text);//得到每一项的text
}
```

