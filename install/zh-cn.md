# Asch 节点安装文档

   * [Asch 节点安装文档](#asch-节点安装文档)
      * [一、系统环境和依赖](#一系统环境和依赖)
         * [1.1 系统要求](#11-系统要求)
         * [1.2 系统依赖安装](#12-系统依赖安装)
         * [1.3 Node.js 安装](#13-nodejs-安装)
      * [二、Asch Mainnet 节点安装](#二asch-mainnet-节点安装)
         * [2.1 下载安装包并解压](#21-下载安装包并解压)
         * [2.2 修改config.json](#22-修改configjson)
         * [2.3 下载数据库快照并解压替换](#23-下载数据库快照并解压替换)
         * [2.4 启动节点，监听区块同步情况](#24-启动节点监听区块同步情况)
      * [三、Asch Testnet 节点安装](#三asch-testnet-节点安装)
         * [3.1 下载安装包并解压](#31-下载安装包并解压)
         * [3.2 修改config.json](#32-修改configjson)
         * [3.3 下载数据库快照并解压替换](#33-下载数据库快照并解压替换)
         * [3.4 启动节点，监听区块同步情况](#34-启动节点监听区块同步情况)
      * [四、Asch Localnet 节点安装](#四asch-localnet-节点安装)
         * [4.1 下载安装包并解压](#41-下载安装包并解压)
         * [4.2 修改config.json](#42-修改configjson)
         * [4.3 启动节点，监听区块同步情况](#43-启动节点监听区块同步情况)
         * [4.4 创世账户](#44-创世账户)
      * [五、源码安装](#五源码安装)
         * [5.1 克隆源码到本地](#51-克隆源码到本地)
         * [5.2 安装依赖](#52-安装依赖)
         * [5.3 修改 app.js](#53-修改-appjs)
         * [5.4 覆盖config.json](#54-覆盖configjson)
         * [5.5 创建依赖目录](#55-创建依赖目录)
         * [5.6 配置网页客户端](#56-配置网页客户端)
         * [5.7 下载快照并解压](#57-下载快照并解压)
         * [5.8 启动节点](#58-启动节点)
      * [六、常见错误处理](#六常见错误处理)
         * [6.1 网页客户端无法访问](#61-网页客户端无法访问)
         * [6.2 受托人节点无法生产区块](#62-受托人节点无法生产区块)
         * [6.3 无法同步区块(卡块)](#63-无法同步区块卡块)
      * [七、节点升级](#七节点升级)
      * [八、常用命令](#八常用命令)
      * [九、受托人配置](#九受托人配置)

## 一、系统环境和依赖

### 1.1 系统要求

- 必须是linux系统，使用 Ubuntu 14.04 以上的64位系统，推荐使用 Ubuntu 16.04以上版本系统
- 必须有公网ip
- 建议4核以上CPU，主频不低于2G
- 建议内存8G以上
- 建议公网带宽5Mb以上
- 建议可用空间32GB以上的SSD硬盘

### 1.2 系统依赖安装

```sh
# Install dependency package
sudo apt-get install curl ntp wget git libssl-dev openssl make gcc g++ autoconf automake python build-essential -y
# libsodium for ubuntu 14.04
sudo apt-get install libtool -y
# libsodium for ubuntu 16.04
sudo apt-get install libtool libtool-bin -y
```

### 1.3 Node.js 安装

ASCH v1.5基于Node.js v10.14开发，**最低要求为v10.14**(推荐使用当前最新LTS版本：v10.15.1)。在安装 node.js 时一定要注意版本是否符合要求。建议使用 nvm 管理版本。

```sh
# Install nvm
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash

# This loads nvm
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# Install node and npm for current user.
nvm install v10

# check node version and it should be v10.x.x
node --version
```

## 二、Asch Mainnet 节点安装

Mainnet 默认端口为8192， P2P 端口为8193。如果开启了防火墙，请确保放行此两个端口的出入数据（TCP协议）

### 2.1 下载安装包并解压

```sh
wget http://china.aschcdn.com/asch-linux-latest-mainnet.tar.gz
tar zxvf asch-linux-latest-mainnet.tar.gz
cd asch-linux-1.4.2-mainnet // 不同版本的安装包解压出来的目录名不同，此处为1.4.2
```

### 2.2 修改config.json

```sh
vim config.json

#修改 publicIp 为自己服务器的公网 IP
```

### 2.3 下载数据库快照并解压替换

主网数据库较大，不建议从头开始同步。可以下载数据库快照，直接解压后替换 asch 目录下的 data 目录。

```sh
wget http://china.aschcdn.com/blockchain-mainnet-snapshot.tar.gz
tar zvxf blockchain-mainnet-snapshot.tar.gz
```

### 2.4 启动节点，监听区块同步情况

执行
`./aschd start`

此时可以监听日志(位于logs/debug.yyyyMMdd.log)查看日志信息或者通过接口 `http://yourip:8192/api/blocks/getHeight`来查看区块高度是否增长。

## 三、Asch Testnet 节点安装

Testnet 默认端口为4096， P2P 端口为4097。如果修改了端口，请两者一并修改，P2P 端口 = 默认端口 + 1

### 3.1 下载安装包并解压

```sh
wget http://china.aschcdn.com/asch-linux-latest-testnet.tar.gz
tar zxvf asch-linux-latest-testnet.tar.gz
cd asch-linux-1.5.0-testnet // 不同版本的安装包解压出来的目录名不同，此处为1.5.0
```

### 3.2 修改config.json

```sh
vim config.json

#修改 publicIp 为自己服务器的公网 IP
```

### 3.3 下载数据库快照并解压替换

主网数据库较大，不建议从头开始同步。可以下载数据库快照，直接解压后替换 asch 目录下的 data 目录。

```sh
wget http://china.aschcdn.com/blockchain-testnet-snapshot.tar.gz
tar zvxf blockchain-testnet-snapshot.tar.gz
```

### 3.4 启动节点，监听区块同步情况

执行
`./aschd start`

此时可以监听日志(logs/debug.2018xxxx.log)或者通过接口 `http://yourip:4096/api/blocks/getHeight`来查看区块高度是否增长。

## 四、Asch Localnet 节点安装

Localnet 默认端口为4096， P2P 端口为4097。如果修改了端口，请两者一并修改，P2P 端口 = 默认端口 + 1

### 4.1 下载安装包并解压

```sh
wget http://china.aschcdn.com/asch-linux-latest-localnet.tar.gz
tar zxvf asch-linux-latest-localnet.tar.gz
#不同版本的安装包解压出来的目录名不同，此处为1.4.2
cd asch-linux-1.4.2-localnet 
```

### 4.2 修改config.json 

```sh
vim config.json

# 修改 publicIp 为自己服务器的公网 IP 或局域网 IP
```

### 4.3 启动节点，监听区块同步情况

执行
`./aschd start`

此时可以监听日志(logs/debug.2018xxxx.log)或者通过接口 `http://yourip:4096/api/blocks/getHeight`来查看区块高度是否增长。

### 4.4 创世账户

在 localnet 里，创世账户会有1亿个初始 XAS。创世账户主密码为：

`stone elephant caught wrong spend traffic success fetch inside blush virtual element`

## 五、源码安装

下面以安装 Mainnet 为例，演示如何通过源码安装 Mainnet 节点，请在安装前确保[系统环境和依赖](#一系统环境和依赖)安装完成

### 5.1 克隆源码到本地

```sh
git clone https://github.com/AschPlatform/asch
```

### 5.2 安装依赖

```sh
npm install
```

**备注**： 此处依赖较多，可能需要较长时间

### 5.3 修改 app.js

```javascript
//搜索testnet,修改为 mainnet。修改后的结果如下：
appConfig.netVersion = process.env.NET_VERSION || 'mainnet'
```

### 5.4 覆盖config.json

默认的config.json 是用于 localnet 调试，Mainnet 需要修改。

```sh
cp config-mainnet.json config.json
```

修改 config.json 里的 publicIp 字段为自己服务器的 IP 地址。

### 5.5 创建依赖目录

```sh
mkdir -p public/dist
mkdir -p data/contracts
mkdir chains
```

### 5.6 配置网页客户端

```sh
# 下载前端源码
git clone https://github.com/AschPlatform/asch-frontend-2.git
# 安装包管理器yarn
npm install -g yarn
# 安装依赖包
yarn install
# 编译 dev: localnet, test: testnet, pro: mainnet
yarn pro
# 把编译后的结果拷至 asch 主目录下的 public/dist目录中
cp -r dist/spa-mat/* ../asch/src/public/dist
# 详细内容请参考前端项目内的文档
```

### 5.7 下载快照并解压

```sh
cd asch
wget http://47.75.26.122/blockchain-mainnet-snapshot.tar.gz
tar zvxf blockchain-mainnet-snapshot.tar.gz
```

### 5.8 启动节点

```sh
./aschd start
```

## 六、常见错误处理

### 6.1 网页客户端无法访问

网页客户端访问地址为：`http://your_ip:your_port`, Mainnet 端口默认为8192， Testnet 以及 Localnet 默认为 4096.

排查步骤：

1. 查看是否改了config.json里的port字段
2. 查看防火墙是否放行端口
3. 查看节点是否启动，执行命令`./aschd status`, 如果没有启动则显示`Asch server is not running`，此时执行`./aschd start`即可

### 6.2 受托人节点无法生产区块

排查步骤：

1. 从网页客户端查看受托人排名是否进入前21
2. 使用下面的命令搜索错误日志`grep Failed logs/debug.log`,如果出现字样`Failed to get public ip, block forging MAY not work!`说明公网ip没有自动获取到，需要手动配置。
3. 使用下面的命令搜索错误日志`grep error logs/debug.log`如果出现字样`Failed to load delegates: Account xxxxxxxxx not found`。说明你配置的账户密钥还没有注册成为受托人，或者注册成为受托人之前就启动了服务，这时重启服务即可

**注意** 如果你的节点正在同步区块，不要立即重启，等同步完成了再重启

```sh
./aschd restart
```

正常情况下应该会出现如下log

```sh
grep Forging logs/debug.log

#Forging enabled on account: xxxxxxxxxxxxxx
```

### 6.3 无法同步区块(卡块)

对比自己节点区块高度和最新区块高度。[最新区块高度](https://wallet.asch.cn/api/blocks/getHeight)。 如果发现自己节点的高度一直落后且不增长，可以断定为自己的节点没有同步区块。

解决方法：

1. 升级到最新版本并重启

```sh
./aschd upgrade
./aschd start
```

2. 重建

```sh
./aschd rebuild
```

## 七、节点升级

在安装完节点以后，后续节点的升级可以通过简单的`./aschd upgrade`来完成，不必重复安装。

进入 asch 目录执行命令：

```sh
./aschd upgrade
./aschd start
```

## 八、常用命令

```sh
# 启动节点
./aschd start

# 停止节点
./aschd stop

# 查看节点运行状态
./aschd status

# 重启节点
./aschd restart

# 升级节点
./aschd upgrade

# 重新同步区块
./aschd rebuild

# 查看节点版本
./aschd version

# 开启区块生产（仅供受托人使用）
./aschd enable "your sercret"

# 查看log
tail -f logs/debug.201xxxxx.log
```

## 九、受托人配置

使用文本编辑工具（比如 vim）打开config.json, 找到secret字段，将你的受托人主密码填进去即可，该字段为 json 字符串数组，一台机器可以配置多个，但不能重复。

**注意** 不管运行了几个节点，请不要重复配置相同的受托人主密码

执行以下命令：

```sh
# 重启节点
./aschd restart

# 打开生产区块开关
./aschd enable "your sercret"
```
