# 安装预先构建二进制文件
---

[[提示 | 预先构建]]

| 如果用户已经使用Shell脚本从源文件构建了EOSIO，那么在同一操作系统中安装预先构建二进制文件时，必须首先运行[卸载脚本](01_build-from-source/01_shell-scripts/05_uninstall-eosio.md)。

## 预先构建二进制文件

预先构建二进制文件适用于如下操作系统。用户可根据自己操作系统选取对应的操作。


### Mac OS X:

#### Mac OS X Brew安装

```sh
brew tap eosio/eosio
brew install eosio
```

#### Mac OS X Brew卸载

```sh
brew remove eosio
```

### Ubuntu Linux:

#### Ubuntu 18.04软件包安装

```sh
wget https://github.com/eosio/eos/releases/download/v2.0.4/eosio_2.0.4-1-ubuntu-18.04_amd64.deb
sudo apt install ./eosio_2.0.4-1-ubuntu-18.04_amd64.deb
```

#### Ubuntu 16.04软件包卸载

```sh
wget https://github.com/eosio/eos/releases/download/v2.0.4/eosio_2.0.4-1-ubuntu-16.04_amd64.deb
sudo apt install ./eosio_2.0.4-1-ubuntu-16.04_amd64.deb
```

#### Ubuntu软件包卸载

```sh
sudo apt remove eosio
```

### 基于RPM的操作系统（包括CentOS、Amazon Linux等）：

#### RPM软件包安装

```sh
wget https://github.com/eosio/eos/releases/download/v2.0.4/eosio-2.0.4-1.el7.x86_64.rpm
sudo yum install ./eosio-2.0.4-1.el7.x86_64.rpm
```

#### RPM软件包卸载

```sh
sudo yum remove eosio
```

## EOSIO二进制安装位置

完成预先构建二进制安装后，实际二进制文件位于：

* `/usr/opt/eosio/<version-string>/bin`目录（Linux）；
* `/usr/local/Cellar/eosio/<version-string>/bin`目录（MacOS）。

其中，`version-string`表示安装的EOSIO版本。

此外，`nodeos`, `cleos`, `keosd`等EOSIO程序，将会在`usr/bin`或`usr/local/bin`系统目录中建立软链接，支持在任意目录中直接执行。


## 前期版本

要安装前期版本的EOSIO预先构建二进制：
To install previous versions of the EOSIO prebuilt binaries:

1. 访问https://github.com/EOSIO/eos/tags网址，选择用户需安装的EOSIO版本。

2. 下拉列表`Release Notes`选取，并下载适用于用户操作系统的软件包或归档文件。 

3. 参照上述命令，在指定操作系统上安装预先构建版本
