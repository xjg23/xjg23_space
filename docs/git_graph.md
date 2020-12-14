# 记录图智能相关方向

https://www.zhihu.com/question/49889826
链接：https://www.zhihu.com/question/49889826/answer/148332420
来源：知乎

OSDI 国内3篇文章 zhuxiaowei 上交chenhaibo 还有zhangmingxing
仅从发表的论文级别看，据我所知，国内有这些研究机构在图处理系统这块做不错：
## 1. 清华大学， 陈文光老师发表的系统GridGraph[1]    Gemini[2]   
[1] Zhu X, Han W, Chen W. GridGraph: Large-Scale Graph Processing on a Single Machine Using 2-Level Hierarchical Partitioning[C]//USENIX Annual Technical Conference. 2015: 375-386.
[2] Zhu X, Chen W, Zheng W, et al. Gemini: A computation-centric distributed graph processing system[C]//12th USENIX Symposium on Operating Systems Design and Implementation (OSDI 16), Savannah, GA. 2016.

清华其他老师的：CUBE[3]    FPGP[4](FPGP是基于FPGA做的图处理框架)
[3]  Zhang M, Wu Y, Chen K, et al. Exploring the hidden dimension in graph processing[C]//12th USENIX Symposium on Operating Systems Design and Implementation (OSDI 16). USENIX Association, 2016: 285-300. 
[4] Dai G, Chi Y, Wang Y, et al. FPGP: Graph Processing Framework on FPGA A Case Study of Breadth-First Search[C]//Proceedings of the 2016 ACM/SIGDA International Symposium on Field-Programmable Gate Arrays. ACM, 2016: 105-110.

## 2.上海交通大学    并行与分布式系统研究所（IPADS）Cyclops[5]  PowerLyra [6]  PowerSwitch[7]
[5]Chen R, Ding X, Wang P, et al. Computation and communication efficient graph processing with distributed immutable view[C]//Proceedings of the 23rd international symposium on High-performance parallel and distributed computing. ACM, 2014: 215-226.
[6]Chen R, Shi J, Chen Y, et al. Powerlyra: Differentiated graph computation and partitioning on skewed graphs[C]//Proceedings of the Tenth European Conference on Computer Systems. ACM, 2015: 1.
[7] Xie C, Chen R, Guan H, et al. Sync or async: Time to fuse for distributed graph-parallel computation[J]. ACM SIGPLAN Notices, 2015, 50(8): 194-204.

## 3. 华中科技大学 袁平鹏老师PathGraph[8]
[8]Yuan P, Zhang W, Xie C, et al. Fast iterative graph computation: A path centric approach[C]// International Conference for High Performance Computing, Networking, Storage and Analysis (SC’14). IEEE, 2014: 401-412. 

好了，我大概就知道这些，至于每个老师有哪些具体的研究方向，很难知道很详细。总之，我认为图计算可能相对其他某些研究方向比较容易入门，但是想做出新东西并不容易。虽然图计算现在很火，但是曾经调研过目前的图系统已经有100多种。
关于研究点，各个系统可能侧重点不一样，有做存储优化，划分优化的，通信优化的等等，但是从整体看都是结合图特点和架构特点优化减少不必要开销，提高计算的速度。具体的建议楼主多看看好的论文，关注一下像PPOPP ，  SIGMOD，ATC，SC等等好的会议相关文章。
最后，安利我们做的基于GPU的图处理Frog: Asynchronous Graph Processing on GPU with Hybrid Coloring Model，可以关注一下，因为国内做基于GPU图处理的研究团队非常之少~。为了不想让我们老师火，所以我并没有在上面放上我们老师的名字，哈哈~



今天搜索了一下，感觉上海交大的IPADS实验室是国内做的最好的，之前以为也许是开放性做的好，但现在看来的确是国内最好，没有之一。
最近他们做了一个Wukong系统，中了OSDI 2016，也有版本支持流式处理。Fast and Concurrent Query Processing on Big (Linked) Data [IPADS]
之前他们还有一部分工作，
DrTM：面向新型硬件架构的内存数据库研究；
Polymer: 基于非均匀访存模型（Non-Uniform Memory Access)的图结构分析框架
PowerLyra: 差异图(Differentiated Graph)计算和划分
PowerSwitch:  图并行计算中的适应性预测和模式转换
Imitator: 大规模图处理中基于副本的容错方法
Cyclops: 支持高效计算与通信的图处理方法
总结的也许不全，可以去看看这个人的主页：Rong Chen (陈榕) [IPADS]他们的所有工作基本都开源，自信+水平的表现吧。

北京大学做了一个Seraph，主要解决了一些并发条件下的查询效率问题。http://net.pku.edu.cn/~xjl/papers/hpdc-xue.pdf
微软开发了Trinity系统，可以通过VS的插件进行二次开发。
Trinity - Microsoft Research
Graph Engine
有一些单位做过偏RDF的工作，跟知识图谱、RDF之类的有关有关：
比如华中科大做了一个TripleBit，
北京大学计算语言实验室和MSRA合作过一个gStore系统，主要通过子图匹配的方式来处理SPARQL查询。

国外的组，我现在看到的：EPFL-LABOS，操作系统实验室Graph Analytics
剑桥和马普所合作的Musketeer团队Musketeer - By CamSaS
伯克利的：LigraLigra 首次提出了图计算

sosp
osdi
系统顶会
