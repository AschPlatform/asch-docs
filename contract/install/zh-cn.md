# 智能合约开发环境安装

ASCH智能合约支持在MacOS、Ubuntu、和Windows三种平台下进行开发。基本安装步骤如下：

- 安装基础依赖环境
- 安装VSCode及相关插件
- 安装ASCH智能合约开发工具
- 安装本地节点（可选）

由于ASCH智能合约开发环境基于Node.js及VSCode为搭建，除了基础依赖环境与系统平台相关外其余部分在不同平台上类似。故基础依赖环境分系统介绍，其余部分统一介绍。

## 1. 安装基础依赖环境

基础依赖环境主要包括：包管理工具(MacOS和Ubuntu)、Node版本管理工具(nvm)、Node.js 及 npm、node-gyp 以及C++编译所依赖的工具，下面分平台进行介绍。

### 1.1. Windows环境

支持Windows 8.1以上版本的Windows操作系统。以下操作在 Win10 x64 简体中文专业版 （版本 1809 17763.194）上验证通过

- **安装 nvm-windows**

目前最新版为v1.1.7[下载地址](https://github.com/coreybutler/nvm-windows/releases/download/1.1.7/nvm-setup.zip)

[安装参考](https://blog.csdn.net/sinat_38334334/article/details/80013648)
**注意使用管理员权限安装，否则安装node后可能无法在命令行中直接运行**

- **安装 node v10.14.1**

以管理员权限在命令行中运行下面的命令

```sh
#安装
nvm install 10.14.1

#使用10.14.1版本
nvm use 10.14.1

#验证安装是否成功
node -v

#应该输出
v10.14.1

 ```

**在Windows环境中如使用10.15.x版，可能会导致ASCH合约开发工具安装失败**

- **安装 node-gyp 及 C++编译工具**

以管理员权限运行下面的命令

```sh
#安装 node-gyp
npm i -g node-gyp

#如果安装过程非常慢，请尝试
npm i -g node-gyp --registry=https://registry.npm.taobao.org

#安装 C++编译工具
npm install --global --production windows-build-tools --vs2015
```

**注意，C++编译工具安装比较费时，视网络情况不同约需要2-4小时**

- **配置 node-gyp 编译参数**

```sh
#使用 vs2015版的Visual Studio项目文件格式
npm config set msvs_version 2015
```

### 1.2. MacOS环境

以下操作在MacOS 10.14.4上验证通过

- **安装 Homebrew**

Homebrew 是 macOS 平台的软件包管理器，相当于 Linux 常用的 apt-get。首先请确保已经安装XCode，如未安装，直接在AppStore中安装即可。

```sh
# 安装
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

#验证
brew -v

#安装成功则显示版本信息，例如：
Homebrew 1.9.1
Homebrew/homebrew-core (git revision 46a29; last commit 2019-04-12)
Homebrew/homebrew-cask (git revision 5ed4f; last commit 2019-04-12)

```

- **安装 nvm 和 Node.js v10.15.1**

```sh
#安装nvm
brew insall nvm

#安装Node.js v10.15.1
nvm install v10.15.1

#切换默认版本
nvm use 10.15.1

#验证
node -v

#成功则输出
v10.15.1

```

- **安装 node-gyp 及 C++编译工具**

```sh
#安装相关编译工具
brew install libtool autoconf automake

#安装 node-gyp
npm i -g node-gyp

#如果安装过程非常慢，请尝试
npm i -g node-gyp --registry=https://registry.npm.taobao.org
```

### 1.3. Ubuntu环境

支持Ubuntu14.04以上版本，以下安装在Ubuntu 16.04上验证通过

- **安装系统工具库**

```sh

#安装系统依赖包
sudo apt-get install curl ntp wget git libssl-dev openssl make gcc g++ autoconf automake python build-essential -y

#Ubuntu 14.04请运行
sudo apt-get install libtool -y

# Ubuntu 16.04请运行
sudo apt-get install libtool libtool-bin -y
```

- **安装nvm 和 Node.js v10.15.1**

```sh
#安装 nvm
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash

#安装Node.js v10.15.1
nvm install v10.15.1

#验证
node --v

#应该输出
v10.15.1

```

- **安装 node-gyp**

```sh
#安装 node-gyp
npm i -g node-gyp

#如果安装过程非常慢，请尝试
npm i -g node-gyp --registry=https://registry.npm.taobao.org
```

## 2. 安装VSCode及相关插件

请访问 [VSCode官网](https://code.visualstudio.com/)，安装最新版VSCode。

推荐安装 `tslint`、`typescript`、`jest`等常用插件

## 3. 安装ASCH智能合约开发工具

**在Windows环境中请使用管理员权限的命令行工具**

```sh
#安装合约开发模板生成工具，
npm i create-asch-contract -g

#如果安装过程非常慢，请尝试
npm i create-asch-contract -g --registry=https://registry.npm.taobao.org
```

## 4. 安装本地节点（可选）

请参考[节点安装](../../install/zh-cn.md)中的相关内容