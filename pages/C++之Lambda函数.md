tags:: #C++

- # 介绍
	- Lambda函数也叫匿名函数，是自定义函数的一种,专指用关键字” lambda”定义的无名短函数，所以也有Lambda表达式这种说法。这种函数得名于省略了用def声明函数的标准步骤，是C++ 11中新增的特性。
- # 语法
	- ```cpp
	  [capture](parameters) -> return_type { /* ... */ }
	  ```
	-
	- [capture] ：[]内为外部变量的传递方式，值、引用等，如下
		- ```cpp
		  []        //表示的是在lambda定义之前的域，对外部参数的调用；
		  [=]       //表示外部参数直接传值
		  [&]       //表示外部参数传引用，可修改值。当默认捕获符是 & 时，后继的简单捕获符必须不以 & 开始。而当默认捕获符是 = 时，后继的简单捕获符必须以 & 开始。
		  [x, &y]   //x is captured by value, y is captured by reference
		  [&, x]    //x is explicitly captured by value. Other variables will be captured by reference
		  [=, &z]   //z is explicitly captured by reference. Other variables will be captured by value
		  ```
		- (parameters) ：（）内为形参，和普通函数的形参一样。
		- -> return_type：->后面为lambda函数的返回类型，如 -> int、-> string等。一般情况下，编译器推出lambda函数的返回值，所以这部分可以省略不写。
		- { /* … */ }：{}内为函数主体，和普通函数一样。
- 参考文章
	- [C++中的Lambda函数](https://blog.csdn.net/weixin_42887343/article/details/122099296)