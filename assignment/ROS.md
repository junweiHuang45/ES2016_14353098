# ROS在Ubuntu的安装

### ROS的介绍

​	Robot operation system是一套框架，底层提供硬件驱动，软件层面支持通用的文件格式。

​	ROS(Robot Operating System）是一个机器人软件平台，它能为异质计算机集群提供类似操作系统的功能。

​	ROS提供一些标准操作系统服务，例如硬件抽象，底层设备控制，常用功能实现，进程间消息以及数据包管理。ROS是基于一种图状架构，从而不同节点的进程能接受，发布，聚合各种信息（例如传感，控制，状态，规划等等）。目前ROS主要支持Ubuntu。
​	ROS可以分成两层，低层是上面描述的操作系统层，高层则是广大用户群贡献的实现不同功能的各种软件包，例如定位绘图，行动规划，感知，模拟等等。



### 安装步骤

​	这个ROS实验是在Ubuntu 16.04下安装的。参考的教程为http://wiki.ros.org/kinetic/Installation/Ubuntu

1. 建立source.list

   sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

2. 设置密钥

   sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116

3. 安装

   sudo apt-get update

   sudo apt-get install ros-kinetic-desktop-full 

4. 初始化ROS开发工具

   sudo rosdep init
   rosdep update 

   ![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/Lab5/2.png)

5. 环境设置

   echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
   source ~/.bashrc

   ![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/Lab5/1.png)

6. 获取rosinstall

   sudo apt-get install python-rosinstall


![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/Lab5/1.png)





### 实验感想

​	这次实验就是照着教程一步一步的进行安装配置，一开始上课的时候没感觉这个软件的作用以及强大性，当后来写报告的时候查了一下，发现这个软件十分的厉害，希望之后有机会能够好好地接触学习一下。

​	这个配置实验相对来说学的东西少了一些，希望最好能够有一到两个小的样例让我们跑一下，我们这样让我们更加深刻的理解。否则，感觉光配置就没有太大的收获。

