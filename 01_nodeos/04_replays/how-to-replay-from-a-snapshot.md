# 如何从快照重播
---

一旦用户获取创建区块链状态所需经验证的快照备份文件，需将文件拷贝到`data/snapshots`目录中，备份或移除现有数据目录中所所有内容。


位置          | 名称                      |  操作
----------------- | -------------------------- | ------------
data/snapshots    | <head block id in hex>.bin | 此处放置替换所需的快照文件
data/             | *                          | 移除

要指定重播快照文件的搜索目录，可在配置文件中设置`snapshots-dir = "snapshots" `选项，也可在命令行使用`--snapshots-dir`选项。指定重播快照文件名称，使用`--snapshot`选项。


```sh
nodeos --snapshot yoursnapshot.name \
  -e -p eosio \
  --plugin eosio::producer_plugin  \
  --plugin eosio::chain_api_plugin \
  --plugin eosio::http_plugin      \
  >> nodeos.log 2>&1 &
```

在从快照文件重播时，推荐移除所有现有数据。如果设置了`blocks.log`文件，那么其中区块高度必须包括大于快照区块高度，此外也可包括高于此高度的额外区块，以在启动时加入节点中。如果`blocks.log`文件存储，但是其中区块高度低于快照，那么重播将抛出异常。所有可用的可撤回区块也将加以应用。

blocks.log               | 快照                  | 操作
------------------------ | --------------------------- | ------
不存在blocks.log            | 不可撤回区块高度为2000 | 正常
包含区块高度1-1999 | 不可撤回区块高度为2000 | 异常
包含区块高度1 - 2001 | 不可撤回区块高度为2000 | 正常，从快照重建，并恢复至高度2001 

从快照文件重建节点，不能对`nodeos`设置`--genesis-json`或`--genesis-timestamp`选项，因为相关信息将从快照文件加载。如果存在`blocks.log`文件，那么其中包含的创世信息将与快照中的创世信息做验证。如果二者创世信息存在差异，重播将失败。也就是说，要检查`blocks.log`文件和快照文件是否来自同一区块链。

