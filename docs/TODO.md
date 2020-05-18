
## 0. 每天做LeetCode  

## 1.  supertile，convolution  
本周完成，写乘法矩阵的工程，仿真，综合，最好搭一个简单的工程，连上dma ipu 、pe ipu、驱动和dpdk上层来做测试。  

### 1.1 周末看异步fifo设计文档（bitmain）  
### 1.2 cnn eyeriss设计  
### 1.3 gemm并行度  

## 2. 笔记记录已做项目，把整体框架、数据流详细的描述记录下来  
    需要从现有项目汲取的经验：  
### 2.1 fpga进docker，多docker共享fpga  
### 2.2 fpga api的标准化、参数化的封装（为了使得一套api适配多个业务）  
    https://yuque.antfin-inc.com/alipay-fpga/gkg6qi/qgsm68  
    可以比较lstm和dnn两个项目目前的api有哪些共同和独立的地方。  
### 2.3 同时思考apu的通用化，使得通用编译器可以在上面使用。  
 
## 3. pcie dma、驱动、ddr-mig  
比较aliyun/aws（xilinx）内核驱动、软件守护进程、硬件守护进程方案的设计  
pciemem.c  
Downloads/01-Heterogeneous Computing & Architecture/FPGA/00--FaaS  

## 4. 每周两篇数学博客、每天一个编程训练题  

## 5. risc-v + nvdla  

## 6. nvdla on fpga  
http://nvdla.org/primer.html  
https://github.com/nvdla/hw/issues/110  

nvdla virtual platform  
https://github.com/nvdla/vp  
http://nvdla.org/vp.html  
http://nvdla.org/vp_fpga.html  

## 7. 多进程线程、高并发  

## 8. 看体系结构书籍  

## 9. apu设计细节（看代码）  
