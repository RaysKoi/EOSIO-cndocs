# EOSIO软件依赖
---

EOSIO在构建二进制文件时需要特定的软件依赖。这些依赖可以从源文件构建，也可以直接安装其二进制文件。可以使用指定的版本，也可以使用当前最新版本。独立于EOSIO软件库的主要依赖包括：


* Clang：EOSIO使用的兼容C++17编译器；
* CMake：EOSIO使用的构建系统；
* Boost：EOSIO使用的C++ Boost软件库；
* OpenSSL：安全通信和加密库；
* LLVM：LLVM编译器/工具链架构。

其它依赖或者是已置于EOSIO代码库中（例如`secp256k1`椭圆曲线DSA算法库），或是仅用于测试和一些杂务，包括：


* automake、autoconf、autotools；
* doxygen、graphviz；
* python2、python3；
* bzip2、zlib；


## 指定依赖

为确保EOSIO不同软件版本间的互操作性，开发人员构建中可考虑重现内部使用的“指定”二进制依赖版本。基于可移植性和稳定性上的考虑，区块生成者会希望安装和运行使用了指定依赖构建的EOSIO软件。指定依赖项通常是从源文件构建的。


## 非指定依赖

一般用户和应用开发人员可能希望安装非指定的EOSIO依赖版本，即最新或是最稳定的依赖版本。使用非指定依赖的优点是降低了安装时间，并可能会提高性能。而指定依赖通常是从二进制文件安装的。


## 自动化依赖安装

EOSIO依赖可在从源文件构建EOSIO时，自动从[构建脚本](../01_shell-scripts/02_build-eosio-binaries.md)构建和安装。在构建指定依赖时，可在调用脚本时指定`-P`选项。否则，可能会安装非指定的依赖版本。需注意的是，`boost` 和`cmake`的版本总是使用指定依赖的：


```sh
cd ~/eosio/eos
./scripts/eosio_build.sh [-P]
```

### 非受支持平台

手工调用[构建脚本](../01_shell-scripts/02_build-eosio-binaries.md)中的命令，可手工构建和安装EOSIO依赖。需要设定特定的环境变量和命令行参数，从脚本直接生成实际执行命令。操作如下：


```sh
cd ~/eosio/eos
export VERBOSE=true && export DRYRUN=true && ./scripts/eosio_build.sh -y [-P]
```
