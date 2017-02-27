# iOS知识点/面试题总结
 
###0.OC的理解与特性
```
OC作为一门面向对象的语言，自然具有面向对象的语言特性：封装、继承、多态。它既具有静态语言的特性（如C++），又有动态语言的效率（动态绑定、动态加载

等）。总体来讲，OC确实是一门不错的编程语言，Objective-C具有相当多的动态特性，表现为三方面：动态类型（Dynamic typing）、动态绑定（Dynamic 

binding）和动态加载（Dynamic loading）。动态——必须到运行时（run time）才会做的一些事情。

动态类型：即运行时再决定对象的类型，这种动态特性在日常的应用中非常常见，简单来说就是id类型。事实上，由于静态类型的固定性和可预知性，从而使用的更加广

泛。静态类型是强类型，而动态类型属于弱类型，运行时决定接受者。

动态绑定：基于动态类型，在某个实例对象被确定后，其类型便被确定了，该对象对应的属性和响应消息也被完全确定。

动态加载：根据需求加载所需要的资源，最基本就是不同机型的适配，例如，在Retina设备上加载@2x的图片，而在老一些的普通苹设备上加载原图，让程序在运行时添

加代码模块以及其他资源，用户可根据需要加载一些可执行代码和资源，而不是在启动时就加载所有组件，可执行代码可以含有和程序运行时整合的新类
```
###1.对面向对象的理解
```
面向对象的语言设计是相对于面向过程的语言设计来讲的,一般是指类在内存中装载的实例,具有相关的成员变量和成员函数,具有抽象性,多态性,封装性等特点,大大地降

低了软件开发的难度,提高了软件开发的效率.
```
###2.内存管理机制
```
栈区(stack)由编译器自动分配释放 ,存放方法(函数)的参数值, 局部变量的值等，栈是向低地址扩展的数据结构，是一块连续的内存的区域。即栈顶的地址和栈的最大容量是系统预先规定好的。

堆区(heap)一般由程序员分配释放, 若程序员不释放,程序结束时由OS回收，向高地址扩展的数据结构，是不连续的内存区域，从而堆获得的空间比较灵活。

碎片问题：对于堆来讲，频繁的new/delete势必会造成内存空间的不连续，从而造成大量的碎片，使程序效率降低。对于栈来讲，则不会存在这个问题，因为栈是先进

后出的队列，他们是如此的一一对应，以至于永远都不可能有一个内存块从栈中间弹出.

配方式：堆都是动态分配的，没有静态分配的堆。栈有2种分配方式：静态分配和动态分配。静态分配是编译器完成的，比如局部变量的分配。动态分配由alloca函数进

行分配，但是栈的动态分配和堆是不同的，他的动态分配是由编译器进行释放，无需我们手工实现。

分配效率：栈是机器系统提供的数据结构，计算机会在底层对栈提供支持：分配专门的寄存器存放栈的地址，压栈出栈都有专门的指令执行，这就决定了栈的效率比较

高。

堆则是C/C++函数库提供的，它的机制是很复杂的。

全局区(静态区)(static),全局变量和静态变量的存储是放在一块 的,初始化的全局变量和静态变量在一块区域, 未初始化的全局变量和未初始化的静态变量在相邻的

另一块区域。程序结束后有系统释放。

文字常量区 — 常量字符串就是放在这里的。程序结束后由系统释放。

程序代码区 — 存放函数体的二进制代码
```
###3.冒泡排序

一种计算机科学领域的较简单的排序算法,它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到

没有再需要交换，也就是说该数列已经排序完成。
```
程序示例:
int main(int argc, const charchar * argv[]) {  
@autoreleasepool {  
/* 
冒泡排序法的基本思想：（以升序为例）含有n个元素的数组原则上要进行n-1次排序。对于每一躺的排序，从第一个数开始，依次比较前一个数与后一个数的大小。   如果前一个数比后一个数大，则进行交换。这样一轮过后，最大的数将会出现称为最末位的数组元素。第二轮则去掉最后一个数，对前n-1个数再按照上面的步骤找出最  大数，该数将称为倒数第二的数组元素......n-1轮过后，就完成了排序。   
*/   
         //n个元素比较n-1趟  
         //每趟比较次数 = 数组元素个数 - 趟数   
         NSMutableArray *numbers = [NSMutableArray arrayWithObjects:@"17",@"28",@"36",@"15",@"39", nil nil];  
         for (int i = 0; i < 5 - 1; i++) {  
             //比较的趟数  
             for (int j = 0; j < 5 - 1 - i; j++) {  
                 //比较的次数  
                 if ([numbers[j] intValue] > [numbers[j + 1] intValue]) {  
                     //这里为升序排序  
                     int temp = [numbers[j] intValue];  
                     numbers[j] = numbers[j + 1];  
                     //OC中的数组只能存储对象，所以这里转换成string对象  
                     numbers[j + 1] = [NSString stringWithFormat:@"%d",temp];  
                 }  
             }  
         }  
         NSLog(@"排序后%@",numbers);  
     }  
     return 0;  
 } 
 
 ```                                     
###4.MVC设计模式

MVC是一种架构模式，M表示Model，V表示视图View，C表示控制器Controller：

Model负责存储、定义、操作数据；

View用来展示给用户，和用户进行操作交互；

Controller是Model和View的协调者，Controller把Model中的数据拿过来给View用。Controller可以直接与Model和View进行通信，而View不能和

Controller直接通信。View与Controller通信需要利用代理协议的方式，当有数据更新时，Model也要与Controller进行通信，这个时候就要用Notification和

KVO，这个方式就像一个广播一样，Model发信号，Controller设置监听接受信号，当有数据更新时就发信号给Controller，Model和View不能直接进行通信，这样

会违背MVC设计模式。

###5.MVVM设计模式

M:Model层

V:ViewController层

VM:ViewModel层，就是View和Model层的粘合剂，他是一个放置用户输入验证逻辑，视图显示逻辑，发起网络请求和其他各种各样的代码的地方。就是把原来

ViewController层的业务逻辑和页面逻辑等剥离出来放到ViewModel层。

###6.iOS APP启动过程

http://www.jianshu.com/p/231b1cebf477 (吴白的技术博客)

###7.iOS 内存管理

http://blog.devtang.com/2016/07/30/ios-memory-management/ (唐巧的技术博客)

###8.iOS 性能调优

http://blog.ibireme.com/2015/11/12/smooth_user_interfaces_for_ios/ (ibireme的技术博客) 

http://www.jianshu.com/p/1b5cbf155b31 (hi_xgb的技术博客)

http://www.jianshu.com/p/ca51c9d3575b (seedante的技术博客)

http://www.jianshu.com/p/05b68c84913a (iOS魏的技术博客)

###9.iOS多线程

http://www.cnblogs.com/kenshincui/p/3983982.html (Kenshin Cui's Blog)

http://www.jianshu.com/p/665261814e24 (天口三水羊的技术博客)

###10.iOS RunLoop

http://www.jianshu.com/p/2d3c8e084205 (Jabber_YQ 的博客)
(RunLoop入门)

http://blog.ibireme.com/2015/05/18/runloop/ (ibireme的技术博客)
(深入理解RunLoop)
###11.iOS RunTime

http://www.jianshu.com/p/ab966e8a82e2 (滕先洪的技术博客)
(RunTime入门)

http://blog.sunnyxx.com/2016/08/13/reunderstanding-runtime-0/ (sunny的技术博客)
(重识 Objective-C Runtime 系列)

###12.iOS KVC/KVO

http://blog.csdn.net/wzzvictory/article/details/9674431?utm_source=tuicool (王中周的技术博客)

https://github.com/minggo620/iOSObserving (minggo620的技术博客)

http://www.cnblogs.com/kenshincui/p/3871178.html (Kenshin Cui's Blog)

https://objccn.io/issue-7-3/

https://www.zybuluo.com/MicroCai/note/66738

###13.iOS Block

http://blog.devtang.com/2013/07/28/a-look-inside-blocks/ (唐巧的技术博客)

###14.iOS 图文混排

http://blog.devtang.com/2015/06/27/using-coretext-1/ (唐巧的技术博客_基础)

http://blog.devtang.com/2015/06/27/using-coretext-2/ (唐巧的技术博客_进阶)

http://www.jianshu.com/p/960e25d72750 王隆帅的技术博客) 

###15.iOS网络

http://www.cnblogs.com/jy578154186/archive/2013/02/26/2933995.html (111111*** 的技术博客)

http://www.jianshu.com/p/1389677a5840

http://www.devstore.cn/essay/essayInfo/2043.html?utm_source=tuicool&utm_medium=referral

###16.iOS 直播

https://github.com/tiantianlan/LiveExplanation (tianlan的技术博客)

http://www.jianshu.com/p/bd42bacbe4cc (袁峥Seemygo的技术博客)

http://www.jianshu.com/p/b8db6c142aad (Monkey_ALin)

###17.iOS APP上架

http://www.jianshu.com/p/b1b77d804254 (冰晨的技术博客)

###18.iOS APNS

http://www.jianshu.com/p/032bfc949917 (OneTea的技术博客)

http://www.cnblogs.com/kenshincui/p/4168532.html (Kenshin Cui's Blog)

###19.iOS AES加密

https://github.com/IMCCP/CCPAESEncode (IMCCP的技术博客)

###20.iOS 相机/相册

https://github.com/IMCCP/CCPCustomCamera (IMCCP的技术博客)

###21.iOS触摸事件、手势识别、摇晃事件、耳机线控(基础)

http://www.cnblogs.com/kenshincui/p/3950646.html (Kenshin Cui's Blog)

###22.iOS 绘图/动画(基础)

http://www.cnblogs.com/kenshincui/p/3959951.html (Kenshin Cui's Blog)

http://www.cnblogs.com/kenshincui/p/3972100.html (Kenshin Cui's Blog)

###23.iOS 音视频(基础)

http://www.cnblogs.com/kenshincui/p/4186022.html (Kenshin Cui's Blog)

###24.iOS 内购/蓝牙相关(基础)

http://www.cnblogs.com/kenshincui/p/4220402.html (Kenshin Cui's Blog)

###25.iOS 二维码

http://www.jianshu.com/p/18cb6632064e (iOS_小松哥的技术博客)

###26.iOS 面试题汇总

https://github.com/ChenYilong/iOSInterviewQuestions (招聘一个靠谱的iOS)

http://www.jianshu.com/p/c687110e552c (答卓同学的iOS面试题)

