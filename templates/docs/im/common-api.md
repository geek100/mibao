IM对接公共API
----
类结构图

![images](/templates/docs/ms/images/ms_structure.png)

###### 1.初始
```java
public void init(Context context, String appKey)
```
###### 2.连接类
```java
//连接
public void connect(token, callback)
//断开连接(断开和融云的连接后，有新消息时，仍然能够收到推送通知)
public void disconnect()
//断开连接(不接收任何推送通知)
public void logout()
```
###### 3.推送(通知类消息)消息接收处理
```java
public class RxIMPushMessageReceiver{
	public void onNotificationMessageArrived(RxMessage message){}
	public void onNotificationMessageClicked(RxMessage message){}
}
```