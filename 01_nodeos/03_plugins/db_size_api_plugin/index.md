# db_size_api_plugin插件

## 描述

`db_size_api_plugin`插件实现区块链上分析情况检索，包括：

* 可用字节数（free_bytes）；
* 已用字节数（used_bytes）；
* 大小；
* 索引。

<!--
## Usage

```console
# Not available
```
-->

## 选项

无

## 依赖关系

* [`chain_plugin`](../chain_plugin/index.md)
* [`http_plugin`](../http_plugin/index.md)

### 加载依赖插件的示例：

```console
# config.ini
plugin = eosio::chain_plugin
[options]
plugin = eosio::http_plugin
[options]
```

```sh
# command-line
nodeos ... --plugin eosio::chain_plugin [operations] [options]  \
           --plugin eosio::http_plugin [options]
```
