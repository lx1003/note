##### 函数的概念：

​	函数，当它被调用时执行的可重复使用的代码块

```javascript
function 函数名(){
	函数体;
}
```

​																																																																																																																														函数分类：内置函数、用户自定义的函数

##### arguments数组

具体传入参数个数不确定

在每一个函数内，都有一个内置的数组，是一个变量，叫做arguments。arguments可以存储当前函数传入的所有参数，而且，是通过传参的顺序进行排列的

##### 作用域

全局作用域         生命的变量就是全局变量

局部作用域         函数局部作用域声明的变量 局部变量的生命周期和生效范围，都是声明该变量的函数区域，当函数调用完成后，就直接销毁



递归

方法：首先找到临界值

递归会在短时间内，使内存剧增											

