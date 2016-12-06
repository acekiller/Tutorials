堆和栈的区别(栈是吃了吐 堆是吃了拉)
栈：由系统编译自动管理，不需要程序员手动管理——堆事动态分配和回收内存的，没有静态分配的堆。
堆：释放工作由程序员手动管理，不及时回收容易产生内存泄露——栈由两种分配方式：静态分配（静态分配是系统编译器完成的，比如局部变量的分配）和动态分配（动态分配是有alloc函数进行分配的，但是栈的动态分配和堆事不同的，它的动态分配也由系统编译进行释放，不需要程序员手动管理(student *stu = [[student alloc] init],stu就是系统动态分配在栈中的指针变量）


MRR／MRC ARC

ARC 是一个编译时概念。最低支持xcode 4.2， OS X 10.6 & iOS 4。 但是 OS X 10.6 & iOS 4 并不支持weak引用。
ARC默认对perporty使用strong
weak不会影响其指向的对象的生命周期。当其指向的对像不在被强引用时，将自动设置为nil。
ARC中我们应当充分利用其修饰词，在编程中管理我们对象。因为arc并不负责解决因为强引用导的循环引用问题。合理的使用若引用关系将帮助确保不会产生循环引用。

生命周期修饰符：
__strong
__weak
__unsafe_unretained
__autoreleasing
1. 对于典型的父子关系相互引用中，需要通过父对象引用子对象采用强引用，子对象引用父对象采用若引用。
2. block objects
堆变量默认初始化为nil.

对ARC, Struct 定义中使用id 定义对象存在的问题。

更多知识：
Advanced Memory Management Programming Guide
Memory Manangement Programming Guide for Core Foundation
Tool-Free Bridged Type
ARC Introduces New Lifetime Qualifiers.
Practial Memory Management
Nib Files
Resource Programming Guide


＃ 内存管理
内存管理是指在程序运行期间内存分配，使用以及使用结束时释放的过程。一个良好的程序将尽可能少的使用内存。区分MRR和ARC.


线程：
并发(Concurrent)与并行(parallel)的概念区分：
并发： 统一执行很多任务，表面上同时发生，但是实际上是计算机分时处理的结果，即CPU在不同的任务之间进行切换，执行一段时间后切换到另一个线程。
并行：真正意义上的同时执行任务。
并发是对并行的一种模拟，采用cpu的切片处理在不同的线程间交替执行。其执行顺序采用的先进先出的原则，但并不保证执行的结束顺序。

同步 和 异步
同步：等操作完成才返回
异步：直接返回

串行队列 和 并发队列
串行队列：一次只执行一个任务

线程是在一个单一应用中可以同时执行不同代码的技术之一。
GCD(Grand central Dispatch)是更现代化切高效的并发技术。
Currency Programming Guide

..
1. About Threaded Programming
2. Thread Management
3. Run Loops
4. Synchronization
5. Thread Safely Summary

