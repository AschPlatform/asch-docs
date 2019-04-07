# ASCH智能合约开发入门

## 1. 概述

### 1.1. 设计目标

ASCH智能合约平台致力于成为一个开发者可以快速上手的安全、高效的智能合约开发和运行平台

- 智能合约容易学习、容易编写、容易验证
- 合约语言必须是图灵完备的，合约运行必须是在有限有的时间内可停止的
- 合约的运行环境是安全的，恶意合约不会对其他合约乃至于整个区块链造成破坏性的影响
- 设计上要灵活，易于扩展，便于将来增加新的特性

### 1.2. 设计理念及约束  

- 安全稳定是第一要素，安全与易用发生矛盾时，安全为先
- 简化合约的编写，通过工具、规范、样例等帮助发人员减少开发中的bug
- 合约运行在基于Node.js的运行环境中
- 优先使用现有的编程语言作为合约语言，而不是设计一个新语言；充分利用语言本身的特性实现合约，减少开发人员的学习成本
- 智能合约应当是在有限的时间内可停止的，并基于使用资源进行计费(消耗的CPU、内存及存储资源)
- 智能合约应该是相对简单的逻辑的轻量级DApp，业务规则过于复杂的DApp使用侧/平行链来实现

### 1.3. 技术选型

#### 1.3.1. 隔离的合约执行进程和存储

基于安全性的考虑，合约代码执行运行在与ASCH链相隔离的独立进程中，虽然带来了引擎本身的复杂度，但好处是明显的。智能合约的恶意代码不会造成ASCH链的数据，修改合约状态只能通过指定的交易才可以实现，恶意代码也难以通过接口直接非法篡改合约状态。同时每个合约也运行在独立的Sandbox中，合约代码无法修改其他合约的状态。

#### 1.3.2. 基于Typescript子集的合约语言

- 不设计新的合约语言

智能合约语言的选择首先要做的决策是设计一门全新的智能合约语言(例如：以太坊的Solidity)还是使用一个现有的语言(例如：以太坊的Vyper)。由于智能合约是一种DSL，理论上来说设计一个新语言是最合适的方式。但设计一个新语言不仅周期长、实现风险高，更重要的是对开发人员来说学习和迁移成本更高。而且设计一个全新的语言同时还需要一个全新的运行环境，可能会引入大量的bug。  
另一方面从语言本身来说，现在流行的主流语言特性是趋同的。基于上述两方面原因，ASCH智能合约平台选择使用已有的成熟语言，而不是设计一个新的合约语言(正因为上述原因，以太坊平台上的新的智能合约语言Vyper是基于Python的)。

- 不支持多语言

对开发人员来说，选择语言需要同时考虑和语言相关的框架、类库等生态。而在智能合约平台中，提供的类库等工具是一样的；支持多语言只是语法上的差别，对实际开发影响并不大。故ASCH智能合约平台暂不支持多语言。

- 不使用WebAssembly

WebAssembly是目前呼声很高的智能合约中间语言，理论上支持使用多种语言编写然后编译成WebAssembly在引擎中运行。WebAssembly相对原生Javascript来说是一种执行效率更高的方案。通过调研我们发现：目前相对成熟的是Rust和C++语言编译成WebAssembly，其他语言的WebAssembly环境中的配套工具严重匮乏，会导致合约编写困难；而Rust和C++对于开发人员来说门槛高、不友好。所以我们选择了Typescript作为合约编写语言编译成Javascript在Node.js引擎环境中运行。在WebAssembly环境成熟后，可以将合约编译成WebAssembly在Node.js中运行，开发人员不需要对合约进行调整。

- 使用Typescript语言作为合约编写语言

TypeScript是一种由微软开发的自由和开源的编程语言，它是JavaScript的一个超集，由实现了静态类型和基于类的面向对象编程。由Anders Hejlsberg设计(他同时还是Delphi和.NET平台的设计师)，Typescript借鉴了许多C#、Java等现代语言的优点，相对Javascript来说具有更为安全、更完善的工具支持、代码更易维护的特点。很多的流行的框架(如：AngularJS、ReactJS、Vue等)都基于Typescript开发。ASCH智能合约平台使用Typescript语言作为智能合约编写语言可以实现对合约代码的有效性检查、减少智能合约编写过程中的bug，通过开发工具的智能提示提升开发效率。

#### 1.3.3. 完全自动的状态管理

合约状态管理是智能合约引擎中一个重要的部分，部分平台的做法是提供底层的持久化接口给开发人员自己手动管理状态，但让开发人员需要关注持久化的细节，这样就增加了不必要的复杂性。在ASCH智能合约中状态的持久化是透明的、自动完成的，开发人员只需要对状态变量进行赋值即可，不需要考虑持久化的细节。这样让开发人员把注意力集中在合约的逻辑本身上，降低合约的开发难度，提高合约代码的可理解和可维护性。

## 2. 智能合约语言

### 2.1. 智能合约语法

ASCH智能合约语言是[Typescript语言](http://www.typescriptlang.org/docs/home.html)的子集，下面是一个简单的例子：

#### 2.1.1. 一个简单智能合约样例

```typescript
const CURRENCY = 'XAS'
const EMPTY_ADDRESS = ''
const MAX_AMOUNT = BigInt(1000 * (10 ** 8))

// 自定义状态类型
class PayState {
  // 转账次数
  payTimes: number
  // 转账总额
  amount: bigint
  constructor() {
    this.payTimes = 0
    this.amount = BigInt(0)
  }
}

// 数据接口类型
interface MaxAmountInfo {
  address?: string
  amount?: bigint
  payTimes?: number
}

// 合约类
export class TestContract extends AschContract {
  // 合约收到的转账, 公开属性
  payStateOfAddress: Mapping<PayState>
  
  // 最大转账的地址，私有状态，外部不可查询
  private maxAmountAddress = EMPTY_ADDRESS
  // 收到的转账总额
  private total = BigInt(0)

  // 初始化方法
  constructor() {
    super()
    this.payStateOfAddress = new Mapping<PayState>()
    this.total = BigInt(0)
  }

  // 默认向合约转账自动调用的方法
  @payable({ isDefault : true })
  onPay(amount: bigint, currency: string) {  
    assert( currency === AVAIBLE_CURRENCY, `Support ${CURRENCY} only` )
    assert( amount > 0 && amount < MAX_AMOUNT , `Amount should greater than 0 and less than ${MAX_AMOUNT}`)

    const address = this.context.senderAddress
    const newAmount = this.payXAS(amount, address)
    if (this.getMaxAmount() < newAmount) {
      this.maxAmountAddress = address
    }
  }

  @constant
  getMaxInfo(): MaxAmountInfo {
    const address = this.maxAmountAddress
    if (address === EMPTY_ADDRESS) return { }

    const { payTimes, amount } = this.payStateOfAddress[address]!
    return { address, payTimes, amount }
  }

  @constant
  getTotal(): bigint {
    return this.total
  }

  // 内部方法，外部不可访问（下同）
  private payXAS(amount: bigint, address: string) : bigint {
    let payState = this.payStateOfAddress[address]
    if (!payState) {
      payState = new PayState()
      this.payStateOfAddress[address] = payState
    }

    payState.payTimes += 1
    payState.amount += amount
    this.total += amount

    return payState.amount
  }

  private getMaxAmount() : bigint {
    return (this.maxAmountAddress === EMPTY_ADDRESS) ?
      BigInt(0) :
      this.getPayInfo(this.maxAmountAddress).amount
  }

  private getPayInfo(address: string) : PayState {
    return this.payStateOfAddress[address] || new PayState()
  }
}
```

上述合约代码实现了一个简单的智能合约，这个合约的功能是接收转账并记录下转账人转账次数和转账总额，同时记录下最大的转账人地址。熟悉Typescript/Javascript/C#/Java等语言的开发者可以会发现读起来几乎没有障碍，非常容易理解。下面我们来详细了解一下这个合约的结构和约定：

#### 2.1.2. 合约结构

通过上面的代码我们可以看到，一个标准的智能合约包括四大部分：  

- **常量**
- **数据接口**
- **状态类**
- **合约类**  

##### 2.1.2.1. 常量定义

一个合约文件中可以有多个常量声明，使用`const`关键字声明，需要注意的是：**常量只能使用四种简单类型**(`string`、`number`、`bigint`、`boolean`)，其他类型包括`object`,`any`等都不支持，例：

```typescript
const DEFAULT_NAME = 'name'
const DEFAULT_INTEVEL = 3 * 1000
```

##### 2.1.2.2. 数据接口定义

一个合约文件中可以有多个数据接口类型声明，数据接口类型**用于公开方法的参数及返回值**，使用`interface`关键字声明，限制如下：

- 成员只能使用简单类型、`Array`、数据接口类型，成员可以是可选的(使用`?`语法声明)
- 不支持联合类型(如`string & number`和`string | number`)
- 如果成员是`Array`，必须指定泛型参数。泛型类型可以是简单类型、`Array`、数据接口类型，泛型类型参数如果本身不是泛型推荐使用简写形式(如：`names: string[]`)
- 数据接口类型的嵌套深度不能超过 3
- 数据接口类型不可以使用泛型定义(不支持`inteface Data<T> {...}`)
- 不支持只读成员(不支持`readonly`)
- 不支持索引访问器

示例：

```typescript
interface AddressInfo {
  province: string
  city: string
  street: string
}

interface PersonInfo {
  name: string
  age?: number
  sex: boolean
  address: Address
}

interface PeopleResultInfo {
  count: number
  pepole: PersonInfo[]
}
```

##### 2.1.2.1. 状态类定义

一个合约文件中可以有多个状态类型声明，**状态类型用于合约状态**，类似于传统的`POJO`使用`class`关键字声明，限制如下：

- 成员只能属性定义或构造函数，属性可以使用简单类型、状态容器、状态类型
  - 状态容器指`Mapping<T>`(类似于`Map<stirng,T>`)或`Vecotr<T>`(类似于`Array<T>`)，状态容器中的数据会自动持久化
- 成员可以是可选的(使用`?`语法定义)，可以初始化默认值。除可选成员外的所有成员属性必须通过默认值或构造器初始化
- 只支持实例成员(不支持`static`)且可见性为公开(`public`可省略)，不支持`private`, `protected`
- 如果成员是状态容器，必须指定泛型参数。泛型类型可以是简单类型、状态容器和状态类型
- 状态类型的嵌套深度不能超过 3
- 状态类不可以使用泛型定义(不支持`class StateData<T> {...}`)
- 不能是抽象类(不支持`abstract`)
- 不支持实现接口(不支持`implements`语法)和继承(不支持`extends`语法)
- 不支持索引访问器
- 不支持只读成员(不支持`readonly`)
- 不支持`getter`和`setter`
- 所有非可选成员必须初始化，可以在声明时初始化或在构造函数中初始化
- 可以声明一个公开的构造函数，**状态类构造函数不能产生异常** 由于状态数据需要从数据库中加载，需要通过无参构造函数初始化(所有的参数都为`undefined`，随后再初始化各个成员属性)。引擎在调用构造函数时不能产生异常，否则会导致合约加载失败

示例：

```typescript
class PayState {
  payTimes: number
  amount: bigint

  constructor() {
    this.payTimes =  0
    this.amount = BigInt(0)
  }
}

class PayStateDefault {
  payTimes = 0
  amount = BigInt(0)
}

class PayStateOptional {
  payTimes = 0
  amount?: bigint
}
```

##### 2.1.2.2. 合约类定义

一个合约文件中必须**有且仅有一个**合约类定义，使用`class`关键字定义，合约类必须是`AschContract`的子类。合约类只允许合约状态和方法两类成员，基本要求如下:

- 使用`export`关键字修饰
- 必须从`AschContract`直接继承，不支持多重继承
- 不能是泛型类(不能有泛型参数)
- 不能是抽象类(不支持`abstract`)
- 不支持实现接口(不支持`implements`语法)
- 不支持索引访问器
- 不支持`getter`和`setter`
- 只支持实例成员，不支持静态成员(不支持`static`)

下面来逐个介绍合约中两类成员的具体规范

- **合约状态**
合约状态是可以自动进行持久化的合约成员属性。开发者只需要给合约的成员属性赋值，引擎会自动把这些状态持久化到区块链中，对于合约状态来说：

  - 类型必须是简单类型、状态类型、状态容器之一，
  - 如果成员是状态容器，必须指定泛型参数。泛型类型可以是简单类型、状态容器和状态类型
  - 状态类型的嵌套深度不能超过 3
  - 所有合约状态成员必须初始化，可以在声明时初始化或在构造函数中初始化
  - **状态不可以是可选的**(不可以是`undefined`)
  - 可见性为公开的状态可以通过HTTP接口查询其状态值(见本文后续介绍)，非公开状态不可直接查询(可通过查询方法实现查询)

- **合约方法**  
  合约类中的方法都必须是成员方法(不支持`static`)，不支持异步语法(`Promise`、`async/await`)和生成器语法(`generator`)。可分为以下几类

  - 构造器
  - 可调用方法(可见性为公开的普通方法)
  - 资产接收方法(使用`payable`注解)
  - 查询方法(使用`constant`注解)
  - 内部方法(可见性为非公开的普通方法`private`或`protected`)
  
  下面来逐个介绍具体规则：

  **(a)构造器**

  一个合约只能有一个构造器，是合约类的初始化方法，名称必须为`constructor`，仅在合约注册时执行一次，具体要求如下：

    - 可见性必须是公开
    - 签名必须是`constructor() {...}`，没有参数也没有返回值
    - 可以访问`this.context`
    - **调用构造器不应产生异常，否则合约无法注册成功**
    - **不可以访问`this.transfer`**，否则会产生异常导致合约无法注册(因为合约注册时，合约账户没有任何资产)

  **(b)可调用方法**

  一个合约可以有多个可调用方法，是合约类中可见性为公开的，且没有注解修饰的成员方法，具体要求如下：

  - 可见性必须是公开，否则外部不可访问
  - 每个参数必须声明明确的类型，参数类型必须是简单类型、`Array`、数据接口类型之一
  - 如果成员是`Array`，必须指定泛型参数。泛型类型可以是简单类型、`Array`、数据接口类型，泛型类型参数如果本身不是泛型推荐使用简写形式(如：`names: string[]`)
  - **不支持可选参数、不支持参数默认值，也不支持展开参数(`...args: string[]`)**
  - 返回值类型同参数类型要求相同，**必须明确声明返回值类型，否则返回值无法从外部获取**
  - 可以访问`this.context`和`this.transfer`(如合约账户余额不足，则会失败)

  **(c)资产接收方法**

  一个合约可以多个资产接收方法，资产接收方法是使用`payable`注解的公开方法，用于接收调用转入智能合约的资产，要求如下：

    - 可见性必须是公开
    - 必须有两个参数分别为金额与资产名称，一般采用 amount 和 currency 命名
      - amount 类型为`bigint`
      - currency 类型必须为`string`
    - 可以不声明返回类型，如果声明了返回类型必须`void`
    - 可以访问`this.context`和`this.transfer`(如合约账户余额不足，则会失败)
    - `payable`有一个可选参数，类型为`{ isDefault?: boolean }`，用于表示是否是默认的资产接受方法(使用`@payable({ isDefault: true })`注解)。**一个合约中最多只能有一个默认资产接受方法**

  **(d)查询方法**

  一个合约可以有多个查询方法，资产接收方法是使用`constant`注解的公开方法，用于实现状态查询等只读状态的计算逻辑，具体要求：

    - 可见性必须是公开
    - 必须有返回类型，且必须是简单类型、`Array`、数据接口类型之一
    - **不可访问`this.context`和`this.transfer`，否则会失败**
    - **只能只读访问状态成员，不能修改状态。否则会失败**

  **(e)内部方法**

  一个合约可以有多个内部方法，可见性为保护(`protected`)或私有(`private`，**推荐**)，具体要求：

    - 可见性必须是保护或私有
    - 不可使用`constant`、`payable`注解

#### 2.1.3. 智能合约其他语法约定

智能合约语言是Typescript语言的子集，除上节描述的结构约定外，其他主要限制如下：  

- 不可以使用引入第三方库
- 不支持`Symbol`
- 不使用`null`、`any`、`never`、`object`、`unknown` 等类型，`undefined`可以使用
- 不使用交叉类型(如`string & number`)和联合类型(如`string | null`)作为公开方法的参数或返回类型
- 不支持生成器和异步语法(不使用`Promise`、`async/await`)
- 不使用强制类型转换(不使用`<string>name`及`name as string`)
- 一个合约文件只能有一个合约类，这个类必须从`AschContract`继承而来
- 不可以定义全局函数、静态函数
- 智能合约中只能使用合约引擎提供的内置类型、方法和对象，未提供的原Node.js内置的对象、函数或类型是不可用的(如`Function`、`Date`都是不可用的)
- 私有或保护方法的参数和返回值的定义比较灵活，但请谨慎使用。尽可能避免不确定性
- 合约中不允许使用`try...catch`语法，也不允许使用`throw`语句。任何时候抛出异常(如使用`assert`语句)即导致中止合约
- 可调用方法和查询方法参数和返回值的额外要求
  - 由于合约调用时所有参数会被序列化为`JSON`传递，故只支持可序化的类型(可参考数据接口类的定义)基于效率考虑，全部参数或返回值序列化后的`JSON`字符串长度应控制在`32K`以内(`length <= 32,767`)
  - 查询方法必须声明返回类型，对于可调用方法，如果未声明返回值类型，返回值将被丢弃(不作为调用结果返回)
- 状态类型和数据接口类嵌套深度不超过**3**
  由于状态容器类型的值可以是状态容器类型或合约状态类型，而状态类型中也可以有状态类型或状态容器(数据接口类似)。基于代码可读性以及状态管理的性能考虑。嵌套的深度不应超过3，如`Mapping<bigint>`深度称为 1，`Vector<Mapping<number>>`深度为2；简单自定义类型本身深度为1，包含一个深度为1的容器类型或自定义状态类型深度为2；以此类推
- 注意，**与以太坊的solidity不同**的是，在solidity中，给存储状态赋值会导致自动的复制。而在ASCH智能合约中，状态容器或自定义状态中使用的是对象的引用。这样的好处是性能更好、编程更灵活、更符合主流语言的习惯，但也会带来一个问题：当两个状态容器中保存相同的对象引用时，可能会导致误操作。合约引擎会自动检查这种情况的存在，当尝试把一个已经属于合约状态一部分的对象赋值给合约状态时，会抛出异常。

### 2.2. 内置对象

#### 2.2.1 内置类型

##### 2.2.1.1. 简单类型  

简单类型为`number`、`bigint`、`string`和`boolean`，这四种类型的行为与Javascript/Typescript环境中的行为是一致的。  

##### 2.2.1.2. 状态容器类型(`Mapping`、`Vector`)  

- `Mapping`的行为与以太坊solidity中的`mapping`接近，类似Javascript中的`Object`，是一个可以通过`key`以下标方式来访问的对象容器
- `Vector`的行为与以太坊solidity中的`Array`接近，只可以在最后`push`或`pop`或通过下标(**下标必须0或正整数**)访问的数组
- 状态容器类型包含一个泛型参数，用于指定容器中的值的类型，如`Mapping<bigint>`、`Vector<string>`、`Mapping<User>`。泛型参数可以是简单类型、状态容器类型或状态类型。

##### 2.2.1.3. 其他内置类型

- `AschContract`
  `AschContract`是智能合约类的基类，包括两个重要的成员：`context`属性和`transfer`方法  
  - `context`属性，是合约调用时环境参数信息。包括三个成员：
    - `transaction`对象，包含合约调用的交易相关信息。
    - `block`对象，待打包区块信息。
    - `senderAddress` 属性，调用者的地址。
  - `transfer`方法，原型为：

    ```typescript
    function transfer(toAddress: string, amount: bigint, currency: string): void
    ```  

    该方法可以实现将合约账户的余额转账到指定的账户地址中，该余额记录在Asch链的区块链数据库中，可以通过Asch链接口进行查询。参数信息如下
    - `toAddress` 类型为`string`，接收人地址
    - `amount` 类型为`bigint`，转账金额
    - `currency`类型为`string`，资产名称

- `ArrayBuffer`
  同Node.js中的`ArrayBuffer`
- `BufferView`
  同Node.js中的`BufferView`
- `Array`
  同Node.js中的`Array`

#### 2.2.2. 工具类/函数

- **`assert`函数**，原型为：

```typescript
function assert(condition: boolean, error: string): void
```

该函数合约方法中使用，用来检查合约执行的前置条件是否满足，如条件不满足(`condition === fasle`)会抛出异常，导致合约终止。

- **内置工具类**  
 主要包括如下类与命名空间，除`Crypto`和`util`外，基本与原生功能保持一致：
  - `Array`
  - `ArrayBuffer`
  - `BufferView`
  - `String`
  - `Number`
  - `Object`
  - `Math`
  - `Bigint`
  - `Crypto`  
  - `util`

工具类及函数的详细说明请参见《Gas计费与内置函数》

### 2.3. 编程规范

编写智能合约代码对可读性和安全性要求比普通的程序要高很多，所以编写一个好的智能合约不仅要求语法正确可以正常编译运行。更多需要考虑可维护性、可验证、安全性等问题，应遵循通用的高维护性、高安全性要求的软件开发规范及模式。下述内容是一些相对特殊的约定：

- 使用[契约式开发](https://en.wikipedia.org/wiki/Design_by_contract)的理念来编写合约代码，任何操作之前应检查前置条件是否成立(使用`assert`函数)。所有的前置条件都检验通过再执行逻辑、修改状态。
- 尽管ASCH智能合约平台的每个合约方法的执行是原子的，我们仍然需要遵循先修改状态再调用转账这种顺序来编写代码(代价越高的操作越靠后)。
- ***避免在合约中发行资产，而使用ASCH内置的发行资产功能***。这是ASCH智能合约和以太坊智能合约一个重要的区别。在以太坊中一般在合约中发行资产，状态记录在合约中。而ASCH拥有标准的数字资产发行接口，可以通过图形化的操作快速、安全的发行数字资产；这样发行的数字资产可以用标准的转账接口进行转账，也可以通过区块链浏览器查询相应的交易。如需自己发行的资产实现众筹功能，可参考第4节的众筹合约样例。
- 合约类型可以有一个无参的构造函数(可省略)
  该方法仅在合约初始化时调用一次，一般在此函数中完成合约状态的初始化工作。虽然可以通过普通合约方法配合`context.senderAddress`实现状态的初始化，但使用构造函数的语义更易于理解。
- 可接受转账的方法，原型为

  ```typescript
  @payable({ isDefalut: true })
  function payableMethod(amount: bigint, currency: string): void
  ```

  **注：**`@payable`注解中的参数`{ isDefalut: true }`是可选的(默认是`false`)，上例所示的是默认转账接收函数(向合约转账时不指定接收方法时默认的接收方法)。开发者应在合约中存储转入合约的资产数额，这样可以在合约内部确定合约账户本身的余额，避免在调用`transfer`时导致余额不足而失败。

- 合约对象本身、合约内部状态和内置对象皆是不可扩展的，增加、修改、删除属性会产生异常
- 建议使用内部方法封装低层次的实现细节，外部可访问合约代码中应是统一的高逻辑层次的合约代码
- 一个合约方法应当是易于理解和验证，一般一个合约方法的[循环复杂度](https://en.wikipedia.org/wiki/Cyclomatic_complexity#Definition)应控制在10以内，且有效内容不宜超过15行
- 除合约类外，不使用`export`语句，尽管语法上不会出错
- 不使用`public`，因为缺省可见性为`public`；使用`private`而不是`protected`，因为`private`更语义化
- 合约类的构造函数必须是没有参数的，构造函数用于合约初始化，仅在合约注册时被引擎自动调用。尽管可以使用缺省的构造函数，但最好显式的声明一个
- 尽管智能合约引擎支持复杂状态类型的嵌套，请尽量减少这么做，因为可读性会因些而大大降低
- 智能合约代码应是可读性高、结果确定性高的的代码，避免实现过于灵活的功能。如：在一个众筹合约中，应该在构造函数中初始化众筹的币种、数量、有效期和成功条件等，这些条件不应是动态的
- 涉及数字资产等可能值比较大的数值时，尽可能使用`bigint`,ECMA的标准中采用IEEE-754标准来处理`number`(请参见[ECMA262](http://www.ecma-international.org/ecma-262/6.0/))，存在最大值限制(`Number.MAX_SAFE_INTEGER` = 9,007,199,254,740,991，约 9 X 10^15 )和浮点精度问题(请参见[IEEE754 wiki](https://en.wikipedia.org/wiki/IEEE_754) )

## 3. Gas 计费

对智能合约的计费相关主要包括三个方面，分别是：  

- 合约代码运行所需要的Gas，每一行代码会根据代码的不同进行计费，如：

  ```typescript
  const variable = 200
  ```  

  上述代码是一个声明变量变赋值的语句，需要消耗3个Gas。
- 内置函数所需要消耗的Gas，不同的函数需要消耗的Gas数量不完全相同。
- 存储合约状态(包括合约代码保存)所消耗的存储资源所消耗的Gas。  
  具体计费规则细节请参见《Gas计费与内置函数》。

## 4. 众筹合约样例

### 4.1. 合约功能简介

下面的样例智能合约实现了一个通过自己发行的数字资产(XXT)实现众筹的功能。由于ASCH平台的拥有强大的一键发行数字资产的功能，所以资产发行功能通过ASCH链的在线客户端直接完成，具体资产发行过程请参见[发行数字资产](https://www.asch.io)

### 4.2. 合约代码

```typescript
const SPONSOR = 'SponsorAddress'   //发起人地址
const OFFERING_TOKEN = 'test.XXT'  //众筹得到的Token

interface FundingInfo {
  tokenAmount: bigint
  xasAmount: bigint
  bchAmount: bigint
}

class Funding {
  // 众筹得到的token数量
  tokenAmount: bigint
  // 参与众筹XAS数量
  xasAmount: bigint
  // 参与众筹BCH数量
  bchAmount: bigint
  constructor() {
    this.tokenAmount = BigInt(0)
    this.xasAmount = BigInt(0)
    this.bchAmount = BigInt(0)
  }
}

// 众筹合约类
export class SimpleCrowdFundgingContract extends AschContract {
  // 记录每个地址的众筹信息
  fundingOfAddress: Mapping<Funding> 
  // 兑换比例
  rateOfCurrency: Mapping<bigint>
  // 总可众筹token数量
  totalFundingToken: bigint
  // 剩余可众筹数量
  avalibleTokenAmount: bigint

  // 初始化方法，会在合约注册时被调用
  constructor() {
    super()

    this.rateOfCurrency = new Mapping<bigint>()
    this.rateOfCurrency['XAS'] = BigInt(100)    // 1 XAS = 100 token
    this.rateOfCurrency['BCH'] = BigInt(30000) // 1 BCH = 30000 token

    this.totalFundingToken = BigInt(0)
    this.avalibleTokenAmount = BigInt(0)
    this.fundingOfAddress = new Mapping<Funding>()
  }

  // 发起人初始注入token，只允许注入一次
  @payable
  payInitialToken(amount: bigint, currency: string): void {
    assert(this.context.senderAddress === SPONSOR, `invalid sponsor address`)
    assert(currency === OFFERING_TOKEN, `invalid offering currency, should be ${OFFERING_TOKEN}`)
    assert(this.totalFundingToken === BigInt(0), `initial ${OFFERING_TOKEN} has paied`)

    this.totalFundingToken = amount
    this.avalibleTokenAmount = amount
  }
  
  // 众筹逻辑
  @payable({ isDefault: true })
  crowdFunding(amount: bigint, currency: string) {
    assert(amount >= 0, 'amount must great than 0')
    assert(currency === 'XAS' || currency === 'BCH', `invalid currency '${currency}', please pay XAS or BCH`)
  
    const rate = this.rateOfCurrency[currency]!

    const tokenAmount = amount * rate
    assert(this.avalibleTokenAmount >= tokenAmount, `insuffient ${OFFERING_TOKEN}`)

    this.avalibleTokenAmount = this.avalibleTokenAmount - tokenAmount
    const partnerAddress = this.context!.senderAddress
    this.updateFunding(partnerAddress, amount, currency, tokenAmount)
    // 调用ASCH链转账
    this.transfer(partnerAddress, tokenAmount, OFFERING_TOKEN)
  }
  
  @constant
  getFunding(address: string): FundingInfo {
    return this.fundingOfAddress[address] || new Funding()
  }

  private updateFunding( address: string, amount: bigint, currency: string, tokenAmount: bigint) : void {
    const funding = this.getOrCreateFunding(address)
    funding.tokenAmount += tokenAmount

    if (currency === 'XAS') {
      funding.xasAmount += amount
    }
    else if (currency === 'BCH') {
      funding.bchAmount += amount
    }
  }
  
  private getOrCreateFunding( address: string ) : Funding {
    if (this.fundingOfAddress[address] === undefined) {
      this.fundingOfAddress[address] = new Funding()
    }
    return this.fundingOfAddress[address]!
  }
  
}

```

**注：该合约代码是为了演示ASCH平台上开发智能合约的一样例代码，供ASCH平台开发者学习智能合约的开发，请注意不要用于学习以外的用途。**  

### 4.3. 合约部署和使用

#### 4.3.1. 合约开发环境准备

请参见[5分钟开发ASCH智能合约](../hello-contract/zh-cn.md#1.-开发环境搭建)

#### 4.3.2. 部署合约  

请参见[5分钟开发ASCH智能合约](../hello-contract/zh-cn.md#4.-在区块链上部署智能合约)

#### 4.3.3. 智能合约相关交易接口

请参见

#### 4.3.4. 合约状态查询

- **简单状态查询**

  智能合约中`public`的状态可以通过`HTTP GET`接口进行查询，查询地址为：`{serverAddress}/api/v2/contracts/{contractName}/states/{statePath}`。注意，本接口仅能查询基本类型的数据，复杂类型请通过状态查询函数来查询。
  请参见[查询智能合约公开的状态](../../http-api/zh-cn.md#2125-查询智能合约公开状态)

- **使用查询方法查询状态**
  智能合约中通过`@constant`注解修饰的方法为状态查询函数，状态查函数的返回值应是基本类型、简单自定义类型、基本类型及简单自定义类型构成的数组。且序列化为`JSON`后的字符串长度小于16K
  状态查询函数通过`HTTP POST`接口访问，访问地址为：`{serverAddress}/api/v2/contracts/{contractName}/constant/{method}`
  请参见[使用智能合约查询方法](../../http-api/zh-cn.md#2.12.7-调用查询方法)

## 5. 常见问题  

- **有没有更方便的调用合约和查询状态的方法**
  `asch-web`是对ASCH链上接口的封装，可自动生成合约方法的代理，使用方便。请参见[asch-web使用指南](../../asch-web/zh-cn.md)

- **gas具体是如何计费的**
  gas计费是一个比较复杂的过程，具体计费规则请参见《Gas计费与内置函数》

- **gas计费规则**
  在合约注册时，有参数可以指定是否优先消耗合约开发者的能量，如果设置为优先消耗开发者的能量，则在开发者能量足够的情况下优先使用开发者的能量作为智能合约的消耗；如果未设置或开发者能量不足，则消耗调用者的能量，当调用者的能量不足时，可选择使用`XAS`作为智能合约的能量消耗。目前，`1 XAS (100,000,000wei) = 10,000 GAS`

- **gasLimit是什么，该传入多少？**  
  gasLimit是一次智能合约访问所最大能消耗的Gas数量，Gas用正整数表示。系统限制一次合约调用所能使用的最大gasLimit应小于 10,000,000。

- **我如何知道一次合约调用会消耗多少Gas?**  
  由于合约代码是动态的，无法精确估计具体Gas的数量，需要开发人员准备模拟环境测试。

- **如何知道智能合约调用的结果？**  
  合约调用的返回结果中包含合约是否调用成功，Gas消耗情况等内容。
