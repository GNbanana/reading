<center><strong>《第一行代码 Android》读书笔记</strong></center>
<div style="text-align:right">巩娜</div>
<pre>
**Android系统的系统架构:**  
   Linux内核层：为各种硬件提供底层驱动  
   系统运行库层：提供主要特性支持  
   应用框架层：提供构建应用程序时可能会用到的API  
   应用层：包含手机上的应用程序
  
**Android系统四大组件：**  
   Activity：包含用户界面，主要用于和用户进行交互；  
   Service：Android中实现程序后台运行的解决方案；  
   Broadcast receiver（广播接收器）：允许应用接受来自各处的广播消息；  
   Content provider（内容提供器）：实现应用程序之间的共享数据。

**Android 项目中的资源：**  
   src: 放置所有Java代码的地方
   gen: 最重要的是R.java，所有res资源都在这里编号  
   libs：存放第三方jar包  
   res：存放项目中使用到的所有图片、布局、字符串等资源  
   menifest：统筹兼顾全局，Android四大组件都要在此注册  
   其中活动注册的代码：  

     <activity  
         android:name="com.test.helloworld.HelloWorldActivity"  
         android:label="@string/app_name" >  
         <intent-filter>  
              <action android:name="android.intent.action.MAIN" />  
              <category android:name="android.intent.category.LAUNCHER" /> 
              /*主活动（点击应用图标，首先启动这个活动）*/
         </intent-filter>  
     </activity>

**Android的日志工具log**  
   Log.v() 打印意义最小的日志信息，对应级别verbose   
   Log.d() 打印一些调试信息，对应级别debug  
   Log.i() 打印一些比较重要的数据，对应级别info  
   Log.w() 打印一些警告信息，对应级别warm      
   Log.e() 打印程序中的错误信息，对应级别warn  
   级别由低到高  

System.out.println()方法也可以来打印日志，但是缺点比较多，比如打印日志不可控制、打印时间无法确定等


在没有接触过java的情况下看程序中的代码还是有些困难的，所以接下来准备边学java边学Android，了解java基
本的语法知识，应该对这本书的学习有很大的帮助；另外，搭建开发环境的过程有些麻烦，目录结构中的内容很多
很复杂，讲解的内容中很多东西没有实际使用过，还是有些抽象。
 


<div style="text-align:right">7.23</div>

