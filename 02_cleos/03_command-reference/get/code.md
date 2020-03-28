## code子命令功能

获取账户的代码和ABI。

## 顺位项说明

- `name` _TEXT_：需检索代码的账户名。

## Options
- `-c,--code` _TEXT_ ：指定保存合约_.wast_内容的文件名。
- `-a,--abi` _TEXT_ ：指定保存合约 _.abi_内容的文件名
- `--wasm`：以wasm格式保存

## 示例

输出eosio.token合约的哈希值

```sh
cleos get code eosio.token
```
```console
code hash: f675e7aeffbf562c033acfaf33eadff255dacb90d002db51c7ad7cbf057eb791
```

检索并保存eosio.token合约的ABI。

```sh
cleos get code eosio.token -a eosio.token.abi
```
```console
code hash: f675e7aeffbf562c033acfaf33eadff255dacb90d002db51c7ad7cbf057eb791
saving abi to eosio.token.abi
```

检索并保存eosio.token合约的wast代码。

```sh
cleos get code eosio.token -c eosio.token.wast
```
```console
code hash: f675e7aeffbf562c033acfaf33eadff255dacb90d002db51c7ad7cbf057eb791
saving wast to eosio.token.wast
```
