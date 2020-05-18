# HeteroCL code and tutorial

https://github.com/cornell-zhang/heterocl 
## 1. install  
git clone --recursive https://github.com/cornell-zhang/heterocl.git< br >
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

## 2. 地方 
