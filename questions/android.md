Android面试题
[面试过程根据各自简历会有不同对待]
-----
###### 1.基础部分
* android的四大组件有哪些?
```text
Activity,Broadcast,Service,ContentProvide
```
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
* Activity启动方式有哪几类，具体都有什么作用?
```text
1.standard 默认模式，可以不用写配置。在这个模式下，都会默认创建一个新的实例。
  因此，在这种模式下，可以有多个相同的实例，也允许多个相同Activity叠加。
2.singleTop 可以有多个实例，但是不允许多个相同Activity叠加。
  即，如果Activity在栈顶的时候，启动相同的Activity，不会创建新的实例，而会调用其onNewIntent方法。
3.singleTask 只有一个实例。在同一个应用程序中启动他的时候，若Activity不存在，则会在当前task创建一个新的实例，
  若存在，则会把task中在其之上的其它Activity destory掉并调用它的onNewIntent方法。
4.singleInstance 只有一个实例，并且这个实例独立运行在一个task中，这个task只有这个实例，不允许有别的Activity存在。
```
* 以下关于内存回收说法哪一项是正确的?【3正确】
```text
1.必须创建一个线程来释放内存;
2.允许主动释放无用的内存;
3.由内存回收程序负责释放无用内存;
4.内存回收程序可以在指定的时间释放内存对象;
```
* EventBus(或事件定阅)的作用是什么，它们是如何进行数据传递的?
```text
作用:
   EventBus是一款针对Android优化的发布/订阅事件总线。
   主要功能是替代Intent,Handler,BroadCast在Fragment，Activity，Service，线程之间传递消息.
   优点是开销小，代码更优雅。以及将发送者和接收者解耦。
使用:
   1.自定义一个类，可以是空类也可以是字符串;作为接收消息类型;
   2.在要接收消息的页面注册eventBus;(页面销毁后需要调用eventBus.unregister)
   3.在接收页面定义一个接收消息的方法,onEventxxxx(3.0后自定义方法并加注解);
   4.通过eventBus.post发送消息;
```
* 开发过程中经常需要对字符串进行操作,那么对于String、StringBuilder与StringBuffer有什么区别?
```text
1.三者在执行速度方面的比较：StringBuilder >  StringBuffer  >  String;
2.String：字符串常量
StringBuffer：字符创变量[线程安全的]
StringBuilder：字符创变量[线程非安全的]
从上面的名字可以看到，String是“字符创常量”，也就是不可改变的对象。对于这句话的理解你可能会产生这样一个疑问，
比如这段代码：
1 String s = "abcd";
2 s = s+1;
3 System.out.print(s);// result : abcd1
我们明明就是改变了String型的变量s的，为什么说是没有改变呢? 
其实这是一种欺骗，JVM是这样解析这段代码的：首先创建对象s，赋予一个abcd，然后再创建一个新的对象s用来执行第二行代码，
也就是说我们之前对象s并没有变化，所以我们说String类型是不可改变的对象了，由于这种机制，每当用String操作字符串时，
实际上是在不断的创建新的对象，而原来的对象就会变为垃圾被ＧＣ回收掉，可想而知这样执行效率会有多底。
而StringBuffer与StringBuilder就不一样了，他们是字符串变量，是可改变的对象，每当我们用它们对字符串做操作时，
实际上是在一个对象上操作的，这样就不会像String一样创建一些而外的对象进行操作了，当然速度就快了。
```
* 简述SharedPreferences存储方式以及SharedPreferences与SQLite数据库的区别
* 开启Service的几种方式, 区别, Service和Activity之间如何传递数据?
* databinding数据绑定如何?
```text
//根据实际情况及面试情况看;
```
* 面试过程中可问一下了解过哪些第三方库(方便开发);
```text
//根据实际情况及面试情况看;
```
* Service和Activity是如何进行通信的?
* 如何避免ANR情况?
* 广播注册有几种方式？如何来接收想要的数据?
* Service的启动有几种方式?说明一下它们各自的生命周期?

###### 2.提高部分
* 横竖屏切换时候 activity 的生命周期有哪些变化?
```text
1.不设置Activity的android:configChanges时,切屏会重新调用各个生命周期,切横屏时会执行一次,切竖屏时会执行两次;
2.设置Activity的android:configChanges="orientation"时,切屏还是会重新调用各个生命周期,切横、竖屏时只会执行一次;
3.设置Activity的android:configChanges="orientation|keyboardHidden"时，
  切屏不会重新调用各个生命周期，只会执行onConfigurationChanged方法

补充:
4.当前Activity产生事件弹出Toast和AlertDialog的时候Activity的生命周期不会有改变;
5.Activity运行时按下HOME键(跟被完全覆盖是一样的)：
  onSaveInstanceState-->onPause-->onStop-->onRestart-->onStart--->onResume
6.Activity未被完全覆盖只是失去焦点：onPause--->onResume
```
* android 中线程与线程，进程与进程之间如何通信?
```text
1.一个Android程序开始运行时，会单独启动一个Process。
  默认情况下，所有这个程序中的Activity或者Service都会跑在这个Process。
  默认情况下，一个Android程序也只有一个Process，但一个Process下却可以有许多个Thread。
2.一个Android程序开始运行时，就有一个主线程Main Thread被创建。
  该线程主要负责UI界面的显示、更新和控件交互，所以又叫UI Thread。
  一个Android程序创建之初，一个Process呈现的是单线程模型--即Main Thread，
  所有的任务都在一个线程中运行。所以Main Thread所调用的每一个函数，其耗时应该越短越好。
  而对于比较费时的工作，应该设法交给子线程去做，以避免阻塞主线程（主线程被阻塞，会导致程序假死 现象）。
3.Android 单线程模型：Android UI操作并不是线程安全的并且这些操作必须在UI线程中执行。
```
* cpu架构有哪些？程序运行时它们对于so包加载顺序是怎样?
```text
armeabi:针对普通的或旧的arm v5 cpu
armeabi-v7a:针对有浮点运算或高级扩展功能的arm v7 cpu(32位ARM设备)
arm64-v8a:64位ARM设备

arm64-v8a是可以向下兼容的，其下有armeabi-v7a，armeabi 
armeabi-v7a向下兼容armeabi

补充:
x86:在平板上用的比较多;
mips:在32位和64位嵌入式领域中历史悠久，获得了不少的成功，可目前Android的采用率在三者中最低
```
* android加固和混淆有什么区别?
* 说明一下图片压缩和双缓存原理?
* 自定义视图onDraw和onMeasure怎么来配合使用?其中requestLayout()和postInvalidate()有什么作用?
* AIDL具体是怎么使用?(大致写一下步骤即可)

###### 3.性能、优化与内存处理部分
* 说明一下对象引用会导致内存泄漏吗,大致有哪些情况?
* android适配是如何做适配的?(具体从几个方面)
```text
1.xml资源;
2.values文件夹;
3.layout文件夹;
4.布局;
5.api版本兼容;
```
* 如何进行apk包的瘦身,从哪些方面入手？(说明一下思路即可)
* 对于用户数据安全是如何做的?
* 若要对某一数据做混淆处理,可否用一种算法来实现，具体思想是什么?(需要可逆)