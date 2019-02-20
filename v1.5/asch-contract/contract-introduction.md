# ASCH智能合约开发入门

## 1. 概述

### 1.1. 设计目标

ASCH智能合约平台致力于成为一个开发者可以快速上手的安全、高效的智能合约开发和运行平台

- 智能合约容易学习、容易编写、容易验证
- 合约语言必须是图灵完备的，合约运行必须是在有限有的时间内可停止的
- 合约是运行安全的，恶意合约不会对区块链造成破坏性的影响
- 设计灵活性，易于扩展

### 1.2. 设计理念及约束  

- 安全稳定是第一要素，安全与易用发生矛盾时，安全为先
- 简化合约的编写，通过工具、规范、样例等帮助发人员减少开发中的bug
- 使用基于Node.js运行环境运行智能合约
- 优先使用现有的编程语言作为合约语言，而不是设计一个新语言；充分利用语言本身的特性实现合约，减少开发人员的学习成本
- 智能合约应当是在有限的时间内可停止的，并基于使用资源进行计费(消耗的CPU、内存及存储资源)
- 智能合约应该是相对简单的逻辑的轻量级DApp，业务规则过于复杂的DApp使用侧/平行链来实现

### 1.3. 技术选型

#### 1.3.1. 隔离的合约执行进程和存储

基于安全性的考虑，合约代码执行运行在与ASCH链相隔离的独立进程中，虽然带来了引擎本身的复杂度，但好处是明显的。智能合约的恶意代码不会造成ASCH链的数据，修改合约状态只能通过指定的交易才可以实现，恶意代码也难以通过接口直接非法篡改合约状态。同时每个合约也运行在独立的Sandbox中，合约代码无法修改其他合约的状态。

#### 1.3.2. 基于Typescript子集的合约语言

##### 不设计新的合约语言

智能合约语言的选择首先要做的决策是设计一门全新的智能合约语言(例如：以太坊的Solidity)还是使用一个现有的语言(例如：以太坊的Vyper)。由于智能合约是一种DSL，理论上来说设计一个新语言是最合适的方式。但设计一个新语言不仅周期长、实现风险高，更重要的是对开发人员来说学习和迁移成本更高。而且设计一个全新的语言同时还需要一个全新的运行环境，可能会引入大量的bug。  
另一方面从语言本身来说，现在流行的主流语言特性是趋同的。基于上述两方面原因，ASCH智能合约平台选择使用已有的成熟语言，而不是设计一个新的合约语言(正因为上述原因，以太坊平台上的新的智能合约语言Vyper是基于Python的)。

##### 不支持多语言

对开发人员来说，选择语言需要同时考虑和语言相关的框架、类库等生态。而在智能合约平台中，提供的类库等工具是一样的；支持多语言只是语法上的差别，对实际开发影响并不大。故ASCH智能合约平台暂不支持多语言。

##### 不使用WebAssembly

WebAssembly是目前呼声很高的智能合约中间语言，理论上支持使用多种语言编写然后编译成WebAssembly在引擎中运行。WebAssembly相对原生Javascript来说是一种执行效率更高的方案。通过调研我们发现：目前相对成熟的是Rust和C++语言编译成WebAssembly，其他语言的WebAssembly环境中的配套工具严重匮乏，会导致合约编写困难；而Rust和C++对于开发人员来说门槛高、不友好。所以我们选择了Typescript作为合约编写语言编译成Javascript在Node.js引擎环境中运行。在WebAssembly环境成熟后，可以将合约编译成WebAssembly在Node.js中运行，开发人员不需要对合约进行调整。

##### 使用Typescript语言作为合约编写语言

TypeScript是一种由微软开发的自由和开源的编程语言，它是JavaScript的一个超集，由实现了静态类型和基于类的面向对象编程。由Anders Hejlsberg设计(他同时还是Delphi和C#的设计师)，Typescript借鉴了许多C#、Java等现代语言的优点，相对Javascript来说具有更为安全、更完善的工具支持、代码更易维护的特点。很多的流行的框架(如：AngularJS、ReactJS、Vue等)都基于Typescript开发。ASCH智能合约平台使用Typescript语言作为智能合约编写语言可以实现对合约代码的有效性检查、减少智能合约编写过程中的bug，通过开发工具的智能提示提升开发效率。

#### 1.3.3. 透明的状态管理

合约状态管理是智能合约引擎中一个重要的部分，部分平台的做法是提供底层的持久化接口给开发人员自己手动管理状态，但让开发人员需要关注持久化的细节，这样就增加了不必要的复杂性。在ASCH智能合约中状态的持久化是透明的，自动完成的开发人员只需要对状态变量进行赋值即可，不需要考虑持久化的细节。这样让开发人员把注意力集中在合约的逻辑本身上，降低合约的开发难度，提高合约代码的可理解和可维护性。

## 2. 智能合约语言

### 2.1. 智能合约语法

ASCH智能合约语言是[Typescript语言](http://www.typescriptlang.org/docs/home.html)的子集，下面是一个简单的例子：

#### 2.1.1. 一个简单智能合约样例

```typescript

// 基础样例

```

上述合约代码实现了一个简单的智能合约，这个合约的功能是接收转账并记录下转账人转账次数和转账总额，同时记录下最大的转账人地址。熟悉Typescript/Javascript/C#/Java等语言的开发者可以会发现读起来几乎没有障碍，非常容易理解。下面我们来详细了解一下这个合约的结构和约定：

#### 2.1.2. 合约结构

通过上面的代码我们可以看到，一个标准的智能合约包括两大部分：  

- **自定义状态类**
- **合约类**  

##### 2.1.2.1. 自定义状态类

自定义状态类必须在合约类定义前，是可选的，可以有多个。合约类只能包括属性定义，不支持方法(`getter`、`setter`也不可以，可以理解成传统的`POJO`)，用来实现复杂的自定义状态。自定义状态类的属性类型必须是由简单类型和状态容器类型构成。只包括简单类型的自定义状态类型称 **简单自定义类型**

##### 2.1.2.2. 合约类

介绍合约类之前，我们先简单介绍一下合约中的类型。合约中类型主要分成五类

- 简单类型 `string`、`number`、`bigint`、`boolean`
- 状态容器类型 `Mapping`、`Vector`，容器类型包含一个泛型参数，用于指定容器中的值的类型，如`Mapping<bigint>`、`Vector<string>`、`Mapping<User>`
- 自定义状态类型，通过`class`关键字定义，由简单类型和状态容器类型的属性成员构成
- 其他内置类型，如`Array`、`ContractContext`、`Transaction`、`Block`等
- 合约类

合约类是实现合约逻辑的的代码，一个合约就是一个从`AschContract`继续来的子类。合约类成员又可以分成两类：合约状态和合约方法。  

- **合约状态**
  - 可见性  
    其中合约状态是可以自动被持久化的成员变量，合约代码执行时对合约状态的任何修改都会被自动持久化到合约状态数据库中，无需程序员手工处理。其中，可见性为`public`(缺省为public)的状态为外部可查询状态，可以通过`api/v2/contracts/{contractName}/states/{stateName}/{stateKey}`进行查询。可见性为`protected`和`private`的代码是内部状态，外部不可访问。
  - 可使用类型  
    合约状态可以使用三种类型：简单类型(`string`、`number`、`boolean`、`bigint`)、状态容器类型(`Mapping`、`Vector`)和自定义的状态类型，其中容器的泛型参数可以是简单类型、状态容器类型和自定义状态类型，自定义类型的成员中也可以包含容器
- **合约方法**  
  - 可见性  
  合约方法的可见性与属性类似，`public`为外部可访问、`private`和`protected`为外部不可访问。
  - 参数与返回值
  对于外部可访问的方法的所有参数和返回值需指定类型
  - 注解  
  合约方法支持两种注解，分别是`payable`和`constant`，分别代表接收转账的方法和只读方法(不改变合约状态，通过查询接口查询)
  
#### 2.1.3. 智能合约语法约定

智能合约语言是Typescript语言的子集，除上节描述的结构约定外，其他主要限制如下：  

- 不允许使用引入第三方库
- 一个合约只能有一个合约类，这个类必须从`AschContract`继承而来
- 不允许声明全局函数、静态函数、全局变量
- 合约类的所有成员属性(变量，不支持`getter`和`setter`)都将作为合约状态，且会被自动持久化
- 合约方法中可以使用引擎中全部可用的类型
- 合约状态只能使用简单类型、合约容器类型、自定义状态类型以及它们的组合
- 合约类型的构造函数(可以是默认的)必须是没有参数且是`public`(可省略)可见性的
- 智能合约中只能使用合约引擎提供的内置类型、方法和对象，未提供的原Node.js内置的对象、函数或类型是不可用的(如`Function`、`Date`都是不可用的)
- 自定义状态类型声明
  - 所有成员必须都是属性，属性名称必须都是字符串
  - 自定义类型中属性可以是：基本类型、状态容器类型或自定义状态类型之一，所有属性都是简单类型的，称为**简单自定义状态类型**
- 外部可调用的合约方法参数和返回值类型要求
  - 参数和返回值必须指定类型，必须是简单类型、简单自定义状态类型或`Array`；不可有可选参数和高级类型的参数(如 `string?`和`string | bigint`都是不允许的)
  - 如果参数或返回值中使用`Array`，的泛型参数必须是简单类型或简单自定义状态类型。另：由于合约调用时所有参数会被序列化为`JSON`传递，基于效率考虑，全部参数或返回值序列化后的`JSON`字符串长度应控制在`16K`以内(`length <= 16,384`)
  - 函数返回值如未声明类型，返回值将被丢弃，不作为调用结果返回
- 复杂状态类型嵌套深度不超过**3**
  由于状态容器类型的值可以是状态容器类型或自定义状态，而自定义状态中也可以有自定义状态或状态容器。基于代码可读性以及状态管理的性能考虑。嵌套的深度不应超过3，如`Mapping<bigint>`深度称为 1，`Vector<Mapping<number>>`深度为2；简单自定义类型本身深度为1，包含一个深度为1的容器类型或自定义状态类型深度为2；以此类推
- 注意，与以太坊的solidity不同的是，在solidity中，给存储状态赋值会导致自动的复制。而在ASCH智能合约中，状态容器或自定义状态中使用的是对象的引用。这样的好处是性能更好、编程更灵活、更符合主流语言的习惯，但也会带来一个问题：当两个状态容器中保存相同的对象引用时，可能会导致误操作。合约引擎会自动检查这种情况的存在，当尝试把一个已经属于合约状态一部分的对象赋值给合约状态时，会抛出异常。(待补充示例)

### 2.2. 内置对象

#### 2.2.1 内置类型

##### 2.2.1.1. 简单类型  

简单类型为`number`、`bigint`、`string`和`boolean`，这四种类型的行为与Javascript/Typescript环境中的行为是一致的。  

##### 2.2.1.2. 状态容器类型(`Mapping`、`Vector`)  

- `Mapping`的行为与以太坊solidity中的`mapping`接近，类似Javascript中的`Object`，是一个可以通过`key`以下标方式来访问的对象容器
- `Vector`的行为与以太坊solidity中的`Array`接近，是一个只可以push(不可以插入或删除元素)或通过下标(**下标必须0或正整数**)访问的数组
- 状态容器类型包含一个泛型参数，用于指定容器中的值的类型，如`Mapping<bigint>`、`Vector<string>`、`Mapping<User>`。泛型参数可以是简单类型、状态容器类型或自定义状态类型。

##### 2.2.1.3. 其他内置类型

- `AschContract`
  `AschContract`是智能合约类的基类，包括两个重要的成员：`context`属性和`transfer`方法  
  - `context`属性，是合约调用时环境参数信息。包括三个成员：
    - `transaction`对象，包含合约调用的交易相关信息。
    - `block`对象，待打包区块信息。
    - `senderAddress` 属性，调用者的地址。
  - `transfer`方法，原型为：

    ```typescript
    function transfer( toAddress: string, amount: number | string | bigint, currency: string ): void
    ```  

    该方法可以实现将合约账户的余额转账到指定的账户地址中，该余额记录在Asch链的区块链数据库中，可以通过Asch链接口进行查询。参数信息如下
    - `toAddress` 类型为`string`，接收人地址
    - `amount` 类型为`string`或`number`或`bigint`，转账金额
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
function assert( condition: boolean, error: string ): void
```

该函数合约方法中使用，用来检查合约执行的前置条件是否满足，如条件不满足(`condition === fasle`)会抛出异常，导致合约终止。

- **内置工具类**  
 主要包括如下类与命名空间，除`Crypto`外，基本与原生功能保持一致：
  - `Array`
  - `ArrayBuffer`
  - `BufferView`
  - `String`
  - `Number`
  - `Object`
  - `Math`
  - `Bigint`
  - `Crypto`  

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
  function payableMethod(amount: number | bigint | string, currency: string): void
  ```

  **注：**`@payable`注解中的参数`{ isDefalut: true }`是可选的(默认是`false`)，上例所示的是默认转账接收函数(向合约转账时不指定接收方法时默认的接收方法)。开发者应在合约中存储转入合约的资产数额，这样可以在合约内部确定合约账户本身的余额，避免在调用`transfer`时导致余额不足而失败。

- 合约方法声明时应包括完整的参数类型信息，不应使用联合类型( `string | number` 或 `string & number` 是不正确的用法)
- 合约中不允许使用`try...catch`语法，也不允许使用`throw`语句。任何时候抛出异常(如使用`assert`语句)即导致中止合约
- 合约对象本身、合约内部状态和内置对象皆是不可扩展的，增加、修改、删除属性会产生异常
- 建议使用内部方法封装低层次的实现细节，外部可访问合约代码中应是统一的高逻辑层次的合约代码
- 一个合约方法应当是易于理解和验证，一般一个合约方法的[循环复杂度](https://en.wikipedia.org/wiki/Cyclomatic_complexity#Definition)应控制在10以内，且有效内容不宜超过15行
- 不使用`export`语句，尽管语法上不会出错
- 不使用`public`，因为缺省可见性为`public`；使用`private`而不是`protected`，因为`private`更语义化
- 合约类的构造函数必须是没有参数的，构造函数用于合约初始化，仅在合约注册时被引擎自动调用。尽管可以使用缺省的构造函数，但请显式的声明一个
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
class FundingInfo {
	// 众筹得到的token数量
	tokenAmount: bigint
	// 参与众筹XAS数量
	xasAmount: bigint
	// 参与众筹BCH数量
	bchAmount: bigint
}

// 众筹合约类
class CrowdFundgingContract extends AschContract {
	// 记录每个地址的众筹信息
	fundingOfAddress: Mapping<FundingInfo> 
	// 兑换比例
	rateOfCurrency: Mapping<bigint>
	// 总可众筹token数量
	totalFundingToken: bigint
	// 剩余可众筹数量
	avalibleToken: bigint
	// 众筹发起人地址，发行token资产的账户地址
	sponsorAddress: string
	// 众筹得到的资产名称
	offeringCurrency: string
	
	// 初始化方法，会在合约注册时被调用

	constructor() {
		super()
		this.offeringCurrency = 'test.XXT'
		this.sponsorAddress = 'SPONSOR_ADDRESS' // 发行 XXT 资产的账户地址
		
		this.rateOfCurrency = new Mapping<bigint>()
		this.rateOfCurrency['XAS'] = 100n    // 1 XAS = 100 token
		this.rateOfCurrency['BCH'] = 30000n // 1 BCH = 30000 token
		
		this.totalFundingToken = 0n
		this.avalibleToken = 0n
		this.fundingOfAddress = new Mapping<FundingInfo>()
	}

	// 发起人初始注入token
	@payable
	payInitialToken(amount: bigint, currency: string): void {
		assert(this.context!.senderAddress === this.sponsorAddress, `invalid sponsor address`)
		assert(currency === this.offeringCurrency, `invalid offering currency, should be ${this.offeringCurrency}`)
		assert(this.totalFundingToken === 0n, `initial ${this.offeringCurrency} has paied`)
		
		this.totalFundingToken = amount
		this.avalibleToken = amount
	}
	
	// 众筹逻辑
	@payable({ isDefault: true })
	crowdFunding(amount: bigint, currency: string): void {
		assert(amount >= 0, 'amount must great than 0')
		assert(currency === 'XAS' || currency === 'BCH', `invalid currency '${currency}', please pay XAS or BCH`)
	
		const rate = this.rateOfCurrency[currency]!
		const tokenAmount = amount * rate
		assert(this.avalibleToken >= tokenAmount, `insuffient ${this.offeringCurrency}`)
		
		this.avalibleToken = this.avalibleToken - tokenAmount
		const partnerAddress = this.context!.senderAddress
		this.updateFunding(partnerAddress, amount, currency, tokenAmount)
		// 调用ASCH链转账
		this.transfer(partnerAddress, tokenAmount, this.offeringCurrency)
	} 
	
	@constant
	getFunding(address: string): FundingInfo {
		return this.fundingOfAddress[address] || { tokenAmount: 0n, xasAmount: 0n, bchAmount: 0n }
	}

	private updateFunding( address: string, amount: bigint, currency: string, tokenAmount: bigint) : void {
		const funding = this.getOrCreateFundingInfo(address)
		funding.tokenAmount += tokenAmount
		
		if (currency === 'XAS') {
			funding.xasAmount += amount
		}
		else if (currency === 'BCH') {
			funding.bchAmount += amount
		}
	}
	
	private getOrCreateFundingInfo( address: string ) : FundingInfo {
		if (this.fundingOfAddress[address] === undefined) {
			this.fundingOfAddress[address] = { tokenAmount: 0n, xasAmount: 0n, bchAmount: 0n }
		} 
		return this.fundingOfAddress[address]!
	}
	
}

```

**注：该合约代码是为了演示ASCH平台上开发智能合约的一样例代码，供ASCH平台开发者学习智能合约的开发，请注意不要用于学习以外的用途。**  

### 4.3. 合约部署和使用

#### 4.3.1. 合约开发工具

为了帮助开发人员更方便的基于ASCH平台开发智能合约，我们开发了ASCH智能合约构建工具帮助开发人员以交互式的方式生成基本的开发环境。其中包括了依赖的npm包、语法检查工具、样例合约、应用模板、测试工具及模拟调试配置等一整套工具。使用方法如下：

- 安装环境
- 生成程序框架
- 编写合约及测试用例
- 调试合约

#### 4.3.2. 部署合约  

使用[ASCH链在线客户端](https://mainnet.asch.io)中的智能合约部署功能，填入合约名称、合约代码及其他信息，提交即可。测试网请使用[ASCH链测试网络客户端](https://testnet.asch.io)。开发请自行搭建本地开发节点，请参见[如何搭建ASCH本地开发环境](https://github.com/AschPlatform/asch-docs/blob/master/install/zh-cn.md)，注意：请使用v1.5版以上的节点安装包。

#### 4.3.3. 合约调用

合约调用是一个ASCH交易，外部可调用的合约方法分成两类，转账到合约(代码602)和调用合约方法(代码601)，交易费为 0 (根据代码运行消耗Gas)。提交交易到区块链请参见 [事务接口](https://github.com/AschPlatform/asch-docs/blob/master/http_api/zh-cn.md#3-%E4%BA%8B%E5%8A%A1%E6%8E%A5%E5%8F%A3)。参数传入如下：  

- **注册合约**
  - type: 600
  - args: [`asLimit`, `name`, `version`, `desc`, `code`, `consumeOwnerEnergy`]
    - gasLimit: `number`类型，最大消耗的Gas, `10,000,000 > gasLimit > 0`
    - name: `string`类型，智能合约名称，全网唯一，3 ~ 32个字母或数字组成
    - version: `string`类型，合约引擎版本，目前请填`v1.0`
    - desc: `string`类型，智能合约的描述，长度不超过255的字符串
    - code: `string`类型，智能合约代码，长度不超过16K
    - consumeOwnerEnergy: `boolean`类型，是否优先消耗合约所有者的能量
- **调用合约方法**
  - type: 601
  - args: [`gasLimit`, `enablePayGasInXAS`, `contractName`, `method`, `methodArgs`]
    - gasLimit: `number`类型，最大消耗的Gas, `10,000,000 > gasLimit > 0`
    - enablePayGasInXAS: `boolean`类型，当调用者能量不足时，是否使用XAS支付Gas
    - contractName: `string`类型，智能合约名称
    - method: `string`类型，要调用的方法名称
    - methodArgs: `Array`类型，调用方法所需要的参数列表
- **转账到合约**
  - type: 602  
  - args: [`gasLimit`, `enablePayGasInXAS`, `receiverPath`, `amount`, `currency`]  
    - gasLimit: `number`类型，最大消耗的Gas, `10,000,000 > gasLimit > 0`
    - enablePayGasInXAS: `boolean`类型，当调用者能量不足时，是否使用XAS支付Gas
    - receiverPath: `string`类型，接收转账的路径（由合约地址或名称、'/'、接收方法名称组成，如接收方法是默认接收方法则'/'和接收方法可以省略）
    - amount: `number`或`string`类型，转账金额
    - currency: `string`类型，转账资产名称

#### 4.3.4. 合约状态查询

- **简单状态查询**

  智能合约中`public`的状态可以通过`HTTP GET`接口进行查询，查询地址为：`{serverAddress}/api/v2/contracts/{contractName}/states/{statePath}`。注意，本接口仅能查询基本类型的数据，复杂类型请通过状态查询函数来查询
  - serverAddress 服务地址
  - contractName 合约名称，部署合约时填入的合约名称
  - statePath 由'.'分隔的状态路径。如 `holding.0`将会查询`contract.holding[0]`
  - 返回值 如路径指向的是简单状态值，则返回值本身。如果是`Mapping`或`Vector`，返回其包含的元素条数，如是自定义类型，返回成员数量

  例如，查询某地址参与众筹的信息可以访问如下地址：  
  `https://testnet.asch.io/api/v2/contracts/CrowdFunding/fundingOf.{Address}`

- **状态查询函数查询**
  智能合约中通过`@constant`注解修饰的方法为状态查询函数，状态查函数的返回值应是基本类型、简单自定义类型、基本类型及简单自定义类型构成的数组。且序列化为`JSON`后的字符串长度小于16K
  状态查询函数通过`HTTP GET`接口访问，访问地址为：`{serverAddress}/api/v2/contracts/{contractName}/constants/{method}/{args}`
  - serverAddress 服务地址
  - method 查询函数名称
  - args 查询函数参数数组转换为`JSON`字符串，如：`'[ "arg1", 2, true ]'`表示三个参数 `"arg1"`、`2`和`true`
  - 返回值 如调用成功，返回查询函数的结果

## 5. 常见问题  

- **gas具体是如何计费的**
  gas计费是一个比较复杂的过程，具体计费规则请参见《Gas计费与内置函数》

- **gas扣费规则**
  在合约注册时，有参数可以指定是否优先消耗合约开发者的能量，如果设置为优先消耗开发者的能量，则在开发者能量足够的情况下优先使用开发者的能量作为智能合约的消耗；如果未设置或开发者能量不足，则消耗调用者的能量，当调用者的能量不足时，可选择使用`XAS`作为智能合约的能量消耗。目前，`1 XAS (100,000,000) = 10,000 GAS`

- **gasLimit是什么，该传入多少？**  
  gasLimit是一次智能合约访问所最大能消耗的Gas数量，Gas用正整数表示，最小单位是1wei。系统限制一次合约调用所能使用的最大gasLimit应小于 10,000,000。

- **我如何知道一次合约调用会消耗多少Gas?**  
  需要开发人员在测试时根据实际数据模拟测算。

- **如何知道智能合约调用的结果？**  
  请使用`{serverAddress}api/v2/contracts/action=getResult&tid={transactionId}`，传入交易id查询合约的调用结果。
