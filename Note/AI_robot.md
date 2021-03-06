AI--机器人  
====
今天, 我们要讨论机器人  

## 机器人概念  
你脑中冒出来的第一个印象估计是类人机器人  
经常在电视剧和电影里看到, 有时候它们是朋友和同事  
但更常见的是阴险无情，身经百战  
我们经常把机器人看成未来科技  
* 但事实是：机器人时代已经来临了  
* 它们是同事, 帮我们把困难的工作，做得更快更好  

## 机器人的定义  
机器人的定义有很多种，但总的来说     
> 机器人由计算机控制，可以自动执行一系列动作的机器  
> 外观并不重要    
>> 可以是给汽车喷漆的机械臂    
>> ![1](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-1.jpg)  
  
以及人形机器人  
有时我们叫虚拟人物"机器人"  
但叫bot甚至agent会更合适  
robot(机器人)一词首次出现在1920年的一部捷克戏剧 
因为"机器人"的潜在含义是存在于现实世界中的机器  
robot源于斯拉夫语词汇robota代表强迫劳动 
代表农民在十九世纪, 欧洲封建社会的强迫劳动  
戏剧没讲太多技术细节  
![2](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-2.jpg)   
> 机器人都是大规模生产，高效不知疲倦，看起来像人的东西    
> 但毫无情感，不会保护自己，没有创造力    
![3](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-3.jpg)   
很多古代发明家发明了能自动运行的机械装置  
比如计时和定时敲钟  
![4](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-4.jpg)  
  
这些不用电，而且肯定没有电子部件的机器, 叫"自动机"  

### 吃饭鸭  
举个例子1739年法国人 Jacques de Vaucans 做了个自动机  
法语叫Canard Digerateur，翻译过来是 "吃饭鸭"  
一个像鸭子的机器，能吃东西然后排便  
伏尔泰在1739年写道:  
> "如果没有吃饭鸭的声音, 还有什么能提醒你法国的荣光呢？"  

### 土耳其行棋傀儡  
一个名声很臭的例子是"土耳其行棋傀儡"  
> 一个能下国际象棋的人形机器人  
> 在1770年建造完成后，就在欧洲各地展览  
> 好棋艺惊叹观众像某种机械人工智能  
>> ![5](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-5.jpg)  

## 第一台计算机控制的机器  
![6](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-6.jpg)  
这些计算机数控的机器，简称CNC机器   
![7](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-7.jpg)  
> 精细的控制让我们能生产之前很难做的物品  
>> 比如从一整块铝 加工出复杂的螺旋桨   
>> 这用普通机械工具很难做到 
>> 并且误差容忍度很小，无法手工加工   
>>> 不仅提高了制造能力和精确度 还降低了生产成本  


### 第一个商业贩卖的，可编程工业机器人  
叫Unimate，于1960年卖给通用汽车公司    
> 它可以把压铸机做出来的热金属成品提起来，然后堆起来  
>> 机器人行业由此开始  
  
很快，机器人开始堆叠货盘，焊接，给汽车喷漆等等  
> 对于简单运动 - 比如机器爪子在轨道上来回移动    
> 可以指示它移动到特定位置  
> 它会一直朝那个方向移动，直到到达, 然后停下来  

### 控制回路做  
这种行为 可以用简单控制回路做  
  
> 首先，判断机器人的位置  
>> 我们到了吗？  
>> 没有  
>>  那么继续前进  
>  
> 再次判断位置  
>> 我们到了吗？  
>> 没有，所以继续前进  
>  
> 我们到了吗？  
>> 是的!  
>> 现在可以停下来了，别问了！    

### 负反馈回路  
* 因为我们在不断缩小 当前位置和目标位置的距离  
	* 这个控制回路 更准确的叫"负反馈回路"  
负反馈回路有三个重要部分    
* 首先是一个传感器，可以测量现实中的东西  
> 比如水压，马达位置，气温或任何你想控制的东西  

* 根据传感器，计算和目标值相差多大  
> 得到一个"错误"  
> 然后"控制器"会处理这个"错误"  

* 决定怎么减小错误  
> 然后用泵，电机，加热元件，或其他物理组件来做出动作    
在严格控制的环境中，这种简单控制回路也够用了  

## 缺  点  
但在很多现实应用中，情况复杂得多  
> 假设爪子很重，哪怕控制回路叫停了
> 惯性让爪子超过了预期位置  
> 然后控制回路又开始运行  
> 叫爪子移动回去  
>> 一个糟糕的控制回路 可能会让爪子不断来回移动, 甚至永远循环  

更糟糕的是，现实世界中  
机器人会受到各种外力影响  
> 比如摩擦力，风，等等  
为了处理这些外力，我们需要更复杂的控制逻辑    
一个使用广泛的机制，有控制回路和反馈机制。  

### 比例-积分-微分控制器(PID控制器)  
叫 "比例-积分-微分控制器"  
这个有点绕口，所以一般简称 "PID控制器"    
它以前是机械设备，现在全是纯软件了   

> 想象有一个机器人，端咖啡给客人  
> ![8](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-8.jpg)   
> 这个速度是理想速度, 安全又合适    
  
当然，环境是会变化的  
> 有时候有风，有时候有上坡下坡  
> 以及其他影响机器人速度的因素  
  
所以，给马达的动力要加大或减少，以保持目标速度  
用机器人的速度传感器，我们可以  
把当前速度和目标速度画张图  
首先是"比例值"，就是"实际值"和"理想值"差多少  
"实际值"可能有一定滞后，或者是实时的  
之前的简单控制回路，用的就是这个值  
"实际值"和"理想值"的差距越大, 就越用力  
* 换句话说，它是"比例控制"的  

#### 算"积分值"  
接下来，算"积分值"  
> 就是一段时间内 误差的总和  
>> 比如最近几秒, 帮助弥补误差  
>> 比如上坡时可能就会产生误差  
>>> 如果这个值很大，说明比例控制不够   
>>> 要继续用力前进  

#### 算"导数值"  
最后有"导数值", 是期望值与实际值之间的变化率  
有助于解决 未来可能出现的错误，有时也叫"预期控制"  
> 比如前进的太快  
> 要稍微放松一点，避免冲过头  

>> 这三个值会一起使用，它们有不同权重,然后用来控制系统    
>> ![9](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-9.jpg)  

> 比如汽车里的巡航控制   
> ![10](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-10.jpg)  
> 以及一些更奇怪的机器人，   
> ![11](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-11.jpg)  
   
更高级的机器人一般需要多个控制回路同时运行   
来保持机器人平衡，调整肢体位置，等等   
   
之前说过，控制回路负责   
把机器人的属性（比如当前位置）变成期望值   
你可能好奇这些值是哪里来的   
这是更高层软件的责任   
   
## 分解任务   
软件负责做出计划 并让机器人执行动作，   
比如制定一条路线来绕过障碍物，或者把任务分成一步步   
比如把拿起一个球，分解成一个个简单连续动作   
用这些技术，机器人已经取得不少令人印象深刻的成就   
> 它们潜到了海洋最深处   
> 在火星上跑了十几年   

但有趣的是，许多对人类来说很简单的任务   
对机器人很困难：   
比如两条腿走路，开门，拿东西时不要捏碎了   
或是穿T恤，或是摸狗, 这些你可能想都不用想   
但有超级计算机能力的机器人却做不到   
   
机器人研究领域在全力解决这些问题   
我们前几集聊过的   
人工智能最有可能解决这些问题  
> 例如，谷歌在进行一项实验  
> 让一堆机器人手臂把各种东西  
> 从一个盒子拿到另一个盒子，不断试错学习  
>> ![12](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-12.jpg)  
>>> 不像人类，机器人可以24小时全天运行  
>>> 而且多个手臂同时练习    
>>> 所以机器人擅长抓东西只是时间问题  
>>> 但现在，小婴儿都比机器人更会抓东西  

## 无人驾驶  
近年最大的突破之一是无人驾驶汽车  
如果你仔细想想，汽车没几个输入  
只是加速减速，左转右转  
> 难的问题是 判断车道，理解路标   
> 预测车流，车流中穿行，留心行人和骑自行车的。  
> 以及各种障碍, 车上布满了传感器  
无人驾驶汽车非常依赖, 计算机视觉算法  


现在也开始出现类人机器人, 外貌和行为像人类的机器人  
不过现在两个目标都没接近(外貌和行为)   
因为看起来一般怪怪的，行为也怪怪的  
但至少有《西部世界》可以看看     
无论如何，对机器人研究者来说，把各种技术结合起来  
> 比如人工智能，计算机视觉和自然语言处理  
> 来让机器人越来越像人，是个诱人的目标  
>> 至于人类为什么如此着迷 做出和我们一样的机器人, 得去简单学下哲学  

在未来好一段时间里     
和人类一样的机器人 依然只能存在科幻小说里  
军队也对机器人很有兴趣, 因为机器人可以替换  
而且力量，耐力，注意力，准确性可以远超人类  
拆弹机器人和无人侦察机如今很常见  
> 但完全自主决定，全副武装的机器人也在慢慢出现  
> ![13](https://github.com/KissMyLady/Computer/blob/master/Image/AI/bo-13.jpg)  
  
## 棘手的问题 
有智力并且可以杀人的机器人叫 "致命自主武器"  
这种武器是复杂又棘手的问题    
> 毫无疑问，它们可以把士兵从战场带离 挽救生命, 甚至阻止战争的发生  
>> 值得注意的是 人们对炸药和核弹也说过一样的话  

另一方面，我们可能会不小心创造出无情又高效的杀人机器  
没有人类般的判断力和同情心  

战争的硝烟会变得更加黑暗和复杂  
机器人会接受命令并高效执行, 但有时人类的命令是错的  

这场辩论会持续很长时间，  
而且随着机器人技术的进步，两边的辩论会越来越激烈  
这也是个老话题了  

## 艾萨克·阿西莫夫  
科幻作家 艾萨克·阿西莫夫 早预见了这种危险  
他在1942年短篇小说Runaround中写了"机器人三定律", 之后又加了"定律0"  
简单说 这些定律指导机器人的行为准则 或者说道德指南  
让机器人不要伤害，特别是不要伤害人类    
这些规则实践起来相当不足，并且有很多模糊的地方    
但阿西莫夫三定律 激发了大量科幻小说讨论和学术讨论    
  
如今有专门讨论机器人伦理的会议  
> 重要的是，阿西莫夫写这些虚构规则  
> 是为了反对 "机器人都很邪恶" 这种常见描述  
  
他童年读的小说里，这样的场景很常见  
机器人脱离控制，然后伤害甚至毁灭创造者  
  
阿西莫夫认为, 机器人有用，可靠，甚至可以让人喜爱  
我想让你思考这种两面性  
> 我们讨论过的许多技术，有好的一面也有坏的一面    
> 我们要认真思考计算机的潜力和危害来改善这个世界    
> 而机器人最能提醒我们这一点了  
