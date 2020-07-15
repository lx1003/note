### 一、JavaScript组成

1.ECMAScript

2.BOM   浏览器

3.DOM   document 文档 整个文档

### 二、JS语法

```javascript
	<script type="text/javascript">
    	alert("Hello World!");//弹出警告框
		document.write("Hello World");//文档输出
    </script>
```

【注】每一条JS语句后都必须加分号

为了语法规范  script标签写在<head>标签中

可以引入多个<script>标签

如果当前的script标签作用引入外部文件，这个标签中，就不能再写js代码了

### 三、JavaScript变量

常量/字面量：确定的值叫做常量

【注】js中数据类型分为两大类

1.基本数据类型

​		<1>：数字 number  100

​		<2>：字符串 string  'hello' "hello"

​		<3>：布尔值 boolean true false

​		<4>特殊数据类型：null空  undefined未声明

 2.复合数据类型

使用变量：

1.声明变量：通过关键字var----在声明变量的时候赋值--初始化

同时声明多个变量

```javascript
var name="xxx",sex="男",age=18;
```

标识符：用户自定的所有名字叫做标识符

标识符必须由数字、字母、下划线和美元$组成

不能以数字开头

区分大小写

标识符必须见名思意

```javascript
typeof 变量名	
```



