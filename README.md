# EOSIO中文文档
-----
（V 1.0，rays.kai@gmail.com）


## 快速上手

* [EOSIO模块](index.md)
* [测试网入门](00_install/index.md)
  * [从源文件安装EOSIO](00_install/01_build-from-source/index.md)
  * [从二进制文件安装EOSIO](00_install/00_install-prebuilt-binaries.md)

## 用户操作

EOSIO是针对智能合约和分布式应用部署的下一代区块链平台。EOSIO提供多种工具，包括：

![EOS组件](eosio_components.png)

* [nodeos](01_nodeos/index.md)：EOS的核心服务进程，实现支持区块生成、API终端和本地开发的节点
  * [使用](01_nodeos/02_usage/index.md)
  * [插件](01_nodeos/03_plugins/index.md)
  * [重播](01_nodeos/04_replays/index.md)
  * [日志](01_nodeos/06_logging/index.md)
  * [升级指南](01_nodeos/07_upgrade-guides/index.md)
  * [故障排除](01_nodeos/08_troubleshooting/index.md)
* [cleos](02_cleos/index.md)：通过`nodeos`实现与区块链进行交互的命令行接口，并通过`cleos`管理钱包应用。
  * [CLI命令选项](02_cleos/03_command-reference\index.md)
  * [操作指南](02_cleos/02_how-to-guides\index.md)
  * [故障排除](02_cleos/04_troubleshooting.md)
  * [常见问题](02_cleos/05_FAQ.md)
* [keosd](03_keosd/index.md)：实现在钱包中管理区块链密钥管理，为数字签名提供安全封装。
  * [使用](03_keosd/10_usage.md)
  * [操作指南](03_keosd/30_how-to-guides/index.md)
  * [插件](03_keosd/15_plugins/index.md)
  * [安全](03_keosd/20_security.md)
  * [钱包规格说明](03_keosd/35_wallet-specification.md)。
  * [故障排除](03_keosd/40_troubleshooting.md)。
  * [常见问题](03_keosd/50_FAQ.md)。
