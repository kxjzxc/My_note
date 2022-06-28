tags:: #ROS

- # 介绍
	- Ignition是下一代Gazebo模拟仿真器，具有更新的体系结构和旨在改善模拟仿真体验的新功能。Ignition的一些新功能包括：
	- 基于插件的物理和渲染抽象-使用您自己的引擎，而无需重新编译模拟仿真器
	    分层系统，仅加载机器人与之交互的世界的一部分-这允许更大的模拟仿真世界
	    在多台机器上分布式模拟仿真
	    高度可定制的基于QtQuick的用户界面
	    超快速2D运动学物理引擎，平凡物理引擎（TPE）
	- 最重要的是，Ignition已经具有许多习惯Gazebo经典使用的功能，例如：
	- 服务器与客户端分离，实现无头模拟仿真
	    内置支持多种传感器，例如摄像机，激光雷达，IMU，深度摄像机，磁力计，高度计，气压传感器等。
	    动画人类演员
	    用于机器人控制的插件，例如差速驱动和防滑转向
	    图形界面，用于处理模型，自省属性，控制视角，插入模型等。
	    ROS 1和2集成
- # 安装
	- ## Ubuntu
		- ### 二进制安装
			- Configure package repositories.
			  ```bash
			  sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
			  wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
			  sudo apt-get update
			  ```
			- Install Ignition Gazebo
			  ```bash
			  sudo apt-get install libignition-gazebo<#>-dev
			  ```
- # 名词解释
	- Entity
		- 实体标识模拟中的单个对象，例如模型、链接或灯光。 在其核心，实体只是一个标识符。
	- EntityComponentManager(ECM)
		- 实体管理器
	- Component
		- 组件