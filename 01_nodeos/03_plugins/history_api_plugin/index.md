# history_api_plugin插件

[[警告| 已禁用功能]]
| `history_api_plugin`插件依赖的`history_plugin`插件已经禁用，并不再维护。请使用[`state_history_plugin`](../state_history_plugin/index.md)插件。

## 描述

`history_api_plugin` 将[`history_plugin`](../history_plugin/index.md)插件功能提供给由[`http_plugin`](../http_plugin/index.md)插件管理的RPC API，为区块链数据提供只读访问。

该插件提供四种RPC API端点：

* get_actions
* get_transaction
* get_key_accounts
* get_controlled_accounts

<!--[[更多信息]]
| See HISTORY section of [RPC API](https://developers.eos.io/eosio-nodeos/reference).-->

上述四种RPC API分别被如下`cleos`命令使用（列出顺序依次对应）：

* get actions
* get transaction
* get accounts
* get servants

## 使用

```console
# config.ini
plugin = eosio::history_api_plugin
```

```sh
# command-line
nodeos ... --plugin eosio::history_api_plugin
```

## 选项

None

## 依赖关系

* [`history_plugin`](../history_plugin/index.md)
* [`chain_plugin`](../chain_plugin/index.md)
* [`http_plugin`](../http_plugin/index.md)

### 加载依赖示例

```console
# config.ini
plugin = eosio::history_plugin
[options]
plugin = eosio::chain_plugin
[options]
plugin = eosio::http_plugin
[options]
```

```sh
# command-line
nodeos ... --plugin eosio::history_plugin [options]  \
           --plugin eosio::chain_plugin [operations] [options]  \
           --plugin eosio::http_plugin [options]
```
