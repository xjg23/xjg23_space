# HLS Paper

## 1. 《Transformations of High-Level Synthesis Codes for High-Performance Computing》by ETH Zurich
### Summary
本文主要总结HLS优化的主要transformations，作者归纳为如下4类:
 a) Pipeline-enabling transformations: 主要是resolve一些阻碍II=1的pipeline的写法, 实现最大throughput. 对于memory bound code保证memory is always consume at line rate 
 b) Scalability transformations: 增加spatial parallelism，减少pipeline iterations,即每个cycle处理更多的input， 实现最小的latency 
 c) Secondary transformations: 主要是一些memory access的优化，保证saturate pipelines with data from memory to avoid stalls in compute logic。for memory bound codes, maximize bandwidth utilization即每个cycle处理更多的input.
 d) Software transformations: 同时适用于HLS的传统软件优化策略

### Target
 a) Perfect pipelining
 b) Scaling/Folding
 c) Saturation

 Basic of pipeline:
 a) Latency(L): 输入进入计算逻辑到输出结果需要的cycles，即number of pipeline stages(for a directed acyclic graph of dependencies between computations, 就是critical path)
 b) Initiation interval of gap(II): 两个连续输入需要间隔的最小cycles。II可以看做是inverse throughput of the pipeline.(II=2cycles, 即流水线每2个cycles就stall一次, throughput相对于perfect pipeline(II=1)下降1/2)
 
 C = L + II*(N-1) cycles, N是输入input数

### Detail
 a) Pipeline-enable transformations
 工具在分析时会根据所有运算dependency graph来决定pipeline operations的II, 通常有以下两方面的问题会阻碍该过程：
  1) Interface contention(intra-iteration): 主要是硬件资源的限制，比如fifo/bram等memory资源的端口限制同一cycle只能有1/2次读写
  2) Loop-carried dependency(inter-iteration): 当前循环的运算依赖于上一层循环运算的结果,而这些运算的latency为L, 即此时pipeline最小的II为L

 通过以下transformations来解决：
  1) Iteration space transposition
    对于上述loop-carried dependency，可以通过reorder the loops, 这会改变memory access pattern，所以需要同时增加额外的buffer来存储中间结果解决。

## 2. 《Parallel Programming for FPGAs》pp4fpgas by Ryan Kastner & Stephen Neuendorffer
