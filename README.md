### Lab2 版本控制 & 文档

#### 1. DOL框架描述

​	分布式操作层(Distributed Operation Layer, DOL) 是一个软件发展框架，用来计算分布式、并行化的应用。DOL可以实现基于Kahn进程网络节点的计算和systemC的仿真引擎的应用。DOL主要包含以下三个部分：

- **分布式操作层（DOL）的应用程序接口**：DOL有一系列的用于操作和沟通的接口，这些接口方便在SHAPES 平台上编程出分布式、并行化的应用。我们没有必要知道接口的具体的实现方式，只需要直接使用即可。事实上，这些接口还是硬件依赖软件层（hardware dependent software layer, HdS) 的更深优化。

- **分布式操作层（DOL）的功能仿真**：为了帮助程序员更好的测试他们的应用，功能仿真框架被开发出来。尽管使用应用程序来进行功能的确定的，这个框架通常被用来在应用层获得程序的参数。

- **分布式操作层（DOL）的映射最优化**：DOL的映射最优化的目的是为了计算在SHAPES体系结构下的一系列应用的最佳映射。首先，基于XML的特定框架会被用来在抽象层中描述应用和体系结构；之后，所有必要的信息会被采集，并且获得一个准确的仿真结果。

  ![pic_1](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/1.png)

  这里有三个层级，一个是硬件实现层级，一个是硬件和软件之间映射的层级，一个是软件实现的层级。

  - 硬件实现层级使用模型分析，在matlab上实现。
  - 软硬件协同层级通过系统同步，HdS层编程结构，通常在一些虚拟平台上仿真或者在实体平台上直接运行。
  - 软件实现层级使用功能仿真，通常在工作站中仿真。

#### 2. DOL安装过程

1.   安装必要的环境

     - update

     - openjdk - 7 - jdk

     - unzip

       ![2](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/2.png)

2.   下载文件

     - $ sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz

     - $ sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip

       ![3](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/3.png)

3.   解压文件

     - $ mkdir dol
     - $ unzip dol_ethz.zip -d dol
     - $ tar -zxvf systemc-2.3.1.tgz

4.   编译systemC

     - $ cd systemc-2.3.1
     - $ mkdir objdir
     - $ cd objdir
     - $ ../configure CXX=g++ --disable-async-updates

     ![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/4.png)

     ![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/5.png)

     - $ sudo make install

     ![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/6.png)

     - cd ../dol
     - $ ant -f build_zip.xml all

     ![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/7.png)

     运行第一个例子：

     - $ cd build/bin/main
     - $ ant -f runexample.xml -Dnumber=1

     ![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/8.png)

     第一个运行的实例：

![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/lab1/9.png)



#### 3. 实验感想

​	这次实验主要是让我们了解github，这个是一个很好的进行版本控制的一个平台。这个是新接触的一个概念，版本控制主要就是让我们在不停地更新当中，自己对于每次的更新能够有很好的把握，这个也适用于集体项目的合作。

​	另外一个是这个DOL的开发环境的配置，整体配置的过程没有什么特别大的障碍，但是整体结构的理解还不是很到位。主要是软硬件之间的协同合作，软件端、硬件端、软硬件协同端，嵌入式系统就是有这些部分，把软件和硬件很好的连接起来。目前理解的还不透彻，希望未来的实验能够一步一步的加深理解。

​	最后就是markdown语言了，这个语言之前也有在使用，也很喜欢，整个文章排版的框架很清晰，标记起来也很简单，但是这个的问题就是插入图片太麻烦，自己也弄了挺久才行。