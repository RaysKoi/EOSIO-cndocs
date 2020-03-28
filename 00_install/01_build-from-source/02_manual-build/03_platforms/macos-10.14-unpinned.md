# MacOS 10.14（原始编译器）
---


本节给出在MacOS 10.14上手动下载、构建、安装、测试和卸载EOSIO及其依赖的Shell命令。


[[提示 | 适用于高级开发人员的EOSIO构建]]

| 对于初次接触EOSIO的用户，建议安装[EOSIO预先构建二进制文件](../../../00_install-prebuilt-binaries.md)，而非从源代码构建。

用户可从下面列表中选取所需任务，将相应Shell命令拷贝到Unix终端中执行：


- [# MacOS 10.14（指定编译器）](#h1-id%22macos-1014e68c87e5ae9ae7bc96e8af91e599a8-39%22macos-1014%e6%8c%87%e5%ae%9a%e7%bc%96%e8%af%91%e5%99%a8h1)
- [下载EOSIO代码库](#%e4%b8%8b%e8%bd%bdeosio%e4%bb%a3%e7%a0%81%e5%ba%93)
- [安装EOSIO依赖](#%e5%ae%89%e8%a3%85eosio%e4%be%9d%e8%b5%96)
- [构建EOSIO](#%e6%9e%84%e5%bb%baeosio)
- [安装EOSIO](#%e5%ae%89%e8%a3%85eosio)
- [测试EOSIO](#%e6%b5%8b%e8%af%95eosio)
- [卸载EOSIO](#%e5%8d%b8%e8%bd%bdeosio)


[[提示 | 要在其它操作系统上构建EOSIO？]]

| 请访问“[从源代码构建EOSIO](../../index.md)”一节内容。



## 下载EOSIO代码库

下面给出的命令将设置EOSIO目录、安装git，并克隆EOSIO代码库。

```sh
# set EOSIO directories
export EOSIO_LOCATION=~/eosio/eos
export EOSIO_INSTALL_LOCATION=$EOSIO_LOCATION/../install
mkdir -p $EOSIO_INSTALL_LOCATION
# install git
brew update && brew install git
# clone EOSIO repository
git clone https://github.com/EOSIO/eos.git $EOSIO_LOCATION
cd $EOSIO_LOCATION && git submodule update --init --recursive
```

## 安装EOSIO依赖

下面给出的命令将安装EOSIO软件依赖。确认已[下载EOSIO代码库](#%e4%b8%8b%e8%bd%bdeosio%e4%bb%a3%e7%a0%81%e5%ba%93) ，并已设置了EOSIO工作目录。

```sh
# install dependencies
brew install cmake python libtool libusb graphviz automake wget gmp pkgconfig doxygen openssl@1.1 jq boost || :
export PATH=$EOSIO_INSTALL_LOCATION/bin:$PATH
# install mongodb
mkdir -p $EOSIO_INSTALL_LOCATION/bin
cd $EOSIO_INSTALL_LOCATION && curl -OL https://fastdl.mongodb.org/osx/mongodb-osx-ssl-x86_64-3.6.3.tgz
    tar -xzf mongodb-osx-ssl-x86_64-3.6.3.tgz && rm -f mongodb-osx-ssl-x86_64-3.6.3.tgz && \
    mv $EOSIO_INSTALL_LOCATION/mongodb-osx-x86_64-3.6.3/bin/* $EOSIO_INSTALL_LOCATION/bin/ && \
    rm -rf $EOSIO_INSTALL_LOCATION/mongodb-osx-x86_64-3.6.3 && rm -rf $EOSIO_INSTALL_LOCATION/mongodb-osx-ssl-x86_64-3.6.3.tgz
# install mongo-c-driver from source
cd $EOSIO_INSTALL_LOCATION && curl -LO https://github.com/mongodb/mongo-c-driver/releases/download/1.13.0/mongo-c-driver-1.13.0.tar.gz && \
    tar -xzf mongo-c-driver-1.13.0.tar.gz && cd mongo-c-driver-1.13.0 && \
    mkdir -p cmake-build && cd cmake-build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=$EOSIO_INSTALL_LOCATION -DENABLE_BSON=ON -DENABLE_SSL=DARWIN -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -DENABLE_STATIC=ON -DENABLE_ICU=OFF -DENABLE_SASL=OFF -DENABLE_SNAPPY=OFF .. && \
    make -j $(getconf _NPROCESSORS_ONLN) && \
    make install && \
    rm -rf $EOSIO_INSTALL_LOCATION/mongo-c-driver-1.13.0.tar.gz $EOSIO_INSTALL_LOCATION/mongo-c-driver-1.13.0
# install mongo-cxx-driver from source
cd $EOSIO_INSTALL_LOCATION && curl -L https://github.com/mongodb/mongo-cxx-driver/archive/r3.4.0.tar.gz -o mongo-cxx-driver-r3.4.0.tar.gz && \
    tar -xzf mongo-cxx-driver-r3.4.0.tar.gz && cd mongo-cxx-driver-r3.4.0/build && \
    cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=$EOSIO_INSTALL_LOCATION .. && \
    make -j $(getconf _NPROCESSORS_ONLN) VERBOSE=1 && \
    make install && \
    rm -rf $EOSIO_INSTALL_LOCATION/mongo-cxx-driver-r3.4.0.tar.gz $EOSIO_INSTALL_LOCATION/mongo-cxx-driver-r3.4.0
```


## 构建EOSIO

下面给出的命令在设定操作系统上构建EOSIO软件。确认已完成[安装EOSIO依赖](#%e5%ae%89%e8%a3%85eosio%e4%be%9d%e8%b5%96)。

```sh
export EOSIO_BUILD_LOCATION=$EOSIO_LOCATION/build
mkdir -p $EOSIO_BUILD_LOCATION
cd $EOSIO_BUILD_LOCATION && cmake -DCMAKE_BUILD_TYPE='Release' -DCMAKE_INSTALL_PREFIX=$EOSIO_INSTALL_LOCATION -DBUILD_MONGO_DB_PLUGIN=true ..
cd $EOSIO_BUILD_LOCATION && make -j$(getconf _NPROCESSORS_ONLN)
```


## 安装EOSIO

下面给出的命令将EOSIO软件安装到指定操作系统上。确认已完成[构建EOSIO](#%e6%9e%84%e5%bb%baeosio)。

```sh
cd $EOSIO_BUILD_LOCATION && make install
```

# 测试EOSIO

下面给出的命令将测试安装在指定操作系统上的EOSIO软件。该步操作是可选的，但在执行前需确认已完成[安装EOSIO](#%e5%ae%89%e8%a3%85eosio)。

```sh
$EOSIO_INSTALL_LOCATION/bin/mongod --fork --logpath $(pwd)/mongod.log --dbpath $(pwd)/mongodata
cd $EOSIO_BUILD_LOCATION && make test
```


## 卸载EOSIO

下面给出的命令完成在指定操作系统上卸载EOSIO软件。

```sh
xargs rm < $EOSIO_BUILD_LOCATION/install_manifest.txt
rm -rf $EOSIO_BUILD_LOCATION
```
