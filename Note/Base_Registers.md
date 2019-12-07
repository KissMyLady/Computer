寄存器(Registers)-内存(RAM)  
==== 

[上节](https://github.com/KissMyLady/Computer/blob/master/Note/Base_com1.md)，我们用逻辑门做了个简单 ALU  
它能执行算术(Arithmetic)和逻辑(Logic)运算   
ALU 里的 A和 L因此得名  
当然，算出来之后如果扔掉就没什么意义了  

## 使用ALU叠加功能    
* 得找个方法存起来  
* 可能还要进行多个连续操作  
这就用到计算机内存了  
> 如果你在主机上打过一场长时间的对局  
> 或玩困难模式的 "扫雷"  
> 然后狗跑过来，被电源线绊倒，把插头拔了出来  
> 你知道失去进度的痛苦  
> ![1](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-1.jpg)  
> 真同情你 :(  

你损失数据的原因是：   
> 电脑用的是"随机存取存储器"，简称"RAM"   
> 它只能在有电的情况下存储东西，比如游戏状态  
 
另一种存储(memory)叫持久存储，电源关闭时数据也不会丢失  
它用来存其他东西，如硬盘，闪存。   

今天我们从简单开始   
> 从做只能存储1位的电路    
> 之后再扩大，做出我们的内存模块    
> 下次和 ALU结合起来，做出CPU！ 

我们至今说过的电路都是单向的  
- 总是向前流动  
比如[上集](https://github.com/KissMyLady/Computer/blob/master/Note/Base_com1.md)的8位 "脉动进位加法器"  
但也可以做回向电路，把输出连回输入    
我们拿一个 OR门试试，把输出连回输入   

#### 看看会发生什么    
> 首先，两个输入都设为 0    
> "0 OR 0" 是 0，所以电路输出0   
> 如果将 A 变成1    
> "1 OR 0" 为 1，所以输出 1   
> 一转眼的功夫，输出回到 B   
> ![2](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-2.jpg)  
>    
> 如果将 A 变成 0，OR 门依然输出 1   
> 现在我们有个电路能记录 "1"  
> 然而有个小问题：这是永久的！  
无论怎么试，都没法从 1 变回 0  


## 锁存器   
我们换成 AND门看看会怎样  
> 开始时，A和 B都设1   
> ![3](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-3.jpg)   
> 如果之后 A设为0，由于是AND门，输出会变成0    
> 这个电路能记录0，和之前那个相反     
> ![4](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-4.jpg)    
   
现在有了能存 0和 1的电路   
为了做出有用的存储 (memory)  
我们把两个电路结合起来    
这叫 "AND-OR 锁存器"   
它有两个输入   
> "设置"输入, 把输出变成 1   
> "复位"输入, 把输出变成 0    
> ![5](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-5.jpg)     
* 也就是说，它存住了 1 位的信息！    
   
存储！  
这叫"锁存", 因为它"锁定"了一个值  
放入数据的动作叫 "写入" ，拿出数据的动作叫 "读取"   
现在我们终于有办法存一个位了！ 
#### 超棒！  


## 门 锁  
麻烦的是, 用两条线 "设置"和"复位" 来输入, 有点难理解   
为了更容易用，我们希望只有一条输入线   
将它设为 0或 1来存储值   
还需要一根线来"启用"内存   
启用时允许写入，没启用时就 "锁定"  
#### 这条线叫 "允许写入线"   
加一些额外逻辑门，可以做出这个电路   
![6](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-6.jpg)       


## 门锁封装  
现在有点复杂了    
我们不想关心单独的逻辑门   
所以我们提升一层抽象  
![7](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-7.jpg)       
把 "门锁" 放到盒子里 - 这个盒子能存一个bit  
我们来测一下新组件！  


### 测试封装的门锁   
> 一切从 0 开始  
> 数据输入从0换到1, 从1换到0
> 什么也不会发生 - 输出依然是 0    
> 因为 "允许写入线" 是关闭的，所以内容不会变化  
> 所以要给 "允许写入线" 输入1, "打开" 门  
> 现在往 "数据线" 放 1，1 就能存起来了  
> 注意输出现在是 1了  
> 成功！  
 
* 现在可以关掉 "允许写入线", 输出会保持1      
* 现在不管给 "数据线" 什么值     
* ![8](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-8.jpg)  
值存起来了     
打开"允许写入线",  "数据线"设为0      
完成, "允许写入线" 关闭，输出 0   
成功了！   
![10](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-10.jpg)



## 寄存器   
当然，只能存 1 bit没什么大用  
* 肯定玩不了游戏, 或做其它事情   
但我们没限制只能用一个锁存器    
> 如果我们并排放 8个锁存器， 
> 可以存8位信息，比如一个8bit数字 
> 一组这样的锁存器叫 "寄存器"   

* 寄存器能存一个数字，这个数字有多少位，叫"位宽"  
早期电脑用 8位寄存器，然后是 16位，32位 
如今许多计算机都有 64 位宽的寄存器  

#### 启动寄存器   
> 写入寄存器前，要先启用里面所有锁存器   
> 我们可以用一根线连接所有"允许输入线", 把它设为 1   
> 然后用8条数据线发数据，然后将"允许写入线"设回 0    
> ![e-11](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-11.jpg)  
> 现在8位的值就存起来了   

#### 大规模寄存器解耦  
> 如果只有很少的位(bits)，把锁存器并排放置，也勉强够用了。     
> 64位寄存器要 64根数据线，64根连到输出端     
> 幸运的是，我们只要 1 根线启用所有锁存器  
> 但加起来也有 129 条线了   
> 如果存 256 位要 513 条线！   
解决方法是矩阵！    

#### 网格矩阵     
在矩阵中，我们不并列排放锁存器     
而是做成网格   
> 存256位，我们用 16x16网格的锁存器，有 16行 16列  
> ![12](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-12.jpg)    
 

### 矩阵细节原理    
放大看看怎么做的   
### 1、写入数据   
> 只有行线和列线均为1 ，AND门才输出1    
> ![13](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-13.jpg)      
> 这种行/列排列法，用一根 "允许写入线" 连所有锁存器    
> 为了让锁存器变成 "允许写入"    
> 行线，列线和 "允许写入线" 都必须是1  
>   
> 每次只有 1个锁存器会这样    
> 代表我们可以只用一根 "数据线"   
> 连所有锁存器来传数据     
> 因为只有一个锁存器会启用，只有那个会存数据    
> 其他锁存器会忽略数据线上的值，因为没有 "允许写入"  

#### 2、读取数据
我们可以用类似的技巧, 做"允许读取线"来读数据  
从一个指定的锁存器，读取数据  
所以对于256位的存储  
只要 35条线  
> 1、1条"数据线"      
> 2、1条"允许写入线"     
> 3、1条"允许读取线"     
> 4、还有16行16列的线用于选择锁存器    
> (16+16=32,  32+3=35)   
> 这省了好多线！   


## 多路复用器   
我们刚刚存了一位的地址是 "12行8列"    
由于最多 16行, 用 4位就够了   
12 用二进制表示为 1100    
列地址也可以这样： 8 用二进制表示为 1000    
刚才说的"12行 8列"可以写成 11001000     
为了将地址转成  行和列   
* 我们需要 "多路复用器"    
* 这个名字起码比 ALU 酷一点   


多路复用器有不同大小  
因为有 16 行，我们需要 1 到 16 多路复用器  
工作方式是：  
> 输入一个 4 位数字，它会把那根线，连到相应的输出线   
> ![e-14](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-14.jpg)    
> 如果输入 0001，会选择下一列，依此类推  
> 
> 一个多路复用器处理行(row) 
> 另一个多路复用器处理列(column) 
> 好吧，开始有点复杂了  


## 多路复用器封装  
那么把 256 位内存当成一个整体好了  
又提升了一层抽象！    
> 它输入一个8位地址:  4位代表列，4位代表行   
>  
> 我们还需要 "允许写入线" 和 "允许读取线"
> 最后，还需要一条数据线，用于读/写数据
> ![e-15](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-15.jpg)  

不幸的是, 256位的内存也没法做什么事 
所以还要扩大规模    
> 把它们并排放置   
> 就像寄存器一样    
> 一行8个，可以存一个 8 位数字    
> 8位也叫一个字节(byte)    
![e-16](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-16.jpg)   
为了存一个8位数字，我们同时给 8个256位内存一样的地址   
每个地址存1位   
意味着这里总共能存256个字节(byte)     
再次，为了简单，我们不管内部    
不看作是一堆独立的存储模块和电路     
而是看成一个整体的可寻址内存    
我们有256个地址    
![e-17](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-17.jpg)   
我们下集做 CPU时会用到这个内存   
现代计算机的内存   
 扩展到上兆字节(MB)和千兆字节(GB)的方式   
和我们这里做的一样   


## 封装到更大规模    
> 不断把内存打包到更大规模   
> 随着内存地址增多，内存地址也必须增长   
> 8 位最多能代表256个内存地址    
> （1111 1111是255，0~255一共256个数字）    
> 只有这么多   

 
## RAM   
要给千兆或十亿字节的内存寻址，需要 32位的地址   
内存的一个重要特性是：可以随时访问任何位置   
![e-18](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-18.jpg)  
因此叫 "随机存取存储器" ，简称 RAM   
> 当你听到有人说 RAM 有多大   
> 他的意思是内存有多大  
> 记录当前在做什么事    
 
#### RAM原理     
比如吃了午饭没，或有没有交电话费   
这是一条真的内存，上面焊了8个内存模块   
> ![e-19](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-19.jpg)   
> 打开其中一个，放大   
> 会看到 32 个内存方块  
> ![e-20](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-20.jpg)    
> 放大  
> ![e-21](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-21.jpg)  
> 再放大，可以看到存一个"位"的矩阵  
> ![e-22](https://github.com/KissMyLady/Computer/blob/master/Image/BASE_ALU_CPU/e-22.jpg)   
> 这个矩阵是128位x64位，总共8192位  
>  
> 每个方格 4 个矩阵     
>     
> 所以一个方格有32768个位(8192 x 4 = 32768)   
> 而一共32个方格     
> 总而言之，1个芯片大约存100万位  
> 也就是1兆字节(1MB)     

#### 1MB如今不算大 -这是1980年代的RAM     
如今你可以买到千兆字节(GB)的RAM        
   
那可是数十亿字节的内存!!       
今天，我们用锁存器做了一块SRAM(静态随机存取存储器)    
还有其他类型的RAM，如DRAM，闪存和NVRAM     
它们在功能上与SRAM相似
但用不同的电路存单个位      
- 比如用不同的逻辑门，电容器，电荷捕获或忆阻器  
  
但根本上  这些技术都是矩阵层层嵌套，来存储大量信息  
就像计算机中的很多事情，底层其实都很简单   
让人难以理解的，是一层层精妙的抽象  
像一个越来越小的俄罗斯套娃  
计算机底层还是很简单的吧   


## 接下来  
