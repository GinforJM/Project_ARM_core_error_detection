# week7_summary



## Hardware Backdoors in x86 CPUs  

challenge:

- the length of the instructions is varible
- the obvious approaches don't work

---



Instructions can be one byte

- inc eax

can be 15 bytes

- lock add qword cs:[eax + 4 * eax + 07e06df23h], 0efcdab89h  
- 2e 67 f0 48 818480 23df067e 89abcdef  



goal: **Quickly skip over bytes that don’t matter  **

The meaningful bytes of an x86 instruction impact either its length or its exception behavior



**The processor's instruction decoder checks the first byte of the instruction.**

[![GVkW59.png](https://s1.ax1x.com/2020/03/29/GVkW59.png)](https://imgchr.com/i/GVkW59)



**If the decoder determines that another byte is necessary, it attempts to fetch it**

[![GVk7DO.png](https://s1.ax1x.com/2020/03/29/GVk7DO.png)](https://imgchr.com/i/GVk7DO)



**This byte is on a non-executable page, so the processor generates a page fault.**

**This byte is on a non-executable page, so the processor generates a page fault.
the #PF exception provides a fault address in the CR2 register.**

[![GVkjPA.png](https://s1.ax1x.com/2020/03/29/GVkjPA.png)](https://imgchr.com/i/GVkjPA)



**Finally get the instruction**

[![GVkzxP.png](https://s1.ax1x.com/2020/03/29/GVkzxP.png)](https://imgchr.com/i/GVkzxP)



Future Plan

- 了解BIST ,  lock-step , split-lock等防御机制和使用方法
- 动手实际操作一下BIOS， 尝试一下BIST的使用



