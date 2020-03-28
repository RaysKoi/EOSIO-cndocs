## 目标

连接到指定的`nodeos`或`keosd`主机，发送命令。

`cleos`和 `keosd`分别支持使用`--url`或`--wallet-url`选项连接到指定节点。选项参数为服务监听的http地址和端口号。

[[提示 | 缺省地址和端口号]]
| 如果`--url`或`--wallet-url`选项未指定参数，那么`cleos`将尝试连接到本地默认端口`127.0.0.1:8888`的`nodeos`或`keosd`。

#
## 准备工作


* 安装了适用版本的`cleos`。

## 操作步骤

### 连接到Nodeos

```sh
cleos -url http://nodeos-host:8888 COMMAND
```

### 连接到Keosd

```sh
cleos --wallet-url http://keosd-host:8888 COMMAND
```
