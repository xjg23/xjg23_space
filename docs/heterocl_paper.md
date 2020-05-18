# 《HeteroCL: A Multi-Paradigm Programming Infrastructure for Software-Defined Reconfigurable Computing》 Jason Cong FPGA-2019

## HeteroCL DSL提供：
1. decouple algorithm specification from three important types of hardware customization in compute, data type and memory architectures.  
2. capture the interdependence amone these different customization techniques。可以帮助用户explore various performance/area/accuracy trade-offs。  
3. high efficient hardware implementations  （combine different types of hardware customization）  

## 目前hls工具的缺陷：  
1）required to use various vendor-specific data types and pragmas/directives  
2）existing hls programing model cannot capture the interdependence among different hardware optimization techniques(这 weakening the support of user-guided or automatic design space exploration) 比如：no easy way to inform the HLS tool that the shape of an on-chip buffer(depth and number of banks) directly depends on the degree of parallelizaiton  
3）HLS users need to extensively restructure the source program to guide the tool to realize specialized architectures （比如data reuse buffers  和 systolic arrays）  

已经有一些通过DSL来进一步简化accelerator programming。Halide 、 Spark、 TVM  
HeteroCL基于TVM Framework，采用different multi-paradigm programming。在两个方向进行了扩展：  
1）programming model mixed declarative and imperative code  
2）optimization with decoupled algorithm and compute/data customization  
具体的创新如下：  
1）Heterocl DSL decouples algorithm specification from 3个重要的hardware customization：compute、data types、memory architecture。同时做了联合优化，即分析不同类型的hardware customization之间的interdependence，可以实现productive and systematic design space exploration  
2）不仅支持separate algorithm specification from temporal compute schedule。还支持bit-accurate types，支持decouple algorithm and data quantization schemes。可以explore the rich design trade-offs between peformance/area and accuracy  
3）nicely blends declarative symbolic expressions with imperative code  
4）后端支持llvm-code for cpu 和 hls-code for fpga，通过PolySA for systolic arrays and SODA for stencil with dataflow architecture  

Imperative programming is a paradigm of computer programming in which the program describes a sequence of steps that change the state of the computer. Unlike declarative programming, which describes "what" a program should accomplish, imperative programming explicitly tells the computer "how" to accomplish it.  
https://www.computerhope.com/jargon/i/imp-programming.htm  
https://www.computerhope.com/jargon/d/declarprog.htm  

## 为什么选择TVM？  
1）python-based DSL。丰富的productive language features(imtrospection and dynamic type system)  
2）tensor-oriented declarative DSL。（compile and excute the computation graph，利于high-level optimization opportunity in extracting parallelism and maximizing data reuse）  
3）inherit the idea of decoupling algorithm specification from temporal schedule from Halide  
除此之外，HeteroCL在两个方面引入了heterogeneity： in hardware optimization techniques and programming paradigms  

## 接下来就主要介绍3反面的hardware customization：  
1）data type customization  
2）memory customization  
3）compute customization  
除此外还要balance the computation time and the data communication time to maximize the hardware efficiency.  


# 《HeteroHalide: From Image Processing DSL to Efficient FPGA Acceleration》
HeteroCL需要对halide程序进行修改，HeteroHalide要做的是直接将Halide程序转换生成fpga code，如Halide-HLS的工作  
他首先开发一个Halide-to-HeteroCL的code generator   
