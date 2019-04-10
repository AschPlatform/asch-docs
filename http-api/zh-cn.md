# ASCH HTTP API文档

Table of Contents
=================

   * [ASCH HTTP API文档](#asch-http-api文档)
      * [<strong>1 API使用说明</strong>](#1-api使用说明)
      * [<strong>2 基本接口</strong>](#2-基本接口)
         * [<strong>2.1 账户accounts</strong>](#21-账户accounts)
            * [<strong>2.1.1 登录</strong>](#211-登录)
               * [<strong>2.1.1.1 本地加密后再登陆（推荐使用）</strong>](#2111-本地加密后再登陆推荐使用)
               * [<strong>2.1.1.2 本地不加密直接登陆</strong>](#2112-本地不加密直接登陆)
            * [<strong>2.1.2 根据地址获取账户信息</strong>](#212-根据地址获取账户信息)
            * [<strong>2.1.3 获取账户资产余额</strong>](#213-获取账户余额)
            * [<strong>2.1.4 根据地址获取其投票列表</strong>](#214-根据地址获取其投票列表)
            * [<strong>2.1.5 生成新账户</strong>](#215-生成新账户)
            * [<strong>2.1.6 获取当前链上账户总个数</strong>](#216-获取当前链上账户总个数)
         * [<strong>2.2 交易transactions</strong>](#22-交易transactions)
            * [<strong>2.2.1 获取交易信息</strong>](#221-获取交易信息)
            * [<strong>2.2.2 根据交易id查看交易详情</strong>](#222-根据交易id查看交易详情)
            * [<strong>2.2.3 根据未确认交易id查看详情</strong>](#223-根据未确认交易id查看详情)
            * [<strong>2.2.4 获取全网所有未确认的交易详情</strong>](#224-获取全网所有未确认的交易详情)
            * [<strong>2.2.5 获取转账记录</strong>](#225-获取转账记录)
         * [<strong>2.3 区块blocks</strong>](#23-区块blocks)
            * [<strong>2.3.1 获取指定区块的详情</strong>](#231-获取指定区块的详情)
            * [<strong>2.3.2 获取区块数据</strong>](#232-获取区块数据)
            * [<strong>2.3.3 根据id或高度获取区块</strong>](#233-根据id或高度获取区块)
            * [<strong>2.3.4 获取区块链高度</strong>](#234-获取区块链高度)
            * [<strong>2.3.5 获取里程碑</strong>](#235-获取里程碑)
            * [<strong>2.3.6 查看单个区块奖励</strong>](#236-查看单个区块奖励)
            * [<strong>2.3.7 获取XAS当前供应量</strong>](#237-获取xas当前供应量)
            * [<strong>2.3.8 获取区块链状态</strong>](#238-获取区块链状态)
            * [<strong>2.3.9 获取指定区块的交易信息</strong>](#239-获取指定区块的交易信息)
         * [<strong>2.4 受托人delegates</strong>](#24-受托人delegates)
            * [<strong>2.4.1 获取受托人总个数</strong>](#241-获取受托人总个数)
            * [<strong>2.4.2 根据受托人名字查看哪些人为其投了票</strong>](#242-根据受托人名字查看哪些人为其投了票)
            * [<strong>2.4.3 根据公钥或者用户名获取受托人详情</strong>](#243-根据公钥或者用户名获取受托人详情)
            * [<strong>2.4.4 获取受托人列表</strong>](#244-获取受托人列表)
            * [<strong>2.4.5 受托人锻造状态查看</strong>](#245-受托人锻造状态查看)
         * [<strong>2.5 节点peers</strong>](#25-节点peers)
            * [<strong>2.5.1 获取本机连接的所有节点信息</strong>](#251-获取本机连接的所有节点信息)
            * [<strong>2.5.2 获取本节点版本号等信息</strong>](#252-获取本节点版本号等信息)
            * [<strong>2.5.3 获取指定ip节点信息</strong>](#253-获取指定ip节点信息)
         * [<strong>2.6 同步和加载</strong>](#26-同步和加载)
            * [<strong>2.6.1 查看本地区块链加载状态</strong>](#261-查看本地区块链加载状态)
            * [<strong>2.6.2 查看区块同步信息</strong>](#262-查看区块同步信息)
         * [<strong>2.7 提案</strong>](#27-提案)
            * [<strong>2.7.1 获取提案列表</strong>](#271-获取提案列表)
            * [<strong>2.7.2 根据提案id获取提案</strong>](#272-根据提案id获取提案)
         * [<strong>2.8 网关</strong>](#28-网关)
            * [<strong>2.8.1 获取所有网关</strong>](#281-获取所有网关)
            * [<strong>2.8.2 获取指定网关的验证者</strong>](#282-获取指定网关的验证者)
            * [<strong>2.8.3 获取支持的所有跨链币种</strong>](#283-获取支持的所有跨链币种)
            * [<strong>2.8.4 获取指定网关的支持币种</strong>](#284-获取指定网关的支持币种)
            * [<strong>2.8.5 获取指定网关的指定账户</strong>](#285-获取指定网关的指定账户)
            * [<strong>2.8.6 获取指定用户地址的所有网关账户</strong>](#286-获取指定用户地址的所有网关账户)
            * [<strong>2.8.7 获取指定用户地址指定币种的所有充值记录</strong>](#287-获取指定用户地址指定币种的所有充值记录)
            * [<strong>2.8.8 获取指定用户地址指定币种的所有充值记录</strong>](#288-获取指定用户地址指定币种的所有充值记录)
         * [<strong>2.9 代理人和Group</strong>](#29-代理人和group)
            * [<strong>2.9.1 获取所有代理人账户</strong>](#291-获取所有代理人账户)
            * [<strong>2.9.2 获取某个代理下的委托客户</strong>](#292-获取某个代理下的委托客户)
            * [<strong>2.9.3 获取Group信息</strong>](#293-获取group信息)
         * [<strong>2.10 侧链DApp查询接口</strong>](#210-dapp查询接口)
            * [<strong>2.10.1 获取所有已注册侧链</strong>](#2101-获取所有已注册侧链)
         * [<strong>2.11 用户自定义资产uia</strong>](#211-用户自定义资产uia)
            * [<strong>2.11.1 获取全网所有发行商</strong>](#2111-获取全网所有发行商)
            * [<strong>2.11.2 查询指定发行商的信息</strong>](#2112-查询指定发行商的信息)
            * [<strong>2.11.3 查看指定发行商的资产</strong>](#2113-查看指定发行商的资产)
            * [<strong>2.11.4 获取全网所有资产信息</strong>](#2114-获取全网所有资产信息)
            * [<strong>2.11.5 获取指定资产信息</strong>](#2115-获取指定资产信息)
            * [<strong>2.11.6 获取指定账户所有uia的余额</strong>](#2116-获取指定账户所有uia的余额)
         * [<strong>2.12 智能合约</strong>](#211-智能合约)
            * [<strong>2.12.1 查询智能合约列表</strong>](#2121-查询智能合约列表)
            * [<strong>2.12.2 查询智能合约详细信息</strong>](#2122-查询智能合约详细信息)
            * [<strong>2.12.3 查询智能合约代码</strong>](#2123-查询智能合约代码)
            * [<strong>2.12.4 查询智能合约元数据</strong>](#2124-查询智能合约元数据)
            * [<strong>2.12.5 查询智能合约公开状态</strong>](#2125-查询智能合约公开状态)
            * [<strong>2.12.6 查询智能合约执行结果</strong>](#2126-查询智能合约执行结果)
            * [<strong>2.12.7 调用查询方法</strong>](#2127-调用查询方法)
      * [<strong>3. 事务接口</strong>](#3-事务接口)
         * [<strong>请求过程说明</strong>](#请求过程说明)
         * [<strong>3.1 基础交易</strong>](#31-基础交易)
            * [<strong>3.1.1 转账</strong>](#311-转账)
            * [<strong>3.1.3 设置二级密码</strong>](#313-设置二级密码)
            * [<strong>3.1.4 锁仓</strong>](#314-锁仓)
            * [<strong>3.1.5 解锁仓库</strong>](#315-解锁仓库)
            * [<strong>3.1.6 设置理事会</strong>](#316-设置理事会)
            * [<strong>3.1.7 注册代理人</strong>](#317-注册代理人)
            * [<strong>3.1.8 设置代理人</strong>](#318-设置代理人)
            * [<strong>3.1.9 取消代理人</strong>](#319-取消代理人)
            * [<strong>3.1.10 注册委托人</strong>](#3110-注册委托人)
            * [<strong>3.1.11 给委托人投票</strong>](#3111-给委托人投票)
            * [<strong>3.1.12 取消给委托人投票</strong>](#3112-取消给委托人投票)
         * [<strong>3.2 资产</strong>](#32-资产)
            * [<strong>3.2.1 注册发行商</strong>](#321-注册发行商)
            * [<strong>3.2.2 注册资产</strong>](#322-注册资产)
            * [<strong>3.2.3 发行资产</strong>](#323-发行资产)
            * [<strong>3.2.4 内部转账</strong>](#324-内部转账)
         * [<strong>3.3 侧链DApp</strong>](#33-侧链DApp)
            * [<strong>3.3.1 注册侧链DApp</strong>](#331-注册侧链DApp)         
            * [<strong>3.3.2 修改委托人</strong>](#332-修改委托人)
            * [<strong>3.3.3 增加委托人</strong>](#333-增加委托人)
            * [<strong>3.3.4 删减委托人</strong>](#334-删减委托人)
            * [<strong>3.3.6 从侧链DApp提现</strong>](#336-从-dapp-提现)
         * [<strong>3.4 提案相关</strong>](#34-提案相关)
            * [<strong>3.4.1 发起提案</strong>](#341-发起提案)
            * [<strong>3.4.2 给提案投票</strong>](#342-给提案投票)
            * [<strong>3.4.3 激活提案</strong>](#343-激活提案)
         * [<strong>3.5 网关</strong>](#35-网关)
            * [<strong>3.5.1 开启网关</strong>](#351-开通网关账户)
            * [<strong>3.5.2 注册成员</strong>](#352-注册成员)
            * [<strong>3.5.3 对网关充值</strong>](#353-对网关充值)
            * [<strong>3.5.4 从网关提现</strong>](#354-从网关提现)
            * [<strong>3.5.5 提交提现交易</strong>](#355-提交提现交易)
            * [<strong>3.5.6 提交交易签名</strong>](#356-提交交易签名)
            * [<strong>3.5.7 提交交易协议</strong>](#357-提交交易协议)
         * [<strong>3.6 理事会</strong>](#36-理事会)
            * [<strong>3.6.1 投票</strong>](#361-投票)
            * [<strong>3.6.2 激活理事会</strong>](#362-激活理事会)
            * [<strong>3.6.3 增加成员</strong>](#363-增加成员)
            * [<strong>3.6.4 移除成员</strong>](#364-移除成员)
         * [<strong>3.7 智能合约</strong>](#37-智能合约)
            * [<strong>3.7.1 注册智能合约</strong>](#371-注册智能合约)
            * [<strong>3.7.2 调用智能合约</strong>](#372-调用智能合约)
            * [<strong>3.7.3 向智能合约转账</strong>](#373-向智能合约转账)
Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc)

## **1 API使用说明**   

1.1 客户端可以使用`asch-js`构造请求数据，数据按照 Asch 提供的接口规则，通过程序生成签名，生成请求数据集合；      

1.2 发送请求数据，把构造完成的数据集合通过POST/GET等提交的方式传递给 Asch 节点；       

1.3 Asch 对请求数据进行处理。服务器在接收到请求后，会首先进行安全校验，验证通过后便会处理该次发送过来的请求；

1.4 返回响应结果数据，Asch 把响应结果以 JSON 的格式反馈给用户，每个响应都包含 success 字段，表示请求是否成功，成功为 true, 失败为 false。 如果失败，则还会包含一个 error 字段，表示失败原因；   

1.5 对获取的返回结果数据进行处理；       


## **2 基本接口**  

### **2.1 账户accounts**   

#### **2.1.1 登录**   

##### **2.1.1.1 本地加密后再登陆（推荐使用）** 

接口地址：/api/accounts/open2/   
请求方式：POST   
支持格式：JSON   
接口备注：根据用户密码在本地客户端用JS代码生成公钥    

请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|publicKey |string |Y    |asch账户公钥      |

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否登陆成功      |
|account|JSON   |账户信息          |

请求示例：
```js
var secret = 'Asch账户密码'  //在浏览器内存中保留
var AschJS = require('asch-js');  // npm install asch-js
var publicKey = AschJS.crypto.getKeys(secret).publicKey;  //根据密码生成公钥 
// var address = AschJS.crypto.getAddress(publicKey);   //根据公钥生成地址

// 将上面生成的数据通过 POST 方法提交到 Asch server   
curl -X POST -H "Content-Type: application/json" -k -d '{"publicKey":"116025d5664ce153b02c69349798ab66144edd2a395e822b13587780ac9c9c09"}' 'http://192.168.1.78:4096/api/accounts/open2/'   
```

JSON返回示例：   
``` 
{
    "success": true,
    "account": {
        "address": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
        "unconfirmedBalance": 8809754854306082,
        "balance": 8809754854306082,
        "secondPublicKey": null,
        "lockHeight": 0,
        "publicKey": "116025d5664ce153b02c69349798ab66144edd2a395e822b13587780ac9c9c09"
    },
    "latestBlock": {
        "height": 31088,
        "timestamp": 67090300
    },
    "version": {
        "version": "1.4.2",
        "build": "21:04:40 09/08/2018",
        "net": "testnet"
    }
}
```

##### **2.1.1.2 本地不加密直接登陆**   
接口地址：/api/accounts/open/   
请求方式：POST   
支持格式：JSON   
接口备注：将密码以明文方式传入到后端，根据生成的地址去查询账户信息。**不推荐在公网坏境使用！**

请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|secret |string |Y    |账户主密码       |

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否登录成功      |
|account|JSON   |账户信息          |

请求示例：   
```bash
curl -X POST -H "Content-Type: application/json" -k -d '{"secret":"tunnel hope keep manual balcony quantum phrase deer prefer vivid deer hazard"}' 'http://192.168.1.78:4096/api/accounts/open/'   
```

JSON返回示例：   
```js
{
    "success": true,
    "account": {
        "address": "AFLqemsfDpZoLqhWkiHzWHncfSjAPNwwBt",
        "unconfirmedBalance": 0,
        "balance": 0,
        "secondPublicKey": "",
        "lockHeight": 0,
        "publicKey": "371ab8e451b413e6db647e3f58d3923eb3b43f3c3c3a46fcc221c58207c158ed"
    },
    "latestBlock": {
        "height": 31105,
        "timestamp": 67090480
    },
    "version": {
        "version": "1.4.2",
        "build": "21:04:40 09/08/2018",
        "net": "testnet"
    }
} 
```
#### **2.1.2 根据地址获取账户信息**   

接口地址：/api/v2/accounts/:address    
请求方式：GET   
支持格式：urlencoded    

请求参数说明：   

|名称	|类型   |必填 |说明              |
|:----: |:---:  |:-:  |:--:              |
|address |string |Y    |账户地址      |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/accounts/ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5'
```
返回参数说明：   

|名称	|类型   |说明              |
|:----: |:---:  |:--:              |
|success|boolean  |是否成功得到数据      |
|account|string   |账户信息          |
|latestBlock|string |最后区块 |
|version|string |版本信息 |

JSON返回示例：   
```js
{
    "success": true,
    "account": {
        "address": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
        "name": null,
        "xas": 4898157546529489,
        "publicKey": null,
        "secondPublicKey": null,
        "isLocked": 0,
        "isAgent": 0,
        "isDelegate": 0,
        "role": 0,
        "lockHeight": 0,
        "agent": null,
        "weight": 0,
        "agentWeight": 0,
        "_version_": 855
    },
    "unconfirmedAccount": {
        "address": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
        "xas": 4898157546529489,
        "name": null,
        "isLocked": 0,
        "isAgent": 0,
        "isDelegate": 0,
        "role": 0,
        "lockHeight": 0,
        "weight": 0,
        "agentWeight": 0,
        "_version_": 855
    },
    "latestBlock": {
        "height": 6630,
        "timestamp": 66723500
    },
    "version": {
        "version": "1.4.1",
        "build": "14:57:08 08/08/2018",
        "net": "testnet"
    }
}
```

#### **2.1.3 获取账户资产余额**   

接口地址：/api/v2/balances/:address 
请求方式：GET
支持格式：urlencoded   

请求参数说明：

|名称	|类型   |必填 |说明              |
|:----: |:---:  |:-:  |:--:              |
|address |string |Y    |账户地址      |

请求示例：

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/balances/A9Evp9iYWtSUSBQc8yuWtBT2ReBkvzXDxB'
```

返回参数说明：   

|名称	|类型   |说明              |
|:----: |:---:  |:--:              |
|success|boolean  |是否成功获得response数据 |
|balances|Array  |余额数组      |

JSON返回示例：   
``` js
{
    "success": true,
    "count": 2,
    "balances": [
        {
            "address": "A9Evp9iYWtSUSBQc8yuWtBT2ReBkvzXDxB",
            "currency": "asch.TSC",
            "balance": "1000000000",
            "flag": 2,
            "_version_": 1,
            "asset": {
                "name": "asch.TSC",
                "tid": "d3d32d1b8b9daddf9d2e4af033dda1a04cb9fefe31121bd2317fe98b53c1ba89",
                "timestamp": 66726839,
                "maximum": "1000000000000",
                "precision": 1,
                "quantity": "1000000000",
                "desc": "test",
                "issuerId": "A9Evp9iYWtSUSBQc8yuWtBT2ReBkvzXDxB",
                "_version_": 2
            }
        },
        {
            "address": "A9Evp9iYWtSUSBQc8yuWtBT2ReBkvzXDxB",
            "currency": "asch.TTC",
            "balance": "100000000000",
            "flag": 2,
            "_version_": 1,
            "asset": {
                "name": "asch.TTC",
                "tid": "17cdd6ac2444f6e50f316ea4f73851a547a797d0fc708b8898094e06f94dffa2",
                "timestamp": 66726992,
                "maximum": "10000000000000000000",
                "precision": 1,
                "quantity": "100000000000",
                "desc": "test2",
                "issuerId": "A9Evp9iYWtSUSBQc8yuWtBT2ReBkvzXDxB",
                "_version_": 2
            }
        }
    ]
}
```

#### **2.1.4 根据地址获取其投票列表**   

接口地址：/api/accounts/delegates
请求方式：GET
支持格式：无   

请求参数:

|  名称   |  类型  |   说明   |
| :-----: | :----: | :------: |
| address | string | 账户地址 |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/accounts/delegates?adddress=APSu9NhiCTtvRGx1EpkeKNubiApiBWMf7T' 
```

返回示例

```js
{
    "success": true,
    "delegates": []    //如果给人投票，会有被投票者信息
}
```

#### **2.1.5 生成新账户**   
接口地址：/api/accounts/new   
请求方式：GET 
支持格式：无   
请求参数：无   

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|secret|string  |主密码      |
|publicKey|string  |公钥      |
|privateKey|string  |私钥      |
|address|string  |地址      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/accounts/new'   
```

JSON返回示例：   
```js  
{
    "success": true,
    "secret": "ginger angle fury grow differ about bamboo swim transfer mixed era radio",
    "publicKey": "bb201d25fae05de56d0450932b0603eb3c6e8b001ea6215a49f392aaa94b241d",
    "privateKey": "026c7eb8876354a9480e1ca1cba4919760d1c1e998830cd66e5e01b6370002f6bb201d25fae05de56d0450932b0603eb3c6e8b001ea6215a49f392aaa94b241d",
    "address": "A3xBcFQHcubF8qUE8mcmFZFN2WdUA8KGvV"
}  
```

#### **2.1.6 获取当前链上账户总个数**   
接口地址：/api/accounts/count   
请求方式：GET
支持格式：无   
请求参数：无    

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|count|integer  |当前链上账户总个数     |

请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/accounts/count'    
```

JSON返回示例：   
```js   
{
    "success": true,
    "count": 144
}
```

### **2.2 交易transactions**   

#### **2.2.1 获取交易信息**   
接口地址：/api/v2/transactions    
请求方式：GET 
支持格式：urlencoded
请求参数说明：   

|名称	|类型   |必填 |说明              |
|:----: |:---:  |:-:  |:--:              |
|orderBy |string |N    |排序方式       |
|height |number |N |交易所所在高度 |
|senderId |string |N |交易签名者地址 |
|message |string |N |交易备注 |
|offset |number |N |偏移量|
|limit |number |N |个数限制 |

请求示例：

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/transactions?senderId=A7Vbt5h3WgaXLSJhUeHnRRcwvkGF3ecS7r&orderBy=height:desc&offset=1&limit=3'
```

返回参数说明：   

|名称	|类型   |说明              |
|:----: |:---:  |:--:              |
|success|boolean  |是否成功得到数据      |
|transactions|Array   |交易数组          |

JSON返回示例：   

```js   
{
    "success": true,
    "transactions": [
        {
            "id": "a567a422dd23940ef194633b67f4659132c402e7c078d758176f72dc9261c578",
            "type": 301,
            "timestamp": 66763492,
            "senderId": "A7Vbt5h3WgaXLSJhUeHnRRcwvkGF3ecS7r",
            "senderPublicKey": "4110e2ab06a075ff540cbcd9af5d7cce3a416595e7c259f15065895f7c84d16f",
            "requestorId": null,
            "fee": 10000000,
            "signatures": [
                "4f1da7d296c3b84ab8bd7e8ffdbe1503db690138d9958f253b02ddaaca65706a55a9fbe75d14cefffb8dae65684fa8e24c3a02403ac01121b2c0fd0cbf44ce04"
            ],
            "secondSignature": null,
            "args": [
                "f4a5cf6c2c989a6d454a828ce0d9a16f883f8a5e180899e0485256f97e76a88a"
            ],
            "height": 38,
            "message": null,
            "mode": 0,
            "_version_": 1
        },
        {
            "id": "70d62c62f9ecf4bfb155cbf3758d2380daa83c4e774a54fc8690b04b26916a16",
            "type": 302,
            "timestamp": 66763452,
            "senderId": "A7Vbt5h3WgaXLSJhUeHnRRcwvkGF3ecS7r",
            "senderPublicKey": "4110e2ab06a075ff540cbcd9af5d7cce3a416595e7c259f15065895f7c84d16f",
            "requestorId": null,
            "fee": 0,
            "signatures": [
                "c8fcfc7543f24fb41d5b7a510bf8a4157bfff80431e5dbfe65f57f2b7071fdedc0c876d284ed84b7ba3c1787654b312667e4eef56eb77e8081537c2d6d1e260c"
            ],
            "secondSignature": null,
            "args": [
                "8b1af4f00e7efb8704faa089cd7c9643a073bd6fddde847a8fdc7ba21c542e7e"
            ],
            "height": 34,
            "message": null,
            "mode": 0,
            "_version_": 1
        },
        {
            "id": "549b787c45d26268d4a51caa6084d7e432c2cc8e75060682ecd80d0f90c84a7c",
            "type": 301,
            "timestamp": 66763442,
            "senderId": "A7Vbt5h3WgaXLSJhUeHnRRcwvkGF3ecS7r",
            "senderPublicKey": "4110e2ab06a075ff540cbcd9af5d7cce3a416595e7c259f15065895f7c84d16f",
            "requestorId": null,
            "fee": 10000000,
            "signatures": [
                "86f0dc7fb6b18ce627966550a85c704fe4c912660f839d384801dacddb19bbe548090672863a3cedd23506dcbb1587dc72293292b78cfc3fc43688c3e961d205"
            ],
            "secondSignature": null,
            "args": [
                "8b1af4f00e7efb8704faa089cd7c9643a073bd6fddde847a8fdc7ba21c542e7e"
            ],
            "height": 33,
            "message": null,
            "mode": 0,
            "_version_": 1
        }
    ],
    "count": 10
}
```
#### **2.2.2 根据交易id查看交易详情**   
接口地址：/api/v2/transactions/:tid 
请求方式：GET
支持格式：urlencoded
请求参数说明：   

|名称	|类型   |必填 |说明              |
|:----: |:---:  |:-:  |:--:              |
|tid |string |Y    |交易ID      |

请求示例：

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/transactions/e19a3ae0090208c3e2e1289d12b80511eca5ceb814d20f0cf37bd2e37942f820'
```

返回参数说明：   

|名称	|类型   |说明              |
|:----: |:---:  |:--:              |
|success|boolean  |是否成功获得response数据 |
|transaction|string  |交易信息      |

JSON返回示例：   
```js   
{
    "success": true,
    "transaction": {
        "id": "e19a3ae0090208c3e2e1289d12b80511eca5ceb814d20f0cf37bd2e37942f820",
        "type": 302,
        "timestamp": 66655963,
        "senderId": "A7Vbt5h3WgaXLSJhUeHnRRcwvkGF3ecS7r",
        "senderPublicKey": "4110e2ab06a075ff540cbcd9af5d7cce3a416595e7c259f15065895f7c84d16f",
        "requestorId": null,
        "fee": 10000000,
        "signatures": [
           "19f3c4d10b2fad290aedbc429ff8f2797789fb2cd547f49d5506fdc3ae7b412def388caf65a24e4c25226d71a3c2644a04f16672c1bf62b004be2e547c9bed0a"
        ],
        "secondSignature": null,
        "args": [
            "52e2f5a04d30cf7e3d22e9c1b57d236d358f581446c7d851e3c0373f97d9f8f4"
        ],
        "height": 145,
        "message": null,
        "mode": 0,
        "_version_": 1
    }
}
```

#### **2.2.3 根据未确认交易id查看详情**   
接口地址：/api/transactions/unconfirmed/get   
请求方式：GET   
支持格式：urlencoded   
请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|id|string |Y    |未确认交易id      |

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|transaction|JSON  |未确认交易详情      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/transactions/unconfirmed/get?id=e19a3ae0090208c3e2e1289d12b80511eca5ceb814d20f0cf37bd2e37942f820'  // 正常情况，该未确认交易存在时间极短0~10秒   
```

JSON返回示例：   
```js   
{
	"success": true,
	"transaction": {
		"type": 0,
		"amount": 10000,
		"senderPublicKey": "3ec1c9ec08c0512641deba37c0e95a0fe5fc3bdf58424009f594d7d6a4e28a2a",
		"requesterPublicKey": null,
		"timestamp": 5082322,
		"asset": {
			
		},
		"recipientId": "16723473400748954103",
		"signature": "3a97f8d63509ef964bda3d816366b8e9e2d9b5d4604a660e7cbeefe210cb910f5de9a51bece06c32d010f55502c62f0f59b8224e1c141731ddfee27206a88d02",
		"id": "7557072430673853692",
		"fee": 10000000,
		"senderId": "15238461869262180695"
	}
}
```


#### **2.2.4 获取[全网所有]未确认的交易详情**   
接口地址：/api/transactions/unconfirmed   
请求方式：GET   
支持格式：urlencoded   
接口说明：如果不加参数，则会获取全网所有未确认交易
请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|senderPublicKey |string |N    |发送者公钥      |
|address |string |N    |地址      |


返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|transactions|Array  |未确认交易列表      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/transactions/unconfirmed'   
```

JSON返回示例：   
```js   
{   
	"success": true,   
	"transactions": []      //全网目前不存在未确认的交易   
}   
```

#### **2.2.5 获取转账记录**   
接口地址：/api/v2/transfers  
请求方式：GET  
支持格式：urlencoded   

请求参数说明

|   名称   |  类型  |          说明          |
| :------: | :----: | :--------------------: |
|  limit   | string | 返回个数限制（默认10） |
|  offset  | string |          偏移          |
| ownerId  | string |     发送/接收者ID      |
| currency | string |          币种          |

返回参数

|   名称    |  类型   |           说明           |
| :-------: | :-----: | :----------------------: |
|  success  | boolean | 是否成功获得response数据 |
| transfers |  Array  |         转账数组         |

请求示例：   

```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/v2/transfers?limit=2'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "count": 258,
    "transfers": [
        {
            "tid": "fd2076bad0516519f3b3592369690c7e618070ad6aa352db9470277d7117a43c",
            "senderId": "A7Z9eGfMbBWXFucRouZpYhGhFCALVAXH9n",
            "recipientId": "AAhRVPqQkiZyAXnfTnCTDqVZBg3nphywfJ",
            "recipientName": "account2",
            "currency": "XAS",
            "amount": "30000000",
            "timestamp": 66767962,
            "height": 465,
            "_version_": 1,
            "transaction": {
                "id": "fd2076bad0516519f3b3592369690c7e618070ad6aa352db9470277d7117a43c",
                "type": 1,
                "timestamp": 66767962,
                "senderId": "A7Z9eGfMbBWXFucRouZpYhGhFCALVAXH9n",
                "senderPublicKey": "c9ca6e4f768946ffc391c22b509f5d69244459e3ffdb45aed1bd52d84d7c069f",
                "requestorId": null,
                "fee": 10000000,
                "signatures": [
                    "63e4d33bbe2ca88eb40bfc454ac83564a535e98a30d4fe03d85cfdd02e527e56faec969655c6aeeb1a4f62411ad3ed1fbbe58c34b1ff9190d469c0c304921901"
                ],
                "secondSignature": "790e01e692ed0f1694d69124de747cc80c9937a108435ed8978aed1ab124e4a22e59568ca85e32ae0835d5b4551d3d7e90636f5a805f5019c0b8cf6b26183807",
                "args": [
                    "30000000",
                    "account2"
                ],
                "height": 465,
                "message": "",
                "mode": 0,
                "_version_": 1
            }
        },
        {
            "tid": "ca1337111343caf92d5f35c960748fb041937b516a8f27c77e7e2581c70c32ec",
            "senderId": "AFcaWmL5tL2sbGaEcxYoiABfCesd8MsS3L",
            "recipientId": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
            "recipientName": "",
            "currency": "ZuoRight.SKR",
            "amount": "123456789",
            "timestamp": 66765287,
            "height": 212,
            "_version_": 1,
            "asset": {
                "name": "ZuoRight.SKR",
                "tid": "6bf841ee5bc6d1586e12d5a88af0ca7fa28898e598a9533fab2964d7e12251ce",
                "timestamp": 66763735,
                "maximum": "100000000000000",
                "precision": 8,
                "quantity": "1100000000000",
                "desc": "赞",
                "issuerId": "AFcaWmL5tL2sbGaEcxYoiABfCesd8MsS3L",
                "_version_": 3
            },
            "transaction": {
                "id": "ca1337111343caf92d5f35c960748fb041937b516a8f27c77e7e2581c70c32ec",
                "type": 103,
                "timestamp": 66765287,
                "senderId": "AFcaWmL5tL2sbGaEcxYoiABfCesd8MsS3L",
                "senderPublicKey": "b304597cf41582a20ebdbb4a832dd461962bf7a20e5361b0447741079df732a0",
                "requestorId": null,
                "fee": 10000000,
                "signatures": [
                    "1ccada819490d1ce5012aab70559a290c7d82a54ea35033ab16e476496db0d752393339ab6a408f923167025b68a4bf8dfc8d0f16f4af404ee55087a6cb78b07"
                ],
                "secondSignature": "9af3ee91364c3d5c789b7d4cb0d558398d260e4928dfbf3491a2e0f4a31f4121e22f292d3e585d3f6a61c4b7f6072b971426fd97959a50e97893b44ef3b5a306",
                "args": [
                    "ZuoRight.SKR",
                    "123456789",
                    "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5"
                ],
                "height": 212,
                "message": "",
                "mode": 0,
                "_version_": 1
            }
        }
    ]
}
```


### **2.3 区块blocks**   

#### **2.3.1 获取指定区块的详情**   

接口地址：/api/blocks/get   
请求方式：GET   
支持格式：urlencoded   
请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|id |string |参数3选1    |区块id      |
|height|string|参数3选1|区块高度|
|hash|string|参数3选1|区块hash|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|block|JSON  |区块详情      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/blocks/get?id=6076474715648888747'   
```

JSON返回示例：   
```js   
{   
	"success": true,   
	"block": {   
		"id": "6076474715648888747",   
		"version": 0,   
		"timestamp": 4734070,   
		"height": 140538,   
		"previousBlock": "16033230167082515105",    //上一个区块id   
		"numberOfTransactions": 0,  //交易数   
		"totalAmount": 0,   //交易额   
		"totalFee": 0,   
		"reward": 350000000,    //奖励   
		"payloadLength": 0,   
		"payloadHash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",   
		"generatorPublicKey": "1d352950c8141e1b35daba4a974a604519d7a2ef3a1ec0a503ce2653646aa052",   
		"generatorId": "6656029629904254066",   
		"blockSignature": "a53de66922cdc2f431acd0a474beec7cf7c420a8460b7b7caf84999be7caebb59fb7fbb7166c2c7013dbb431585ea7294722166cb08bf9663abf50b6bd81cd05",   
		"confirmations": "2",   
		"totalForged": 350000000   
	}   
}   
```

#### **2.3.2 获取区块数据**   

接口地址：/api/v2/blocks
请求方式：GET      
支持格式：urlencoded   
接口说明：不加参数默认获取前20块   
请求参数说明：   

|名称	|类型   |说明 |
|:----: |:---:  |:-:  |
|limit |Integer |个数限制（默认）    |
|offset |Integer |偏移量 |
|orderBy |String |height:desc(目前提供的排序方法) |
|transactions |String |如果有该关键字，区块会附带交易信息 |

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|blocks|Array  |由区块详情JSON串构成的数组 |
|count|integer|区块链高度|


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/v2/blocks?limit=2&offset=350'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "count": 72470,
    "blocks": [
        {
            "version": 0,
            "delegate": "fb44b7597d9cca1edbfa5a6f9bb0cf90a1f060921908f9138e25fe4892030ef5",
            "height": 350,
            "prevBlockId": "731edb7ffa2e0d25b6ed33d47dc913e4ef539e496552d78c8ece62d4424625c9",
            "timestamp": 67078540,
            "count": 0,
            "fees": 0,
            "payloadHash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
            "reward": 350000000,
            "signature": "7222d07abe4a97c02824981e76eb7d7409f5b427387f9672681eebb89731281691d10dfae948f440a863acea0e4d57ef55764a155969f5f7dfe98a07afac1e0a",
            "id": "d6a0cc3d2c09e1105d3fb8479c8fc235baeb35d262968be6e46f4a971e42bb46"
        },
        {
            "version": 0,
            "delegate": "4c67e2710cc368019668e7a08deb293bc066ab638c7e9dbb280815bcb79f10e9",
            "height": 351,
            "prevBlockId": "d6a0cc3d2c09e1105d3fb8479c8fc235baeb35d262968be6e46f4a971e42bb46",
            "timestamp": 67078550,
            "count": 0,
            "fees": 0,
            "payloadHash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
            "reward": 350000000,
            "signature": "cf8316cf84253dcde0148ea343805433df6f41b653e95a1ff4638beb1a4a116d4e1f6f3d0eba0c1fc1fd6661657b6db9fd4a571c3fb4838439ab078e69baa40f",
            "id": "426e6b99b7308416d87509da9a485fdbecd61e19fdd139a306ee4938949f1844"
        }
    ]
}
```

####  **2.3.3 根据id或高度获取区块**

接口地址：/api/v2/blocks/:idOrHeight
请求方式：GET      
支持格式：urlencoded     

请求参数说明：

|    名称    |  类型  |   说明   |
| :--------: | :----: | :------: |
| idOrHeight | String | id或高度 |

返回参数说明：

|  名称   |  类型   |           说明           |
| :-----: | :-----: | :----------------------: |
| success | boolean | 是否成功获得response数据 |
| blocks  |  Json   |      由区块详情JSON      |

请求示例：

```js
curl -k -X GET 'http://192.168.1.78:4096/api/v2/blocks/351'
curl -k -X GET 'http://192.168.1.78:4096/api/v2/blocks/426e6b99b7308416d87509da9a485fdbecd61e19fdd139a306ee4938949f1844'
```

返回示例：

```js
{
    "success": true,
    "block": {
        "version": 0,
        "delegate": "4c67e2710cc368019668e7a08deb293bc066ab638c7e9dbb280815bcb79f10e9",
        "height": 351,
        "prevBlockId": "d6a0cc3d2c09e1105d3fb8479c8fc235baeb35d262968be6e46f4a971e42bb46",
        "timestamp": 67078550,
        "count": 0,
        "fees": 0,
        "payloadHash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
        "reward": 350000000,
        "signature": "cf8316cf84253dcde0148ea343805433df6f41b653e95a1ff4638beb1a4a116d4e1f6f3d0eba0c1fc1fd6661657b6db9fd4a571c3fb4838439ab078e69baa40f",
        "id": "426e6b99b7308416d87509da9a485fdbecd61e19fdd139a306ee4938949f1844"
    }
}
```

#### **2.3.4 获取区块链高度**   

接口地址：/api/blocks/getHeight   
请求方式：GET     
支持格式：无   
请求参数说明：无   

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|height|integer  |区块链高度      |

请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/blocks/getheight'    
```

JSON返回示例：   
```js   
{
    "success": true,
    "height": 31363
} 
```

#### **2.3.5 获取里程碑**   
接口地址：/api/blocks/getMilestone   
请求方式：GET      
支持格式：无   
请求参数说明：无   
返回参数说明：   

|名称	|类型类型   |说明              |
|:----: |:---:  |:--:              |
|success|boolean  |是否成功获得response数据 |
|milestone|integer  |      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/blocks/getMilestone'    
```

JSON返回示例：   
```js   
{
    "success": true,
    "milestone": 0
}
```

#### **2.3.6 查看单个区块奖励**  

接口地址：/api/blocks/getReward   
请求方式：GET   
支持格式：无   
请求参数说明：无   

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|reward|integer  |区块奖励，包含受托人奖励和手续费      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/blocks/getReward'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "reward": 350000000
} //每个生成一个block奖励3.5 XAS   
```

#### **2.3.7 获取XAS当前供应量**   

接口地址：/api/blocks/getSupply   
请求方式：GET      
支持格式：无   
请求参数说明：无   

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|supply|integer  |全网XAS个数      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/blocks/getSupply'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "supply": 10010958150000000
} //当前testnet共有100109581.5XAS   
```

#### **2.3.8 获取区块链状态**  

接口地址：/api/blocks/getStatus   
请求方式：GET   
支持格式：无   
请求参数说明：无   

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|height|integer  |区块链高度      |
|fee|integer  |交易手续费      |
|milestone|integer  |      |
|reward|integer  |区块奖励      |
|supply|integer  |全网XAS个数      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/blocks/getStatus'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "height": 31385,
    "fee": 10000000,
    "milestone": 0,
    "reward": 350000000,
    "supply": 10010958150000000
}  
```

#### **2.3.9 获取指定区块的交易信息**   

接口地址：/api/blocks/full   
请求方式：GET   
支持格式：无   
请求参数说明：无  

请求参数说明：

|名称	|类型   |必填    |说明              |
|------ |-----  |----   |----           |
|id |string |参数2选1    |区块id      |
|height|string|参数2选1|区块高度|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|block|JSON  |区块详情，包含交易信息transactions      |

请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/blocks/full?height=34'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "block": {
        "id": "256e00b56508346cc1a98977781a08052a9a5ec6d94c1a7e1941b4ea06433be1",
        "version": 0,
        "timestamp": 66763460,
        "height": 34,
        "payloadHash": "faa4237e78e2793eb9a55fcec17febaa08f40c0e58584e14fee382b99109b75a",
        "previousBlock": "f892df4f142ec84a28318b660cd4d4f17651f72699afb973779e7ffd0584f816",
        "numberOfTransactions": 6,
        "totalFee": 50000000,
        "generatorPublicKey": "992ba4a33527432dbe05b26c783ec72e151867c035c0e91194b812ab92703e0b",
        "blockSignature": "db97d94aa73d6ce522eeb5e2a28fb148d0ca94d9e0120aed6bf6f5e1f476843ac966d11c27cb5f5dcc9daff940a628fed0ca7ce9df6bf1b99da2baa60498b20e",
        "confirmations": 31370,
        "transactions": [
            {
                "id": "14ada84f1ba58dad5cbaf386af0e101eaacbaa20ac1e5de40a75b202f4018ebf",
                "height": 34,
                "timestamp": 66763431,
                "senderPublicKey": "30620e9f06c11fdb4466b3bfcc031568de60a518da07cd5daffbac0d4c6b3858",
                "senderId": "G3sQzuWpvXZjxhoYnvvJvnfUUEo8aNzKdj",
                "message": null,
                "fee": 20000000,
                "blockId": "256e00b56508346cc1a98977781a08052a9a5ec6d94c1a7e1941b4ea06433be1",
                "recipientId": "A3gmKrzbTALHpJv2SDZ2SaoyA44Ei9miJC",
                "amount": 11230,
                "asset": {},
                "confirmations": 31370,
                "type": 0,
                "signature": "c80b6fc96176df8f13d80b893fe961ee97d3ed8220d33c9b166eb5582d71468e07721ad8a6f1e96a28de98ee6bda19db65829cf307d2703bacaeb213cf9f440a",
                "signatures": null,
                "args": {},
                "argsNew": [
                    11230,
                    "A3gmKrzbTALHpJv2SDZ2SaoyA44Ei9miJC"
                ]
            }
            
            {
                "id": "b7a1e870c72afe435a8b969d96b0882bbe20a46ee269cf0040d5d84f0ef96c15",
                "height": 34,
                "timestamp": 66763453,
                "senderPublicKey": "0493ad806622a6976146f976e7fe843df741897617a635201c778d094aab09ba",
                "senderId": "AECGLMi8yQVvQRDpDCB6u8qHHQF7oD7VP7",
                "message": null,
                "fee": 10000000,
                "blockId": "256e00b56508346cc1a98977781a08052a9a5ec6d94c1a7e1941b4ea06433be1",
                "recipientId": "ALqyjLbk3Ci45SPUiHU38qa9xmqkMreftq",
                "amount": 0,
                "asset": {
                    "uiaTransfer": {
                        "currency": "CCTime.XCT",
                        "amount": "100000"
                    }
                },
                "confirmations": 31370,
                "type": 14,
                "signature": "25afd59c09d3e84a03268b39fd7418c15ad7216e9000ea9cb2568253b716c1de20aa29ed8cf5104a0d816ed671b8cad6fc6afa504d607aa7fbdb74b8189e2f00",
                "signatures": null,
                "args": {},
                "argsNew": [
                    "CCTime.XCT",
                    "100000",
                    "ALqyjLbk3Ci45SPUiHU38qa9xmqkMreftq"
                ]
            }    
        ]
    }
}
```


### **2.4 受托人delegates**   

#### **2.4.1 获取受托人总个数**   
接口地址：/api/delegates/count   
请求方式：GET   
支持格式：无   
请求参数说明：无   

返回参数说明：   
    
|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|count|integer   |受托人总个数      |

请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/delegates/count'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "count": 106
}   
```

#### **2.4.2 根据受托人名字查看哪些人为其投了票**   
接口地址：/api/delegates/voters   
请求方式：GET   
支持格式：urlencoded   
请求参数说明：   

|名称	|类型   |必填 |说明              |
|:----: |:---:  |:-:  |:--:              |
|name |string |Y    |受托人名字      |

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|accounts|Array  |账户JSON串组成的数组      |

请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/delegates/voters?name=asch_g59'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "accounts": [
        {
            "address": "AAhRVPqQkiZyAXnfTnCTDqVZBg3nphywfJ",
            "name": "account2",
            "xas": 9990120000000,
            "publicKey": null,
            "secondPublicKey": null,
            "isLocked": 0,
            "isAgent": 1,
            "isDelegate": 0,
            "role": 2,
            "lockHeight": 0,
            "agent": null,
            "weight": 0,
            "agentWeight": 0,
            "_version_": 10,
            "balance": 9990120000000,
            "weightRatio": 0
        },
        {
            "address": "ABVm72Qty9Uxeyp6MEUHjvuh3drwVcbD41",
            "name": "100000",
            "xas": 799938450000000,
            "publicKey": null,
            "secondPublicKey": "b072613d5dbe9be82f3a771e566b1a3ce9d1116c9b0cc0b36214f831ae5c6969",
            "isLocked": 1,
            "isAgent": 0,
            "isDelegate": 0,
            "role": 0,
            "lockHeight": 536618,
            "agent": null,
            "weight": 200000000000000,
            "agentWeight": 0,
            "_version_": 14,
            "balance": 799938450000000,
            "weightRatio": 1.9978037144864793
        },
        {
            "address": "AFcaWmL5tL2sbGaEcxYoiABfCesd8MsS3L",
            "name": "7c",
            "xas": 9890515354322,
            "publicKey": null,
            "secondPublicKey": "816cdcf53d1464c362e4503345662f0788fe55899525a4b85732637abd8a728b",
            "isLocked": 1,
            "isAgent": 0,
            "isDelegate": 1,
            "role": 1,
            "lockHeight": 267944,
            "agent": null,
            "weight": 10000000000,
            "agentWeight": 0,
            "_version_": 28,
            "balance": 9890515354322,
            "weightRatio": 0.00009989018572432396
        }
    ]
}
```

#### **2.4.3 根据公钥或者用户名获取受托人详情**   
接口地址： /api/delegates/get   
请求方式：GET      
支持格式：urlencoded   
接口备注：通过公钥或者用户名获取受托人信息   
请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|publickey |string |二选一    |受托人公钥      |
|name  |string |二选一    |受托人用户名      |

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|delegate|JSON  |委托人详情      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/delegates/get?publicKey=ff6ea4945fee31f64439030f84bac934604468cf5d0b441bec761cfc1911653a'   
curl -k -X GET 'http://192.168.1.78:4096/api/delegates/get?name=asch_g59'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "delegate": {
        "address": "ADcPTKHLnDfxBjWyxVVMquPQDjfBNBwnvT",
        "name": "asch_g59",
        "tid": "ac569d1e0f0e74101606c617e4547fcceea47f83d63ddc9be282ad890d1fe09a",
        "publicKey": "ff6ea4945fee31f64439030f84bac934604468cf5d0b441bec761cfc1911653a",
        "votes": 200010000000000,
        "producedBlocks": 326,
        "missedBlocks": 0,
        "fees": 0,
        "rewards": 0,
        "_version_": 333,
        "rate": 1,
        "approval": 1.9979036046722034,
        "productivity": "100.00",
        "vote": 200010000000000,
        "missedblocks": 0,
        "producedblocks": 326
    }
}
```

#### **2.4.4 获取受托人列表**   

接口地址：/api/delegates   
请求方式：GET   
支持格式：urlencoded   
接口说明：如果不加参数则会返回全网受托人列表   
请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|address |string |N    |受托人地址      |
|limit|int  |N       |限制返回结果数据集的个数       |
|offset|integer  |N       |偏移量，最小值：0      |
|orderBy|string  |N       |排序字段:排序规则，如:desc      |


返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|delegates|Array  |受托人详情列表      |

请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/delegates?limit=5'
```

JSON返回示例：   
```js   
{   
	"success": true,   
	"delegates": [{   
		"username": "wgl_002",  //受托人名字   
		"address": "14636456069025293113",  //受托人地址   
		"publicKey": "ae256559d06409435c04bd62628b3e7ea3894c43298556f52b1cfb01fb3e3dc7",    //受托人公钥   
		"vote": 9901984015600500,   //得票数   
		"producedblocks": 1371, //生成的区块数   
		"missedblocks": 6,  //丢失的区块数   
		"fees": 12588514990,       
		"rewards": 276850000000,    //已经得到的奖励   
		"rate": 1,   
		"approval": 98.54,  //得票率   
		"productivity": 99.56,  //生产率   
		"forged": "289438514990"    //锻造产生的所有奖励   
	},   
	{
            "address": "ADcPTKHLnDfxBjWyxVVMquPQDjfBNBwnvT",
            "name": "asch_g59",   //受托人名字
            "tid": "ac569d1e0f0e74101606c617e4547fcceea47f83d63ddc9be282ad890d1fe09a",
            "publicKey": "ff6ea4945fee31f64439030f84bac934604468cf5d0b441bec761cfc1911653a",
            "votes": 200010000000000,
            "producedBlocks": 326,
            "missedBlocks": 0,
            "fees": 0,
            "rewards": 0,       //已经得到的奖励
            "_version_": 333,
            "rate": 1, 
            "approval": 1.9979036046722034,   //得票率
            "productivity": "100.00",    //生产率
            "vote": 200010000000000,   //得票数
            "missedblocks": 0,
            "producedblocks": 326   
        }],   
	"totalCount": 233   
}   
```

#### **2.4.5 受托人锻造状态查看**   

接口地址：/api/delegates/forging/status      
请求方式：GET   
支持格式：urlencoded    
请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|publicKey|string  |Y      |公钥|


返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|enabled|string  |锻造是否开启      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/delegates/forging/status?publicKey=fafcd01f6b813fdeb3c086e60bc7fa9bfc8ef70ae7be47ce0ac5d06e7b1a8575'        
```

JSON返回示例：   
```js   
{"success":true,"enabled":false}    
```

### **2.5 节点peers**   

#### **2.5.1 获取本机连接的所有节点信息**   
接口地址：/api/peers   
请求方式：GET   
支持格式：urlencoded   
备注：展示节点只是和本机有连接的节点，并不是全网所有的节点    
请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|state |integer |N    |节点状态,0 ,1,2,3     |
|os|string|N|内核版本|
|version|string|N|asch版本号|
|port|integer|N|端口，1~65535|


返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|peers|Array  |节点信息JSON构成的数组     |
|totalCount|integer|当前正在运行的节点个数|


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/peers?limit=3'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "count": 25,
    "peers": [
        {
            "id": "d2a1553f6a5bca24a2d706b4103539f47a8f4cca",
            "host": "192.168.1.82",
            "port": 8231,
            "distance": 0,
            "seen": 1534132283145,
            "_id": "w01lWBusDx4JtQD3"
        },
        {
            "id": "fc5a058f941ee5421ad85b848262b5736efef9bd",
            "host": "192.168.1.76",
            "port": 4097,
            "distance": 0,
            "seen": 1533894206475,
            "_id": "PTXTz6HyrzoGJLHl"
        },
        {
            "id": "e5949bbc303551774928899ef70f34aff2946875",
            "host": "192.168.1.79",
            "port": 7901,
            "distance": 0,
            "seen": 1533820788984,
            "_id": "tYDqBjtlHOLg2d9o"
        }
    ]
}   
```

#### **2.5.2 获取本节点版本号等信息**   
接口地址：/api/peers/version   
请求方式：GET   
支持格式：无   
请求参数说明：无参数   

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|version|string  |版本号      |
|build  |timestamp |构建时间     |
|net    |string  |主链或者测试链     |


请求示例：   
```bash   
curl -k -X 'GET http://192.168.1.78:4096/api/peers/version'   
```

JSON返回示例：   
```js   
{
    "success": true,
    "version": "1.4.2",
    "build": "21:04:40 09/08/2018",
    "net": "testnet"
}
```

#### **2.5.3 获取指定ip节点信息**   

接口地址：/api/peers/get   
请求方式：GET      
支持格式：urlencoded   
请求参数说明：   

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|ip |string |Y    |待查询节点ip      |
|port|integer|Y|待查询节点端口，1~65535|


返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|peer|JSON  |      |


请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/peers/get?ip=45.32.248.33&port=4096'   
```

JSON返回示例：   
```js   
{   
	"success": true,   
}   
```

### **2.6 同步和加载**   
#### **2.6.1 查看本地区块链加载状态**   
接口地址：/api/loader/status   
请求方式：GET   
支持格式：无   
请求参数说明：无参数   

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|loaded |boolean    |          |
|blocksCount|integer||

请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/loader/status'
```

JSON返回示例：   
```js   
{   
	"success": true,   
	"loaded": true,   
	"blocksCount": 0   
}   
```

#### **2.6.2 查看区块同步信息**   

接口地址：/api/loader/status/sync   
请求方式：GET   
支持格式：无   
请求参数说明：无参数   

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功获得response数据 |
|height |int    |区块高度          |

请求示例：   
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/loader/status/sync'
```

JSON返回示例：   
```js   
{
    "success": true,
    "syncing": false,     //目前没有数据可以同步，所以为false
    "blocks": 0,
    "height": 31580
} 
```

### **2.7 提案**

#### **2.7.1 获取提案列表**

接口地址：/api/v2/proposals
请求方式：GET      
支持格式：urlencoded 

请求参数

|  名称  |  类型  |            说明            |
| :----: | :----: | :------------------------: |
| limit  | string | 返回数据个数限制（默认20） |
| offset | string |           偏移量           |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/proposals?limit=2'
```

返回示例

```js
{
    "success": true,
    "count": 5,
    "proposals": [
        {
            "tid": "33b4f51cee0a49b377ed416aafb0ec806f15a67134fc03f5b58dd09ca41ead81",
            "timestamp": 66763252,
            "title": "Register bitcoinbash gateway",
            "senderId": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
            "desc": "This is a proposal about register bitcoincash gateway",
            "topic": "gateway_register",
            "content": "{\"name\":\"bitcoincash\",\"desc\":\"bitcoincash gateway description\",\"updateInterval\":86400,\"minimumMembers\":3,\"currency\":{\"symbol\":\"BCH\",\"desc\":\"BCH description\",\"precision\":8}}",
            "activated": 1,
            "endHeight": 10000,
            "height": 14,
            "_version_": 2
        },
        {
            "tid": "c58fbea59446364f1d0f9b780bc7bd5d137746b6e1032e6a2ed4ff4f8cd45a9e",
            "timestamp": 66763301,
            "title": "Init bitcoincash gateway validators",
            "senderId": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
            "desc": "This is a proposal about init bitcoincash gateway",
            "topic": "gateway_init",
            "content": "{\"gateway\":\"bitcoincash\",\"members\":[\"A28yFDa4vYUFafNDK9fZwBK3qhH2xYxxrz\",\"AMAwe1qp6qFpGkdJ2nugovXvtRzedprvqh\",\"ABcur7keRpcZC2A1Y7qe2BV5VtKaYHt8ax\"]}",
            "activated": 1,
            "endHeight": 10000,
            "height": 19,
            "_version_": 2
        }
    ]
}
```

#### **2.7.2 根据提案id获取提案**

接口地址：/api/v2/proposals/:id
请求方式：GET   
支持格式：urlencoded 

参数说明

| 名称 |  类型  |  说明  |
| :--: | :----: | :----: |
|  id  | string | 提案id |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/proposals/c58fbea59446364f1d0f9b780bc7bd5d137746b6e1032e6a2ed4ff4f8cd45a9e'  
```

返回示例

```js
{
    "success": true,
    "proposal": {
        "tid": "c58fbea59446364f1d0f9b780bc7bd5d137746b6e1032e6a2ed4ff4f8cd45a9e",
        "timestamp": 66763301,
        "title": "Init bitcoincash gateway validators",
        "senderId": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
        "desc": "This is a proposal about init bitcoincash gateway",
        "topic": "gateway_init",
        "content": "{\"gateway\":\"bitcoincash\",\"members\":[\"A28yFDa4vYUFafNDK9fZwBK3qhH2xYxxrz\",\"AMAwe1qp6qFpGkdJ2nugovXvtRzedprvqh\",\"ABcur7keRpcZC2A1Y7qe2BV5VtKaYHt8ax\"]}",
        "activated": 1,
        "endHeight": 10000,
        "height": 19,
        "_version_": 2
    }
}
```

### **2.8 网关**

#### **2.8.1 获取所有网关**

接口地址：/api/v2/gateways 
请求方式：GET      
支持格式：urlencoded 

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/gateways?limit=2'
```

返回示例

```js
{
    "success": true,
    "count": 2,
    "gateways": [
        {
            "name": "bitcoincash",
            "desc": "bitcoincash gateway description",
            "updateInterval": 86400,
            "minimumMembers": 3,
            "lastUpdateHeight": 16,
            "activated": 1,
            "revoked": 0,
            "version": 1,
            "createTime": 66763272,
            "_version_": 2,
            "validatorNumber": 3
        },
        {
            "name": "bitcoin",
            "desc": "bitcoin gateway description",
            "updateInterval": 86400,
            "minimumMembers": 3,
            "lastUpdateHeight": 34,
            "activated": 1,
            "revoked": 0,
            "version": 1,
            "createTime": 66763452,
            "_version_": 2,
            "validatorNumber": 3
        }
    ]
}
```

#### **2.8.2 获取指定网关的验证者**

接口地址：/api/v2/gateways/:name/validators 
请求方式：GET   
支持格式：urlencoded 

请求参数说明

| 名称 |  类型  |   说明   |
| :--: | :----: | :------: |
| name | string | 网关名字 |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/gateways/bitcoin/validators'  
```

返回示例

```js
{
    "success": true,
    "count": 4,
    "validators": [
        {
            "address": "A5eTVn2Mz5p2j6SjGKdgvmUc2vMsSvKzuy",
            "gateway": "bitcoin",
            "desc": "Validator description of bitcoin gateway",
            "outPublicKey": "03729f44c98f73a3f6ddc98d4870aeb63413059229252424fa4743a96e086a00c1",
            "elected": 1,
            "_version_": 2,
            "name": "bv1"
        },
        {
            "address": "A3SmW61ZwxmNc26BbfKLbHkaNbmUQzexuj",
            "gateway": "bitcoin",
            "desc": "Validator description of bitcoin gateway",
            "outPublicKey": "0295925ebd0a122df74dbce4b6e5185bb46e0f2deaa4a95dc62715d422c864ba1a",
            "elected": 1,
            "_version_": 2,
            "name": "bv2"
        },
        {
            "address": "A4ncaYtKRrD8YS2Mi82HbwGEE9DxqsbEr9",
            "gateway": "bitcoin",
            "desc": "Validator description of bitcoin gateway",
            "outPublicKey": "0371595356796bdd46a1b87d240d8543ad0541a4e98fc14443a194215c0a4624da",
            "elected": 1,
            "_version_": 2,
            "name": "bv3"
        },
        {
            "address": "AGAeGrdGVXsry7LYbe2bC6ucrzWvq3PTvM",
            "gateway": "bitcoin",
            "desc": "Validator description of bitcoin gateway",
            "outPublicKey": "039a994e68f9897af9beb9f7dfb271745d7ee78b5852881b8631b50113abeb0d72",
            "elected": 0,
            "_version_": 1,
            "name": "bv4"
        }
    ]
}
```

#### **2.8.3 获取支持的所有跨链币种**

接口地址：/api/v2/gateways/currencies  
请求方式：GET   
支持格式：urlencoded 

请求参数说明：无

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/gateways/currencies' 
```

返回示例

```js
{
    "success": true,
    "count": 2,
    "currencies": [
        {
            "gateway": "bitcoincash",
            "symbol": "BCH",
            "desc": "BCH description",
            "precision": 8,
            "revoked": 0,
            "_version_": 1
        },
        {
            "gateway": "bitcoin",
            "symbol": "BTC",
            "desc": "BTC description",
            "precision": 8,
            "revoked": 0,
            "_version_": 1
        }
    ]
}
```

#### **2.8.4 获取指定网关的支持币种**

接口地址：/api/v2/gateways/:name/currencies  
请求方式：GET   
支持格式：urlencoded 

请求参数说明

| 名称 |  类型  |   说明   |
| :--: | :----: | :------: |
| name | string | 网关名称 |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/gateways/bitcoin/currencies'  
```

返回示例

```js
{
    "success": true,
    "count": 1,
    "currencies": [
        {
            "gateway": "bitcoin",
            "symbol": "BTC",
            "desc": "BTC description",
            "precision": 8,
            "revoked": 0,
            "_version_": 1
        }
    ]
}
```

#### **2.8.5 获取指定网关的指定账户**

接口地址：/api/v2/gateways/:name/accounts/:address
请求方式：GET   
支持格式：urlencoded 

请求参数说明

|  名称   |  类型  |   说明   |
| :-----: | :----: | :------: |
|  name   | string | 网关名字 |
| address | string | 账户地址 |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/gateways/bitcoin/accounts/AGw5h2cYK2iYGwp8czhn59Dbr8LMz2BaU'   
```

返回示例

```js
{
    success: true,
    account: {
        address: "AGw5h2cYK2iYGwp8czhn59Dbr8LMz2BaUC",
        seq: 1,
        gateway: "bitcoin",
        outAddress: "2N8qAZHVsG8yaAyQHCdbry6iHYxCxyMDd6W",
        attachment: "522103729f44c98f73a3f6ddc98d4870aeb63413059229252424fa4743a96e086a00c1210295925ebd0a122df74dbce4b6e5185bb46e0f2deaa4a95dc62715d422c864ba1a210371595356796bdd46a1b87d240d8543ad0541a4e98fc14443a194215c0a4624da53ae",
        version: 1
    }
}
```

#### **2.8.6 获取指定用户地址的所有网关账户**

接口地址：/api/v2/gateways/accounts/:address   
请求方式：GET      
支持格式：urlencoded 

参数说明

|  名称   |  类型  |   说明   |
| :-----: | :----: | :------: |
| address | string | 账户地址 |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/gateways/accounts/AGw5h2cYK2iYGwp8czhn59Dbr8LMz2BaUC'    
```

返回示例

```js
{
    success: true,
    count: 1,
    accounts: [{
        address: "AGw5h2cYK2iYGwp8czhn59Dbr8LMz2BaUC",
        seq: 1,
        gateway: "bitcoin",
        outAddress: "2N8qAZHVsG8yaAyQHCdbry6iHYxCxyMDd6W",
        attachment: "522103729f44c98f73a3f6ddc98d4870aeb63413059229252424fa4743a96e086a00c1210295925ebd0a122df74dbce4b6e5185bb46e0f2deaa4a95dc62715d422c864ba1a210371595356796bdd46a1b87d240d8543ad0541a4e98fc14443a194215c0a4624da53ae",
        version: 1
    }]
}
```

#### **2.8.7 获取指定用户地址指定币种的所有充值记录**

接口地址：/api/v2/gateways/deposits/:address/:currency    
请求方式：GET   
支持格式：urlencoded 

参数说明

|   名称   |  类型  |   说明   |
| :------: | :----: | :------: |
| address  | string | 账户地址 |
| currency | string |   币种   |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/gateways/deposits/mvGfGo9YfNiTJK6MDnfwDwr5jTdWR1ovdC/BTC'    
```

返回示例

```js
{
    success: true,
    count: 1,
    deposits: [{
        tid: "2bfc06d4984a2e8d1a0d55513c29fadcd8dc535de753e4cd584dec38ae91686c",
        currency: "BTC",
        amount: "10.5",
        address: "mvGfGo9YfNiTJK6MDnfwDwr5jTdWR1ovdC",
        confirmations: 1,
        processed: 0,
        oid: "02195dfafc389e465efe8e5bfc2ad4d5aa7b248eb81700b76fa25d657536aafdfe"
    }]
}
```

#### **2.8.8 获取指定用户地址指定币种的所有充值记录**

接口地址：/api/v2/gateways/withdrawals/:address/:currency    
请求方式：GET   
支持格式：urlencoded 

请求参数说明

|   名称   |  类型  |   说明   |
| :------: | :----: | :------: |
| address  | string | 账户地址 |
| currency | string |   币种   |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/gateways/withdrawals/APSu9NhiCTtvRGx1EpkeKNubiApiBWMf7T/BTC'   
```

返回示例

```js
{
    success: true,
    count: 1,
    withdrawals: [{
        tid: "3d4331b5dc8252e0104684b6118f94a5d8f48ab32e4cf6e4e86146b28bca57b5",
        gateway: "bitcoin",
        senderId: "APSu9NhiCTtvRGx1EpkeKNubiApiBWMf7T",
        recipientId: "2MzAnWPQWN4eRoxtDRDWuXsTyHXv8KkmEMi",
        currency: "BTC",
        seq: 1,
        amount: "10090000",
        fee: "10000",
        outTransaction: "{"txhex ":"0100000001f823dd6bec281e20355a4da44221bdd69c089b89e00e7c695e65e9c564366c380100000000ffffffff0210f699000000000017a9144bf1f23966f4f815980e089f18519f1f87d9ae73875847a5060000000017a914aaf52a57317ed5c8f1ccdd80fc3f21f63a9f2cba8700000000 ","input ":["2N8qAZHVsG8yaAyQHCdbry6iHYxCxyMDd6W "]}",
        signs: 2,
        ready: 1,
        oid: "",
        _version_: 3
    }]
}

```

### **2.9 代理人和Group**

#### **2.9.1 获取所有代理人账户**

接口地址：/api/v2/agents  
请求方式：GET   
支持格式：urlencoded 

请求参数说明

|  名称  |  类型  |          说明          |
| :----: | :----: | :--------------------: |
| limit  | string | 返回个数限制（默认20） |
| offset | string |         偏移量         |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/agents'      
```

返回示例

```js
{
    "success": true,
    "count": 2,
    "agents": [
        {
            "address": "AAhRVPqQkiZyAXnfTnCTDqVZBg3nphywfJ",
            "name": "account2",
            "xas": 9990120000000,
            "publicKey": null,
            "secondPublicKey": null,
            "isLocked": 0,
            "isAgent": 1,
            "isDelegate": 0,
            "role": 2,
            "lockHeight": 0,
            "agent": null,
            "weight": 0,
            "agentWeight": 0,
            "_version_": 10
        },
        {
            "address": "ALqyjLbk3Ci45SPUiHU38qa9xmqkMreftq",
            "name": "agent001",
            "xas": 13980000000,
            "publicKey": null,
            "secondPublicKey": null,
            "isLocked": 0,
            "isAgent": 1,
            "isDelegate": 0,
            "role": 2,
            "lockHeight": 0,
            "agent": null,
            "weight": 0,
            "agentWeight": 0,
            "_version_": 9
        }
    ]
}
```

#### **2.9.2 获取某个代理下的委托客户**

接口地址：api/v2/agents/:name/clienteles   
请求方式：GET   
支持格式：urlencoded 

参数说明

| 名称 |  类型  |    说明    |
| :--: | :----: | :--------: |
| name | string | 代理人名字 |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/agents/agent001/clienteles'     
```

返回示例

```js
{
    success: true,
    count: 3,
    clienteles: [{
        tid: "5cfac8d84d8e222615f933567dcbe4056c3cd13ce5c43cb582d605bfcee77f1a",
        agent: "agent001",
        clientele: "A8cwRrxgmL6MRcM9tJNBaVnkHeCHVmiuLY",
        t_timestamp: 57860693,
        t_type: 8,
        t_height: 716,
        account: {
            address: "A8cwRrxgmL6MRcM9tJNBaVnkHeCHVmiuLY",
            name: "",
            xas: 608605516348,
            publicKey: "",
            secondPublicKey: "",
            isLocked: 1,
            isAgent: 0,
            isDelegate: 0,
            lockHeight: 608635526348,
            agent: "agent001",
            weight: 10000,
            agentWeight: 0
        }
    }]
}
```

#### **2.9.3 获取Group信息**

接口地址：api/v2/groups/:address    
请求方式：GET   
支持格式：urlencoded 

请求参数说明

|  名称   |  类型  |   说明    |
| :-----: | :----: | :-------: |
| address | string | Group地址 |

请求示例

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/groups/G3sQzuWpvXZjxhoYnvvJvnfUUEo8aNzKdj'     
```

返回示例

```js
{
    success: true,
    group: {
        name: "test_group",
        address: "G3sQzuWpvXZjxhoYnvvJvnfUUEo8aNzKdj",
        tid: "0a273f9bac2005318ece1940dc3302ea9f28768b1c7a36b663fab6699358b17a",
        min: 5,
        max: 7,
        m: 2,
        updateInterval: 6,
        createTime: 62336692,
        _version_: 2,
        members: [{
            member: "A3gmKrzbTALHpJv2SDZ2SaoyA44Ei9miJC",
            name: "test_group",
            weight: 1,
            _version_: 1
        },
        {
            member: "AB5fFHae3syga1R81Ef797vUo3gFrNkQ3y",
            name: "test_group",
            weight: 1,
            _version_: 1
        },
        {
            member: "AJwotHuyfLsFvii2t1vqZaVHpgwMdgxYN9",
            name: "test_group",
            weight: 1,
            _version_: 1
        },
        {
            member: "ABnDYHEQzs6B8CGWk79n8vHKNAwp2QjyTz",
            name: "test_group",
            weight: 1,
            _version_: 1
        }]
    }
}
```

### **2.10 侧链DApp查询接口**

#### **2.10.1 获取所有已注册侧链**

接口地址：api/v2/chains
请求方式：GET   
支持格式：urlencoded 

请求示例

|  名称  |  类型  |          说明          |
| :----: | :----: | :--------------------: |
| limit  | string | 返回个数限制（默认20） |
| offset | string |         偏移量         |


```bash
curl -k -X GET 'http://192.168.1.78:4096/api/v2/chains'   
```

返回示例

```js
{
    success: true,
    count: 1,
    chains: [{
        tid: "4f322b6932870e710254c92a77fd892e81462aabd347ea3f0108173c5538d620",
        name: "test",
        desc: "test chain",
        link: "https://github.com/testchain.zip",
        icon: "https://github.com/testchain.png",
        unlockNumber: 3,
        t_timestamp: 57400250,
        t_type: 200,
        t_height: 30
    }]
}
```

###  **2.11 用户自定义资产uia**  

#### **2.11.1 获取全网所有发行商**  
接口地址：/api/v2/uia/issuers  
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|limit|integer|N|限制结果集个数，最小值：0,最大值：100|
|offset|integer|N|偏移量，最小值0|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|issuers|list|元素为字典，每个字典代表一个发行商，包含发行商名字、描述、id（Asch地址）|
|count|integer|发行商总个数|

请求示例：   
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://192.168.1.78:4096/api/v2/uia/issuers?offset=0&limit=2' && echo
```

JSON返回示例：   
```js  
{
    "success": true,
    "count": 6,
    "issues": [
        {
            "tid": "e47cb4a324c079bac99158a93417a8d1bcae5c605e33b7da2eef5dfc575476b6",
            "name": "ChinaBank",
            "issuerId": "AM5ntHM1ncF2TRT2Fif7QD1zpt3xtzdyBG",
            "desc": "ChinaBank description",
            "_version_": 1
        },
        {
            "tid": "d60f9235527c960c78238b3a908fb82925ce037faab7f1475acda548a8c2a616",
            "name": "CCTime",
            "issuerId": "AECGLMi8yQVvQRDpDCB6u8qHHQF7oD7VP7",
            "desc": "CCTime desc",
            "_version_": 1
        }
    ]
}
```

#### **2.11.2 查询指定发行商的信息** 
接口地址：/api/v2/uia/issuers/:address  
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|address|string|Y|Asch账户地址|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|issuers|dict|包含发行商名字、描述、id（Asch地址）|

请求示例：   
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://192.168.1.78:4096/api/uia/issuers/ChinaBank' 
```

JSON返回示例：   
```js  
{
    "success": true,
    "issuer": {
        "tid": "e47cb4a324c079bac99158a93417a8d1bcae5c605e33b7da2eef5dfc575476b6",
        "name": "ChinaBank",
        "issuerId": "AM5ntHM1ncF2TRT2Fif7QD1zpt3xtzdyBG",
        "desc": "ChinaBank description",
        "_version_": 1
    }
}
```

#### **2.11.3 查看指定发行商的资产** 
接口地址：/api/v2/uia/issuers/:address/assets  
请求方式：GET      
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|address|string|Y|Asch账户地址|
|limit|integer|N|限制结果集个数，最小值：0,最大值：100|
|offset|integer|N|偏移量，最小值0|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|assets|list|每个元素是一个字典，每个字典是一个资产详情，包含资产名字、描述、上限（最大发行量=真实发行量*10**精度）、精度、策略、当前发行量、发行高度、发行商id，acl模式（0：黑名单，1：白名单）、是否注销|
|count|interger|该发行商注册的资产总个数（包含已注销的）|


请求示例：   
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://192.168.1.78:4096/api/v2/uia/issuers/CCTime/assets/'
```

JSON返回示例：   
```js  
{
    "success": true,
    "count": 1,
    "assets": [
        {
            "name": "koumei.KMC",
            "tid": "265a358d74e8b9ec9101028b558e89ac13b7c44a4e8e7a334dae72335b83d1ae",
            "timestamp": 66763432,
            "maximum": "100000000000000000",
            "precision": 8,
            "quantity": "10000000000000000",
            "desc": "koumei.KMC description",
            "issuerId": "AMRRCyxxgQeRwhdtFXjozsqKxFBEfF1uvJ",
            "_version_": 2
        }
    ]
}
```

#### **2.11.4 获取全网所有资产信息** 
接口地址：/api/v2/uia/assets  
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|limit|integer|N|限制结果集个数，最小值：0,最大值：100|
|offset|integer|N|偏移量，最小值0|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|assets|list|每个元素是一个字典，每个字典是一个资产详情，包含资产名字、描述、上限、精度、策略、当前发行量、发行高度、发行商id，acl、是否注销|
|count|integer|所有资产的个数|

请求示例：   
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://192.168.1.78:4096/api/uia/assets?offset=0&limit=2' && echo
```

JSON返回示例：   
```js  
{
    "success": true,
    "count": 7,
    "assets": [
        {
            "name": "ChinaBank.BTC",
            "desc": "ChinaBank.BTC description",
            "maximum": "2100000000000000",
            "precision": 8,
            "quantity": "100000000000000",
            "issuerId": "AM5ntHM1ncF2TRT2Fif7QD1zpt3xtzdyBG",
            "writeoff": 0,
            "maximumShow": "21000000",
            "quantityShow": "1000000"
        },
        {
            "name": "ChinaBank.CNY",
            "desc": "ChinaBank.CNY description",
            "maximum": "500000000000",
            "precision": 3,
            "quantity": "2000000000",
            "issuerId": "AM5ntHM1ncF2TRT2Fif7QD1zpt3xtzdyBG",
            "writeoff": 0,
            "maximumShow": "500000000",
            "quantityShow": "2000000"
        },
        {
            "name": "CCTime.XCT",
            "desc": "CCTime.XCT description",
            "maximum": "1000000000000000000",
            "precision": 8,
            "quantity": "50000000000000000",
            "issuerId": "AECGLMi8yQVvQRDpDCB6u8qHHQF7oD7VP7",
            "writeoff": 0,
            "maximumShow": "10000000000",
            "quantityShow": "500000000"
        }
    ]
}
```

#### **2.11.5 获取指定资产信息** 
接口地址：/api/v2/uia/assets/:name  
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|name|string|Y|资产名|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|assets|dict|包含资产名字、描述、上限、精度、当前发行量、发行高度、发行商id|

请求示例：   
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://192.168.1.78:4096/api/v2/uia/assets/CCTime.XCT'
```

JSON返回示例：   
```js  
{
    "success": true,
    "asset": {
        "name": "CCTime.XCT",
        "desc": "CCTime.XCT description",
        "maximum": "1000000000000000000",
        "precision": 8,
        "quantity": "50000000000000000",
        "issuerId": "AECGLMi8yQVvQRDpDCB6u8qHHQF7oD7VP7",
        "writeoff": 0,
        "maximumShow": "10000000000",
        "quantityShow": "500000000"
    }
}
```

#### **2.11.6 获取指定账户所有uia的余额** 
接口地址：/api/uia/balances/:address  
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|address|string|Y|账户地址|
|limit|integer|N|限制结果集个数，最小值：0,最大值：100|
|offset|integer|N|偏移量，最小值0|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|balances|list|拥有的资产详情列表，每个元素是一个资产，包含资产名、余额、上限、精度、当前发行量、是否注销（0：未注销，1：已注销）|
|count|integer|当前该地址拥有的资产个数|

请求示例：   
```js   
curl -X GET -H "Content-Type: application/JSON" 'http://192.168.1.78:4096/api/uia/balances/AKKHPvQb2A119LNicCQWLZQDFxhGVEY57a' && echo
```

JSON返回示例：  


### **2.12 智能合约**
#### **2.12.1 查询智能合约列表**
接口地址：/api/v2/contracts/  
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|name|string|N|合约名称|
|ownerId|string|N|创建人地址|
|address|string|N|合约地址|
|limit|integer|N|限制结果集个数，最小值：0,最大值：100|
|offset|integer|N|偏移量，最小值0|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|contracts|list|合约信息列表，包括：合约Id, 合约名称，交易Id，合约地址，合约创建者地址，合约虚拟机版本，是否优先使用创建者能量，合约描述，创建时间
|count|integer|符合条件的合约数量|

请求示例：   
```sh   
curl -X GET -H "Content-Type: application/JSON" 'http://192.168.1.78:4096/api/v2/contracts/?ownerId=ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5' && echo
```
返回示例
```json
{
  "success": true,
  "count": 1,
  "contracts": [
    {
      "id": 58,
      "name": "test-contract",
      "tid": "2273aeb3aedff822d4263066216ed8709995d9701d2dd6239f9dceb8813c4604",
      "address": "SFcxEbU7sK2UuYRgqeK6chBX4uDAs8eyLj",
      "ownerId": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
      "vmVersion": "v0.1",
      "consumeOwnerEnergy": 0,
      "desc": "test contract",
      "timestamp": 87580096
    }
  ]
}
```

#### **2.12.2 查询智能合约详细信息**
接口地址：/api/v2/contracts/:name 
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|name|string|Y|合约名称|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|contract|object|合约详细信息，包括：合约Id, 合约名称，交易Id，合约地址，合约创建者地址，合约虚拟机版本，是否优先使用创建者能量，合约描述，合约代码，合约元数据，创建时间


请求示例：   
```sh   
curl -X GET -H "Content-Type: application/JSON" 'http://192.168.1.78:4096/api/v2/contracts/sample' && echo
```
返回示例
```json
{
  "success": true,
  "contract": {
    "id": 58,
    "tid": "2273aeb3aedff822d4263066216ed8709995d9701d2dd6239f9dceb8813c4604",
    "name": "test-contract",
    "address": "SFcxEbU7sK2UuYRgqeK6chBX4uDAs8eyLj",
    "ownerId": "ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5",
    "consumeOwnerEnergy": 0,
    "desc": "test contract",
    "vmVersion": "v0.1",
    "code": "...", //省略详细代码
    "metadata": {...} //省略详细元数据
    "timestamp": 87580096
  }
}
```

#### **2.12.3 查询智能合约代码**
接口地址：/api/v2/contracts/:name/code
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|name|string|Y|合约名称|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|code|string|合约代码 |

请求示例：   
```sh   
curl -X GET -H "Content-Type: application/JSON" 'http://192.168.1.78:4096/api/v2/contracts/sample/code' && echo
```
返回示例
```json
{
  "success": true,
  "code": "..." //省略详细代码
}
```
#### **2.12.4 查询智能合约元数据**
接口地址：/api/v2/contracts/:name/metadata
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|name|string|Y|合约名称|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|metadata|object|合约元数据 |

请求示例：   
```sh   
curl -X GET -H "Content-Type: application/JSON" 'http://192.168.1.78:4096/api/v2/contracts/sample/metadata' && echo
```
返回示例
```json
{
  "success": true,
  "metadata": {...} //省略详细元数据
}
```
#### **2.12.5 查询智能合约公开状态**
接口地址：/api/v2/contracts/:name/states/:path
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|name|string|Y|合约名称|
|path|string|Y|状态的路径，状态路径是用'.'号分隔的一个字符串，表示要查询的状态所在的合约对象的位置。如：'amount'表示查询合约的amount属性，'payments.0'表示payments对象的第0个元素，'paymentOfAddress.ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5'表示合约的paymentOfAddress['ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5']。以此类推|

需要注意的是，**该方法仅可查询公开的简单属性的值，否则会失败**。如amount是`private`的则查询会失败。如paymentOfAddress的类型是`Mapping<Payment>`这种复杂类型，查询也会失败。如需实现更复杂的查询，请参考智能合约开发文档，使用查询方法。

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|data|any|状态值|

请求示例：   
```sh   
curl -X GET -H "Content-Type: application/JSON" 'http://192.168.1.78:4096/api/v2/contracts/sample/states/amount' && echo
```
返回示例
```json
{
  "success": true,
  "amount": 100
}
```
#### **2.12.6 查询智能合约执行结果**
接口地址：/api/v2/contracts/:name/results/:tid
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|name|string|Y|合约名称|
|tid|string|Y|执行合约的交易Id|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|result|object|合约执行结果(包括合约注册、合约调用或向合约转账), 包括是否执行成功，错误信息(如果失败），消耗的Gas等信息|

请求示例：   
```sh   
curl -X GET -H "Content-Type: application/JSON" 'http://192.168.1.78:4096/api/v2/contracts/sample/results/2273aeb3aedff822d4263066216ed8709995d9701d2dd6239f9dceb8813c4604' && echo
```
返回示例
```json
{
  "success": true,
  "result": {
    "gas": 5492,
    "error": "",
    "stateChangesHash": "5feceb66ffc86f38d952786c6d696c79c2dbc239dd4e91b46729d73a27fb57e9",
    "tid": "2273aeb3aedff822d4263066216ed8709995d9701d2dd6239f9dceb8813c4604",
    "contractId": 58,
    "success": true
  }
}
```

#### **2.12.7 调用查询方法**
接口地址：/api/v2/contracts/:name/constants/:method
请求方式：GET   
支持格式：urlencoded 

请求参数说明：

|名称	|类型   |必填 |说明              |
|------ |-----  |---  |----              |
|name|string|Y|合约名称|
|method|string|Y|查询方法名称|
|args|json|Y|查询方法参数数组，以json形式放在请求的body中。查询方法参数必须是数组，如果没有参数请使用空数组|

返回参数说明：   

|名称	|类型   |说明              |
|------ |-----  |----              |
|success|boolean  |是否成功 |
|data|any|查询方法返回的结果|

请求示例
```sh
curl -H "Content-Type: application/json" -k -X POST -d '["ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5"]' 'http://192.168.1.78:4096/api/v2/contracts/sample/constant/getTimes'
```
表示如下调用的返回结果
```javascript
  getTimes('ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5')
```

返回示例
```json
{
  "success": true,
  "data": 100
}
```

## **3. 事务接口**   

### **请求过程说明**

通过asch-js里面封装好的transaction.createTransactionEx(params)方法获得到transaction,然后将这个transaction POST 发送到peer/transactions路由。

params是一个对象，先介绍下它的所含属性。

- **type：     交易类型**

- **fee：        手续费**

- **args：      交易所需参数**

- **message：备注**

- **secret：     发送者密码**

- **secondSecret：二级密码**

  对于不同的交易，交易类型，手续费及所需要的参数是不同的。

  下面列举一个转账交易的例子

```js
let message = '备注' ，amount = 50*100000000,
    recipient = 'A3w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ',  //(只是给出地址格式，并非有效地址)
    mySecret = 'cat craft often annual face marriage lyrics clutch room helmet crowd biology',
    secondSecret = 'abcd12345'
let args = [amount,recipient],  //第一个参数是转账金额，第二个参数是目标地址
     
//构造params对象
let params = {
        type:1,      //转账的交易类型是1  
        fee:0.1*100000000,    //转账的手续费是0.1XAS
        args：args  //交易所需要的参数
        message,    //做一些备注（非必需）
        secret:mySecret,   //我的密码（发送这笔交易的人的secret）
        secondSecret:mySecondSecret}  //二级密码（没设置可以填null，但有些交易必需使用）

//到这里位置所需要的params对象就构造好了，下面将这个对象交给asch-js里的createTransactionEx()接口
let aschjs = require('asch-js')
//这个方法返回的transaction就是需要提交到服务器的交易数据
let transaction = aschjs.transaction.createTransactionEx(params) 

//http.POST(transaction)  transaction
//这里的http.POST就是将transaction提交上去的概念，并非有效代码

//下面使用curl命令举个例子
curl -H "Content-Type: application/json" -H "magic:594fe0f3" -H "version:''" -k -X POST -d '{"transaction":transaction}' 'http://192.168.1.78:4096/peer/transaction'

//JS代码举例  http.POST()函数内容示例如下 
 axios({
        method: 'post',
        url: 'http://192.168.1.78:4096/peer/transactions',
        json:true,
        data:{
            transaction:transaction
        },
        headers:{
            'Content-Type':'application/json',
            'version':'',
            'magic':'594fe0f3'
        }
    }).then(function(response){
        console.log(response.data)
    }).catch(function(error){
        //logger.error(error)
        console.error(error)
    })

//上述步骤成功后应该返回的是成功交易的交易ID
{success: true,transactionId:"609074700dcea17b56e5a98bbfeee5f6416935b6b444c0750e5cb319d818a502"}
```

以上就是调用一次交易的全部过程，其实对于不同的交易，所需要变换的变量有type，fee，args这三个属性。

下面枚举所有交易所需要的这三个属性（主要是这三个属性）

XAS的精度是小数点后八位，所以使用XAS币的时候需要乘上100000000，为了简洁，下面使用XAS的时候替换如下：

  **const   XAS = 100000000**

### **3.1 基础交易**   

#### **3.1.1 转账**   
- **type：1**

- **fee：   0.1*XAS**

- **args： [amount，recipient]**

  |   名称    |  类型  |   说明   |
  | :-------: | :----: | :------: |
  |  amount   | number | 转账金额 |
  | recipient | string | 接收地址 |

  代码示例

  ```js
  //args参数示例
  let amount =  100*XAS   //转账金额
  let recipent = 'A3w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'    //接收地址
  let args = [amount,recipent]
  
  //构造params对象
  let params = {
          type:1,      //转账的交易类型是1  
          fee:0.1*100000000,    //转账的手续费是0.1XAS
          args：args  //交易所需要的参数
          message,    //做一些备注（非必需）
          secret:mySecret,   //我的密码（发送这笔交易的人的secret）
          secondSecret:mySecondSecret}  //二级密码（没设置可以填null，但有些交易必需使用）
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.2 设置昵称**

- **type：2**

- **fee：  1/10/40/80/100/200 *XAS**

- **args： [name]**

  这里对手续费要左下说明，对于名字越长，手续费越便宜（有上限）

  len-fee关系表

  | len  |   fee   |
  | :--: | :-----: |
  |  2   | 200*XAS |
  |  3   | 100*XAS |
  |  4   | 80*XAS  |
  |  5   | 40*XAS  |
  | 6-10 | 10*XAS  |
  | >10  |  1*XAS  |

  | 名称 |  类型  | 说明 |
  | :--: | :----: | :--: |
  | name | string | 昵称 |

  代码示例

  ```js
  //args参数示例
  let name = 'username1'
  let args = [name]
  
  //构造params对象
  let params = {
          type:2,      //转账的交易类型是1  
          fee:10*100000000,    //转账的手续费是0.1XAS
          args：args  //交易所需要的参数
          message,    //做一些备注（非必需）
          secret:mySecret,   //我的密码（发送这笔交易的人的secret）
          secondSecret:mySecondSecret}  //二级密码（没设置可以填null，但有些交易必需使用）
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
   http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.3 设置二级密码**   

- **type：3**

- **fee：   5*XAS**

- **args： [secondSecret]**

  |     名称     |  类型  |       说明       |
  | :----------: | :----: | :--------------: |
  | secondSecret | string | 二级密码(加密后) |

  ```js
  
  //这个SecondSecret是加密后的字符串
  let password = 'asch123456'
  let hash = sha256Bytes(new Buffer(password))
  let keypair = nacl.sign.keyPair.fromSeed(hash);
  let secondSecret = new Buffer(keypair.publicKey).toString("hex")
  //得到将password加密后的secondSecret作为参数
  let args = [secondSecret]  
  //构造params对象
  let params = {
          type:3,  
          fee:5*100000000,    
          args：args
          message,   
          secret:mySecret,   
          secondSecret:null} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```


#### **3.1.4 锁仓**

- **type：4**

- **fee：   0.1*XAS**

- **args： [height,amount]**

  |  名称  |  类型  |    说明    |
  | :----: | :----: | :--------: |
  | height | number | 锁定的高度 |
  | amount | number | 锁定的金额 |

  代码示例	

  ```js
  //args参数示例
  let height = 64200,amount = 20000*XAS
  let args = [height,amount]
  //构造params对象
  let params = {
          type:4,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.5 解锁仓库**

- **type：5**

- **fee：  0*XAS**

- **args： []**

  代码示例

  ```js
  let params = {
          type:5,   
          fee:0*100000000,  
          args：[]  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.6 设置理事会**

- **type：6**

- **fee：   5*XAS**

- **args： [name,members,min,max,m,updateInterval]**

  |      名称      |  类型  |        说明         |
  | :------------: | :----: | :-----------------: |
  |      name      | string |     理事会名称      |
  |    members     | array  |       成员组        |
  |      min       | number | 最少决策数(最少为3) |
  |      max       | number |     最多决策数      |
  |       m        | number |   决策权值最小值    |
  | undateInterval | number |      更新间隔       |

  代码示例

  ```js
  let name = 'group1'
  let members = [
      {
          name:'asch_g1',      //成员名称
          weight:2,            //成员的权重
          address:'ANge1aRG19tdXcFKu8x6mGHg9PgGdXN69L'   //成员地址
      },
      {
          name:'asch_g2',
          weight:3,
          address:'AFr8jiEcwDV4P1t73xTF19N86HvufFGCzE'
      },
      {
          name:'asch_g1',
          weight:6,
          address:'AMshd1Q5rp3jWpkx9BvgYT6NmeBMxe5TZo'
      },
      {
          name:'asch_g1',
          weight:1
          address:'ADSGULRigKYJAtc29zAqM4gGk9LuCJmryv'
      },
      {
          name:'asch_g1',
          weight:1,
          address:'A3rfxqBbL1bkEnAXT8CsJEnoRg2NzGiXFQ'
      }
  ]
  let min = 3
  let max = 5
  let m = 6
  let undateInterval = 1
  let params = {
          type:6,   
          fee:5*100000000,  
          args：[name,members,min,max,m,undateInterval]  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.7 注册代理人**

- **type：7**

- **fee：   100*XAS**

- **args： []**

  说明：无需传入参数

  代码示例

  ```js
  let params = {
          type:7,   
          fee:100*100000000,  
          args：[]  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.8 设置代理人**

- **type：8**

- **fee：   0.1*XAS**

- **args： [agent]**

  | 名称  |  类型  |     说明     |
  | :---: | :----: | :----------: |
  | agent | string | 代理人的昵称 |

  ```js
  let agent = 'user1'
  let args = [agent]
  
  let params = {
          type:8,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.9 取消代理人**

- **type：9**

- **fee：   0*XAS**

- **args： []**

  代码示例

  ```js
  let params = {
          type:9,   
          fee:0*100000000,  
          args：[]  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.10 注册委托人**

- **type：10**

- **fee：   100*XAS**

- **args： []**

  代码示例

  ```js
  let params = {
          type:10,   
          fee:100*100000000,  
          args：[]  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.11 给委托人投票**

- **type：11**

- **fee：   0.1*XAS**

- **args： [delegates]**

  |   名称    |  类型  |       说明       |
  | :-------: | :----: | :--------------: |
  | delegates | string | 一些受托人的名字 |

  代码示例

  ```js
  //delegate1,delegate2,delegate3分别为三个受托人的姓名
  let delegates = 'delegate1,delegate2,delegate3'   
  let args = [delegates]
  
  let params = {
          type:11,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.1.12 取消给委托人投票**

- **type：12**

- **fee：   0.1*XAS**

- **args： [delegates]**

  |   名称    |  类型  |       说明       |
  | :-------: | :----: | :--------------: |
  | delegates | string | 一些受托人的名字 |

  代码示例

  ```js
  let delegates = 'delegate1,delegate2'   //delegate1,delegate2,delegate3分别为三个受托人的姓名 
  let args = [delegates]
  let params = {
          type:12,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

###  **3.2 资产**

#### **3.2.1 注册发行商**

- **type：100**

- **fee：   100*XAS**

- **args： [name,desc]**

  | 名称 |  类型  |     说明     |
  | :--: | :----: | :----------: |
  | name | string |  发行商名字  |
  | desc | string | 一些文字描述 |

  代码示例

  ```js
  //args参数示例
  let name = 'TEST'
  let desc = 'my first issuer'
  let args = [name,desc]
  
  let params = {
          type:100,   
          fee:100*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.2.2 注册资产**

- **type：101**

- **fee：   500*XAS**

- **args： [symbol,desc,maximum,precsion]**

  |   名称   |  类型  |     说明     |
  | :------: | :----: | :----------: |
  |  symbol  | string |   资产名称   |
  |   desc   | string | 一些文字描述 |
  | maximum  | string |  最大发行量  |
  | precsion | number |     精度     |

  代码示例

  ```js
  //args参数示例
  let symbol = 'TXC'   //资产名由三个大写字母组成
  let desc = 'my first asset'
  let maximum = '100000000000'
  let precsion = 1     //取值范围是1-16之间的整数
  //组成args
  let args = [symbol,desc,maximum,precsion]
  let params = {
          type:101,   
          fee:500*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.2.3 发行资产**

- **type：102**

- **fee：   0.1*XAS**

- **args： [name,amount]**

  |  名称  |  类型  |      说明      |
  | :----: | :----: | :------------: |
  |  name  | string | 要发行的资产名 |
  | amount | string |    发行数量    |

  代码示例

  ```js
  //args参数示例
  let name = 'TEST.TXC'    //资产名=发行商名称.代币名
  let amount = '1000000000'
  let args = [name,amount]
  let params = {
          type:102,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.2.4 内部转账**

- **type：103**

- **fee：   0.1*XAS**

- **args： [currency,amount,recipient]**

  |   名称    |  类型  |    说明    |
  | :-------: | :----: | :--------: |
  | currency  | string | 内部资产名 |
  |  amount   | string |  转账金额  |
  | recipient | string |  接收地址  |

  代码示例

  ```js
  //args参数示例
  let currency = 'TEST.TXC'
  let amount = '10000000'
  let recipient = 'A3w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'
  //args组成
  let args = [currency,amount,recipient]
  let params = {
          type:103,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

### **3.3 侧链DApp**

#### **3.3.1 注册侧链DApp**

- **type：200**

- **fee：   100*XAS**

- **args： [name,desc,link,icon,delegates,unlockNumber]**

  |     名称     |  类型  |    说明    |
  | :----------: | :----: | :--------: |
  |     name     | string |   dapp名   |
  |     desc     | string |    描述    |
  |     link     | string |    链接    |
  |     icon     | string |    图标    |
  |  delegates   | string |   委托人   |
  | unlockNumber | number | 最少需求数 |

  代码示例

  ```js
  //args内参数说明
  let name = 'dappTest'        //dapp名称
  let desc = '一些文本描述'
  let link = 'http://yourdomain/dapp.zip'     //dapp的安装文件链接
  let icon = 'htpps//yourdomain/logo.png'     //dapp的图标链接
  //委托人数组delegate是一个数组，里面的数据是委托人的私钥
  let delegates = [
      "0352486d87c928918638c8a13c7e4765f2c9fa075318bd680b8d95e1cf1d616f",
      "cbb3671d343628fe03fba2f0139b783a7b86445f79ee55c99bf5bbe380e4fb46",
      "2f23a9659e32032910b8e078c0c980c6cb7c3a052a235a59079bfd6d608ecc95",
      "351c081c470f41620f4709b6b3ca3721dc920d4e528b27b8fa4d88635e53e128",
      "cbd808111a08081f7dc93aafd9fe26a70216e3f42d927660ab8d15b7bdf8998c"
  ]
  //最少需要的委托人个数（需要委托人共同决定）
  let unlockNumber = 3
  //构建args
  let args = [name,desc,link,icon,delegates,unlockNumber]
  
  let params = {
          type:200,   
          fee:100*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.3.2 修改委托人**

- **type：201**
- **fee：   1*XAS**
- **args： [chain,from,to]**

#### **3.3.3 增加委托人**

- **type：202**
- **fee：   1*XAS**
- **args： [chain,key]**

#### **3.3.4 删减委托人**

- **type：203**
- **fee：   1*XAS**
- **args： [chain,key]**

#### **3.3.5 充值到侧链DApp**

- **type：204**

- **fee：   0.1*XAS**

- **args： [chainName,currency,amount]**

  |   名称    |  类型  |      说明      |
  | :-------: | :----: | :------------: |
  | chainName | string | 应用名（dapp） |
  | currency  | string |    资产币名    |
  |  amount   | string |    金额数量    |

  代码示例

  ```js
  //args参数示例
  let chainName = 'dappTest'
  let currency = 'XAS'   //也可以是TEST.TXC内部资产币
  let amount = '1000000000'
  //args构造
  let args = [chainName,currency,amount]
  let params = {
          type:204,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.3.6 从侧链DApp提现**

- **type：205**

- **fee：   0.1*XAS**

- **args： [chainName,recipient,currency,amount,oid,seq]**

  |   名称    |  类型  |   说明   |
  | :-------: | :----: | :------: |
  | chainName | string |  应用名  |
  | recipient | string | 接收地址 |
  | currency  | string |  资产名  |
  |  amount   | string | 提现金额 |
  |    oid    | string |          |
  |    seq    | string |          |

  **备注**：该交易不由用户或开发者发起

### **3.4 提案相关**

#### **3.4.1 发起提案**

- **type：300**

- **fee：   10*XAS**

- **args： [title,desc,topic,content,endHeight]**

  |   名称    |  类型  |     说明     |
  | :-------: | :----: | :----------: |
  |   title   | string |   提案标题   |
  |   desc    | string |     描述     |
  |   topic   | string |   提案类型   |
  |  content  | string |     内容     |
  | endHeight | string | 提案结束日期 |

  代码示例

  ```js
  //args参数示例
  let title = 'title fo propose'     //  len: 10-100
  let desc = 'some describes of this propose'
  let topic = '提案的类型(下面详细介绍)'
  let content = '提案类型所需要的参数（下面详细介绍）'
  let endHeight = 50000     //结束高度
  //构造args
  let args = [title,desc,topic,content,endHeight]
  let params = {
          type:300,   
          fee:10*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

  对不同提案类型给出不同的参数

  1. 新增网关

  ```js
  //提案类型
  let topic = 'gateway_register'
  //下面构造content,对于新增网关提案，需要提供提案的名称，描述，最少成员，更新间隔，资产信息等
  let name = 'aschCoin'   //3-16位大小写字母数字
  let desc = 'test the gateway register'
  let minimumMembers = 3      //网关最少成员数，这个数值的范围应当在3-33之间的整数，
  let updateInterval = 8640   //更新频率，这个值应当是大于8640的
  
  let symbol = 'TEC'   //比如发行的币叫TEC
  let currencyDesc = 'some describes of currency'    //资产描述
  let precision = 1      //资产精度
  let currency = {symbol:symbol,
                  desc:currencyDesc,
                  precision:precision}
  //下面构造这个content
  let content = {name:name,
                 desc:desc,
                 minimumMembers:minimumMembers,
                 updateInterval:updateInterval,
                 currency:currency}
  ```

  2. 网关初始化

  ```js
  //提案类型
  let topic = 'gateway_init'
  //下面构造content
  let gateway = 'bitcoin'     //网关的名字
  let members = [             //初始网关的成员
      'A5eTVn2Mz5p2j6SjGKdgvmUc2vMsSvKzuy',
      'A3SmW61ZwxmNc26BbfKLbHkaNbmUQzexuj',
      'A4ncaYtKRrD8YS2Mi82HbwGEE9DxqsbEr9'
  ]
  //下面构造这个content
  let content = {gateway:gateway,
                 members:members
                }
  ```

  3.  更新网关成员

  ```js
  //提案类型
  let topic = 'gateway_update_member'
  //下面构造content
  let gateway = 'bitcoin'     //网关的名字
  let from = 'A3SmW61ZwxmNc26BbfKLbHkaNbmUQzexuj'   //要撤销的成员地址
  let to = 'A7w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'     //要添加的成员地址
  //下面构造这个content
  let content = {gateway:gateway,
                 from:from,
                 to:to
                }
  ```

  4. 网关撤销

  ```js
  //提案类型
  let topic = 'gateway_revoke'     //这个参数较少，只需要网关的名字即可
  //下面构造content
  let gateway = 'bitcoin'     //网关的名字
  //下面构造这个content
  let content = {gateway:gateway}
  ```

#### **3.4.2 给提案投票**

- **type：301**

- **fee：   0.1*XAS**

- **args： [pid]**

  | 名称 |  类型  |    说明    |
  | :--: | :----: | :--------: |
  | pid  | string | 提案的编号 |

  代码示例

  ```js
  //args参数示例
  let pid = 'aer074700dcea17b56e5a98bbfeee5f6416935b6b444c0750e5cb319d818a502'        /*发起提案的交易id*/
  //构造args
  let args = [pid]
  let params = {
          type:301,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.4.3 激活提案**

- **type：302**

- **fee：   0*XAS**

- **args： [pid]**

  | 名称 |  类型  |    说明    |
  | :--: | :----: | :--------: |
  | pid  | string | 提案的编号 |

  代码示例

  ```js
  //args参数示例
  let pid = 'aer074700dcea17b56e5a98bbfeee5f6416935b6b444c0750e5cb319d818a502'        /*发起提案的交易id*/
  //构造args
  let args = [pid]
  let params = {
          type:302,   
          fee:0*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

### **3.5 网关**

#### **3.5.1 开通网关账户**

- **type：400**

- **fee：   0.1*XAS**

- **args： [gateway]**

  |  名称   |  类型  |    说明    |
  | :-----: | :----: | :--------: |
  | gateway | string | 网关的名字 |

  代码示例

  ```js
  //args参数示例
  let gateway = 'bitcoin'     //网关名字
  let args = [gateway]
  let params = {
          type:400,   
          fee:0.1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.5.2 注册成员**

- **type：401**

- **fee：   100*XAS**

- **args： [pid]**

  |   名称    |  类型  |   说明   |
  | :-------: | :----: | :------: |
  |  gateway  | string | 网关名字 |
  | publicKey | string | 成员公钥 |
  |   desc    | string |   描述   |

  代码示例

  ```js
  //args参数示例
  let gateway = 'bitcoin'
  let publicKey = 'c03e43c7e8aefe3b5a83e02a7b4dc8cce84bb787202650338e85d1b7758065d6'
  let desc = 'some describes of resgiter member'
  //构造args
  let args = [gateway,publicKey,desc]
  
  let params = {
          type:401,   
          fee:100*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.5.3 对网关充值**

- **type：402**

- **fee：   0.01*XAS**

- **args： [gateway,address,currency,amount,oid]**

  |   名称   |  类型  |   说明   |
  | :------: | :----: | :------: |
  | gateway  | string | 网关名字 |
  | address  | string | 存款地址 |
  | currency | string |   货币   |
  |  amount  | string |   数额   |
  |   oid    | string |          |

  代码示例

  ```js
  //args参数示例
  let gateway = 'bitcoin'
  let address = 'A7w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'
  let currency = 'BTC'
  let amount = '100000000000'
  let oid = ''
  //构造args
  let args = [gateway,address,currency,amount,oid]
  let params = {
          type:402,   
          fee:0.01*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.5.4 从网关提现**

- **type：403**

- **fee：   0*XAS**

- **args： [address,gateway,currency,amount,fee]**

  |   名称   |  类型  |   说明   |
  | :------: | :----: | :------: |
  | address  | string | 提现地址 |
  | gateway  | string | 网关名字 |
  | currency | string |   货币   |
  |  amount  | string |   数量   |
  |   fee    | string |  手续费  |

  代码示例

  ```js
  //args参数说明
  let gateway = 'bitcoin'
  let address = 'A7w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'
  let currency = 'BTC'
  let amount = '100000000000'    //转账的金额
  let fee = '200000000'          //网关收取的手续费
  //构造args
  let args = [address,gateway,currency,amount,fee]
  let params = {
          type:403,   
          fee:0*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.5.5 提交提现交易**

- **type：404**

- **fee：   0.01*XAS**

- **args： [wid,ot,ots]**

  | 名称 |  类型  |   说明   |
  | :--: | :----: | :------: |
  | wid  | string |  提现id  |
  |  ot  | string | 交易数据 |
  | ots  | string |          |

**备注**：该操作由系统自动完成，不由用户或开发者发起


#### **3.5.6 提交交易签名**

- **type：405**

- **fee：   0.01*XAS**

- **args： [wid,signature]**

  |   名称    |  类型  |  说明  |
  | :-------: | :----: | :----: |
  |    wid    | string | 提现id |
  | signature | string |  签名  |

**备注**：该操作由系统自动完成，不由用户或开发者发起


#### **3.5.7 提交交易协议**

- **type：406**

- **fee：   0.01*XAS**

- **args： [wid,oid]**

  | 名称 |  类型  |  说明  |
  | :--: | :----: | :----: |
  | wid  | string | 提现id |
  | oid  | string |        |


### **3.6 理事会**

#### **3.6.1 投票**

- **type：500**

- **fee：   0*XAS**

- **args： [targetId]**

  |   名称   |  类型  |  说明  |
  | :------: | :----: | :----: |
  | targetId | string | 目标ID |

  代码示例

  ```js
  //args参数示例
  let targetId = 'f80dcf3d520cc14e963ddf4aedd6ae42db92795fc80ac3738c2be5b3aa5c9238'  //交易id
  let args = [targetId]
  let params = {
          type:500,   
          fee:0*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.6.2 激活理事会**

- **type：501**

- **fee：   0*XAS**

- **args： [targetId]**

  |   名称   |  类型  |  说明  |
  | :------: | :----: | :----: |
  | targetId | string | 目标ID |

  代码示例

  ```js
  //args参数示例
  let targetId = 'f80dcf3d520cc14e963ddf4aedd6ae42db92795fc80ac3738c2be5b3aa5c9238'  //交易id
  let args = [targetId]
  let params = {
          type:501,   
          fee:0*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.6.3 增加成员**

- **type：502**

- **fee：  1*XAS**

- **args： [address,weight,m]**

  |  名称   |  类型  |   说明   |
  | :-----: | :----: | :------: |
  | address | string | 成员地址 |
  | weight  | string |   权重   |
  |    m    | number |          |

  代码示例

  ```js
  //args参数示例
  let address = 'AMySpLqC4bEgQ8VoYK1iWNEEuhRtjS59Bt'  
  let weight = ''
  let m = 1
  let args = [address,weight,m]
  let params = {
          type:502,   
          fee:1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.6.4 移除成员**

- **type：503**

- **fee：   1*XAS**

- **args： [address,m]**

  |  名称   |  类型  | 说明     |
  | :-----: | :----: | -------- |
  | address | string | 成员地址 |
  |    m    | number |          |

  代码示例

  ```js
  //args参数示例
  let address = 'AMySpLqC4bEgQ8VoYK1iWNEEuhRtjS59Bt'  
  let m = 1
  let args = [address,m]
  let params = {
          type:503,   
          fee:1*100000000,  
          args：args  
          message, 
          secret:mySecret,  
          secondSecret:mySecondSecret} 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

### **3.7 智能合约**

#### **3.7.1 注册智能合约**
- **type：600**

- **fee：  0**

- **args： [gasLimit, name, version, desc, code, consumeOwnerEnergy]**

  |  名称   |  类型  | 说明     |
  | :-----: | :----: | -------- |
  | gasLimit | number | 注册合约最大可消耗的Gas，100 <= gasLimit <= 10000000 |
  | name     | string | 智能合约名称，全网唯一，4~32 个字符组成。必须是字母开头，可包含字母、数字或下划线  |
  | version  | string | 合约引擎版本，该参数未来可能取消，测试时请填v0.3  | 
  | desc     | string | 不超过255个字符，对合约描述信息 | 
  | code     | string | 合约代码，长度不超过32K | 
  |consumeOwnerEnergy|boolean|是否优先消耗创建者能量|

  代码示例

  ```js
  //args参数示例
  const gasLimit = 5000000
  const name = 'test-contract'
  const version = 'v0.3'
  const desc = '这是一个测试合约'
  const code = '...'// 合约代码
  
  let args = [gasLimit, name, version, desc, code, true]
  let params = {
    type:600,   
    fee: 0,  
    args, 
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret } 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明
  ```

#### **3.7.2 调用智能合约**
- **type：601**

- **fee：  0**

- **args： [gasLimit, enablePayGasInXAS, name, method, methodArgs]**

  |  名称   |  类型  | 说明     |
  | :-----: | :----: | -------- |
  | gasLimit | number | 注册合约最大可消耗的Gas，100 <= gasLimit <= 10000000 |
  |enablePayGasInXAS|boolean|当调用者能量不足时是否使用XAS抵扣Gas|  
  | name     | string | 智能合约名称|
  | method   | string | 调用的合约方法名称 | 
  | methodArgs| array | 调用合约方法的参数数组 | 

  代码示例

  ```js
  //args参数示例
  const gasLimit = 5000000
  const name = 'test-contract'
  const method = 'increase'
  const methodArgs = [1, 'test']
  
  let args = [gasLimit, name, true,  method, methodArgs]
  let params = {
    type:601,   
    fee: 0,  
    args, 
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret } 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明

  //上述代码相当于调用合约中的方法如下：
  increase(1, 'test')

  ```

#### **3.7.3 向智能合约转账**
- **type：602**

- **fee：  0**

- **args： [gasLimit, enablePayGasInXAS, receiverPath, amount, currency]**

  |  名称   |  类型  | 说明     |
  | :-----: | :----: | -------- |
  | gasLimit | number | 注册合约最大可消耗的Gas，100 <= gasLimit <= 10000000 |
  |enablePayGasInXAS|boolean|当调用者能量不足时是否使用XAS抵扣Gas|  
  | receiverPath| string | 接收资产的方法路径，格式为：'合约名称或地址/接收方法名'，如果是默认的转账接收方法(请参见智能合约开发文档)，只需要写合约名称或地址即可 |
  | amount   | bigint / string | 转入合约的资产数量 | 
  | currency| string | 转入合约的资产名称 | 

**注意：由于bigint不可作为json传输**,故系统支持将字符串自动转换为`bigint`类型。`amount`支持传入bigint或string

  代码示例

  ```js
  //args参数示例
  const gasLimit = 5000000
  const reciverPath = 'test-contract/onPay'
  const amount = BigInt(100 * (10 ** 8)) // 100 XAS
  const currency = 'XAS'
  
  let args = [gasLimit, true, reciverPath, amount, currency]
  let params = {
    type:602,   
    fee: 0,  
    args, 
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret } 
  //使用asch-js生成交易信息
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  //详情见请求过程说明

  ```