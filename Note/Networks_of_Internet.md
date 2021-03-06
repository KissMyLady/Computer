互联网  
====

上集讲到，你的计算机和一个巨大的分布式网络连在一起  
这个网络叫互联网, 而你现在就在网上看网页呀  
互联网由无数互联设备组成，而且日益增多


## 数据流通过程   
计算机为了获取这个视频/网页     
首先要连到局域网, 也叫LAN   
> ![1](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-1.jpg)   
>> ![2](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-2.jpg)     
>> WAN的路由器一般属于你的"互联网服务提供商"(ISP)  
>> 比如Comcast，AT&T和Verizon这样的公司  
>    
> ![3](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-3.jpg)   
>> ![4](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-4.jpg)  
> 
> 可能再跳几次，但最终会到达互联网主干  
> 互联网主干由一群超大型、带宽超高路由器组成  

为了从YouTube获得这个视频，  
数据包(packet)要先到互联网主干  
沿着主干到达有对应视频文件的YouTube服务器   
数据包从你的计算机跳到Youtube服务器，可能要跳个10次  
* 先跳4次到互联网主干，2次穿过主干  
* 主干出来可能再跳4次，  
* 然后到Youtube服务器      
如果你在用 Windows, Mac OS或 Linux系统     
可以用traceroute来看跳了几次 

windows: tracert www.yahoo.com      
[traceroute使用方法详解](https://kb.intermedia.net/article/682)  
[ping, tracert和traceroute命令详解](https://www.cnblogs.com/wyxy2005/archive/2010/03/03/1676909.html)


我们在"印第安纳波利斯"的Chad&Stacy Emigholz工作室  
访问加州的DFTBA服务器    
经历了11次中转  
从192.168.0.1出发，这是我的电脑在局域网(LAN)里的IP地址    
然后到工作室的WIFI路由器    
然后穿过一个个地区路由器，到达主干.    
然后从主干出来，又跳了几次，到达"DFTBA.com”的服务器   
* 但数据包到底是怎么过去的？   
* 如果传输时数据包被弄丢了，会发生什么？     
* 如果在浏览器里输 "DFTBA.com"，浏览器怎么知道服务器的地址多少？ 
我们今天会讨论这些话题    


## 互联网协议 
互联网是一个巨型分布式网络  
会把数据拆成一个个数据包来传输  
如果要发的数据很大，比如邮件附件 
数据会被拆成多个小数据包    
> 举例，你现在看的这个视频  
> 就是一个个到达你电脑的数据包
> 而不是一整个大文件发过来

## IP协议
数据包(packet)想在互联网上传输
要符合"互联网协议"的标准，简称IP    
就像邮寄手写信一样，邮寄是有标准的  
> 每封信需要一个地址，而且地址必须是独特的  
> 并且大小和重量是有限制的  
> 违反这些规定，信件就无法送达.  

因为IP是一个非常底层的协议  
数据包的头部只有目标地址, 头部存 "关于数据的数据"    
![5](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-5.jpg)  
也叫元数据(metadata)   
这意味着当数据包到达对方电脑    
对方不知道把包交给哪个程序，是交给Skype还是使命召唤？    
因此需要在IP之上，开发更高级的协议.    


## UDP
这些协议里最简单最常见的叫"用户数据报协议"，简称 UDP 
![6](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-6.jpg)  
每个想访问网络的程序, 都要向操作系统申请一个端口号   
比如Skype会申请端口3478   
当一个数据包到达时    
接收方的操作系统会读UDP头部，读里面的端口号    

如果看到端口号是3478，就把数据包交给Skype  
总结：  
> IP负责把数据包送到正确的计算机  
> UDP 负责把数据包送到正确的程序  


### 校验和  
* 检查方式是把数据求和来对比  
以下是个简单例子  
假设UDP数据包里
原始数据是: 89 111 33 32 58 41  
> 在发送数据包前, 电脑会把所有数据加在一起, 算出"校验和"  
>> 89+111+33+... 以此类推  
>> 得到 364，这就是"校验和"   
>>> ![ww-7](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-7.jpg)

当接收方电脑收到这个数据包  
它会重复这个步骤   
> 把所有数据加在一起，89+111+33... 以此类推  
> 如果结果和头部中的校验和一致  
> 代表一切正常  
>> 如果不一致，数据肯定坏掉了  
>> 也许传输时碰到了功率波动，或电缆出故障了  

不幸的是，UDP不提供数据修复或数据重发的机制      
接收方知道数据损坏后，一般只是扔掉.   
而且，UDP 无法得知数据包是否到达.   
发送方发了之后，无法知道数据包是否到达目的地   

这些特性听起来很糟糕，但是有些程序不在意这些问题  
因为UDP又简单又快.  


拿微信举例:  
它用UDP来做视频通话，能处理坏数据或缺失数据  
所以网速慢的时候微信卡卡的    
因为只有一部分数据包到了你的电脑    
但对于其他一些数据，这个方法不适用.    


## TCP  
> 如果"所有数据必须到达"     
> 就用"传输控制协议"(TCP)     
> 因此，人们叫这个组合TCP/IP     

TCP头部也有"端口号"和"校验和"  
但TCP有更高级的功能，这里只介绍重要的几个  
[三次握手, 四次挥手](https://github.com/KissMyLady/Web-of-Python/blob/master/Web_Server/3hand.md)
### 1、TCP数据包有序号   
> 15号之后是16号，     
> 16号之后是17号，以此类推....    
> 发上百万个数据包也是有可能的    
序号使接收方可以把数据包排成正确顺序，即使到达时间不同.    
哪怕到达顺序是乱的，TCP协议也能把顺序排对   
  
### 2、TCP要求接收方的电脑收到数据包， 
并且"校验和"检查无误后，数据没有损坏，    
给发送方发一个确认码，代表收到了     
"确认码"(ACK)    
得知上一个数据包成功抵达后，发送方会发下一个数据包    
 
假设这次发出去之后，没收到确认码     
那么肯定哪里错了       
  
如果过了一定时间还没收到确认码   
发送方会再发一次     
  
注意, 数据包可能的确到了  
只是确认码延误了很久，或传输中丢失了  
但这不碍事 因为收件方有序列号  
如果收到重复的数据包就删掉  

#### 还有，TCP不是只能一个包一个包发
![8](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-8.jpg)  

有趣的是，确认码的成功率和来回时间  
可以推测网络的拥堵程度  

简单说TCP可以处理乱序和丢失数据包，丢了就重发     

还可以根据拥挤情况自动调整传输率   
相当厉害！    
既然TCP那么厉害，还有人用UDP吗？     

但并没有传输更多信息  
有时候这种代价是不值得的   
特别是对时间要求很高的程序，比如在线射击游戏     
![9](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-9.jpg)  
如果你玩游戏很卡，你也会觉得这样不值!   


## DNS(域名系统)  
当计算机访问一个网站时   
需要两个东西：1、IP地址 2、端口号      
 
例如, 172.217.7.238的80端口  
> 这是谷歌的IP地址和端口号    
> 事实上，你可以输到浏览器里，然后你会进入谷歌首页  
> 有了这两个东西就能访问正确的网站  
> 但记一长串数字很讨厌   
所以互联网有个特殊服务      
负责把域名和IP地址一一对应 
就像专为互联网的电话簿, 它叫"域名系统"(DNS)     

### 运作原理  
它的运作原理你可能猜到了  
> 在浏览器里输youtube.com  
> 浏览器会去问DNS服务器，它的IP地址是多少  

![10](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-10.jpg)     
如果你乱敲键盘加个.com然后按回车  
你很可能会看到DNS错误  
因为那个网站不存在，所以DNS无法返回给你一个地址    
> 如果你输的是有效地址，比如youtube.com  
> DNS按理会返回一个地址  
> 然后浏览器会给这个IP地址, 发送TCP请求

### 域名区分  
如今有三千万个注册域名，所以为了更好管理   
顶级域名(TLD)在最顶部，比如.com 和.gov   
> 下一层是二级域名，比如.com下面有  
>> google.com和dftba.com  
>
> 再下一层叫子域名，
>> 比如images.google.com,  store.dftba.com

#### 这个树超！级！大！
![11](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-11.jpg)  
前面说的"三千万个域名"只是二级域名, 不是所有子域名   
> 因此，这些数据散布在很多DNS服务器上  
> 不同服务器负责树的不同部分  
> 我们到了一层新抽象(封装)！   


## 各种网络层
线路里的电信号，以及无线网络里的无线信号  
这些叫"物理层"  
而"数据链路层"负责操控"物理层"，
数据链路层有：
> 媒体访问控制地址(MAC)，碰撞检测，
? 指数退避，以及其他一些底层协议


再上一层是"网络层"
负责各种报文交换和路由
而今天，我们讲了"传输层"里一大部分，比如UDP和TCP这些协议,  
负责在计算机之间进行点到点的传输  
而且还会检测和修复错误  
我们还讲了一点点"会话层" 
  
"会话层"会使用TCP和UDP来创建连接，传递信息，然后关掉连接


## 会  话 
这一整套叫"会话"  
查询DNS或看网页时，就会发生这一套流程   
这个概念性框架, 把网络通信划分成多层    
![12](https://github.com/KissMyLady/Computer/blob/master/Image/Works/ww-12.jpg)    
每一层处理各自的问题
如果不分层, 直接从上到下捏在一起实现网络通信, 是完全不可能的  

抽象使得科学家和工程师能分工同时改进多个层  不被整体复杂度难倒  
封装使得可以摆脱系统整体的复杂，降低耦合度  


## 接下来  
- [返回Computer主页](https://github.com/KissMyLady/Computer)
- [计算机网络](https://github.com/KissMyLady/Computer/blob/master/Note/Networks_of_com.md)    
- [万维网-WWW](https://github.com/KissMyLady/Computer/blob/master/Note/WWW.md)   
- [计算机安全](https://github.com/KissMyLady/Computer/blob/master/Note/Notework_of_safety.md)  
- [密码学--传输信息加密机制](https://github.com/KissMyLady/Computer/blob/master/Note/Noteworks_of_password.md)   
