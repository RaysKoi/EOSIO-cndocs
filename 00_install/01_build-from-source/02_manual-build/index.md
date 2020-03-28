# 手工构建EOSIO（目录）
---

[[提示 | 手工构建适用于高级开发人员]]

| 文档中给出的手工操作适用于高级开发人员。推荐使用[Shell脚本](../01_shell-scripts/index.md)从源文件构建EOSIO。如果在用户平台上执行脚本时出现错误，或者用户平台并非受支持的操作系统操作，可尝试采用此处给出的操作。

## EOSIO依赖关系

在手工执行构建时，需要安装EOSIO软件依赖的特性软件包。依赖关系细节，提供在[EOSIO软件依赖](00_eosio-dependencies.md)一节中。


## 平台

代码库提供了手工下载、构建、安装、测试和卸载EOSIO软件及其依赖的Shell脚本。请访问[受支持的平台列表](03_platforms/index.md)。


## 外部编译（Out-of-source Builds）

在构建EOSIO二进制及其依赖时，支持外部编译。具体参见`cmake`帮助文档。


## 其它编译方式

为替代`clang`默认的编译器工具链，在`cmake`命令行中添加如下选项：

`-DCMAKE_CXX_COMPILER=/path/to/c++ -DCMAKE_C_COMPILER=/path/to/cc`

## 构建的调试

为在构建中支持调试，在`cmake`命令行中添加`-DCMAKE_BUILD_TYPE=Debug`选项。其它`cmake`常用选项包括`Release`和`RelWithDebInfo`。
