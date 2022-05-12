tags:: #ROS

- roscore cannot run as another roscore/master is already running. Please kill other roscore/master
	- 明明已经关闭了所有终端，但是重新打开终端运行roscore的时候提示以上错误
	- 解决办法是在终端中输入:
		- ```bash
		  killall -9 roscore
		  killall -9 rosmaster
		  ```
	-