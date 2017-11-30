Android面试题
-----
###### 1.基础部分
* Handler的机制原理是什么?
```text
	Andriod提供了 Handler 和 Looper 来满足线程间的通信。Handler 先进先出原则。
	Looper类用来管理特定线程内对象之间的消息交换(Message Exchange)。
	Looper: 一个线程可以产生一个Looper对象，由它来管理此线程里的Message Queue(消息队列)。
	Handler: 你可以构造Handler对象来与Looper沟通，以便push新消息到Message Queue里；
			 或者接收Looper从Message Queue取出)所送来的消息。
	Message Queue(消息队列):用来存放线程放入的消息。
	线程：UI thread 通常就是main thread，而Android启动程序时会替它建立一个Message Queue。
```
###### 2.提高部分
###### 3.性能、优化与内存处理部分