# 安装EOSIO二进制文件
---

## EOSIO安装脚本

为便于开发智能合约，用户可使用`eos/scripts`文件夹中提供的`eosio_install.sh`脚本，将构建生成内容可安装到`/usr/local`文件夹中。执行该脚本需要操作系统文件夹的相应权限。操作如下：


```sh
cd ~/eosio/eos
sudo ./scripts/eosio_install.sh
```

## EOSIO手动安装

作为替代`eosio_install.sh`脚本，用户可以在`eos/build`文件夹中调用`make install`命令，完成EOSIO二进制文件的安装。同样，执行该命令需要操作系统文件夹的相应权限。操作如下：


```sh
cd ~/eosio/eos/build
sudo make install
```

[下一条]

| [Nodeos](../../../01_nodeos/index.md)的配置和使用。

| （可选）[测试EOSIO二进制文件](04_test-eosio-binaries.md)。
