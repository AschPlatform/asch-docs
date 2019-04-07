
# 5分钟开发ASCH智能合约

阿希智能合约平台是基于ASCH链的轻量级DApp解决方案，使用Typescript作为智能合约语言，以Node.js为运行环境的全新智能合约平台。平台以安全、高效、易用、低成本为目标，帮助传统开发人员快速掌握区块链DApp开发。

## 1. 开发环境搭建

阿希智能合约平台要求的Node.js版本为v10，推荐安装最新LTS版本(目前为v10.15.1)

### 1.1. 智能合约开发工具安装

智能合约平台开发使用[vscode](https://code.visualstudio.com/)作为开发环境，请提前安装好 Node.js 和vscode。

`create-asch-contract`是一个交互式一键生成智能合约vscode项目模板的工具，请在准备好的智能合约开发目录中运行下述命令安装。（注：部分网络服务商在安装npm包时可能会有较大延时甚至失败的可能，请耐心重试）

```sh
npm i create-asch-contract -g
create-asch-contract
cd [my-asch-contract] && npm test
```

### 1.2. 本地全节点安装

我们建议开发者安装本地合约运行环境[请参见链接](../../install/zh-cn.md)，对智能合约进行本地测试。由于目前testnet属于测试阶段，请通过源码方式安装本地测试节点，并手动安装npm包。如不选择搭建本地开发环境

```sh
git clone https://github.com/AschPlatform/asch/tree/v1.5.0-beta
cd asch
npm install

#手动创建相关目录
mkdir chains
mkdir -p data/contracts
mkdir -p public/dist
```

## 2. 编写智能合约

如前所述，智能合约使用的是Typescript作为合约开发语言。它是Javascript基础上增加了静态类型的超级，与主流语言特性接近。大部分开发人员可以很快掌握[请参见智能合约开发入门](../introduction/zh-cn.md)。我们下面看一个最简单的智能合约：



## 3. 对合约进行测试

### 3.1. 模拟测试

根据智能合约的逻辑编写测试用例进行测试，参考合约模板自带的Demo的所自带的测试用例

### 3.2. 在本地节点上进行测试

由于模拟测试是在普通的Node.js环境中，通过moke的方法对合约逻辑进行测试。不是在合约的VM中运行，不能代表实际的合约运行情况，故需要将合约部署到本地节点上进行测试(部署方法见第4节)。

--TODO: 使用asch-web调用合约


## 4. 在区块链上部署智能合约

使用ASCH自带的客户端环境，或使用测试网的网页客户端，找到`智能合约->我发布的合约`，单击`提交新合约`。填写智能合约名称、智能合约代码、合约描述、gasLimit以及是否优先消耗合约创建者的能量等参数，单击`提交合约`进行提交。

如果提交失败系统会提示错误信息，提交成功后，稍后会在`我发布的合约`中看到刚提交的合约。

## 5. 更多

诚然，实际的智能合约开发内容比本文档中描述的复杂。智能合约开发过程中也有一些注意事项与语法约定。具体请参考 [ASCH智能合约开发入门](../introduction/zh-cn.md)和[ASCH智能合约开发实战](../contract-in-action/zh-cn.md)