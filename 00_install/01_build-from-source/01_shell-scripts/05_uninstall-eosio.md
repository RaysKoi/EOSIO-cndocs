# 卸载EOSIO
---

如果用户先前曾经从源代码构建了EOSIO，并希望现在重新安装构建好的二进制文件，或是希望再次从源代码重新构建，推荐运行`eos/scripts`文件夹中提供的`eosio_uninstall.sh`脚本。操作如下：


```sh
cd ~/eosio/eos
sudo ./scripts/eosio_uninstall.sh
```

[卸载依赖]

| 卸载脚本还会提示用户去卸载EOSIO相关依赖。如果用户需要安装预先构建的EOSIO软件，或是首次从源代码构建EOSIO，推荐卸载相关依赖。
