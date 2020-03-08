# Week3

## Meeting Part

### CPU

#### Round-Off error(舍入误差)

​	典型案例:1996年6月4日，在亚利安五号运载火箭发射后37秒，偏离预定轨道而炸毁。原因是软件系统试图将64位浮点数转换为16位浮点数，造成溢出错误.

​	将一个浮点数在计算机中表示，可能会引起误差，EG：如果CPU的计算精度为8位，则π在计算机中被存储为3.14159265，那么当CPU对π(≈3.141592653589793)-3.14159265进行计算时得到的结果为0，当这种误差不断累计下去，CPU就会产生故障。

#### 状态标识位错误

##### 什么是状态标识位？

​		16位的存放条件标志、控制标志寄存器

##### 状态标识位的目的？

​		反映处理器的状态，记录算术和逻辑运算的特征。进位，借位，结果溢出情况>>提供错误反馈

| 标志位（外语缩写） | 标志位名称及外语全称              | =1                       | =0                           |
| ------------------ | --------------------------------- | ------------------------ | ---------------------------- |
| CF                 | 进位标志/Carry Flag               | CY/Carry/进位            | NC/No Carry/无进位           |
| PF                 | 奇偶标志/Parity Flag              | PE/Parity Even/偶        | PO/Parity Odd/奇             |
| AF                 | 辅助进位标志/Auxiliary Carry Flag | AC/Auxiliary Carry/进位  | NA/No Auxiliary Carry/无进位 |
| ZF                 | 零标志/Zero Flag                  | ZR/Zero/等于零           | NZ/Not Zero/不等于零         |
| SF                 | 符号标志/Sign Flag                | NG/Negative/负           | PL/Positive/非负             |
| TF                 | 跟踪标志/Trace Flag               |                          |                              |
| IF                 | 中断标志/Interrupt Flag           | EI/Enable Interrupt/允许 | DI/Disable Interrupt/禁止    |
| DF                 | 方向标志/Direction Flag           | DN/Down/减少             | UP/增加                      |
| OF                 | 溢出标志/Overflow Flag            | OV/Overflow/溢出         | NV/Not Overflow/未溢出       |

**Slides中提到的状态标识位错误是什么？它的产生原理是什么？**



#### 	多线程的并发问题

其中一个例子便是2017年AMD Ryzen系列在linux下进行并行编译出现的segfault bug

###### 			CPU缓存导致的可见性问题

​					硬盘>内存>CPU缓存>内存>硬盘

​					由于多个CPU缓存之间独立不可见，因此线程各自的执行结果对别的线程不可见，导致error

​							线程A>CPU1>CPU1的缓存>内存

​							线程B>CPU2>CPU2的缓存>内存

Example：

```java
public class TestCase {  
  
    private  int number=0;  

    public void addNumber(){  
        for (int i=0;i<100000;i++){  
                number=number+1;  
        }  
    }  
  
     public static void main(String[] args) throws Exception {  
        TestCase testCase=new TestCase();  
        Thread threadA=new Thread(new Runnable() {  
            @Override public void run(){testCase.addNumber();}  
        });  

        Thread threadB=new Thread(new Runnable() {  
            @Override public void run(){testCase.addNumber();}  
        });  

        threadA.start();  
        threadB.start();  
        threadA.join();  
        threadB.join();  
        System.out.println("number="+testCase.number);  
    } 
}
```
这是一个简单的JAVA程序，两个线程同时调用addNumber()方法对int number+1循环10w次，两个线程执行结束后，预期结果number为20w。

​	四核8线程 i7-7700HQ windows10 1909 运行多次 每次结果不同

​		number：148256，116620，134364，151952，136300

​	VM分配1核2线程的Ubuntu 18.04.4LTS(确保在同一个CPU核心下运行)，运行多次 每次结果都为实际预测结果number=200000

​	(均为java11.0.6)



##  RAS summary of ARMv8-M series

### Taxonomy of errors  

- Architectural error propagation
- Architecturally infected, contained, and uncontained
- Architecturally consumed errors 
- other

 ### generate error exception

- Uncontainable error  
- Unrecoverable error  
- Recoverable error  
- Restartable error  

### Error Synchronization Barrier (ESB)  

The RAS Extension introduces a new instruction, the Error Synchronization Barrier (ESB).  

ESB does not itself update any registers, but any ensuing BusFault exception will update at least BFSR and RFSR  

### Implicit Error Synchronization (IESB)  

IESB only updates at least one of BFSR or RFSR if there was a latent asynchronous bus error that was synchronized  

### Fault handling  

- A bus error in response to an action from the PE
-  An error recovery interrupt.
-  A Fault handling interrupt.
-  A critical error interrupt.  

### RAS error records  

### Multiple BusFault exceptions  

- Uncontained error.
- Unrecoverable error.
-  Restartable error.
- Recoverable error.  

### Error Recovery reset  

### Minimal RAS implementation  



### Question:

1、方向问题：

在研究“内核故障检测工具“时，是否需要对CPU故障发生的原因和本质进行更加深入地了解，或是仅对于故障进行初步了解，然后逐个分析现有解决方案对CPU故障的解决方案，汇总提出可行的故障检测设计。





## Meeting Summary

#### 再次明确研究方向

1、从基础做起（创新实验需要自己寻找方向），研究核故障是什么，核故障的发生原理是什么

2、研究Intel BIST对核故障的解决方案

3、横向对比ARMv8的M系列和R系列的技术手册，寻找两种系列对故障处理的方法

3、研读老师发来的关于arm 核故障的paper以及相关的reference



