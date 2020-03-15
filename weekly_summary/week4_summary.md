# week4_summary

## paper summary

- 一些无文档记录的指令 --- > 未定义的错误，系统安全问题

- 如今的开发者都致力于软件栈，而CPU相当于一个黑盒

​         - Pentium f00f-bug [3]  

- X86架构 vs RISC架构
  - x86trap标志，可变长度
    - Domas
  - RISC，不可变长度
- iScanU  
- 支持ISP和RISC混合长度和固定长度编码
- 将执行指令字时的处理器行为与ISA指定的行为进行比较，使用操作系统信号来确定指令字的有效性。当执行无效的指令字时，操作系统会向出错的进程发送一个SIGILL信号。
- 反编译器编译非文档指令会报错
- ptrace 
- memcage  approach
  - 确保每一条指令都放在内存中，都有对应的信号

[![83FYX6.png](https://s1.ax1x.com/2020/03/15/83FYX6.png)](https://imgchr.com/i/83FYX6)



# CPU故障

CPU故障：核不能正常工作，挂起或崩溃无法继续执行指令。

## Ex1

单粒子效应：电路是靠着电容上积累的电荷确定0或者1的，任何形式的辐射，都会伤害无保护的电路。然后如果有宇宙射线、辐射、太阳黑子爆发或者芯片封装材料中的放射性同位素发生衰变，高能粒子以轰击或者电离的形式导致电子逸出，发生单粒子效应，使CPU发生软失效甚至核故障。

同理，电压电流不稳定也会造成上述故障



软失效：寄存器存储的一个值0001 0111中的一个bit改变，变成了0010 0111。主要通过检错纠错码技术，如Error Correcting Code(ECC)或者奇偶校验等手段修正。

核故障：CPU核重要的控制位发生偏转，或者软失效不断累积，导致核故障发生

单粒子入射产生瞬态电流造成设备损坏；单粒子能级过高，直接击穿电路（此两种情况日常概率极低，一般在航空领域被考虑）。



EG:2004年，Xilinx 公司的部分 FPGA 芯片，单粒子效应问题。

芯片封装材料中的放射性同位素引起

出问题的 Xilinx FPGA 芯片采用了倒封装工艺，Flip-Chip焊球距离晶片上的晶体管有源区只有几个微米的距离。焊锡（铅锡合金）中的微量放射性同位素会发生alpha衰变。

[![83FzC9.jpg](https://s1.ax1x.com/2020/03/15/83FzC9.jpg)](https://imgchr.com/i/83FzC9)



Reference：Xilinx White Paper 208 (2004)



# future work

-  try to exercise：尝试使用qemu模拟器，模拟undocument/invalid instruction的执行情况（编译helloworld.cpp，将所生成文件其中的指令替换， gcc inline）
- 搜寻更多的核故障例子，及其故障原因
- 从reference入手，在学术界更多的相关论文
- 研读一下CPU架构的手册，了解更多的检测方法



