AI--机器学习与深度学习
====


计算机很擅长存放，整理，获取和处理大量数据
很适合有上百万商品的电商网站
或是存几十亿条健康记录，方便医生看

但如果想根据数据做决定呢？
这是机器学习的本质

## 机器学习
* 机器学习算法让计算机可以从数据中学习, 然后自行做出预测和决定  
	* 能自我学习的程序很有用, 比如判断是不是垃圾邮件, 这人有心律失常吗？  
	* ![1](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-1.jpg)  
虽然有用，但我们不会说它有人类一般的智能

虽然AI和ML这两词经常混着用  
大多数计算机科学家会说:  
* 机器学习是为了实现人工智能这个更宏大目标的技术之一  


人工智能简称AI    
机器学习和人工智能算法一般都很复杂  
所以我们不讲具体细节, 重点讲概念  


## 判断种类
我们从简单例子开始

### 分类器  
* 判断飞蛾是"月蛾"还是"帝蛾"，这叫"分类"  
* 做分类的算法叫 "分类器"  
虽然我们可以用, 照片和声音来训练算法  
> 很多算法会减少复杂性, 把数据简化成 "特征"
> "特征"是用来帮助"分类"的值
对于之前的飞蛾分类例子, 我们用两个特征:"翼展"和"重量"  

### 训练数据    
为了训练"分类器"做出好的预测, 我们需要"训练数据"   
为了得到数据    
![2](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-2.jpg)   

### 标记数据  
> 专家可以认出不同飞蛾，  
> 所以专家不只记录特征值，还会把种类也写上    
> ![3](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-3.jpg)   

因为只有两个特征, 很容易用散点图把数据视觉化  
> ![4](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-4.jpg)      
> 可以看到大致分成了两组, 但中间有一定重叠  
所以想完全区分两个组比较困难  


## 机器学习算法登场, 找出最佳区分    
### 决策边界  
> 我用肉眼大致估算下
>> 然后判断, 翼展小于45毫米的很可能是帝蛾  
>> 可以再加一个条件，重量必须小于.75才算是帝蛾   
>> ![5](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-5.jpg)  
   
### 混淆矩阵    
> 如果仔细看数据   
>> ![6](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-6.jpg)  
>> 但剩下14只在错误的区域  
> 
>> 另一方面，82只月蛾在正确的区域     
>> ![7](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-7.jpg)   
这里有个表 记录正确数和错误数    
#### 这表叫"混淆矩阵"    
![8](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-8.jpg)  


注意我们没法画出100%正确分类的线  
降低翼展的决策边界，会把更多"帝蛾"误分类成"月蛾"  

如果提高，会把更多月蛾分错类     
机器学习算法的目的:   
* 是最大化正确分类 + 最小化错误分类
> 在训练数据中，有168个正确，32个错误
> 平均准确率84％


### 未标签数据
如果我们进入森林，碰到一只不认识的飞蛾，  
我们可以测量它的特征, 并绘制到决策空间上, 这叫 "未标签数据"
决策边界可以猜测飞蛾种类   
这里我们预测是"月蛾"


### 决策树
这个把决策空间切成几个盒子的简单方法  
可以用"决策树"来表示  
画成图像，会像左侧用if语句写代码，会像右侧  
> 生成决策树的机器学习算法需要选择用什么特征来分类    
> 每个特征用什么值    
>> ![9](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-9.jpg)  


"决策树"只是机器学习的一个简单例子
如今有数百种算法，而且新算法不断出现

### 森 林
一些算法甚至用多个"决策树"来预测
计算机科学家叫这个"森林"，因为有多颗树嘛
也有不用树的方法，比如"支持向量机"
本质上是用任意线段来切分"决策空间"
不一定是直线, 可以是多项式或其他数学函数
就像之前，机器学习算法负责
![10](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-10.jpg)  
之前的例子只有两个特征，人类也可以轻松做到   
> 如果加第3个特征，比如"触角长度" 
> 那么2D线段，会变成3D平面, 在三个维度上做决策边界  
> 这些平面不必是直的   

![11](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-11.jpg)  
你可能会同意, 现在变得太复杂了
但这也只是个简单例子: 只有3个特征和5个品种
我们依然可以用 3D散点图 画出来

### 超平面
不幸的是，一次性看4个或20个特征，没有好的方法  
更别说成百上千的特征了  
但这正是机器学习要面临的问题  
> 你能想象靠手工在一个上千维度的决策空间里  
> 给超平面(Hyperplane)找出一个方程吗, 大概不行

但聪明的机器学习算法可以做到
"决策树"和"支持向量机"这样的技术，发源自统计学
统计学早在计算机出现前，就在用数据做决定


## 深度学习
有一大类机器学习算法用了统计学吗，但也有不用统计学的算法
其中最值得注意的是: 人工神经网络, 灵感来自大脑里的神经元

神经元是细胞, 
> 用电信号和化学信号来处理和传输消息  
> 它从其他细胞得到一个或多个输入  
>> 然后处理信号并发出信号   
>> 形成巨大的互联网络，能处理复杂的信息
就像你的大脑在看这个视频
人造神经元很类似
> 可以接收多个输入，然后整合并发出一个信号
> 它不用电信号或化学信号
>> 而是吃数字进去，吐数字出来
>> 它们被放成一层层形成神经元网络, 因此得名神经网络


### 输入层
回到飞蛾例子，看如何用神经网络分类   
我们的第一层: 输入层   
* 提供需要被分类的单个飞蛾数据  
* 同样，这次也用重量和翼展  

### 输出层
另一边是输出层，有两个神经元：
一个是帝蛾，一个是月蛾
2个神经元里最兴奋的, 就是分类结果

### 隐藏层  
中间有一个隐藏层  
> 负责把输入变成输出，负责干分类这个重活   
> ![12](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-12.jpg)  

为了看看它是如何分类的   
> 我们放大"隐藏层"里的一个神经元    
>> 神经元做的第一件事, 是把每个输入乘以一个权重  
>>> 假设2.8是第一个输入，0.1是第二个输入。  
>>> 然后它会相加输入
>>> 总共是9.7
>>> ![13](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-13.jpg)  
> 
> 然后对这个结果，用一个偏差值处理  
> 意思是加或减一个固定值  
>> 比如-6，得到3.74  
>> ![14](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-14.jpg)  


### 标记数据  
做神经网络时，这些偏差和权重，一开始会设置成随机值  
然后算法会调整这些值来训练神经网络    
使用"标记数据"来训练和测试, 逐渐提高准确性, 很像人类学习的过程  

### 激活函数(传递函数)    
* 神经元有激活函数，它也叫传递函数会应用于输出，对结果执行最后一次数学修改
> ![15](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-15.jpg)    
> 例如，把值限制在-1和+1之间  
> 或把负数改成0  
  
我们用线性传递函数，它不会改变值   
> 所以3.74还是3.74  
> 所以这里的例子, 输入0.55和82，输出3.74  
这只是一个神经元，但加权，求和，偏置，激活函数  
会应用于一层里的每个神经元, 并向前传播，一次一层    
![16](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-16.jpg)   
数字最高的就是结果：月蛾   


### 很多层隐藏层
重要的是，隐藏层不是只能有一层，可以有很多层  
![17](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-17.jpg)    
"深度学习"因此得名
> 训练更复杂的网络 需要更多的计算量和数据
>> 尽管神经网络50多年前就发明了
>> 深层神经网络直到最近才成为可能
>>> 感谢强大的处理器和超快的GPU
>>> 感谢游戏玩家对帧率的苛刻要求！

几年前，Google和Facebook  
展示了深度神经网络, 在照片中识别人脸的准确率，和人一样高  
人类可是很擅长这个的！  
这是个巨大的里程碑  


## 弱AI和窄AI
现在有深层神经网络开车，翻译，诊断医疗状况等等  
这些算法非常复杂，但还不够"聪明"  
它们只能做一件事，分类飞蛾，找人脸，翻译  
这种AI叫"弱AI"或"窄AI"，只能做特定任务  
但这不意味着它没用  
能自动做出诊断的医疗设备，  
和自动驾驶的汽车真是太棒了！  
但我们是否需要这些计算机来创作音乐  
在空闲时间找美味食谱呢？  
也许不要  
如果有的话 还挺酷的 


### 强AI
真正通用的，像人一样聪明的AI，叫 "强AI"
目前没人能做出来 接近人类智能的 AI
有人认为不可能做出来
> 但许多人说,数字化知识的爆炸性增长比如维基百科，网页和Youtube视频是"强 AI"的完美引燃物  
>> 你一天最多只能看24小时的YouTube, 计算机可以看上百万小时


### IBM沃森
比如，IBM的沃森吸收了2亿个网页的内容
包括维基百科的全文
![18](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-18.jpg)  


### AlphaGo  
2016年Google的AlphaGo   
![19](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-19.jpg)  
它和自己的克隆版下无数次围棋，从而打败最好的人类围棋选手  


学习什么管用，什么不管用自己发现成功的策略  
这叫 "强化学习"是一种很强大的方法

深度学习和人类的学习方式非常类似  
> ![20](https://github.com/KissMyLady/Computer/blob/master/Image/AI/dp-20.jpg)  
计算机现在才刚学会反复试错来学习  
对于很多狭窄的问题，强化学习已被广泛使用  
> 有趣的是，如果这类技术可以更广泛地应用 
> 创造出类似人类的"强AI"能像人类小孩一样学习，但学习速度超快  
> 如果这发生了，对人类可能有相当大的影响
>> 这样，[奇点](#)将会来临
感谢浏览.  我们下章见

## 接下来  
- [返回Computer主页](https://github.com/KissMyLady/Computer)
- [AI--计算机视觉](https://github.com/KissMyLady/Computer/blob/master/Note/AI_I_see.md)   
- [AI--自然语言处理](https://github.com/KissMyLady/Computer/blob/master/Note/AI_language.md)
- [AI--机器人](https://github.com/KissMyLady/Computer/blob/master/Note/AI_robot.md)
- [AI--计算机心理学](https://github.com/KissMyLady/Computer/blob/master/Note/AI_xinli.md)
- [AI--科技教育](https://github.com/KissMyLady/Computer/blob/master/Note/AI_educational.md)
- [AI--奇点、天网、未来](https://github.com/KissMyLady/Computer/blob/master/Note/AI_future.md)  
