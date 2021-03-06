储存介质发展史   
====

我们多次谈到内存(Memory), 甚至在设计了一个简单内存  
> 一般来说,电脑内存是 "非永久性", 如果Xbox电源线不小心拔掉了,内存里所有数据都会丢失
>> 所以内存叫"易失性"存储器  
我们还没谈过的话题是存储器(Storage)
存储器(Storage)和内存(Memory)有点不同
任何写入"存储器"的数据, 比如你的硬盘, 数据会一直存着, 直到被覆盖或删除,断电也不会丢失

存储器是"非易失性"的
以前是"易失性"的速度快, "非易失性"的速度慢, 但随着技术发展, 两者的差异越来越小

如今我们认为稀松平常的技术, 比如这个U盘能低成本+ 可靠+ 长时间存储上GB的数据  
但以前可不是这样的



## 打孔纸卡
最早的存储介质是, 打孔纸卡, 以及纸卡的亲戚, 打孔纸带  
![1](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-1.jpg)  
到1940年代,纸卡标准是80列x12行, 一张卡能存960位数据(80x12=960)  
据我们所知的最大纸卡程序是美国军方的"半自动地面防空系统"简称SAGE一个在1958年投入使用的防空系统  
![2](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-2.jpg)   
大小 5MB 左右, 相当如今手机拍张照  
纸卡用了十几年,因为不用电而且便宜耐用  
  
缺 点:    
> 然而坏处是读取慢,只能写入一次, 打的孔无法轻易补上  
>　对于存临时值,　纸卡不好用  
我们需要更快更大更灵活的存储方式  
  
  
  
## 延迟线存储器  
"延迟线存储器"(Delay Line Memory)原理如下  
> 拿一个管子装满液体,如水银  
> 管子一端放扬声器,另一端放麦克风  
> 扬声器发出脉冲时  会产生压力波  
> ![3](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-3.jpg)    
  
>> 麦克风将压力波 转换回电信号.  
>> 我们可以用压力波的传播延迟  来存储数据！  
  
> 假设有压力波代表 1,没有代表 0  
> 扬声器可以输出 1010 0111  
> 压力波沿管子传播,过了一会儿,撞上麦克风, 将信号转换回 1和 0    
>> 如果加一个电路,连接麦克风和扬声器  
>> 再加一个放大器(Amplifier)来弥补信号衰弱就能做一个存储数据的循环  
  
* ![4](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-4.jpg)   
* 但管子中可以存储多个位(bit)  
  
忙完 ENIAC后,Eckert和同事 John Mauchly  
着手做一个更大更好的计算机叫 EDVAC,使用了延迟线存储器  
总共有 128条延迟线,每条能存352位(bits)  
  
总共能存 45,000位(bit)  
对 1949 年来说还不错！  
这使得 EDVAC 成为最早的 "存储程序计算机" 之一  
  
缺 点:    
> 每一个时刻只能读一位 (bit) 数据  
>> 如果想访问一个特定的bit,比如第 112位(bit)你得等待它从循环中出现  
* 所以又叫 "顺序存储器"或"循环存储器"  
而我们想要的是 "随机存取存储器" 可以随时访问任何位置  
  
### 增加内存密度也是一个挑战  
把压力波变得更紧密  意味着更容易混在一起  
  
### 磁致伸缩延迟存储器  
所以出现了其他类型的 "延迟线存储器"  
如 "磁致伸缩延迟存储器"  
> ![5](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-5.jpg)   
> 通过把线卷成线圈,1英尺×1英尺的面积能存储大概 1000位(bit)  
  
然而,延迟线存储器在 1950 年代中期就基本过时了  
因为出现了新技术,性能,可靠性和成本都更好于"磁芯存储器"  



## 磁芯存储器  
用了小型磁圈, 如果给磁芯绕上电线,并施加电流,可以将磁化在一个方向  
![6](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-6.jpg)  
> 如果关掉电流,磁芯保持磁化,  
> 如果沿相反方向施加电流, 磁化的方向(极性)会翻转  
>> 这样就可以存 1和0！  

### 排列成网格  
如果只存 1位不够有用,所以把小甜甜圈排列成网格  
![7](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-7.jpg)  

> ![8](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-8.jpg)  
> ![9](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-9.jpg)  
> 所以能存 1024位(bit),(32x32=1024)  
>> 总共 9个黄色方格, 所以这块板子最多能存 9216位(bit) (1024x9=9216)  
>> 换算过来大约是 9千字节(9216 bit ~= 9kb)  
  
### 第一次大规模运用  
磁芯内存的第一次大规模运用是1953年麻省理工学院的 Whirlwind 1计算机  
磁芯排列是 32×32  
> 用了 16 块板子,能存储大约16000位(bit)  
> 更重要的是, 不像"延迟线存储器"磁芯存储器能随时访问任何一位(bit)  
> 这在当时非常了不起  
  
### 成本还是非常高  
![10](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-10.jpg)  
而且一般还是手工编织的！  
刚开始时  存储成本大约 1美元 1位(bit)到1970年代,下降到 1美分左右  
不幸的是,即使每位 1美分也不够便宜  
之前提过,现代手机随便拍张照片都有 5MB  
> 5MB 约等于 4000万bit, 你愿意花40万美元在"磁芯存储器"上存照片吗？  
如果你有这么多钱  
  
  
## 磁  带  
当时对存储技术进行了大量的研究  
到 1951年,Eckert和 Mauchly创立了自己的公司  
设计了一台叫 UNIVAC的新电脑  
最早进行商业销售的电脑之一, 它推出了一种新存储：磁带    
> 磁带是纤薄柔软的一长条磁性带子  卷在轴上  
> 磁带可以在"磁带驱动器"内前后移动  
>> 里面有一个"写头"绕了电线,电流通过产生磁场， 导致磁带的一小部分被磁化  
>> 电流方向决定了极性,代表 1和0  
>>> ![11](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-11.jpg)  
>    
> 磁带每英寸可存 128位数据, 每卷有1200英尺长  
> ![12](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-12.jpg)  
> 接近2兆字节！(2MB)  
![13](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-13.jpg)
因此磁带至今仍用于存档  
* 磁带的主要缺点是访问速度  
* 磁带是连续的,必须倒带或快进到达特定位置  
可能要几百英尺才能得到某个字节(byte),这很慢  
  
  
## 磁鼓存储器  
1950,60年代,有个类似技术是 "磁鼓存储器"  
> 有金属圆筒,盖满了磁性材料以记录数据, 滚筒会持续旋转,周围有数十个读写头  
> ![14](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-14.jpg)  
> 等滚筒转到正确的位置  读写头会读或写 1位(bit)数据  
> 为了尽可能缩短延迟, 鼓轮每分钟上千转！  

到1953年,磁鼓技术飞速发展, 可以买到存80,000 位的"磁鼓存储器", 也就是10KB  
但到1970年代 "磁鼓存储器" 不再生产   
然而,磁鼓导致了硬盘的发展硬盘和磁鼓很相似  
不过硬盘用的是盘, 不像磁鼓用圆柱体, 因此得名  
原理是一样的, 磁盘表面有磁性    
写入头和读取头, 可以处理上面的1和0    
  
  
## 硬  盘  
硬盘的好处是薄,可以叠在一起, 提供更多表面积来存数据  
顺便一说名字不错  
它有 50张 24英寸直径的磁盘,总共能存 5 MB左右  
太棒啦! 终于能存一张现代手机的照片了！这年是 1956 年  
  
  
### 寻道时间  
> 要访问某个特定 bit, 一个读/写磁头会向上或向下移动,找到正确的磁盘  
> 然后磁头会滑进去就像磁鼓存储器一样, 磁盘也会高速旋转  
> 所以读写头要等到正确的部分转过来也叫寻道时间  
  
虽然六分之一秒对存储器来说算不错   但对内存来说还不够快  
所以RAMAC 305还有"磁鼓存储器"和"磁芯存储器"  
这是"内存层次结构"的一个例子  
> 一小部分高速 + 昂贵的内存  
> 一部分稍慢 + 相对便宜些的内存  
> 还有更慢 + 更便宜的内存  
>> 这种混合在成本和速度间取得平衡  


  
1970年代, 硬盘大幅度改进并变得普遍  
> 如今的硬盘可以轻易容 1TB的数据能存 20万张 5MB的照片！网上最低 40美元就可以买到  
> 每bit成本0.0000000005美分  
>> 比磁芯内存 1 美分 1 bit 好多了！  
>> 另外,现代硬盘的平均寻道时间低于 1/100 秒  
  
  
## 软  盘  
除了磁盘是软的,其他基本一样  
你可能见过某些程序的保存图标是一个软盘  
> ![15](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-15.jpg)  
> 软盘曾经是真实存在的东西！  
> 软盘是为了便携, 在1970~1990非常流行  
如今当杯垫挺不错的  
  
密度更高的软盘, 如Zip Disks,在90年代中期流行起来  
但十年内就消失了  
  
  
## 光  盘  
光学存储器于 1972 年出现,12 英寸的"激光盘"  
![16](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-16.jpg)  
你可能对后来的产品更熟：光盘(简称 CD)  
以及 90年代流行的 DVD  
功能和硬盘软盘一样,都是存数据.  
但用的不是磁性  
> ![17](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-17.jpg)  
> 光盘表面有很多小坑,造成光的不同反射  
> 光学传感器会捕获到,并解码为 1 和 0  

  
  
## 固态存储  
如今,存储技术在朝固态前进,没有机械活动部件  
比如硬盘, 以及U盘里面是集成电路  
  
第一个RAM集成电路出现于 1972年,  成本每比特 1美分  
使"磁芯存储器"迅速过时如今成本下降了  
更多机械硬盘被固态硬盘逐渐替代,简称SSD  
  
> 由于 SSD 没有移动部件  
> 磁头不用等磁盘转, 所以SSD访问时间低于1/1000秒  
> ![19](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-19.jpg)  
> 这很快！ 但还是比RAM慢很多倍  
> ![20](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-20.jpg)  

  
所以现代计算机 仍然用存储层次结构  
我们从 1940 年代到现在进步巨大  
  

晶体管数量有摩尔定律, 内存和存储技术也有类似的趋势  
从早期每 MB成本上百万美元,下滑到2000年只要几分钱,如今远远低于 1分钱  
![21](https://github.com/KissMyLady/Computer/blob/master/Image/com/r-21.jpg)  
完全没有打孔纸卡  
你能想象SEGA的纸卡房间风一吹会怎样吗？  
62,500张卡  
我想都不敢想  


