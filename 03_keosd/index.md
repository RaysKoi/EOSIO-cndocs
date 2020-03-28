# Keosd
---


## 本章索引

* [使用](10_usage.md)
* [操作指南](30_how-to-guides/index.md)
* [插件](15_plugins/index.md)
* [安全](20_security.md)
* [钱包规格说明](35_wallet-specification.md)。
* [故障排除](40_troubleshooting.md)。
* [常见问题](50_FAQ.md)。


## 引言

`keosd`是提供密钥管理服务的驻留进程，实现存储私钥和数字签名消息。`keosd`提供了一种安全的密钥存储媒介，将密钥合理加密保存到相应的钱包文件中。`keosd`还为`cleos`或第三方创建的签名交易提供了安全封装。

## 安装

`keosd`作为[EOSIO software suite](https://github.com/EOSIO/eos/blob/master/README.md)组成发布。安装`keosd`请参考文档“[EOSIO软件安装](../00_install/index.md)”一章内容。

## 操作

一旦钱包使用相应密码解锁，`cleos`就请求`keosd`使用相应密钥对交易做签名。此外，`keosd`也支持硬件钱包，包括 Secure Encalve和YubiHSM等。

[[提示]]
| `keosd`设计上仅针对EOSIO开发者。
