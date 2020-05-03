# week11_summary



## BIST Response Compaction  

- Bit-by-bit comparison is inefficient
- Compress information into “signature”  

**Response compacting or compressing?**  

[![JzLxaj.png](https://s1.ax1x.com/2020/05/03/JzLxaj.png)](https://imgchr.com/i/JzLxaj)

**Compression Techniques**   

- Ones Count
- Transition Count
- Parity Checking
- Syndrome Checking
- Signature Analysis  



Easy to implement, part of BIST logic

- Small performance degradation

- High degree of compaction

- No or small aliasing errors

  **Problems**:

  1. Aliasing error:
     signature (faulty ckt) = signature (fault-free ckt)
  2. Reference (good) signature calculation:
     Simulation
     Golden unit
     Fault tolerant  

**distinguish between compression and compaction**

Circuit response compression is lossless, because the original output sequence can be completely regenerated from the compressed sequence . 

Compaction, results in information loss, so regenerating the original circuit response in formation is not possible.

 Compression schemes, at present, are impractical for BIST response analysis, because they inadequately reduce the huge volume of data, so we use only compact ion schemes. In mathematical words, compression functions are invertible, but compaction functions are not. Signature analysis is the process of compacting the circuit responses into a very small bit length number,
representing a statistical circuit property, for economical on-chip comparison of the behavior of a possibly defective chip with a good machine chip. The signature must preserve as much of the fault information contained in the circuit output response before compaction as possible, and the circuitry used to implement the compacter should be small. All compaction techniques require that the fault-free circuit
signature be known.



### Future plan

- work together on Lockstep , and make some experiments on it