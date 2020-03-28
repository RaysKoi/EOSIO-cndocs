# Ubuntu 18.04 （非指定）
---


本节给出在Ubuntu 18.04上手动下载、构建、安装、测试和卸载EOSIO及其依赖的Shell命令。


[[提示 | 适用于高级开发人员的EOSIO构建]]

| 对于初次接触EOSIO的用户，建议安装[EOSIO预先构建二进制文件](../../../00_install-prebuilt-binaries.md)，而非从源代码构建。

用户可从下面列表中选取所需任务，将相应Shell命令拷贝到Unix终端中执行：


- [# Ubuntu 16.04（指定）](#h1-id%22ubuntu-1604e68c87e5ae9a-4%22ubuntu-1604%e6%8c%87%e5%ae%9ah1)
- [下载EOSIO代码库](#%e4%b8%8b%e8%bd%bdeosio%e4%bb%a3%e7%a0%81%e5%ba%93)
- [Install EOSIO Dependencies](#install-eosio-dependencies)
- [Build EOSIO](#build-eosio)
- [Install EOSIO](#install-eosio)
- [Test EOSIO](#test-eosio)
- [Uninstall EOSIO](#uninstall-eosio)


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
apt-get update && apt-get upgrade -y && DEBIAN_FRONTEND=noninteractive apt-get install -y git
# clone EOSIO repository
git clone https://github.com/EOSIO/eos.git $EOSIO_LOCATION
cd $EOSIO_LOCATION && git submodule update --init --recursive
```

## 安装EOSIO依赖

下面给出的命令将安装EOSIO软件依赖。确认已[下载EOSIO代码库](#%e4%b8%8b%e8%bd%bdeosio%e4%bb%a3%e7%a0%81%e5%ba%93) ，并已设置了EOSIO工作目录。

```sh
# install dependencies
apt-get install -y make bzip2 automake libbz2-dev libssl-dev doxygen graphviz libgmp3-dev \
    autotools-dev libicu-dev python2.7 python2.7-dev python3 python3-dev \
    autoconf libtool curl zlib1g-dev sudo ruby libusb-1.0-0-dev \
    libcurl4-gnutls-dev pkg-config patch llvm-7-dev clang-7 vim-common jq
# build cmake
export PATH=$EOSIO_INSTALL_LOCATION/bin:$PATH
cd $EOSIO_INSTALL_LOCATION && curl -LO https://cmake.org/files/v3.13/cmake-3.13.2.tar.gz && \
    tar -xzf cmake-3.13.2.tar.gz && \
    cd cmake-3.13.2 && \
    ./bootstrap --prefix=$EOSIO_INSTALL_LOCATION && \
    make -j$(nproc) && \
    make install && \
    rm -rf $EOSIO_INSTALL_LOCATION/cmake-3.13.2.tar.gz $EOSIO_INSTALL_LOCATION/cmake-3.13.2
# build boost
cd $EOSIO_INSTALL_LOCATION && curl -LO https://dl.bintray.com/boostorg/release/1.71.0/source/boost_1_71_0.tar.bz2 && \
    tar -xjf boost_1_71_0.tar.bz2 && \
    cd boost_1_71_0 && \
    ./bootstrap.sh --prefix=$EOSIO_INSTALL_LOCATION && \
    ./b2 --with-iostreams --with-date_time --with-filesystem --with-system --with-program_options --with-chrono --with-test -q -j$(nproc) install && \
    rm -rf $EOSIO_INSTALL_LOCATION/boost_1_71_0.tar.bz2 $EOSIO_INSTALL_LOCATION/boost_1_71_0
# build mongodb
cd $EOSIO_INSTALL_LOCATION && curl -LO https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1804-4.1.1.tgz && \
    tar -xzf mongodb-linux-x86_64-ubuntu1804-4.1.1.tgz && rm -f mongodb-linux-x86_64-ubuntu1804-4.1.1.tgz && \
    mv $EOSIO_INSTALL_LOCATION/mongodb-linux-x86_64-ubuntu1804-4.1.1/bin/* $EOSIO_INSTALL_LOCATION/bin/ && \
    rm -rf $EOSIO_INSTALL_LOCATION/mongodb-linux-x86_64-ubuntu1804-4.1.1
# build mongodb c driver
cd $EOSIO_INSTALL_LOCATION && curl -LO https://github.com/mongodb/mongo-c-driver/releases/download/1.13.0/mongo-c-driver-1.13.0.tar.gz && \
    tar -xzf mongo-c-driver-1.13.0.tar.gz && cd mongo-c-driver-1.13.0 && \
    mkdir -p build && cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=$EOSIO_INSTALL_LOCATION -DENABLE_BSON=ON -DENABLE_SSL=OPENSSL -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -DENABLE_STATIC=ON -DENABLE_ICU=OFF -DENABLE_SNAPPY=OFF .. && \
    make -j$(nproc) && \
    make install && \
    rm -rf $EOSIO_INSTALL_LOCATION/mongo-c-driver-1.13.0.tar.gz $EOSIO_INSTALL_LOCATION/mongo-c-driver-1.13.0
# build mongodb cxx driver
cd $EOSIO_INSTALL_LOCATION && curl -L https://github.com/mongodb/mongo-cxx-driver/archive/r3.4.0.tar.gz -o mongo-cxx-driver-r3.4.0.tar.gz && \
    tar -xzf mongo-cxx-driver-r3.4.0.tar.gz && cd mongo-cxx-driver-r3.4.0 && \
    sed -i 's/\"maxAwaitTimeMS\", count/\"maxAwaitTimeMS\", static_cast<int64_t>(count)/' src/mongocxx/options/change_stream.cpp && \
    sed -i 's/add_subdirectory(test)//' src/mongocxx/CMakeLists.txt src/bsoncxx/CMakeLists.txt && \
    mkdir -p build && cd build && \
    cmake -DBUILD_SHARED_LIBS=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=$EOSIO_INSTALL_LOCATION .. && \
    make -j$(nproc) && \
    make install && \
    rm -rf $EOSIO_INSTALL_LOCATION/mongo-cxx-driver-r3.4.0.tar.gz $EOSIO_INSTALL_LOCATION/mongo-cxx-driver-r3.4.0
```


## 构建EOSIO

下面给出的命令在设定操作系统上构建EOSIO软件。确认已完成[安装EOSIO依赖](#%e5%ae%89%e8%a3%85eosio%e4%be%9d%e8%b5%96)。

```sh
export EOSIO_BUILD_LOCATION=$EOSIO_LOCATION/build
mkdir -p $EOSIO_BUILD_LOCATION
cd $EOSIO_BUILD_LOCATION && cmake -DCMAKE_BUILD_TYPE='Release' -DCMAKE_CXX_COMPILER='clang++-7' -DCMAKE_C_COMPILER='clang-7' -DLLVM_DIR='/usr/lib/llvm-7/lib/cmake/llvm' -DCMAKE_INSTALL_PREFIX=$EOSIO_INSTALL_LOCATION -DBUILD_MONGO_DB_PLUGIN=true ..
cd $EOSIO_BUILD_LOCATION && make -j$(nproc)
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
