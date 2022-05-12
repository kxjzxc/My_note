tags:: #C++

- # future库
	- future对象提供访问异步操作结果的机制
	- ## std::future
		- ### 成员函数
			- **get()**
				- 当共享状态就绪时，返回存储在共享状态中的值(或抛出异常)。
				- 如果共享状态尚未就绪(即提供者尚未设置其值或异常)，则该函数将阻塞调用的线程直到就绪。
				- 当共享状态就绪后，则该函数将取消阻塞并返回(或抛出)，同时释放其共享状态，这使得future对象不再有效，因此对于每一个future共享状态，该函数最多应被调用一次。
				- 不返回任何值，但仍等待共享状态就绪并释放它。
			- **share()**
				- 获取共享的future，返回一个std::shared_future对象，该对象获取future对象的共享状态。future对象将不再有效。
			- **wait()**
				- 等待共享状态就绪，未就绪则该函数将阻塞调用的线程直到就绪。
				- 当共享状态就绪后，则该函数将取消阻塞并void返回。
			- **wait_for()**
				- 该函数将本线程阻塞在当前，并等待一段时间，后继续执行，若在等待时间内wait_for()绑定线程执行完毕，则返回ready，未执行完毕则返回timeout
				- 此函数的返回值类型为枚举类future_status。
				-
	- ```cpp
	  enum class future_status
	  {
	    ready,      //成功
	    timeout,    //超时
	    deferred    //延迟
	    };
	  ```
- 参考文章
	- [std::thread从入门到精通系列链接](https://zhuanlan.zhihu.com/p/463537452)
	- [C++ 多线程(二)：std::future](https://blog.csdn.net/qq_33726635/article/details/124085694)