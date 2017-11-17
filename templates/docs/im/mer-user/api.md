消息沟通API【完善中】
----
###### 1.文本消息
```java
//发送文本消息
public void sendMessage(RxConversationType,targetId,RxMessage,RxMessageCallback)
RxConversationType:会话类型
targetId:发送目标
RxMessage:消息对象
RxMessageCallback:
		//保存数据库成功
		public void onAttached(RxMessage message)
		//发送成功
		public void onSuccess(RxMessage message)
		//发送失败
		public void onError(RxMessage message)


```
###### 2.图片消息
```java
//发送图片消息
public void sendImageMessage(RxConversationType,targetId,RxMessage,RxImageMessageCallback)
RxConversationType:会话类型
targetId:发送目标
RxMessage:消息对象
RxImageMessageCallback:
			//保存数据库成功
			public void onAttached(RxMessage message)
			//发送失败
			public void onError(RxMessage message)
			//发送成功
			public void onSuccess(RxMessage message)
			//发送进度
			public void onProgress(Message message, int progress)
```