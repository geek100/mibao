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
* 说说MVC(或MVP)模式的原理，它在Android中的运用
```text
MVC(Model_view_controller)” 模型-视图-控制器”。 MVC应用程序总是由这三个部分组成。
Event(事件)导致Controller改变Model或View，或者同时改变两者。
只要 Controller改变了Models的数据或者属性，所有依赖的View都会自动更新。
类似的，只要Controller改变了View，View会从潜在的Model中获取数据来刷新自己。
```
* Activity的生命周期及每个间段的都起到了哪些作用?
```text
@Override
 protected void onCreate(Bundle savedInstanceState) {
     super.onCreate(savedInstanceState);
     setContentView(R.layout.activity_main);
     //在这里创建界面，做一些数据的初始化工作。
 }

 @Override
 protected void onStart() {
     super.onStart();
     //到这一步变成用户可见不可交互的。
 }

 @Override
 protected void onRestart() {
     super.onRestart();
     //從stop重新開始
 }

 @Override
 protected void onResume() {
     super.onResume();
     //变成和用户可交互的
 }

 @Override
 protected void onPause() {
     super.onPause();
     //到这一步是可见但不可交互的，系统会停止动画等消耗CPU的事情从上文的描述已经知道，应该在这里保存你的一些数据，
     // 因为这个时候你的程序的优先级降低，有可能被系统收回。在这里保存的数据，应该在 onResume里读出来，
     // 注意：这个方法里做的事情时间要短，因为下一个activity不会等到这个方法完成才启动。
 }

 @Override
 protected void onStop() {
     super.onStop();
     //变得不可见，被下一个activity覆盖了。
 }

 @Override
 protected void onDestroy() {
     super.onDestroy();
     //这是activity被干掉前最后一个被调用方法了，可能是外面类调用finish方法或者是系统为了
     // 节省空间将它暂时性的干掉，可以用isFinishing()来判断它，
     // 如果你有一个Progress Dialog在线程中转动，请在onDestroy里把他cancel掉，
     // 不然等线程结束的时候，调用Dialog的cancel方法会抛异常的。
 }
```
###### 2.提高部分
###### 3.性能、优化与内存处理部分