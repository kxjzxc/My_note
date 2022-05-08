tags:: #ROS

- # 消息类型
	- ros消息类型，即是ros话题的格式，可视为ros的数据类型，基本上是指同一个意思。
	- ros消息类型是基于C++基本类型封装为.msg文件实现，rosmsg指令用于消息管理。
	- ## 预定义消息类型
		- 基本数据类型
			- 在 std_msgs 包下，
			- 字符型、整型以及浮点型等
		- 常用的数据类型
			- 在 common_msgs 包下
			- 传感器数据类型、导航数据类型以及几何数据类型等。
- # 自定义消息类型
	- 在功能包下创建msg文件夹，与src文件夹同级
	- 在msg文件夹下创建一个`.msg`文件，并在文件中自定义内容
		- 示例
		  ```msg
		  float32[] data
		  float32 vel
		  geometry_msgs/Pose pose
		  string name
		  ```
		- 输入完成后，保存并关闭文件.
	- 修改CMakeLists.txt
		- ```CMake
		  cmake_minimum_required(VERSION 2.8.3)
		  project(custom_msg_topic)
		  # 调用find_package查找依赖的包
		  find_package(catkin REQUIRED COMPONENTS
		    roscpp
		    std_msgs
		    message_generation
		  )
		  # 指定msg文件
		  add_message_files(
		    FILES
		    custom_msg.msg
		  )
		  # 指定生成消息文件时的依赖项
		  generate_messages(
		    DEPENDENCIES
		    std_msgs
		  )
		  设置运行依赖
		  catkin_package(
		    LIBRARIES custom_msg_topic
		    CATKIN_DEPENDS roscpp message_runtime
		  )
		  include_directories(
		    ${catkin_INCLUDE_DIRS}
		  )
		  ```
	- 注意点：
		- 编译之后会在devel/include文件夹下生成头文件，而且消息类型是`vector`，可以用assign函数赋值。
- 参考文章
	- [ROS 消息](https://zhuanlan.zhihu.com/p/94338630)
	- [ROS自定义msg类型及使用](https://blog.csdn.net/u013453604/article/details/72903398)
-