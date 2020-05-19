# TVM全面学习knickoff  

## 目标：可以为TVM更好的支持FPGA后端commit代码  
  
## 实施方法：用1个月时间每天坚持学习TVM，学习tvm使用（tutorial可以帮助了解tvm能干嘛），学习tvm代码（掌握tvm的内部原理）  
结合对比tvm的变种、扩展（包括woodpecker）  
深入学习halide及其变种  
xla、mlir、tensor comprehensions、facebook glow、Intel NGraph, Nvidia TensorRT、MIT  Tiramisu、PlaidML  
onnx、nnef、NVDLA开源编译器  
  
## 好的课程：  
CS217 of Stanford，Hardware/Software Co-Optimization for Machine Learning；唐杉 公众号StarryHeavensAbove有讲义推荐https://zhuanlan.zhihu.com/p/51791683  
华盛顿大学关于硬件加速的课程https://courses.cs.washington.edu/courses/cse599s/18sp/  
chrome-extension://oemmndcbldboiebfnladdacbdfmadadm/https://dlsys.cs.washington.edu/pdf/lecture7.pdf  
  
## TVM知乎专栏：  
https://zhuanlan.zhihu.com/tvmai  
专栏会对每个月的tvm commit进行汇总总结  
  
TVM是一个宝库!!!!可以学习很多东西，上到模型编译优化下到硬件（runtime、hls、chisel等）  
  
这个是阿里alios部门的吴钊（2018.4加入 P7）  
技术预调研NNVM/TVM等编译优化思想的深度学习框架，并成功推动基于编译优化技术的深度学习Inference框架TVM在Ali OS智能汽车系统中的应用  
让NNVM支持Tensorflow / CoreML等模型文件，包括但不限于MobileNet / Resnet50 / SSD-MobileNet / DeepLab等  
针对Ali OS硬件平台，针对业务场景模型进行针对性的调优，如对相关模型Schedule调度优化，如Resnet50，在ARM CPU提速3X。  
针对TVM，实现Tensorflow Quantization-Aware Training的INT8量化的支持，并能成功解析TFLite量化模型，并针对INT8量化模型进行调优，在ARM CPU上，某些业务模性能上领先TFLite 3.2X.  
针对TVM实现Hexagon DSP支持，在TVM中添加LLVM CodeGen Hexagon后端，实现Hexagon相关硬件指令，如vadd / vavg等HVX指令，并支持计算函数Offload到Hexagon DSP中。  
  
作者：蓝色  
链接：https://www.zhihu.com/question/268423574/answer/506008668  
来源：知乎  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。  
  
或许和很多人不同，以我的经验来看，觉得理解TVM，或者推理框架一定要从前端开始。即你从一个Tensorflow模型 / MXNet模型等，是如何转为NNVM的，然后再应该是后续的图优化，以及后续的TVM Tensor，LLVM代码生成等东西。  
  
为什么我会这么强调从前端开始呢？因为不理解前端模型，就很难理解后续TVM为什么是这样，而且出了错以后很难知道到底是什么原因，比如很多时候找了半天，其实只是你忘记了模型输入图片的预处理，却误认为是后续卷积的调度优化做的有问题，所以我强烈建议先从一个模型前端开始，在tvm/nnvm/frontend里面选取一个前端。而选取前端开始不应该仅仅是看，Bug / 需求驱动永远是最好学习源代码的方式，建议从一个固化好的模型开始，然后补足NNVM算子，比如Mobilenet / Resnet50等，这里也是让你熟悉工具，熟悉NNVM的开始，可能会遇到很多问题，但是一个一个克服会收获很多，这里面推荐一个看模型的好工具: https://github.com/lutzroeder/Netron 我也是看苹果公司一个人用了以后发现的，确实是好东西。  
  
接下来你应该首先理解TOPI，这是架设在NNVM与TVM之间的东西(首先忽略图优化，你后面再去看)，因为你需要理解NNVM Symbol (其它模型在转为NNVM前端表示时会以Symbol形式的Api表示) 如何与TVM之间是如何连接起来的，在这里面你会有点迷糊，因为TVM是C++和Python混合的工程，这里面你需要在这两者跳来跳去，但是你这一步你最重要的是抓住两个核心: FTVMCompute (@reg.register_compute) / @reg.register_schedule，这一个你需要分别在nnvm/top里面的C++ / Python去找，top里面会告诉你是如何从NNVM进入topi的。  
  
这一步完成以后，你则需要进入topi里面的任意一个后端Target去看，我暂时推荐x86后端，因为这一个后端还没有被AutoTVM改造。对于你来说，理解起来更容易。在这里你会遇到topi/nn里面的@tvm.target.generic_func到类似具体@generic.schedule_conv2d_nchw.register(["cpu"])的改变，这是TVM的核心所在，对于卷积这样的数据负载处理，为了优化而沿用Halide的思想: 计算与调度分离。为了理解这个，你最好参考一下这个文档: https://docs.tvm.ai/tutorials/optimize/opt_gemm.html#sphx-glr-tutorials-optimize-opt-gemm-py  
  
到这一步理解好以后，后续的TVM底层API大部分情况下你都不需要去动，包括后续的LLVM自动生成，优化等你也大部分不需要去动，因为类似CNN这样的网络，大部分你要做的工作就是在调度上，如何减少Cache Miss ，如何更好的让数据Locality是更关键的地方。  
  
到这一步以后，你可以再回过头去理解图优化的部分，如Operator Fusion / FoldScaleAxis等，以及包括TVM目前最核心最与众不同的地方: AutoTVM(https://docs.tvm.ai/tutorials/autotvm/tune_nnvm_arm.html#sphx-glr-tutorials-autotvm-tune-nnvm-arm-py)，这是TVM去击败NCNN等用手写汇编的推理框架的关键一环，用机器学习去解决机器学习的问题，让你从调度参数的设置中解放出来，而专心写调度算法。这里面目前ARM CPU的调度算法并非是最优的，但是从测试来看，至少在测试中使用硬件和环境来看，已经超过能找到的推理框架。后续我将撰写一篇文章到TVM社区，将我在ARM CPU的工作写出来，这将改善目前ARM CPU的官方调度版本，这将在Mobilenet等模型中有很好的提升，敬请关注！  
  
https://tvm.ai/2018/01/16/opt-mali-gpu  
  
TVM是很好的一个项目，这种基于编译优化思想的深度学习推理框架正是我赞同的，虽然还有很多工作需要做，但是我认为它已经走在一个很好的方向上了。  
  
=====================================================================  
  
手把手带你遨游TVM  
  
手把手带你遨游TVM  
蓝色  
蓝色  
C++、编程语言、编程 等 4 个话题的优秀回答者  
已关注  
小乖他爹  
、  
陈天奇  
等 431 人赞同了该文章  
人工智能无疑是目前风口浪尖的话题，大部分提到人工智能都关注在了算法，然而若要让人工智能落脚在实际应用中，工程化是至关重要的。  
  
让我们再细化一点这个问题，我们目前要让一个算法落地下来，或者说我们要产生一个模型，然后部署到目标设备上进行运行。我们需要分两步：Training + Inference，目前对于Training来说，比较流行的是TensorFlow，PyTorch等，市场主流框架基本上已经确定下来了。而对于Inference来说，以我之所见，其实是“群雄逐鹿”，因为模型Training一次，但是会跑到的设备可能会是多种多样的，如Intel CPU / Intel GPU / ARM CPU / ARM GPU / NV GPU / FPGA / AI芯片等，而要在这多种多样的设备中都保持一个高效的Inference性能，其实是一件很有挑战的事情，也是作为程序员很喜欢的一件事情，知难而上，挑战难题达到颅内高潮的那种感觉也不是任何一件事情能达到的。  
  
让我们图例化这一点：  
  
其实要达到这一个目标并不容易，各种硬件设备的特性千差万别，要如何保持一个统一的高效执行，是一个非常难做到的事情。而各大硬件厂商针对这样的情况都推出了自己的Inference 框架（相比TensorFlow等这样的框架孱弱的Inference性能，各大设备厂商的Inference框架性能都比较不错），比如Intel的OpenVINO，ARM的ARM NN，NV的TensorRT等，但是这里面有一个问题，各大设备厂商的框架并不具备通用性，比如对训练框架模型产生的算子支持不全（尤其是像TensorFlow这种算子很多的），通常在一个设备厂商的Inference框架能跑，但是不一定在另外一个设备厂商的Inference框架上能跑。同时，对于业务开发来说也是非常痛苦的事情，我在这个硬件上要用这个，我在另外一个硬件上要用另外一个，而且两者还没有统一的使用体验，算子支持也不一样，性能还不一定是最好的...其实对于业务方来说，也是想要一个统一的Inference框架，然后我业务场景的各种硬件设备都能高效的跑，使用体验都是一致的，我只要换一个device_target参数就好了。  
  
以我之所见，其实我们并不是第一次遇到这样的问题，我们曾经出现了很多种编程语言，有很多种硬件，历史上最开始也是一种语言对应一种硬件，从而造成编译器的维护困难与爆炸。  
  
而编译器后面解决了这个问题，其具体解决办法是这样的：抽象出编译器前端，编译器中端，编译器后端等概念，引入IR (Intermediate Representation)  
  
编译器前端：接收C / C++ / Fortran等不同语言，进行代码生成，吐出IR  
编译器中端：接收IR，进行不同编译器后端可以共享的优化，如常量替换，死代码消除，循环优化等，吐出优化后的IR  
编译器后端：接收优化后的IR，进行不同硬件的平台相关优化与硬件指令生成，吐出目标文件  
类似这样的架构：  
  
其实对于Inference框架也是类似的道理，我们也想要得到类似的架构：  
  
我们把各种模型抽象看成各种编程语言，于是我们引入一个新的编译器，负责把这些编程语言识别，吐出IR  
  
接下来我们就可以对这种中间的IR进行优化，而深度学习中是计算图，所以我们可以称为Graph IR  
  
于是，我们得到这样的架构：  
  
这就是我们想要解决的问题了。所以，就来到我们今天的重点了，我们能不能做一个基于编译优化思想的推理框架呢？答案就是：TVM (https://tvm.ai/).  
  
让我们给出一副更详尽，更漂亮的一张图：  
  
这就是TVM官方给的架构图。在我们图中的CPU目标是通过什么来做到的呢？LLVM。当然，也包括了AMD GPU，也是LLVM来做到的，但是这张图里面没有列举出来。在这张图里面，对于NV GPU的支持是产生CUDA，但是从我的角度来看，其实也是可以产生NVVM的，然后走LLVM的路线。  
  
TVM基本上就是基于编译优化思想的深度学习推理框架的完美体现，自从加入了AutoTVM(https://arxiv.org/pdf/1805.08166.pdf)机制以后，可以用一个词来形容，就是如虎添翼，击败NCNN等（https://github.com/Tencent/ncnn）框架是没有任何问题的，可参考这篇文章的对比：Automatic Kernel Optimization for Deep Learning on All Hardware Platforms，并且这里的性能还没有应用上我这个PR：  
  
[ARM][Performance] Improve ARM CPU depthwise convolution performance by FrozenGene · Pull Request #2345 · dmlc/tvm  
  
我的这个PR可以将深度卷积的性能提高近2倍。  
  
而AutoTVM的存在最厉害的是具有非常强的适应性，很多Inference框架在一些标准模型上表现的很好，但是一遇到业务模型就性能急剧下降，比如来个257 * 513这种输入，但是AutoTVM不会存在这个问题。若有后续，我会来讲AutoTVM到底完成了什么样的事情。  
  
然而TVM的代码并不容易阅读，比如今天在TVM论坛看到的：  
  
即使学习了两个月，他都觉得一顿混沌。所以，我想以我的角度来带大家手把手遨游一下。  
  
下一篇时间：未定 （毕竟我经常挖坑而不填坑，或者长时间以后才来填坑）  
  
=====================================================================  
  
如何看待Tensor Comprehensions？与TVM有何异同？  
  
https://www.zhihu.com/question/267167829  
  
贾扬清  
贾扬清  
深度学习（Deep Learning）、机器学习 话题的优秀回答者  
陈天奇  
等 120 人赞同了该回答  
主要的区别在于如何进行计算的scheduling。将数学表达和计算顺序分开的想法由来已久，最近几年里较早的工作是Halide。TVM和TC都在一定程度上使用了Halide的中间表达（intermediate representation）。  
  
Halide最初的设计是为了计算图形学而设计的，TVM和TC都在此基础上加强了对于深度学习的支持。  
  
两者的不同在于TVM比较注重对于不同后端的coverage，而在优化上延续了Halide的想法，也就是简化计算顺序的建模，但是依然比较强地借助手工建模来加速；TC目前注重实用多面体优化（polyhedral optimization）来进行自动的计算顺序搜索，这样不需要手工建模，对于简化科研人员的工作很有帮助。目前TC支持的后端较少，主要注重CUDA，也在进一步支持CPU，因为这是工程领域目前最重要的两个平台。  
  
Polyhedral optimization本身是一个很大的研究方向，如何对于硬件的建模，然后如何实现寻优，这都是目前没有完全解决的问题。在一些复杂的情况下，寻优的结果往往不如手工的结果来得高效。如何提高寻优的效果非常值得研究。在这个方向上法国的Inria团队建树颇深，这次我们FB的工作也是和他们合作的。  
  
另外广告一下，Halide的原作者Andrew Adams也在Facebook。  
  
如果你对深度学习的计算优化有经验，然后有兴趣和这些大牛一起工作的话，欢迎给我发邮件 me@daggerfs.com 。  
编辑于 2018-02-15  
  
陈天奇  
CS. PhD 机器学习系统  
SIY.Z  
 等 105 人赞同了该回答  
目前的主要的差别在于代码生成技术路线上，TC采用了polyhedra model，目前TVM采用的还是schedule space模型。polyhedra model相对于schedule primitive更加自动化一些，在TVM过去的工作中我们只采用了比较简单的auto tuning，这一点是TVM未来可以向TC学习的地方。在性能上，就目前发布的结果来看TVM的技术路线还是有更好的性能，如何互相学习提高是未来TVM团队会努力的方向  
  
TVM目前的主要关注点在后端支持以及在如何获得最好的性能，最近的新东西是如何对未来深度学习加速器的支持，有兴趣的同学可以看我们刚出来的论文 End-to-End Optimization Stack for Deep Learning 。TVM采取这一路线以达到最好的性能，并且进一步支持深度学习的加速器。  
以上的评论适用于是对于两个项目当前状况。TC (tensor comprehension) 在早期内部开发的时候参考了TVM的设计。主要作者nicholas也参与了TVM的贡献。两个项目的技术路线不同，在一定程度上是互补的，未来相信会有更多有趣的东西出现。  
  
总的来说自动生成高效代码这条技术路线的可行性随着大家的努力逐渐明朗，大家应该可以多来尝试使用交流。去年TVM在arm，mobile gpu和加速器都有一些结果，开源社区的同学也都找到了不错的去处，这个方向还有不少的东西可以研究，欢迎对深度学习系统和编译高性能计算感兴趣的同学联系我们参与一起来探索这个方向。  
  
编辑于 2018-02-15  

阿里巴巴PAI团队穆琢  
  
杨军  
深度学习（Deep Learning）、机器学习 话题的优秀回答者  
陈天奇  
等 73 人赞同了该回答  
最近在开展的一些项目里既有用到XLA，也有用到TVM，也有过一些思考，看到了TC的工作，还是有几分心有戚戚的感觉。从我所关注的角度补充一些内容供大家参考讨论吧。  
  
Deep Learning的coarse-level的建模特性，让建模同学可以把更多精力从底层的特征工程转移到模型结构的设计上，随着建模知识的越来越普及，计算力的进一步增强，以及模型分析手段和调试工具的进一步完善，DL建模工作未来会更像经典的programming task我觉得并不应该惊讶，虽然目前确实还有一段距离。  
  
模型结构的演化灵活性，总会带来上层workload与底层计算设备的性能gap的问题，这个gap目前来看不太可能靠硬件厂商提供的library来彻底解决，原因也很简单，因为这个链路太长。无论是单机还是分布式执行，都会存在这个gap，这个gap的存在本质上是浪费计算效率的，这个效率的优化就是一个可以通过中间层软件（compiler）或是手工优化来完成的。  
  
TVM、 TC实际上都是期望通过引入一种比较principal的策略来解决上层workload与底层计算设备的高效mapping的手段，解放或减少手工优化的负担。如果透过计算机行业的发展历史来看，这也正是compiler要做的工作。Google在研发XLA的时候，一开始是为了TPU服务，后来意外发现某些优化特性对于GPU和CPU也适用，算是类似的考虑（比如把大量小op做fusion以及根据具体shape信息做specialization优化）。只不过，XLA在GPU上的性能表现方差较大，并且存在一些坑和bug就是另外的story了，那是个实现细节的问题，倒不算是设计层面的问题。  
  
优化问题按照出现频率实际上可以分为两大类，一类是long-tail的问题，出现频率不高，existing library的支持力度往往不够，通常对应于实验性的model结构(比如TensorRT或是cuDNN对于像Transformer这些比较新的模型的支持不够）；另一类是高频问题，出现频率足够高，比如经典卷积和sequential model。对于两类问题的优化手段也有所区别，高频问题，其实手工优化会更划算，因为本质上来说，机器优化的code的性能上界是手工优化（这个观点可能引起分歧，我先不展开），但是不能scale，而long-tail的问题，就是XLA、TVM或是TC适合解的问题了。  
  
XLA解决的路子是引入一个HLO IR将计算op映射到这个HLO IR上，进行graph优化之后，再通过LLVM backend完成各个device上target code的生成。图优化层面下面的高效kernel的撰写实际上是依赖于工程师的手工优化的，只不过使用的语言从上层CUDA C变成了HLO IR。  
  
TVM将图优化层面之下的计算kernel的撰写的负担进行了简化，这是相较于XLA不小的一个改进，我们在真实的应用场景中在完成了TVM的学习曲线的适应之后，也确实发现通过TVM可以快速高效地完成计算kernel的批量生成，虽然有时候代码量并不一定少，但撰写的负担实际上是减轻了很多。这也是我们比较喜欢，并开始严肃考虑将更多工作基于TVM展开的一个motivation了。  
  
TC的论文我go through了一下，跟TVM想解决的问题是一样的，不过在具体手段上有所区别，看起来TC希望进一步简化用户的撰写负担，但从我们目前了解到的经验来看，Polyhedral的方法虽然很优雅，但在生成高效代码上，很多时候，未必比看起来ad-hoc的手工规则驱动的方法更好，甚至还会有性能不逮的时候。但这通常是针对经典通用编译器而言的，对于Deep Learning这样一个将计算语义缩减至相对窄的scope的场景，基于Polyhedral的方法是不是可以进一步缩小跟手工规则驱动的方法的差异，我觉得是值得期待的。  
  
针对深度学习的Compiler是一个很有趣的inter-discipline领域，既需要经典编译器技术的背景，也需要对上层DL workload的理解和认识，还需要对异构计算的优化技术有好的sense，这两年也在不断出现新的工作进展(比较有代表性的XLA、TVM、DLVM、还有现在的TC等等)，与之相对应的是底层计算硬件也出现了大量的变化和可能性，这就使得DL compiler的重要性变得更加突显。我倾向于认为未来还会有一段时间在这个领域出现更多结合上层workload导向的针对Deep Learning workload的compiler技术的创新进展，而且个工作最好的发源地是在拥有多样化业务场景的大公司里，因为有足够复杂多变的问题需要去解决，阿里也在这个方面有着专注的投入，有兴趣的同学欢迎联系我们，可以直接邮件我muzhuo.yj@alibaba-inc.com，想了解招聘细节信息可以参见这里：  
  
阿里PAI团队大规模算法组--Deep Learning团队招聘  
  
要术甲杰  
找不到来时的路  
李博杰  
、  
袁进辉  
等 49 人赞同了该回答  
前面几位大牛对Tensor Comprehensions（TC）和TVM之间的的异同进行了回答， 我对前面°±是在这上面做自动变换 。TVM据说是对一些IR node类型进行了扩展。  
两者都是在把DL 应用转化成HPC代码的过程中实现了并行性和局部性优化，TVM是通过schedule指令向用户提供schedule的接口，让用户指定把计算如何映射到硬件上，以此来保证并行，同时也提供了做tiling的schedule指令，满足挖掘局部性的要求。例如图3里面，首先通过split把tensor加运算的（隐藏）循环层做一个strip-ming操作，然后再用bind命令把strip-mine之后的循环层对应到GPU的线程块和线程物理结构。TC这些映射以及各种循环变化等都是在polyhedral model上直接自动完成，从图4可以看出TC里面给出计算定义之后就通过tc.compile把这个计算交给后面的编译程序了。  
两者都使用了tuning来寻优，前者是auto-tuning，后者使用了machine learning。这个在图里面都没有标出，可以看两者的论文描述。  
二. TVM和TC的不同点  
  
现在整个TVM框架是由图层优化的nnvm和算子层优化的tvm两部分构成。为了区分，我把算子层面的用tvm表示。  
  
整体架构的区别。TC不存在图层优化编译，而TVM是“图层+算子层”两部分。这个从图1和图2中就可以看出。  
实现的优化不同。TVM是在nnvm层上进行fusion和data layout优化，剩下的mapping和tiling等各种循环优化都通过tvm的schedule指令来实现。TC不存在图层，没有实现data layout优化，但是TC将算子打开之后可以实现算子层面的fusion，包括其它循环优化都是交给polyhedral model来自动实现。  
TVM的DSL中不仅支持描述算子的计算，还支持输入/输出tensor定义，也就是说到了算子层面的tvm，用户完全可以不依靠DL framework就可以写出tvm的输入。图3里面看到A、B和C等tensor都是通过tvm定义的。TC的DSL中仅支持计算描述，输入/输出tensor是在DL framework中定义，如图4里面，A和B这两个tensor是通过pytorch定义的而不是TC。TC的一个算子计算描述中所有的tensor都必须要么是输入要么是输出，不能作为临时数据。这也是TC为什么目前没有实现data layout优化的一个原因吧。  
TVM的schedule是通过指令用户手工指定，而TC在前面的DSL描述完计算之后就完全交给后面的编译程序来实现schedule的自动变换，这也是TVM和TC最大的区别。这个前面几位都已经提到了。  
TVM中输出tensor的shape是在计算描述的过程当中指定的，在图3里面，计算C这个tensor的时候需要给定shape，也就是A.shape这个参数。而TC输出tensor的size是根据输入tensor的size还有DSL的计算描述推断出来的，图4里面并没有C的shape相关描述。  
TC和TVM我都安装使用了，通过实际使用发现TVM的安装过程比较舒适，按照网站上给出的步骤一步一步执行就可以了。TC的安装，槽点很多，最开始的时候TC提供了conda安装、源代码编译安装以及镜像安装等几种方式，现在只剩下conda安装了。感觉TC的documentation做得不好，而且更新也不够及时，经常在安装过程中因为pytorch、python等版本问题配置/编译出错，更新不够及时。  
以上就是我在使用过程中发现的TC和TVM的异同，如果是想使用TC和TVM的话，这个回答到看到这里应该就可以结束了。下面说说在使用TVM和TC的过程中我的一点思考，写下来和大家探讨探讨。  
  
三. TVM vs. TC  
  
首先来看面向的用户群。  
  
TC和TVM最大的区别在于schedule部分。也就是说，TC把TVM里面的schedule部分用polyhedral model实现了，这在一定程度上减缓了用户的压力。我认为这个区别导致了TC和TVM面向的用户群是不一样的。TVM向用户提供了各种schedule指令，这就要求用户需要对底层硬件比较了解，知道如何对隐藏的循环进行各种变换和映射等。所以，在DL和HPC之间，我认为TVM更适合HPC领域的人员使用，他们熟悉底层硬件的知识，躆第二阶段优化的挑战，这也是这些编译器出彩的地方，我们在下一个要点里讨论第二阶段优化。对第一阶段优化来说，XLA做的相当全面了，可能是最全面的。  
  
2，剑宗还是气宗？在特定体系结构上自动生成最优代码，可以看出有俩套路，一个套路可以称之为剑宗，也好似一种自底向上的办法，即把专家手工优化代码的经验提炼出来，形成一些粗线条的rule, 这是TVM的路线，也就是来自Halide的思路，那些rule称为schedule，Halide的最重要贡献是提出了问题表示方法，但没有解决自动化这个问题，当然自动化问题很困难。还有一个套路可称之为气宗，寻求一种高层次的数学抽象来描述和求解代码生成问题，这个代表就是TC, Tiramisu, MLIR等依赖的Polyhedral 方法。  
  
关于多面体方法，我简要说说自己的理解。  
  
深度学习编译器和传统编译器技术很不相同，它只解决一类特定问题，不去解决控制流问题，基本上是解决多重循环优化，也就是稠密计算问题。  
  
Polyhedral method 是一种对多重循环程序的表示方法，问题表示出来之后，并不一定要借助isl求解。isl是什么？对一个比较复杂的cost model, 一个polyhedral 表示的计算，生成什么样的代码最优？这是一个离散解空间上的组合优化问题，有时可描述成整数线性规划，isl (integer set library)就是来求解这个问题的一个开源库。像TC， Tiramisu 用了isl, PlaidML和MLIR仅仅用了多面体表示却没有借助isl, 猜测：问题搜索空间太大时，isl 也不行。多面体方法只解决表示问题，不解决自动化问题。  
  
用多面体与否实际上和前端是否用DSL也有关，用Polyhedral 的都用DSL, 表明多面体的表达能力和能求解的问题范围非常广，用DSL但不用Polyhedral 也有，譬如Halide, TVM, Tiramisu 作者对Halide表达能力有所批评，需要注意的是， Halide和Tiramisu 作者们其实是同一位MIT教授的学生，这是自己对自己的批评。  
  
我深深的相信polyhedral 的未来，是近些年发展出来的最优雅的抽象方法。如果感兴趣什么是polyhedral method 建议关注 ﻿@要术甲杰﻿ ，他博士毕业于该方法的策源地。Halide出现后，就有人把它扩展到polyhedral求解，那个工作叫PolyMage, 据说现在华为有人在为TVM添加Polyhedral支持，拭目以待。  
  
未来真正的方案可能是剑宗和气宗结合，bottom up 经验有助于缩小搜索空间。PlaidML和Tiramisu 这方面做得很好。  
  
目前编译器技术，主要是解决单芯片上性能优化，可以计算训练或推理，现在这方面还大量依靠专家手工优化代码，完全自动生成的代码还没办法超过专家手工优化的代码，希望这一天早日到来。  
  
深度学习编译器是专门来优化多重循环的技术（我称之为多重循环是过分简化了，但更容易理解），当然也有MIT学者去搞了稀疏运算的编译技术，好像叫Taco。  
  
好想组织一个学习班，大家一块儿学习进步。  
