# HeteroCL code and tutorial

https://github.com/cornell-zhang/heterocl 
## 1. install  
env: ENV_DNN_python3.74
目前支持python3
git clone --recursive https://github.com/cornell-zhang/heterocl.git  
make -j8  
会检查cmake和llvm的版本是否ok，在pks/cmake/Makefile中进行，下载较慢，可以先下载  
mkdir build/pkgs/cmake/build  
cd build/pkgs/cmake/build  
wget https://cmake.org/files/v3.10/cmake-3.10.2-Linux-x86_64.tar.gz  
tar -zxf cmake-3.10.2-Linux-x86_64.tar.gz  
mv cmake-3.10.2-Linux-x86_64 cmake  
mkdir build/pkgs/llvm  
cd build/pkgs/llvm  
wget http://releases.llvm.org/6.0.0/llvm-6.0.0.src.tar.xz  

在Makefile中进行python setup.py install --user
这里的--user指定了~/.local/lib/python3.7/site-packages/为python的安装目录，其不是PYTHONPATH，导致env下找不heterocl
需要去掉

## 2. tutorial  
http://heterocl.csl.cornell.edu/doc/installation.html  
http://heterocl.csl.cornell.edu/doc/tutorials/index.html  

