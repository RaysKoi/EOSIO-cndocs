# 下载EOSIO源文件
---

下载EOSIO源代码，需对`eos`代码库及其子模块执行clone操作。建议用户首先在自己的HOME目录中创建一个`eosio`文件夹，并下载所有EOSIO相关代码块内容。示例操作如下：


```sh
mkdir -p ~/eosio && cd ~/eosio
git clone --recursive https://github.com/EOSIO/eos
```

## 子模块的更新

如果在代码库clone操作中使用了`--recursive`选项，那么在开始构建前，必须更新所有子模块。操作如下：

```sh
cd ~/eosio/eos
git submodule update --init --recursive
```

## 拉取代码库中的更改

在拉取（pull）代码库更改时，尤其是切换代码库分支后，也必须更新所有子模块。可以通过上面给出的`git submodule`命令实现，也可以直接使用`git pull`命令。操作如下：

```sh
[git checkout <branch>]  (optional)

git pull --recurse-submodules
```

[下一条]

| [构建EOSIO二进制文件](02_build-eosio-binaries.md)
