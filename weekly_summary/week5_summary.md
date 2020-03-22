# week5_summary

## CPU errors result from a malfunction of a hardware element, such as 

- **a timing facility**
- **instruction-processing hardware**
- **microcode**

## 故障原因之一

- **there are millions of transistors in a modern PC,It may only require one transistor to fail before a CPU stops functioning**

现代PC中有数百万个晶体管，在一个CPU停止工作之前，可能只需要一个晶体管出现故障

- **Even simply clock frequency jitter which manifests itself as a miniscule phase shift(s) can change the value of the bitstream.**

即使是简单的时钟频率抖动，表现为一个非常小的相移，也可以改变位流的值。



## CPU

- ALU

**case**:

RTfloat  fValue = 4195835.0f - ( ( 4195835.0f / 3145727.0f ) * 3145727.0f );
RTdouble  dValue = 4195835.0L - ( ( 4195835.0L / 3145727.0L ) * 3145727.0L );

Results:
Intel 486 CPU = 0
Intel Pentium CPU = 256
All the rest Intel CPUs = 0

**resolution**

 functional redundancy checking support

 - two Pentiums perform the same calculations, comparing results after each step. If the results do not match, processors repeat the calculations.
- CU





# cpu error

无效指令

eg：Intel f00f Bug

16进制序列f0 0f c7 c8=汇编指令lock cmpxchg8b %eax

1. cmpxchg8b：比较并互换两个64bit的数，目标只能是memory中的数值，不能指向temporary register eax

2. lock前缀只能用于基于内存的“读—修改—写”型的指令，而上面的指令同样也不符合这一要求。

理想情况中，任一错误都会导致invalid opcode，CPU会进行错误处理。但是当CPU执行f0 0f c7 c8时，会发生如下情况：

1. 执行 `cmpxchg8b %eax`，发现指令不合法，产生invalid opcode异常，寻找对应处理函数
2. CPU错误地执行`#LOCK`指令
3. 因为执行 `#LOCK`，CPU 必须要等待「写」，才会释放 lock，但是没有可执行的write指令，CPU锁死

此命令可以在任何等级的权限下执行



lockstep

lockstep是一种计算机冗余设计的容错系统：多个CPU同时执行同一组指令，将结果输入一个比较逻辑中，周期性比较输出结果是否相同。如果相同，则继续运行；如果不同，则采取一定的措施诊断出故障处理器，及时阻止故障发生。

典型的Lockstep处理器系统包括两个独立CPU，通常一个为主CPU，负责输出结果，另一个为副CPU，负责检测主CPU的输出正确性，同时还需要故障检测和恢复功能，例如预存多个已知结果的指令，在检测到故障发生时，两个cpu同时执行该指令，从而判断哪个cpu发生错误，主CPU发生错误，则关闭主CPU，负责检测的副CPU允许输出结果，成为主CPU，副CPU发生错误则关闭副CPU。与此同时，故障CPU进行重启或调用内部的故障修复工具进行故障排查，确认故障被修复后，则重新启用，否则提示故障警报，需要人工排查或进行维修。

Cortex-A、Cortex-R系列中的部分产品都集成了类似于lockstep的技术，“Split-lock”，Split-Lock’可以被配置成两种模式：‘split mode’，两个CPU可以独立执行不同的程序或任务，从而使处理器获得更高的性能； ‘lock mode’ ，两个CPU执行锁步模式，使处理器的运行更加安全且不容易出错。这种技术可以支持如果两个CPU中的一个损坏，可以在降级模式下继续运行，即只运行好的那个CPU。



# fucture plan

- lock-step 和 split-lock

- find the paper about X86 domas
- look for  deeper understanding of the causes and nature of CPU failures 





