# caffe-installation
caffe cuda8.0, cudnn7, openBLAS, opencv 2.4.13

1、Ubuntu14.04 参考教程 http://coldmooon.github.io/2015/08/03/caffe_install/

## OpenBLAS 配置注意：

1 下载之后，make编译，还需要执行 sudo make install, 以确保安装到系统环境。默认位置为/opt/OpenBLAS。

### 修改caffe Makefile.conf 文件如下
‵‵‵
BLAS := open
 Custom (MKL/ATLAS/OpenBLAS) include and lib directories.
 Leave commented to accept the defaults for your choice of BLAS
 (which should work)!
BLAS_INCLUDE :=  /opt/OpenBLAS/include
BLAS_LIB := /opt/OpenBLAS/lib
```

参考：http://blog.csdn.net/sinat_17196995/article/details/53466524

### 如果编译时openblas报错：
error while loading shared libraries: libopenblas.so.0: cannot open shared object file: No such file or directory
找不到链接库xxx.so，这种问题的解决方法是：
在 /etc/ld.so.conf文件中加入xxx.so 所在的目录。此处即为加入/opt/OpenBLAS/lib
参考：http://www.cnblogs.com/amboyna/archive/2008/02/06/1065322.html

## opencv 安装脚本
在文件中更改版本号即可。

## c++/g++问题
修改这一步是为了避免出现string.h ‘memcy’ was not declared in this scope这样的错误，这种错误通常是由于gcc版本太新而导致的
修改 Makefile 文件
```
NVCCFLAGS += -ccbin=$(CXX) -Xcompiler -fPIC $(COMMON_FLAGS)  #这行去掉
#改为：
NVCCFLAGS += -D_FORCE_INLINES -ccbin=$(CXX) -Xcompiler -fPIC $(COMMON_FLAGS)
```
