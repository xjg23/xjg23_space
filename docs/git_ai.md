# 记录开源项目和前沿paper   

## 论文目录
https://github.com/qiulinzhang/TopPaper.git
http://redstonewill.com/

## tensorflow源码解析blog
https://www.cnblogs.com/jicanghai/p/9589412.html
https://github.com/tengkz/tensorflow_notes
https://github.com/Yunlong-He/TensorFlowInternals

## 分布式训练做的比较不错的framework
uber的https://github.com/horovod/horovod
  
## 腾讯TNN  
https://github.com/Tencent/TNN   
https://zhuanlan.zhihu.com/p/147028361   
  
## 腾讯NCNN   
https://github.com/Tencent/ncnn   
  
## AI用于视频处理和理解   
1. AI视频插帧   
《Depth-Aware Video Frame Interpolation》 cvpr2019   
https://github.com/baowenbo/DAIN   
https://sites.google.com/view/wenbobao/dain   
  
《AdaCoF: Adaptive Collaboration of Flows for Video Frame Interpolation》cvpr2020   
https://github.com/HyeongminLEE/AdaCoF-pytorch   
https://www.groundai.com/project/adacof-adaptive-collaboration-of-flows-for-video-frame-interpolation/   
  
《Blurry Video Frame Interpolation》  
https://github.com/laomao0/BIN   
https://www.groundai.com/project/blurry-video-frame-interpolation/   
https://zhuanlan.zhihu.com/p/117237115   
  
《edsc multiple video frame interpolation via 。。。》新paper，效果比上面的AdaCoF和DAIN网络好   
  
《Zooming Slow-Mo:  Fast and Accurate One-Stage Space-Time Video Super-Resolution》  
https://www.cnblogs.com/wujianming-110117/p/12573719.html   
论文链接：https://arxiv.org/pdf/2002.11616.pdf   
The source code is released in：https://github.com/Mukosame/ZoomingSlowMo-CVPR-2020   
  
## AI用于视频目标分割
DAVIS Challenge on Video Object Segmentation 2020
https://davischallenge.org/challenge2020/publications.html


## Reinforcement Learning 
http://karpathy.github.io/2016/05/31/rl/
This is a long overdue blog post on Reinforcement Learning (RL). RL is hot! You may have noticed that computers can now automatically learn to play ATARI games (from raw game pixels!), they are beating world champions at Go, simulated quadrupeds are learning to run and leap, and robots are learning how to perform complex manipulation tasks that defy explicit programming. It turns out that all of these advances fall under the umbrella of RL research. I also became interested in RL myself over the last ~year: I worked through Richard Sutton’s book, read through David Silver’s course, watched John Schulmann’s lectures, wrote an RL library in Javascript, over the summer interned at DeepMind working in the DeepRL group, and most recently pitched in a little with the design/development of OpenAI Gym, a new RL benchmarking toolkit. So I’ve certainly been on this funwagon for at least a year but until now I haven’t gotten around to writing up a short post on why RL is a big deal, what it’s about, how it all developed and where it might be going.
[Richard Sutton’s book]: https://webdocs.cs.ualberta.ca/~sutton/book/the-book.html
[David Silver’s cours]: http://www0.cs.ucl.ac.uk/staff/d.silver/web/Teaching.html
[John Schulmann’s lectures]: https://www.youtube.com/watch?v=oPGVsoBonLM


## 关于量化与模型压缩(待整理)
https://github.com/Xilinx/graffitist
《TRAINEDQUANTIZATIONTHRESHOLDS FORACCURATE ANDEFFICIENTFIXED-POINTINFERENCE OFDEEPNEURALNETWORKS》
本文是xilinx的4bit量化工具和paper

## 关于pybind11
https://github.com/tensorflow/community/blob/master/rfcs/20190208-pybind11.md#replace-swig-with-pybind11

## 关于convolution layer 和 deconvolution layer的可视化项目
https://github.com/vdumoulin/conv_arithmetic
https://blog.csdn.net/u013139259/article/details/53318477
https://arxiv.org/ftp/arxiv/papers/1609/1609.07009.pdf
https://arxiv.org/pdf/1603.07285.pdf
https://medium.com/@_init_/an-illustrated-explanation-of-performing-2d-convolutions-using-matrix-multiplications-1e8de8cd2544
https://cs231n.github.io/convolutional-networks/#conv

## ai compiler
1.在华为的片子上围绕计算密集算子codegen以及计算子图codegen做过比较专的工作，这是很好的亮点，讨论了跨 convolution的计算密集算子fusion，能够给出清晰的细节描述，比如在N的维度进行fusion，以及在H或W维度的fusion，这里涉及到一些比较精细的细节，回答是让我满意的。也讨论了计算子图fusion&codegen的细节，能够从底层的loop层次结构的融合变换给出比较清晰且符合问题本质的描述，这个让我满意 。
2.对领域里的最新的技术进展的关注感觉不够系统，让我有些担心如果脱离了自有芯片的加成，在成熟硬件上做，是不是能够获得类似的效果。比如他们在升腾芯片上推进过类似auto-schedule的工作，也提到了遇到的挑战，但对于领域里最新的工作，比如Halide和FlexTensor的工作，只知道大概概念，没有关注里面的细节，给我的回答是他认为这些research工作不work，对他们没太大参考价值，这让我有些意外，认为其技术思维开放度有提升的空间。
3.对于自己负责工作之外的AI技术方向的关注稍微少了一些，比如一些跟他的方向直接相关的内容，包括MindSpore里ME的部分，以及GE里分布式策略的部分关注比较有限，做算子编译的架构对这些方面如果能够有关注会更佳。（注：ME指mind expression，即前端表示层 GE指graph engineGE专门负责和Ascend芯片交互）

## 广慈在intel做的lib 对标MKL
https://github.com/intel/deep-learning-math-kernel-research
