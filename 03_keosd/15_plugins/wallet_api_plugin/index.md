# wallet_api_plugin插件

## 功能描述

`wallet_api_plugin`向[`http_plugin`](../http_plugin/index.md)插件管理的RPC API接口提供[`wallet_plugin`](../wallet_plugin/index.md)功能。

[[注意]]
| 该插件提供钱包操作，因此不建议在公开可访问网络上运行该插件。`nodeos` 1.2.0不再支持`wallet_api_plugin`插件。

## 使用

```sh
# config.ini
plugin = eosio::wallet_api_plugin

# command-line
nodeos ... --plugin eosio::wallet_api_plugin
```

## 选项说明

无

## 依赖关系

* [`wallet_plugin`](../wallet_plugin/index.md)
* [`http_plugin`](../http_plugin/index.md)

### 加载依赖示例

```sh
# config.ini
plugin = eosio::wallet_plugin
[options]
plugin = eosio::http_plugin
[options]

# command-line
nodeos ... --plugin eosio::wallet_plugin [options]  \
           --plugin eosio::http_plugin [options]
```
