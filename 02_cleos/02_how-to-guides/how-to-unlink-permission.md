## 目标

解除许可的链接

将许可链接到合约操作。

## 准备工作

* 安装了适用版本的`cleos`。

  
* 理解以下概念：
  * 账户；
  * 许可等级；
  * 操作。

## 操作步骤

取消链接到合约`hodlcontract`动作`transfer`上的许可等级：


```sh
cleos set action permission alice hodlcontract transfer NULL
```