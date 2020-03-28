## servants子命令功能

获取指定账户的控制账户信息。

## 操作
```sh
cleos get servants
```

**output**

```console
Usage: cleos get servants account

Positionals:
  account TEXT                The name of the controlling account
```

## 命令

```sh
cleos get servants inita
```

## 输出

```json
{
  "controlled_accounts": [
    "tester"
  ]
}
```
