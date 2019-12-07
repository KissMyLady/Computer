中央处理器--CPU  
=====

* 提示下, 这节可能是最难的一小段  
* 所以一旦你理解了，就会变得超厉害der~  

## 回顾上两章节  
1、我们已经做了一个算术逻辑单元(ALU)    
> 输入二进制，它会执行计算  

2、我们还做了两种内存：  
> 寄存器: 很小的一块内存，能存一个值  
> 之后我们增大做出了RAM   
* 现在是时候把这些放在一起，组建计算机的"心脏"了    
* 但这个 "心脏" 不会有任何包袱，比如人类情感.  


## 开始组装  
计算机的心脏是"中央处理单元"，简称 "CPU"  
#### 程序由一个个操作组成   
> ![1](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-1.jpg)     
> * 如果是数学指令，比如加/减  
> * 也可能是内存指令，CPU 会和内存通信，然后读/写值  

#### 我们把重点放在功能，而不是一根根线具体怎么连    
当我们用一条线连接两个组件时      
* 这条线只是所有必须线路的一个抽象    
* 这种高层次视角叫"微体系架构"  


## 组装内存  
好，我们首先要一些内存，把做的RAM拿来就行     
1、为了保持简单，假设它只有16个位置，每个位置存8位      
2、再来四个8位寄存器，叫 A，B，C，D  
3、![2](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-2.jpg)    

我们已经知道数据, 是以二进制值存在内存里   
程序也可以存在内存里   
我们可以给CPU支持的所有指令，分配一个ID  
![3](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-3.jpg)   


## 内存启动程序演示(重点)    
在这个假设的例子  
我们用前四位存"操作代码"(operation code)  
简称"操作码"(opcode)  
后四位代表数据来自哪里  
* 可以是寄存器或内存地址   
我们还需要两个寄存器，来完成CPU。     
> 1、一个寄存器追踪程序运行到哪里了，我们叫它  "指令地址寄存器"   
>    顾名思义，存当前指令的内存地址  
> 2、另一个寄存器存当前指令，叫  "指令寄存器"   




## 启动CPU   
当启动计算机时，所有寄存器从0开始    
![4](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-4.jpg)   
 
### 1、首先，将"指令地址寄存器" 连到 RAM   
> 1、寄存器值为0，因此RAM返回0的值   
> ![5](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-5.jpg)   


### 2、现在指令拿到了   
> 要弄清是什么指令，才能执行(execute)    
> 而不是杀死(kill)它  

这是"解码阶段"  
* 前 4位 0010是 LOAD A指令    
	* 意思是, 把 RAM的值放入寄存器A    
* 后 4位 1110是 RAM的地址, 转成十进制是14    


### 3、接下来，指令由"控制单元"进行解码     
就像之前的所有东西, "控制单元"也是逻辑门组成的    
> 比如，为了识别"LOAD A"指令    
> 需要一个电路, 检查操作码是不是0010   
![6](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-6.jpg)   
我们可以用很少的逻辑门来实现.   
现在知道了是什么指令,就可以开始执行了   
 

### 4、开始 "执行阶段"    
* 用 "检查是否 LOAD_A 指令的电路"    
> 打开 RAM 的 "允许读", 把地址 14 传过去        
> ![7](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-7.jpg)     
> 因为是 LOAD_A 指令     
> 我们想把这个值只放到寄存器 A，其他寄存器不受影响     
> 所以需要一根线，把RAM连到4个寄存器  
> 用 "检查是否LOAD_A指令的电路"   
> 启用寄存器A的"允许写入线"  
> ![8](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-8.jpg)   


### 5、关 闭  
- 把 RAM地址14的值，放到了寄存器 A   
既然指令完成了，我们可以关掉所有线路  
去拿下一条指令  


### 6、下一条指令   
我们把 "指令地址寄存器"+1，"执行阶段"就此结束.   
![9](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-9.jpg)     


### 7、升级--封装过程  
具体分析这些解码电路太繁琐了   
既然已经看了1个例子，  
干脆把"控制单元"包成一个整体，简洁一些.  
![10](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-10.jpg)    
控制单元就像管弦乐队的指挥   
> "指挥"CPU的所有组件  


#### 8、封装后--取指令   
"指令地址寄存器" 现在的值是 1    
所以 RAM返回地址 1里的值：0001 1111     
![f-11](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-11.jpg)    

### 9、封装后--解码
到"解码"阶段！     
0001是LOAD B指令:    
> 从RAM里把一个值复制到寄存器B   
> 这次内存地址是1111，十进制的15   


### 10、封装后--执行  
现在到 "执行阶段"！    
成功，我们把值0000 1110     
也就是十进制的 14 存到了寄存器 B    
![f-12](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-12.jpg)    


### 11、封装后--计数  
最后一件事是 "指令地址寄存器" +1  
我们又完成了一个循环    


### 12、下一条指令  
1、取指令1000 0100，1000是ADD指令   
> 这次后面的 4位不是 RAM地址，     
> 而是 2位 2位分别代表 2个寄存器    
> 2 位可以表示 4 个值  
> 所以足够表示 4 个寄存器  
> 第一个地址是 01, 代表寄存器B 
> 第二个地址是 00, 代表寄存器A  
> 因此，1000 0100，代表把寄存器B的值，加到寄存器A里  
> ![13](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-13.jpg)  


## 13、拿ALU进行封装  
> 为了执行这个指令，我们要整合第 5 集的 ALU    
> "控制单元": 负责选择正确的寄存器作为输入   
> 对于 "ADD" 指令，
> 启动B，作为ALU的第一输入  
> 启动A，作为ALU的第二输入   
  
  
### 寄存器    
ALU可以执行不同操作   
> ![14](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-14.jpg)  
最后，结果应该存到寄存器A   
* 但不能直接写入寄存器A  
	* 这样新值会进入ALU ，不断和自己相加    
	* 因此，控制单元用一个自己的寄存器暂时保存结果  

关闭ALU，然后把值写入正确的寄存器   
这里 3+14=17，二进制是0001 0001  
> 现在存到了寄存器 A   
> 最后, 指令地址 +1 (变成0000 0011)   
> 完成  


### 14、下一个指令  
最后一个指令：0100 1101     
> 解码得知是STORE A指令(把寄存器 A的值放入内存)  
> RAM地址13  

接下来，把地址传给 RAM  
> 但这次不是 "允许读取" ，而是 "允许写入"  
> 同时，打开寄存器 A 的 "允许读取"  
> 这样就可以把寄存器 A 里的值，传给RAM  
> ![15](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-15.jpg)  


## 恭喜，我们刚运行了第一个电脑程序！    
它从内存中加载两个值，相加，然后把结果放回内存    
刚刚是我一步步来讲的,   
我们人工CPU的状态 "取指令→解码→执行"   
但不是每台电脑里都有一个迷你 Carrie Anne   
其实是 "时钟" 来负责管理CPU的节奏  
时钟以精确的间隔，触发电信号  
![16](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-16.jpg)    
确保一切按步骤进行  
* 就像罗马帆船的船头，有一个人负责按节奏的击鼓,
* 让所有划船的人同步... 就像节拍器一样
* 节奏不能太快    
因为就算是电也要一定时间来传输  


## CUP时钟  
1赫兹代表一秒1个周期     
因为我花了大概 6分钟，给你讲了 4条指令        
所以我的时钟速度大概是 0.03赫兹   
我承认我算数不快  
但哪怕有人算数很快，最多也就是一秒一次，或 1赫兹  

> ![17](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-17.jpg)  
> 1971年发布的4位CPU  
> ![18](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-18.jpg)    
> 虽然是第一个单芯片的处理器  
> 但它的时钟速度达到了740千赫兹 - 每秒74万次     

你可能觉得很快   
但和如今的处理器相比不值一提      
> 一兆赫兹是 1秒 1百万个时钟周期 
> ![f-19](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-19.jpg)   
> 这可是1秒数10亿次时钟周期  

## 超  频    
你可能听过有人会把计算机超频 
意思是修改时钟速度，加快CPU的速度   
* 就像罗马帆船要撞另一艘船时，鼓手会加快敲鼓速度  
> 芯片制造商经常给 CPU 留一点余地，可以接受一点超频  
> ![20](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-20.jpg)  
> 或产生乱码，因为信号跟不上时钟  

## 降  频   
你可能很少听说降频     
但降频其实很有用     
> 有时没必要让处理器全速运行    
> 可能用户走开了，或者在跑一个性能要求较低的程序    
> 把 CPU 的速度降下来，可以省很多电   
> 省电对用电池的设备很重要，比如笔记本和手机     
为了尽可能省电   
很多现代处理器可以按需求, 加快或减慢时钟速度    
这叫 "动态调整频率" 

## 时钟封装  
加上时钟后，CPU 才是完整的.  
现在可以放到盒子里，变成一个独立组件  
![f21](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/f-21.jpg)  
一层新的抽象(封装)！     
  
看到这里，是否对电脑的内存、CPU有进一步了解？  
去买电脑知道什么重要了吧...

如有疑问, [欢迎提问](https://github.com/KissMyLady/Computer/issues)，或是加QQ群讨论: 36877 9008     
欢迎你的加入！    
  
## 接下来 
- [返回主页-Computer](https://github.com/KissMyLady/Computer)  
- [算数逻辑单元-ALU](https://github.com/KissMyLady/Computer/blob/master/Note/Base_com1.md)  
- [寄存器(Registers)-内存(RAM)](https://github.com/KissMyLady/Computer/blob/master/Note/Base_Registers.md)    
