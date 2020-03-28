# producer_api_plugin插件

## 描述

`producer_api_plugin`为[`producer_plugin`](../producer_plugin/index.md)插件提供多个由[`http_plugin`](../http_plugin/index.md)插件管理的RPC API接口。

## 使用

```console
# config.ini
plugin = eosio::producer_api_plugin
```

```sh
# nodeos startup params
nodeos ... --plugin eosio::producer_api_plugin
```

## 选项

无

## 依赖关系

* [`producer_plugin`](../producer_plugin/index.md)
* [`chain_plugin`](../chain_plugin/index.md)
* [`http_plugin`](../http_plugin/index.md)

### 加载依赖示例

```console
# config.ini
plugin = eosio::producer_plugin
[options]
plugin = eosio::chain_plugin
[options]
plugin = eosio::http_plugin
[options]
```

```sh
# command-line
nodeos ... --plugin eosio::producer_plugin [options]  \
           --plugin eosio::chain_plugin [operations] [options]  \
           --plugin eosio::http_plugin [options]
```
