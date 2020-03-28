# Keosd故障排除
---

## 如何解决错误"Failed to lock access to wallet directory; is another `keosd` running"?

由于可以使用`cleos`加载`keosd`实例，这样有可能最终会运行多个`keosd`实例，进而导致操作异常，并给出如上错误信息。

解决该问题，用户可中止所有在运行的`keosd`实例，然后重启`keosd`。下面命令将查找并终止系统中所有运行中的`keosd`实例：


```sh
pkill keosd
```
