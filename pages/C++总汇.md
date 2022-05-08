tags:: #编程语言

- # std::numeric_limits
	- 在库编译平台提供基础算术类型的极值等属性信息
- # size_t
	- C中任何对象所能达到的最大长度，是无符号整数
	-
	- 使用size_t可能会提高代码的可移植性、有效性或者可读性，或许同时提高这三者
	- 参考文章
		- [Why size_t matters](https://jeremybai.github.io/blog/2014/09/10/size-t)
- # STL库
	- ## fill函数
		- 用法用途
			- 按照单元赋值，将一个区间的元素都赋同一个值
			- fill(arr, arr + n, 要填入的内容);
		- 头文件：algorithm
		- 示例
			- ```cpp
			  #include <cstdio>
			  #include <algorithm>
			  using namespace std;
			  int main() {
			    int arr[10][10];
			    fill(arr[0], arr[0] + 10 * 10, 2);
			    return 0;
			  }
			  ```
		- 与memset()函数的区别
			- 两者都可以用来对数组填充。
			- memset是对按照字节来填充的，所以一般用来填充char型数组，也经常用于填充int型的全0或全-1操作
			- fill是按照单元来填充的，所以可以填充一个区间的任意值。
		- 参考文章
			- [Fill-百度百科](https://baike.baidu.com/item/Fill/18733662)
		- ## vector
			- emplace_back()
				- 直接在容器的尾部创建这个元素，省去了拷贝或移动元素的过程
				- 与push_back()的区别
					- push_back()方法要调用构造函数和复制构造函数，这也就代表着要先构造一个临时对象，然后把临时的copy构造函数拷贝或者移动到容器最后面。
					- ```cpp
					  vector<pair<int, int>> ret;
					  ret.push_back(1,1)//会报错，因为没有构造一个临时对象
					  ret.push_back(pair(1,1))//不会报错，因为构成了一个pair对象
					  ret.emplace_back(1,1)//不会报错，因为直接在容器的尾部创建对象
					  vector<vector<int>> ans;
					  ans.emplace_back();//这里的emplace_back()直接在ans的尾部创建一个类型为vector<int>的空对象，如果省去这一行，后面的ans.back()会是一个空指针而报错。
					  ```
				- 性能分析
					- emplace_back() 函数在原理上比 push_back() 有了一定的改进
					- **内存优化**主要体现在使用了就地构造（直接在容器内构造对象，不用拷贝一个复制品再使用）+强制类型转换的方法来实现
					- 在**运行效率**方面，由于省去了拷贝构造过程，因此也有一定的提升。
				- 参考文章
					- [关于emplace_back()的理解](https://blog.csdn.net/mmm123213/article/details/119282296)
					- [C++中push_back和emplace_back的区别](https://zhuanlan.zhihu.com/p/213853588)