tags:: #ROS

- # 介绍
	- 机器人不停部位之间的坐标转换。坐标转换包括位置和姿态两方面，ROS中的tf是一个让用户随时记录多个坐标系的软件包。tf保持缓存的树形结构中的坐标系之间的关系，并允许用户在任何期望的时间点在任何两个坐标系之间转换点、矢量等。
- # TF功能包
	- 一个允许用户随时跟踪多个坐标系的功能包
	- ## 类
		- ## TransformBroadcaster
			- tf发布对象
		- ## StampedTransform
			- TF变换的数据类型
		- ## Quaternion
			- 四元数类
		- ## Matrix3x3
			- 旋转矩类
	- ## 常用函数
		- |*函数名*|*函数功能*|
		  |removeNaNFromPointCloud|去除无效点|
		  |createQuaternionMsgFromRollPitchYaw|从三轴数据返回四元数|
		-
- 参考文章
	- [坐标变换学习笔记—代码篇ROS](https://blog.csdn.net/sunqin_csdn/article/details/108045463#t4)
	- [ROS学习笔记(十三） TF介绍（一）]