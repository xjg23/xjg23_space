# walk-through  
  
本周从两个方向开始，首先按部就班 从前端开始 选择一个模型 ，同时学习tvm的代码结构，看walk-through文档  
1）   
第一步：  
或许和很多人不同，以我的经验来看，觉得理解TVM，或者推理框架一定要从前端开始。即你从一个Tensorflow模型 / MXNet模型等，是如何转为NNVM的，然后再应该是后续的图优化，以及后续的TVM Tensor，LLVM代码生成等东西。  
  
为什么我会这么强调从前端开始呢？因为不理解前端模型，就很难理解后续TVM为什么是这样，而且出了错以后很难知道到底是什么原因，比如很多时候找了半天，其实只是你忘记了模型输入图片的预处理，却误认为是后续卷积的调度优化做的有问题，所以我强烈建议先从一个模型前端开始，在tvm/nnvm/frontend里面选取一个前端。而选取前端开始不应该仅仅是看，Bug / 需求驱动永远是最好学习源代码的方式，建议从一个固化好的模型开始，然后补足NNVM算子，比如Mobilenet / Resnet50等，这里也是让你熟悉工具，熟悉NNVM的开始，可能会遇到很多问题，但是一个一个克服会收获很多，这里面推荐一个看模型的好工具: https://github.com/lutzroeder/Netron 我也是看苹果公司一个人用了以后发现的，确实是好东西。  
  
首先跑nnvm tutorial：  
前端：  
https://github.com/dmlc/tvm/blob/master/nnvm/python/nnvm/frontend/tensorflow.py  
https://github.com/dmlc/tvm/blob/master/nnvm/tutorials/from_tensorflow.py  
  
然后跑最新的relay tutorial  
前端：https://github.com/dmlc/tvm/blob/master/python/tvm/relay/frontend/tensorflow.py  
https://docs.tvm.ai/tutorials/frontend/from_tensorflow.html  
https://github.com/dmlc/tvm/blob/master/tutorials/frontend/from_tensorflow.py  
https://github.com/dmlc/tvm/blob/master/docs/frontend/tensorflow.md  
  
2）tvm code walk-through  
https://docs.tvm.ai/dev/codebase_walkthrough.html  
