## 目标

设置一个需要对交易进行多签的账户。


## 准备工作

* 具有一个账户。

* 账户持有足量的通证。

* 安装了适用版本的`cleos`。

* 理解以下概念：
  * 什么是账户？
  * 什么是交易？


## 操作步骤：

```sh
cleos set account permission multisig active '{\"threshold\" : 1, \"accounts\" :[{\"permission\":{\"actor\":\"eosio\",\"permission\":\"active\"},\"weight\":1},{\"permission\":{\"actor\":\"customera\",\"permission\":\"active\"},\"weight\":1}]}' owner -p multisig@owner"
```