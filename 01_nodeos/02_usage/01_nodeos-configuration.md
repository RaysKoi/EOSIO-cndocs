# Nodeos配置
---

插件特定配置可使用命令行选项或`config.ini`配置文件设置，而nodeos特定选项只能使用命令行设置。`nodeos --help`给出了所有命令行选项和`config.ini`配置文件选项信息。

每个`config.ini`配置文件选项对于与一个命令行选项。但是，并非所有命令行选项都可设置在`config.ini`配置文件中。大部分只需操作的插件特定选项不能设置在`config.ini`配置文件中。例如，`state_history_plugin`的`--delete-state-history`选项。

例如，CLI选项`--plugin eosio::chain_api_plugin`可通过在`config.ini`配置文件中添加`plugin = eosio::chain_api_plugin`进行设置。

## `config.ini`配置文件的位置

`config.ini`配置文件的默认位置是：

- Mac OS: `~/Library/Application Support/eosio/nodeos/config`
- Linux: `~/.local/share/eosio/nodeos/config`

可通过指定`nodeos`的`--config path/to/config.ini`选项，设置`config.ini`配置文件位置。

## Nodeos示例

下例给出了`nodeos`的一个典型应用，即启动要给区块生成节点：

```sh
nodeos --replay-blockchain \
  -e -p eosio \
  --plugin eosio::producer_plugin  \
  --plugin eosio::chain_api_plugin \
  --plugin eosio::http_plugin      \
  >> nodeos.log 2>&1 &
```

```sh
nodeos \
  -e -p eosio \
  --data-dir /users/mydir/eosio/data     \
  --config-dir /users/mydir/eosio/config \
  --plugin eosio::producer_plugin      \
  --plugin eosio::chain_plugin         \
  --plugin eosio::http_plugin          \
  --plugin eosio::state_history_plugin \
  --contracts-console   \
  --disable-replay-opts \
  --access-control-allow-origin='*' \
  --http-validate-host=false        \
  --verbose-http-errors             \
  --state-history-dir /shpdata \
  --trace-history              \
  --chain-state-history        \
  >> nodeos.log 2>&1 &
```

上面的`nodeos`启动生产者节点时指定的选项分别为：

* 启用区块生成(`-e`)；
* 识别"eosio"自身为区块链生产者 (`-p`)；
* 设置区块链数据存放目录(`--data-dir`)；
* 设置`config.ini`配置文件目录 (`--config-dir`)；
* 加载插件`producer_plugin`、`chain_plugin`、`http_plugin`和`state_history_plugin` (`--plugin`)
* 传递`chain_plugin`选项(`--contracts-console`, `--disable-replay-opts`)；
* 传递`http-plugin`选项(`--access-control-allow-origin`, `--http-validate-host`, `--verbose-http-errors`)；
* 传递`state_history`选项(`--state-history-dir`, `--trace-history`, `--chain-state-history`)；
* 将`stdout`和`stderr`重定向到`nodeos.log`日志文件；
* 后台运行命令(&)。
