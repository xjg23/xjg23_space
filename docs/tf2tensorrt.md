# tf2tensorrt 学习  
  
## source code  
https://github.com/tensorflow/tensorflow/tree/master/tensorflow/compiler/tf2tensorrt  
https://github.com/tensorflow/tensorflow/tree/master/tensorflow/python/compiler/tensorrt  

https://github.com/NVIDIA/TensorRT

## doc  
Nvidia关于tf2tensorrt的介绍
https://developer.nvidia.com/blog/tensorrt-integration-speeds-tensorflow-inference/  
https://medium.com/tensorflow/high-performance-inference-with-tensorrt-integration-c4d78795fbfe
https://blog.tensorflow.org/2019/06/high-performance-inference-with-TensorRT.html
上述2篇官方blog详细介绍了 tftrt的详细流程

https://developer.nvidia.com/blog/speeding-up-deep-learning-inference-using-tensorrt/
https://sayak.dev/tf.keras/tensorrt/tensorflow/2020/07/01/accelerated-inference-trt.html
https://developer.nvidia.com/tensorrt
https://docs.nvidia.com/deeplearning/tensorrt/developer-guide/index.html

TF-TRT
This method accelerates a TensorFlow graph with TensorRT even if there are TensorFlow operators in the graph that are not supported by TensorRT (or TF-TRT). The subgraphs that are supported by TensorRT and TF-TRT are accelerated and the resulting graph is still a TensorFlow graph that you can execute as usual. For step-by-step instructions on how to accelerate inference in TF-TRT, see the TF-TRT User Guide. For TF-TRT examples, see Examples for TensorRT in TensorFlow (TF-TRT).

TF-TRT examples: https://github.com/tensorflow/tensorrt
TF-TRT User Guide: https://docs.nvidia.com/deeplearning/frameworks/tf-trt-user-guide/index.html

