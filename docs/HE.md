# HE 
  
## HE for AI
intel 
《nGraph-HE: A Graph Compiler for DeepLearning on Homomorphically Encrypted Data》

microsoft 
《CrypTFlow: Secure TensorFlow Inference》
《CHET- Compiler and Runtime for Homomorphic Evaluation of Tensor Programs》
《EzPC- Programmable, Efficient, and Scalable Secure Two-Party Computation for Machine Learning》
https://github.com/mpc-msri/EzPC
https://www.microsoft.com/en-us/research/project/ezpc-easy-secure-multi-party-computation/
https://pratik-bhatu.medium.com/privacy-preserving-machine-learning-for-healthcare-using-cryptflow-cc6c379fbab7
《EzPC- Programmable, Efficient, and Scalable Secure Two-Party Computation for Machine Learning》
《SecureNN- Efficient and Private Neural Network Training》
《A review of homomorphic encryption and software tools for encrypted statistical machine learning》

Secret Sharing
ABY – A Framework for Efficient Mixed-Protocol Secure Two-Party Computation. Daniel Demmler et al. NDSS, 2015. [pdf]
ABY3: A Mixed Protocol Framework for Machine Learning. Payman Mohassel, Peter Rindal. CCS, 2018. [pdf]
Homomorphic Encryption
Secure Multiple Linear Regression Based on Homomorphic Encryption. Rob Hall et al. Journal of Official Statistics, 2011. [pdf]
Secure Logistic Regression Based on Homomorphic Encryption: Design and Evaluation. Miran Kim et al. Journal of Medical Internet Research, 2018. [pdf]
SecureBoost: A Lossless Federated Learning Framework. Kewei Cheng et al. arxiv.org, 2019. [pdf]



library
https://github.com/NVlabs/xmp (CUDA accelerated(X) Multi-Precision library)
https://github.com/vernamlab/cuHE
phe：Paillier scheme，加法同态，Python实现
Microsoft SEAL：BFV/CKKS scheme，支持整型、浮点型加法和乘法同态，C++实现

open project:
tf-encrypted：Dropout Labs出品，基于tensorflow。主要采用SS，近期也开始采用HE，与SS形成技术互补，详见这篇文章。tf-encrypted定位是production purpose，技术成熟度相对较高。
PySyft：OpenMined出品，基于pytorch。主要采用Fedrated Learning, Differential Sharing, MPC。关注数、贡献数、技术成熟度相比tf-encrypted都更高。
Crypten：Facebook出品，基于pytorch。主要采用Secret Sharing，定位research purpose，前段时间刚开源，整体成熟度不高。

tensorflow-privacy：Google，差分隐私框架
tensorflow-federated：Google，联邦学习框架，大量的移动设备共同训练一个模型。数据不出域，使用Secret Sharing聚合模型梯度。
tf-encrypted：Dropout Labs，基于tensorflow的MPC框架
PySyft：OpenMined，基于pytorch的Fedrated Learning, Differential Privacy, MPC框架
CrypTen：Facebook，基于pytorch的MPC框架
FATE：Webank，基于HE和MPC，支持LR、Tree(RF, GBDT)、DNN

其他
awesome-mpc：mpc资料集合
https://github.com/rdragos/awesome-mpc/
安全计算与密码学：知乎专栏
Dropout Labs：medium专栏
Microsoft: Security, privacy, and cryptography专栏


## tf-encrypted
https://github.com/tf-encrypted/tf-encrypted
https://github.com/tf-encrypted/tf-encrypted#background--further-reading
https://blog.tensorflow.org/2019/03/introducing-tensorflow-privacy-learning.html

https://github.com/tensorflow/privacy
https://github.com/tensorflow/federated
https://www.multipartycomputation.com/

