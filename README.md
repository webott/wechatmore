大家都知道，正常情况下，电脑微信客户端只能打开一个微信，如果再次点击是没法打开第二个的。微信是怎么实现，禁止一个客户端打开多个微信的呢？

![image](https://user-images.githubusercontent.com/73727649/118353270-1a8c7080-b598-11eb-826e-eefae0438e6c.png)
微信每次启动的时候，都调用：OpenMutexA(	)函数，微信有一个自己的互斥体名称，每次调用这个函数，如果函数返回真，则说明找到了，说明微信已经打开一个了。他就不让再打开第二个了。如果没找到，就打开一个新微信，就是这个原理实现的。
![image](https://user-images.githubusercontent.com/73727649/118353274-211ae800-b598-11eb-9187-960cc7b682ee.png)
在OD中（如下图），用快捷键Ctrl+G ，弹出搜：CreateMuteW（微信是宽字符） ,搜索之后，下断点，
![image](https://user-images.githubusercontent.com/73727649/118353281-26783280-b598-11eb-8d8c-a72fb3fe8278.png)
断点之后，找到该函数，其中有三个参数：一个是互斥体名称，一个是bool值，一个他写的null
![image](https://user-images.githubusercontent.com/73727649/118353343-650ded00-b598-11eb-8d48-6ea4e0be72d2.png)
然后用CE 找他他这个名称，把他的互斥体名称改掉，如下图：
![image](https://user-images.githubusercontent.com/73727649/118353350-6a6b3780-b598-11eb-8831-54433c2122c5.png)
改掉之后，在OD里面把断点取消，然后自动就启动了一个微信。然后在自己电脑上，再点击微信图标，打开，就又打开一个微信。这样就打开了两个微信，实现了多开。

现在已经实现了发送接收消息，群管，加好友等等有趣的功能，可提供接口，欢迎交流。
![image](https://user-images.githubusercontent.com/73727649/118353388-8d95e700-b598-11eb-945f-103d1e50a8d3.png)

