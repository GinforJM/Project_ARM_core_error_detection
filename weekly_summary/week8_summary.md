# week8_summary

## BIST

REFERENCE : 

[https://books.google.com/books?id=r8ziBwAAQBAJ&pg=PR12&lpg=PR12&dq=How+BIST+works&source=bl&ots=tKzm17DKHt&sig=ACfU3U0fWamqerkCPIjAqfZiHE6NPaPW9g&hl=zh-CN&sa=X&ved=2ahUKEwjnpp343uHoAhWRCqYKHel6BhQ4ChDoATAIegQIDBA1#v=onepage&q=How%20BIST%20works&f=false](https://books.google.com/books?id=r8ziBwAAQBAJ&pg=PR12&lpg=PR12&dq=How+BIST+works&source=bl&ots=tKzm17DKHt&sig=ACfU3U0fWamqerkCPIjAqfZiHE6NPaPW9g&hl=zh-CN&sa=X&ved=2ahUKEwjnpp343uHoAhWRCqYKHel6BhQ4ChDoATAIegQIDBA1#v=onepage&q=How BIST works&f=false)

《A Designer’s Guide to Built-In Self-Test》, Charles E. Stroud, University of North Carolina at Charlotte



WHAT IS BIST?

BIST的基本思想，以其最简单的形式，就是设计一个电路，使电路能够自我测试，并确定它是“好的”还是“坏的”(分别是无故障的或有故障的)。这通常需要将额外的电路和功能整合到电路的设计中，以方便自我测试功能。这个额外的功能必须能够生成测试模式，并提供一种机制来确定被测电路的输出响应(切到测试模式对应于无故障电路的输出响应)。



图下为BIST电路的代表性结构。该BIST体系结构包括两个基本功能和两个附加功能，这两个功能是在系统中执行自我测试功能所必需的。两个基本功能包括测试模式生成器(TPG)和输出响应分析器(ORA)。当TPG为测试CUT生成一系列模式时，ORA将CUT的输出响应压缩为某种类型的通过/失败指示。系统级使用BIST所需的其他两个功能包括测试控制器(或BIST控制器)和输入隔离电路。除了正常的系统1/0引脚外，BIST的加入还可能需要额外的IO引脚来激活BIST序列(BIST启动控制信号)。报告BIST的结果(通过/失败指示)



[![Gq5Pnx.png](https://s1.ax1x.com/2020/04/12/Gq5Pnx.png)](https://imgchr.com/i/Gq5Pnx)





---

通过/失败指标通过激活的低复位输入到两个同步复位/设置(RS)锁存器。通过将BIST Start设置为逻辑1来激活BIST序列，在逻辑1中，计数器开始依次计数。寻址和阅读输入测试模式从TPG ROM和相应的预期输出响应ORA作为输入测试模式从TPG ROM读取应用于减少通过输入隔离多路复用器,输出响应比较预期的输出响应读取从奥拉罗奥拉比较器将产生逻辑1的预期和实际输出响应之间的任何不匹配,它将通过活动高集输入在通过/失败RS锁存器的输出端产生逻辑1。

[![Gq5iB6.png](https://s1.ax1x.com/2020/04/12/Gq5iB6.png)](https://imgchr.com/i/Gq5iB6)





这种类型的BIST架构很少在实际应用中使用，因为它需要常规的测试向量开发和相当大的电路面积，用于TPG和ORA rom以及计数器。当测试向量集和期望输出响应的位数和向量数都很大时，尤其如此。这种方法也有其他缺点。对CUT的一个微小的设计更改可能需要重新生成测试向量和预期的输出响应。在最好的情况下需要重新编程rom，在最坏的情况下需要调整rom和计数器的大小。作为一个结果。对CUT的微小设计更改可能需要在BIST实现中进行主更改。此外，比较器不会在BIST序列中被完全测试，这样就需要额外的测试来确保比较器是无故障的(就像dis一样)

[![GqLv40.png](https://s1.ax1x.com/2020/04/12/GqLv40.png)](https://imgchr.com/i/GqLv40)

到目前为止讨论的优点和缺点总结在表1.1中。尽管存在缺点，但大多数BIST应用案例研究表明，BIST的好处几乎总是弥补了BIST的成本(包括额外的设计工作、芯片面积的增加和项目的潜在风险)。当BIST电路被设计成可在系统中进行离线系统级测试时尤其如此。例如，考虑一个设备在其生命周期中可能被测试的次数。该设备在制造测试过程中只能测试十次左右;这包括晶圆级测试、封装测试、老化测试、板级设备级测试，以及产品交付现场之前的单元级和系统级测试。在制造测试期间，测试成本的显著节省必须与BIST方法相关联，以克服BIST所需的区域开销和额外设计工作的成本。但是，一旦产品进入现场并投入使用，设备可能会进行测试，频率和频率为每天一到两次。在这种情况下，制造测试只占芯片生命周期中测试总次数的一小部分。因此，BIST的系统级使用为克服BIST的成本和从投资BIST中获得利润提供了最好的舞台。这是本书的另一个目的——不仅展示如何实施BIST，而且展示如何在最小化惩罚和风险的同时最大化BIST的有效性。因此，我们将在接下来的章节中回到BIST的这些优点和缺点，并讨论新的优点和缺点。

## Lock step

reference:

1.《Error detection and fault isolation for lockstep processor systems》,United States Patent, US5915082.
2.《Dual-dual lockstep processor assembles and modules》,United States Patent, US7979746B2.

[![GLuFqH.png](https://s1.ax1x.com/2020/04/12/GLuFqH.png)](https://imgchr.com/i/GLuFqH)



[![GLumJP.png](https://s1.ax1x.com/2020/04/12/GLumJP.png)](https://imgchr.com/i/GLumJP)



两个独立CPU，通常一个为主CPU，另一个为副CPU，使用一个detection & isolation模块负责在检测到CPU出错以后关闭错误CPU和lockstep，并且反馈给selector模块，告知其输出正常CPU的运行结果

## FUTURE WORK

- **BIST**:  尝试搞清楚，system input 部分是否可以自定义，用自己的方式去定义测试样例，及预期结果是如何得到的，这个过程是如何得到的
- **Lockstep**: detection & isolation模块是如何检测出哪个CPU是故障的；故障处理和修复是如何进行的；

