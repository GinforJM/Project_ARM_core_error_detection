

# week9_summary

### BIST

The test machine, also referred to as the automatic test equipment (ATE), applies the test vectors to the fabricated circuit and compares the output responses to the expected responses obtained from the design verification simulatior environment for the fault-free (and hopefully, design error-free) circuit. A "faulty" circuit is now considered to be a circuit with manufacturing defects.

[![JuhXTJ.png](https://s1.ax1x.com/2020/04/19/JuhXTJ.png)](https://imgchr.com/i/JuhXTJ)



**FC = D / T**
D is the number of the detected faults 
T is the number of all the faults in the list



- gate-level faults
- transistor-level faults
- bridging faults
- delay faults



BIST pattern generation

1. ROM	一种方法是将一个好的测试模式集(来自ATPG程序)存储在芯片上的ROM中，但是这在芯片领域是非常昂贵的
2. LFSR 使用线性反馈移位寄存器(LFSR)来生成伪随机测试。这通常需要100万个序列或者通过更多的测试来获得高的故障覆盖率，但是这种方法只使用很少的硬件，并且是目前首选的BIST模式生成方法



| ** **  | **介绍**                                               | **缺点**                                     | **优点**         |
| ------ | ------------------------------------------------------ | -------------------------------------------- | ---------------- |
| 穷举   | 对于一个n输入电路，必须用全部2^n个输入向量来测试电路。 | 当n>为20时，这导致穷举测试不切实际           | 简单，覆盖率大   |
| 伪穷举 |                                                        | 覆盖率可达到100%                             | 测试模式相对较少 |
| 伪随机 | 硬件通过算法产生的随机模式                             | 长测试模式序列可能仍然需要获得足够的故障覆盖 | 测试的模式最少   |

### Lock-Step

[![Ju5kvV.png](https://s1.ax1x.com/2020/04/19/Ju5kvV.png)](https://imgchr.com/i/Ju5kvV)

[![Ju5EuT.png](https://s1.ax1x.com/2020/04/19/Ju5EuT.png)](https://imgchr.com/i/Ju5EuT)

​		Bus 附带冗余的奇偶校验：确保数据传输过程中的准确性

​		奇校验：1000110 已有3个1，为技术，在校验位添加0，接收方根据校验位的数字为0/1，校验“1”的个数是否为奇数，从而确定传输代码的正确性

​		Parity Check奇偶校验器：在数字设备中，数据的传输是大量的，传输的数据都是由0和1构成的进制数字组成。在数据传输或数字通信中，由于存在噪声和干扰，二进制信息的传输可能会出现差错(0 变为1，或者1变为0)。为了检验这种错误，常采用奇偶校验的方法。在接收端，对接收的代码进行检验的电路称为奇(或偶) 校验器

recovery mode = 0/1

Processor 1 error = 0/1

Processor 2 error = 0/1

| Master      | Slave                 | Situation | Action                                                       |
| ----------- | --------------------- | --------- | ------------------------------------------------------------ |
| Processor 1 | Processor 2           | No Error  | None                                                         |
| Processor 1 | Processor 2           | Error     | recovery mode = 1 > Isolate ，Disable Processor 2,Processor 1 error = 0,Processor 2 error = 0 |
| Processor 1 | Processor 2(Disabled) | Error     | Disable Processor 1, Restart Processor 2, Switch Master Processor 1 error = 1,Processor 2 error = 0 |
|             |                       | No Error  | Processor 1 error = 0,Processor 2 error = 1                  |
| Processor 2 | Processor 1(Disabled) | Error     | Processor 1 error = 1,Processor 2 error = 1,Stop System      |
|             |                       | No Error  | Processor 1 error = 1,Processor 2 error = 2                  |



## Future plan

1. 尝试找测试集，和尝试找到实验的设备和方法