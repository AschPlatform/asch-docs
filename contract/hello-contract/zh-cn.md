
# 5分钟开发ASCH智能合约

阿希智能合约平台是基于ASCH链的轻量级DApp解决方案，使用Typescript作为智能合约语言，以Node.js为运行环境的全新智能合约平台。平台以安全、高效、易用、低成本为目标，帮助传统开发人员快速掌握区块链DApp开发。

## 1. 开发环境搭建

阿希智能合约平台要求的Node.js版本不低于v10.14，推荐安装最新LTS版本(MacOS和Ubuntu环境推荐使用v10.15.1，Windows环境请使用v10.14.1)

### 1.1. 智能合约开发工具安装

智能合约平台开发使用[vscode](https://code.visualstudio.com/)作为开发环境，请提前安装好 Node.js 和vscode。

`create-asch-contract`是一个交互式一键生成智能合约vscode项目模板的工具，请在准备好的智能合约开发目录中运行下述命令安装。（注：部分网络服务商在安装npm包时可能会有较大延时甚至失败的可能，请耐心重试）

```sh
npm i create-asch-contract -g
create-asch-contract init my-asch-contract
cd [my-asch-contract] && npm test
```

### 1.2. 本地全节点安装

开发者可以安装本地合约运行环境[请参见节点安装](../../install/zh-cn.md)，对智能合约进行本地测试。由于目前testnet属于测试阶段，请通过源码方式安装本地测试节点，并手动安装npm包。

```sh
git clone https://github.com/AschPlatform/asch

cd asch
git checkout develop
git pull

npm install

#手动创建相关目录
mkdir chains
mkdir -p data/contracts
mkdir -p public/dist
```

详细开发环境搭建请见[智能合约开发环境安装](../install/zh-cn.md)

## 2. 编写智能合约

如前所述，智能合约使用的是Typescript作为合约开发语言。它是Javascript基础上增加了静态类型的超级，与主流语言特性接近。大部分开发人员可以很快掌握[语法参见智能合约开发入门](../introduction/zh-cn.md)。我们下面看一个最简单的智能合约：

```typescript
const CURRENCY = 'XAS'

class Payment {
  address: string
  amount: bigint

  constructor(address: string, amount: bigint) {
    this.address = address
    this.amount = amount
  }
}

export class HelloContract extends AschContract {
  private total: bigint
  private payments: Vector<Payment>

  constructor() {
    super()
    this.total = BigInt(0)
    this.payments = new Vector<Payment>()
  }

  @payable({ isDefault: true })
  onPay(amount: bigint, currency: string) {
    assert(amount > 0, `Amount should greater than 0`)
    assert(currency === CURRENCY, `Please pay ${CURRENCY}`)

    this.total += amount
    const payment = new Payment(this.context.senderAddress, amount)
    this.payments.push(payment)
  }

  @constant
  getPayTimes(): number {
    return this.payments.size()
  }

  @constant
  getTotal(): bigint {
    return this.total
  }
}
```

上述合约非常简单，先定义了一个合约状态的类型`Payment`，用于保存合约的状态。
然后实现了一个合约类`HelloContract`，包括：

- `total`和`payments`两个状态，分别存储总余额和转账历史
- `onPay`方法，通过`@payable`注解进行修饰，表示当合约默认接收转账的处理方法。该方法只是简单记录下转账的地址和金额，同时更新合约账户总余额
- `@constant`注解修饰的两个方法，用于查询合约内部状态。

## 3. 对合约进行调试与测试

### 3.1. 合约代码模拟调试

#### 3.1.1. 通过jest-runner插件进行调试

  1. 安装 [Jest Runner](https://marketplace.visualstudio.com/items?itemName=firsttris.vscode-jest-runner)
  2. 在 __tests__/SimpleContract.test.ts 某个 it 测试里添加断点，右键选择「Debug Jest」

#### 3.1.2. 设置vscode的调试配置

  1. 自己编写 test.ts，引入 mock.ts 和 SimpleContract.ts
  2. 设置 .vscode/launch.json 如下：

  ```json
  {
    "version": "0.2.0",
    "configurations": [
      {
        "type": "node",
        "request": "launch",
        "name": "Test Contract",
        "args": [
          "-r",
          "${workspaceFolder}/node_modules/ts-node/register",
          "${workspaceFolder}/test.ts"
        ]
      }
    ]
  }
  ```

  3. 在 SimpleContract.ts 添加断点
  4. 启动调试

### 3.2. 合约测试

### 3.2.1. 合约模拟单元测试

请参考模板项目中的示例测试代码编写单元测试用例，通过测试工具进行单元测试。

### 3.2.2. 在本地节点上进行测试

由于模拟测试是在普通的Node.js环境中，通过moke的方法对合约逻辑进行测试。不是在合约的VM中运行，不能代表实际的合约运行情况，故需要将合约部署到本地节点上进行测试(部署方法见第4节)。

可以通过[智能合约查询接口](../../http-api/zh-cn.md#212-智能合约)、[智能合约交易接口](../../http-api/zh-cn.md#37-智能合约)或[asch-web](../../asch-web/zh-cn.md)提供的方法实现合约注册、向合约转账、调用合约方法以及访问合约中的状态，测试合约在区块链上的运行效果。

## 4. 在区块链上部署智能合约

目前可以通过下面几种方法部署智能合约：

- 使用ASCH平台的Web客户端界面操作注册合约

使用ASCH自带的客户端环境，或使用测试网的网页客户端，找到`智能合约->我发布的合约`，单击`提交新合约`。填写智能合约名称、智能合约代码、合约描述、gasLimit以及是否优先消耗合约创建者的能量等参数，单击`提交合约`进行提交。

如果提交失败系统会提示错误信息，提交成功后，稍后会在`我发布的合约`中看到刚提交的合约。

- 使用HTTP接口注册合约

通过[智能合约交易接口](../../http-api/zh-cn.md#371-注册智能合约)提交交易的方式来注册合约

## 5. 访问智能合约

可以通过接口

### 5.1. 状态查询

- 简单合约状态查询

简单类型的公开合约状态可直接通过HTTP接口进行查询。请参见[查询智能合约公开状态](../../http-api/zh-cn.md#2125-查询智能合约公开状态)

- 通过查询方法查询

查询方法指用`@constant`注解修饰的方法，对合约的状态只可以只读访问。但可以实现一些查询的逻辑。查询方法可以通过HTTP接口进行访问。请参见[调用查询方法](../../http-api/zh-cn.md#2127-调用查询方法)

### 5.2. 调用合约方法

合约类中的除`constructor`外的所有没有注解修饰的公开方法都是外部可调用方法，通过ASCH链类型为`601`的交易实现调用。请参见[调用智能合约](../../http-api/zh-cn.md#372-调用智能合约)

### 5.1. 向合约转账

合约类中使用`@payable`修饰的方法为接收资产转账的方法，资产接收方法通过ASCH链类型为`602`的交易实现调用。请参见[向合约转账](../../http-api/zh-cn.md#373-向智能合约转账)

## 6. 进一步阅读

诚然，实际的智能合约开发内容比本文档中描述的复杂。智能合约开发过程中也有一些注意事项与语法约定。更多文档请参考：

- [ASCH智能合约开发概述](../introduction/zh-cn.md)
- [ASCH智能合约开发实战](../contract-in-action/README.md)
- [Gas与内置函数](../contract-in-action/5.1%20附录一：燃料计费表和智能合约内置函数.md)
- [asch-web使用指南](../../asch-web/zh-cn.md)