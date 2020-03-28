## 目标

列出所有的密钥对。

## 准备工作

* 安装了适用版本的`cleos`。

  
* 理解以下概念：
  * 账户；
  * 密钥对。
  
## 操作步骤

解锁钱包：

```sh
cleos wallet unlock
```

列出所有公钥：

```sh
cleos wallet keys
```

列出所有私钥：

```sh
cleos wallet private_keys

```

[[警告]]
| 永远不要在生产环境中展示自己的私钥。
