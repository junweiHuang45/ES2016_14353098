# Lab4 死锁

### 1. 死锁实验的截图

count值为7000的结果

![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/Lab4/7000.jpg)

count值为10000的结果

![](https://raw.githubusercontent.com/junweiHuang45/learngit/master/Lab4/10000.jpg)

### 2.产生死锁的四个必要条件

1. **<u>互斥条件</u>**：一个资源每次只能被一个进程使用
2. **<u>请求与保持条件</u>**：一个进程因请求资源而阻塞时，对已获得的资源保持不放
3. **<u>不剥夺条件</u>**：进程已获得的资源，在未使用完之前，不能强行剥夺。
4. **<u>循环等待条件</u>**：若干进程之间形成一种头尾相接的循环等待资源关系。

### 3. 对程序产生死锁的解释

整个程序的代码如下：

```java
class A{
  synchronized void methodA(B b){
      b.last();
  }
  synchronized void last(){
      System.out.println("Inside A.last()");
  }
}
class B{
	synchronized void methodB(A a){
		a.last();
	}
	synchronized void last(){
		System.out.println("Inside B.last()");
	}
}
class Deadlock implements Runnable{
	A a = new A();
	B b = new B();
	Deadlock(){
		Thread t = new Thread(this);
		int count = 20000;//可该参数，使其死锁
		t.start();
		while(count-->0);
		a.methodA(b);
	}
	public void run(){
		b.methodB(a);
	}
	public static void main(String args[]){
		new Deadlock();
	}
}
```
​	我们创建了两个类A，B，类A会调用函数b.last()，使用类B的函数，输出字符串"Inside B.last()"；同样地，类B会调用函数a.last()，使用类A的函数，输出字符串"Inside A.last()"。

​	在主函数Runnable中，主函数调用的是Deadlock()函数，在该函数里面，创建了一个新的线程t，线程t开始后，线程t就会调用函数run()，在该函数里，运行函数b.methodB(a)，这个时候b就需要请求a的资源，接着等待一段时间（count自减至零的时间），主线程就运行函数a.methodA(b);，这个时候a就需要请求b的资源，如果此时线程t还没有运行完b.methodB(a)，即b还在请求a的资源的时候，a正好也在请求b的资源，这样子就会产生死锁。

​	如果count时间过长，即b.methodB(a)运行完了，a.methodA(b);还没运行，结果就会先输出Inside A.last()，再输出Inside B.last()。

​	如果count时间过短，即a.methodA(b)运行完了，b.methodB(a)还在运行，结果就会先输出Inside B.last()，再输出Inside A.last()。

​	因此，只有找到合适的count的值，才有可能造成死锁。在实验中，也即运行了好几十次，才有可能发生一次死锁。



​	以下，从理论上分析该程序死锁发生的原因：我们知道，若想发生死锁，那就需要同时满足以下四个条件：

#####1. 互斥条件

​	对于a，b对象，每一个对象只能在一个线程当中运行，不能被两个线程运行。因为线程t是调用b对象，而主线程调用a对象，他们没有机会同时被两个线程调用。

#####2. 请求与保持条件

​	当对象a请求对象b的资源时，即使其请求不到，也不会释放它a的资源。反之对于b也适用。

#####3. 不剥夺条件

​	当线程t获得了对象b的资源，当它没有完成结束之前，它不会释放对象b的资源，同样对于主线程至于对象a也是如此。

#####4. 循环等待条件

​	对象a等待着对象b的资源，对象b等待着对象a的资源，形成了循环等待。



##### 实验分析

​	由此可知，该程序在一定的条件和概率下，满足了以上的四个必要条件，产生了死锁。

​	也根据实验可得，死锁发生的概率不高，但是一旦发生，确实十分麻烦。

​	这个程序比较简单，不复杂，但还是有一定的几率发生死锁现象，当程序很复杂的时候，一旦出现死锁，既难debug，也难处理。

​	而count的值的选择过大过小都不合适，只有刚刚好才能造成死锁。