tags:: #ROS

- # 自定义功能包
	- 功能包是一个存在于工作空间目录src目录下的一个目录
	- 一个功能包必须以下几部分组成：
		- 必须包括一个package.xml文件;
		- 必须包括一个CMakeLists.txt文件。
	- 在每一个功能包目录下不允许有其它的功能包，也就是不允许功能包嵌套。一个典型的工作空间结构如下：
		- ```
		  workspace_folder/          -- WORKSPACE  
		    src/                               -- SOURCE SPACE  
		      CMakeLists.txt           -- 'Toplevel' CMake file, provided by catkin  
		      package_1/  
		        CMakeLists.txt         -- CMakeLists.txt file for package_1  
		        package.xml            -- Package manifest for package_1  
		      ...  
		      package_n/  
		        CMakeLists.txt        -- CMakeLists.txt file for package_n  
		        package.xml           -- Package manifest for package_n 
		  ```
	- 创建功能包
		- ```bash
		  catkin_create_pkg <package_name> [depend1] [depend2] [depend3]
		  ```
	- package.xml编写
		- https://dlonng.com/posts/ros-package
	- 查看依赖
- # 常用功能包
  id:: 62739567-1727-46e1-902d-4ef3737c08bd
	- id:: 20981552-953e-48e0-b300-1f20975e3552
	  |*功能包名*|*功能*|
	  |tf [[ROS之TF树]] |一个允许用户随时跟踪多个坐标系的功能包|
	  |roscpp|ROS的C++库，是目前最广泛应用的ROS客户端库，执行效率高|
	  |rospy|ROS的Python库，开发效率高|
	  |cv_bridge|在ROS图像消息和OpenCV图像之间进行转换|
	  |image_transport|为低带宽压缩格式(compressed formats)image传输提供透明支持|
	  |std_msgs|标准的ros消息类型|
	  |nav_msgs|用于与导航堆栈交互的常见消息|
	  |geometry_msgs|常见的几何图元（如点、向量和姿势）提供消息|
	  |message_generation|对生成消息的语言绑定的构建时依赖项进行包建模|
	  |pcl_ros|PCL（点云库）ROS接口堆栈|
	  |pcl_conversions|提供从PCL数据类型和ROS消息类型的转换 |
	-
	-
- #
- 参考文章
	- [ROS创建工作空间和功能包](https://blog.csdn.net/weicao1990/article/details/72677768)