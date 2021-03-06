AI--计算机视觉  
 ====


我们来思考视觉的重要性   
> 大部分人靠视觉来做饭
>> 越过障碍
>> 读路牌
>> 看视频
>> 以及无数其它任务
![1](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-1.jpg)  

因此半个世纪来, 计算机科学家一直在想办法让计算机有视觉  
因此诞生了"计算机视觉"这个领域  
* 目标是让计算机理解图像和视频  
用过相机或手机的都知道, 可以拍出有惊人保真度和细节的照片  
比人类强得多  
但正如计算机视觉教授最近说的  
> "听到"不等于"听懂"    
> "看到"不等于"看懂"   

## 图像RGB    
图像是像素网格  
> 每个像素的颜色  通过三种基色定义：红，绿，蓝    
> ![2](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-2.jpg)   

### 颜色跟踪算法  
最合适拿来入门的, 是跟踪一个颜色物体，比如一个粉色的球      
> 首先，我们记下球的颜色，保存最中心像素的RGB值       
> ![3](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-3.jpg)  
> 然后给程序喂入图像，让它找最接近这个颜色的像素   
>> 算法可以从左上角开始，逐个检查像素    
>> 计算和目标颜色的差异    
>> ![4](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-4.jpg)  

### 很少用这类   
不只是图片, 我们可以在视频的每一帧图片跑这个算法跟踪球的位置       
当然因为光线，阴影和其它影响      
球的颜色会有变化，不会和存的RGB值完全一样, 但会很接近    
> 如果情况更极端一些， 比如比赛是在晚上，追踪效果可能会很差   
> ![5](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-5.jpg)      
* 因此很少用这类颜色跟踪算法, 除非环境可以严格控制    

颜色跟踪算法是一个个像素搜索, 因为颜色是在一个像素里    
* 但这种方法不适合占多个像素的特征      
	* 比如物体的边缘，是多个像素组成的  

## 块识别   
为了识别这些特征，算法要一块块像素来处理       
每一块都叫"块"    
> ![6](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-6.jpg)  
> 假设用来帮无人机躲避障碍  
为了简单，我们把图片转成灰度, 不过大部分算法可以处理颜色   
![7](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-7.jpg)  
可以很容易地看到 杆子的左边缘从哪里开始    
> ![8](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-8.jpg)  
> 因为有垂直的颜色变化, 我们可以弄个规则说    
>> 某像素是垂直边缘的可能性, 取决于左右两边像素的颜色差异程度    
>> ![9](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-9.jpg)  
> 如果色差很小，就不是边缘  
>> ![10](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-10.jpg)  
>> 里面的数字用来做像素乘法  
总和存到中心像素里  

## 卷  积  
我已经把所有像素转成了灰度值   
现在把"核"的中心，对准感兴趣的像素    
这指定了每个像素要乘的值, 然后把所有数字加起来    
在这里，最后结果是147   
![11](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-11.jpg)

现在我们把"核"应用到另一个像素    
![12](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-12.jpg)   
如果把"核"用于照片中每个像素，结果会像这样:    
> ![13](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-13.jpg)  
>> 注意，水平边缘（比如背景里的平台）  
>> 几乎看不见  
> 如果要突出那些特征  
> 要用不同的"核"  

用对水平边缘敏感的"核"    
这两个边缘增强的核叫"Prewitt算子"     
以发明者命名, 这只是众多"核"的两个例子     
 
## 核有很多作用    
> "核"能做很多种图像转换    
>> 比如"核"能锐化图像, 这个"核"能模糊图像      
>> "核"也可以像饼干模具一样，匹配特定形状    

之前做边缘检测的"核", 会检查左右或上下的差异       
但我们也可以做出:   
> 擅长找线段的"核"    
> 或者包了一圈对比色的区域     
这类"核"可以描述简单的形状   

> ![14](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-14.jpg)  
> 所以线段敏感的"核"对这里的值更高, 眼睛也很独特    
>> ![15](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-15.jpg)  
>> 有其它"核"对这种模式敏感   

### 人脸检测算法   
当计算机扫描图像时，最常见的是用一个窗口来扫   
可以找出人脸的特征组合    
* 虽然每个"核"单独找出脸的能力很弱, 但组合在一起会相当准确      
* ![16](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-16.jpg)  
* 不是脸但又有一堆脸的特征在正确的位置, 这种情况不太可能    
这是一个早期很有影响力的算法的基础 
叫维奥拉·琼斯人脸检测算法    
 
### 卷积神经网络算法   
如今的热门算法是 "卷积神经网络"     
> 神经网络的最基本单位，是神经元     
> 它有多个输入，然后会把每个输入乘一个权重值  
> ![17](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-17.jpg)       
听起来好像挺耳熟，因为它很像"卷积"   

如果我们给神经元输入二维像素
![18](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-18.jpg)   
> 输入权重等于"核"的值, 但和预定义"核"不同  
> 神经网络可以学习对自己有用的"核"，来识别图像中的特征   
> "卷积神经网络"用一堆神经元处理图像数据   
>> 每个都会输出一个新图像，本质上是被不同的"核"处理了   
>> 输出会被后面一层神经元处理, 卷积卷积再卷积   
>>> 第一层可能会发现"边缘"这样的特征  
>>> 单次卷积可以识别出这样的东西   

之前说过, 下一层可以在这些基础上识别   
比如由"边缘"组成的角落  
然后下一层可以在"角落"上继续卷积  
> 下一些可能有识别简单物体的神经元, 比如嘴和眉毛  
> 然后不断重复，逐渐增加复杂度  
> 直到某一层把所有特征放到一起：  
>> 眼睛，耳朵，嘴巴，鼻子  
>> ![19](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-19.jpg)   

## 深度学习  
"卷积神经网络"不是非要很多很多层        
但一般会有很多层，来识别复杂物体和场景        
所以算是"深度学习"       
* "维奥拉·琼斯"和"卷积神经网络", 不只是认人脸，还可以识别手写文字      
* 在CT扫描中发现肿瘤，监测马路是否拥堵   

### 定位面部标志   
但我们这里接着用人脸举例     
> 不管用什么算法，识别出脸之后     
> 可以用更专用的计算机视觉算法, 来定位面部标志     
>> 比如鼻尖和嘴角     
>> 有了标志点，判断眼睛有没有张开就很容易了     
>> 只是点之间的距离罢了     
>> ![20](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-20.jpg)  
也可以跟踪眉毛的位置     
> 眉毛相对眼睛的位置可以代表惊喜或喜悦     
> 根据嘴巴的标志点，检测出微笑也很简单     

### 情感识别算法    
这些信息可以用"情感识别算法"来识别       
> 让电脑知道你是开心，忧伤，沮丧，困惑等等    
>> 然后计算机可以做出合适的行为.    
>>> 比如当你不明白时 给你提示    
>>> 你心情不好时，就不弹更新提示了   
这只是计算机通过视觉感知周围的一个例子  
不只是物理环境, 比如是不是在上班，或是在火车上  
还有社交环境, 比如是朋友的生日派对，还是正式商务会议     
你在不同环境会有不同行为，计算机也应如此  
如果它们够聪明的话...   


面部标记点 也可以捕捉脸的形状  
比如两只眼睛之间的距离，以及前额有多高  
做生物识别  
让有摄像头的计算机能认出你  
不管是手机解锁 还是政府用摄像头跟踪人  

人脸识别有无限应用场景  
另外  跟踪手臂和全身的标记点，最近也有一些突破  
![21](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-21.jpg)  
比如用户给联网微波炉的手势  
正如系列中常说的，抽象是构建复杂系统的关键  

## 无处不在的应用   
硬件层面，有工程师在造更好的摄像头, 让计算机有越来越好的视力  
我自己的视力却不能这样    
> 用来自摄像头的数据, 可以用视觉算法找出脸和手  
> 然后可以用其他算法接着处理，解释图片中的东西  
>> 比如用户的表情和手势  
>> 有了这些，人们可以做出新的交互体验  
>>> 比如智能电视和智能辅导系统, 会根据用户的手势和表情来回应  
   
这里的每一层都是活跃的研究领域  
每年都有突破，这只是冰山一角  
> 如今计算机视觉无处不在 
>> ![22](https://github.com/KissMyLady/Computer/blob/master/Image/AI/see-22.jpg)  
>> 或是美颜相机里添加胡子的滤镜  
令人兴奋的是, 一切才刚刚开始  
最近的技术发展，比如超快的GPU，会开启越来越多可能性  
视觉能力达到人类水平的计算机, 会彻底改变交互方式  
当然，如果计算机能听懂我们然后回话，就更好了 
下章我们讨论计算机的[自然语言处理](#)    

## 接下来  
- [返回Computer主页](https://github.com/KissMyLady/Computer)
- [AI--机器学习与深度学习](https://github.com/KissMyLady/Computer/blob/master/Note/AI_Deep_learn.md)
- [AI--自然语言处理](https://github.com/KissMyLady/Computer/blob/master/Note/AI_language.md)
- [AI--机器人](https://github.com/KissMyLady/Computer/blob/master/Note/AI_robot.md)
- [AI--计算机心理学](https://github.com/KissMyLady/Computer/blob/master/Note/AI_xinli.md)
- [AI--科技教育](https://github.com/KissMyLady/Computer/blob/master/Note/AI_educational.md)
- [AI--奇点、天网、未来](https://github.com/KissMyLady/Computer/blob/master/Note/AI_future.md)  

