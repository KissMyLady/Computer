算数逻辑单元  
=====

## 二进制
二进制 00101010是十进制的42  
表示和存储数字是计算机的重要功能  
但真正的目标是计算，有意义的处理数字  
比如把两个数字相加  
这些操作由计算机的"算术逻辑单元"处理  
> ![1](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-1.jpg)  
> 但大家会简称：ALU  
> 等你理解了 ALU 的设计和功能之后  
> 你就理解了现代计算机的基石  


## 英特尔 74181  
先来看看这个美人   
![2](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-2.jpg)   
1970 年发布时，它是第一个封装在单个芯片内的完整 ALU  

这在当时是惊人的工程壮举   
#### 接下来我们将用布尔逻辑门   
> 做一个简单的ALU电路，功能和74181一样    
> 然后接下来几集，用它从头做出一台电脑   
> 会有点复杂   
> 但我觉得你能搞的定  


## 算数单元   
> 先讲"算术单元"，它负责计算机里的所有数字操作   
比如加减法   
它还做很多其他事情，比如给某个数字+1    
这叫增量运算，我们之后会说    
今天的重点是一切的根本   
- "把两个数字相加"   


## 最简单的加法电路  
我们会用到 AND，OR，NOT和 XOR逻辑门  
最简单的加法电路， 
是拿2个bit加在一起(bit 是0 或1）  
> 有2个输入：A和B， 
> 有1个输出：就是两个数字的和  

需要注意的是：A, B,输出，这3个都是单个Bit(0 或1）    
输入只有四种可能  
前三个是 
0 + 0 = 0  
1 + 0 = 1 
0 + 1 = 1  
1 + 0 = 1 
0 + 1 = 1  


## 1位加法器    
记住二进制里，1与true相同，0与false相同   
这组输入和输出，和XOR门的逻辑完全一样   
![4](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-4.jpg)    
所以我们可以把 XOR 用作 1位加法器（adder）  

但第四个输入组合，1+1，是个特例   
> 1+1=2（显然）     
> 但二进制里没有 2   
> 二进制 1+1 的结果是0，1进到下一位    
> 和是 10 (二进制)  


## 半加器  
#### 但我们需要一根额外的线代表 "进位"   
![5](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-5.jpg)   
只有输入是 1和 1时，进位才是"true"  
因为算出来的结果用 1个bit存不下  
方便的是，我们刚好有个逻辑门能做这个事！   
没那么复杂 - 就两个逻辑门而已   


## 半加器封装    
让我们抽象化  
![6](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-6.jpg)   
两个输入，A和B都是 1 位   
两个输出，"总和" 与 "进位"  
这进入了另一层抽象  
我好像说了很多次，说不定会变成一个梗    


## 全加器   
如果想处理超过 1+1 的运算，我们需要"全加器"   
半加器 输出了进位   
意味着，我们算下一列的时候   
还有之后的每一列，我们得加3个位在一起，并不是2个    
全加器复杂了一点点   
全加器表格   

有 3个输入：A,B,C（都是 1 个 bit)   
所以最大的可能是 1 + 1 + 1   
"总和"1 "进位"1   
 所以要两条输出线： "总和"和"进位"   
#### 我们可以用 半加器做全加器   
我们先用半加器将 A和 B相加   
然后把 C输入到第二个半加器   
![7](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-7.jpg)    
这样就做出了一个全加器！   


## 全加器封装  
我们可以再提升一层抽象，把全加器作为独立组件:(FA)    
全加器会把 A，B，C 三个输入加起来    
输出 "总和"和"进位"    

## 8位加法器  
现在有了新组件，我们可以相加两个8位数字      
> 叫两个数字叫 A 和 B 好了  
> 我们从 A 和 B的第一位开始  
> 叫 A0 和 B0 好了  
> 现在不用处理任何进位，因为是第一次加法  
> 所以我们可以用半加器，来加这2个数字  
> 输出叫 sum0    
> 
> 现在加 A1和 B1   
> 因为 A0和 B0的结果有可能进位  
> 所以这次要用全加器，除了 A1和 B1，还要连上进位  
> 输出叫 sum1  
> 然后，把这个全加器的进位  
> 连到下个全加器的输入，处理 A2 和 B2     
> #### 以此类推，把 8个bit都搞定     
> ![8](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-8.jpg)  
注意每个进位是怎么连到下一个全加器的    
#### 所以叫 "8位行波进位加法器"   
 

## 溢 出    
> ![9](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-9.jpg)  
如果第9位有进位，代表着2个数字的和太大了，超过了8位     
这叫 "溢出" (overflow)    
一般来说 "溢出" 的意思是, 两个数字的和太大了    
超过了用来表示的位数  
这会导致错误和不可预期的结果   
> 著名的例子是，吃豆人用8位存当前关卡数  
> 如果你玩到了第256关（ 8位 bit最大表示255）  
> 造成一连串错误和乱码，使得该关卡无法进行  
> ![10](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-10.jpg)   


## 更高位加法器   
如果想避免溢出  
- 我们可以加更多全加器，可以操作 16或 32位数字  
- 让溢出更难发生，但代价是更多逻辑门   


#### 另外一个缺点是，每次进位都要一点时间   
当然时间不久，因为电子移动的很快  
但如今的量级是每秒几十亿次运算，所以会造成影响  
所以，现代计算机用的加法电路有点不同  


## 叫 "超前进位加法器"   
它更快，做的事情是一样的 - 把二进制数相加  
一般支持这8个操作  
> 就像加法器一样，这些操作也是由逻辑门构成的    
> 有趣的是，你可能注意到没有乘法和除法  
>     
> 因为简单的 ALU没有专门的电路来处理    
> 而是把乘法用多次加法来实现   
> 
> 假设想算 12x5    
> 这和把 "12" 加 5 次是一样的   
> 所以要 5 次 ALU 操作来实现这个乘法   


#### 很多简单处理器都是这样做的  
比如恒温器，电视遥控器和微波炉  
慢是慢，但是搞的定  
然而笔记本和手机有更好的处理器  
有专门做乘法的算术单元  
你可能猜到了，乘法电路比加法复杂  
* 没什么魔法，只是更多逻辑门  
	* 所以便宜的处理器没有.  

## 逻辑单元  
好了，我们现在讲 ALU 的另一半：逻辑单元  
逻辑单元执行逻辑操作   
比如之前讨论过的 AND，OR和 NOT操作   
> 它也能做简单的数值测试  
> 比如一个数字是不是负数  

#### 例如，这是检查 ALU 输出是否为 0 的电路  
> 它用一堆 OR门检查其中一位是否为 1  
> 哪怕只有一个 Bit(位) 是1，  
> 我们就知道那个数字肯定不是 0，然后用一个 NOT 门取反  
> ![11](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-11.jpg)    


以上就是 ALU 的一个高层次概括   
我们甚至从零做了几个主要组件，比如行波进位加法器   
它们只是一大堆逻辑门巧妙的连在一起而已.   

## 英特尔74181的ALU    
让我们回到视频开始时的 ALU，英特尔74181  
和我们刚刚做的 8位 ALU不同，74181 只能处理 4位输入  
也就是说  
你刚做了一个比英特尔 74181还好的 ALU！  
其实 差不多啦..    
我们虽然没有全部造出来, 但你理解了整体概念     
![12](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-12.jpg)    
但它向小型化迈出了一大步   
让计算机可以更强大更便宜   

## ALU封装    
4位 ALU已经要很多逻辑门了     
但我们的 8位 ALU 会需要数百个逻辑门    
工程师不想在用 ALU时去想那些事情,    
![13](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-13.jpg)     
又一层抽象(封装)！    


## 8位ALU   
* 我们的 8位 ALU有两个输入，A和B，都是8位 (bits)     
* 我们还需要告诉 ALU 执行什么操作    
例如加法或减法     
> 所以我们用 4位的操作代码    
>   
> 简言之,"1000"可能代表加法命令   
> "1100"代表减法命令    


#### 操作代码告诉 ALU 执行什么操作  
输出结果是 8 位的    
 ![14](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-14.jpg)  
比如相减两个数字，结果为 0  
我们的零测试电路（前面做的）  
会将零标志设为 True（1）    
![15](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-15.jpg)  
如果想知道： A 是否小于 B  
可以用 ALU来算 A 减B，看负标志是否为true   
如果是true，我们就知道 A 小于 B  
最后，还有一条线连到加法器的进位  
![16](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/d-16.jpg)  
这叫溢出标志   
高级 ALU 有更多标志   
但这 3 个标志是 ALU 普遍用的   
其实，我们之后的视频会用到它们  
现在你知道了  
计算机是怎样在没有齿轮或杠杆的情况下 进行运算    
恭喜你向现代化迈进了一大步，为自己鼓鼓掌   


## 接下来 
- [返回主页-Computer](https://github.com/KissMyLady/Computer)  
- [寄存器(Registers)-内存(RAM)](https://github.com/KissMyLady/Computer/blob/master/Note/Base_Registers.md)    
- [中央处理器--CPU](https://github.com/KissMyLady/Computer/blob/master/Note/Base_CPU.md) 

