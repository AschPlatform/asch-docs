阿希是一个多链架构的区块链应用开发平台，想要基于阿希开发区块链应用，一般要经历如下步骤：

### 一、了解阿希

阿希白皮书：http://asch-public.oss-cn-beijing.aliyuncs.com/asch.io/Asch-whitepaper-zh.pdf

阿希官网：https://www.asch.io

阿希区块链浏览器：https://explorer.asch.io

阿希源码: https://github.com/AschPlatform/asch

阿希相关文档：https://github.com/AschPlatform/asch/tree/master/docs

### 二、开发区块链应用

1.搭建本地开发节点

2.启动localnet并安装asch-cli

3.本地创建一个 Dapp 模板

4.注册应用到主链

5.部署应用代码及子网络

6.实现业务逻辑

详细可参考:

https://github.com/AschPlatform/asch/blob/master/docs/dapp_docs/1_hello.md



### 三、使用阿希开发工具

阿希为区块链应用开发提供了一系列的开发工具，包括SDK、命令行工具以及一系列的REST API接口。 开发者可以根据自己的喜好和环境选择合适的开发工具。以下是以生成账户为例，使用不同工具完成的方法：

#### 1. 调用API
```
请求：
curl -k -X GET 'http://45.32.248.33:4096/api/accounts/new'

返回JSON：
{    
	success: true,
	secret: "during crush zoo wealth horror left night upset spike iron divert lawn", // 密码 
	publicKey: "261fa56f389c324fddbe8777dbc0ef3341ee7b75d1ffdc82192265633b90d503", // 公钥 
	privateKey: "67c9523b7622704c4bcfe960cb32d7fa04d3eb94e30e7964d3c6a24a3647a0a3261fa56f389c324fddbe8777dbc0ef3341ee7b75d1ffdc82192265633b90d503", // 私钥 
	address: "ANfXDQUZroMnrQ6vRGR7UXXtbPn3fhEVRJ" // 地址 
}
```
#### 2. 使用asch-js

```
const AschJS = require('asch-js')
const Mnemonic = require('bitcore-mnemonic')

module.exports = {
  createNewAccount: function () {
    let secret = new Mnemonic(Mnemonic.Words.ENGLISH).toString()
    let keypair = AschJS.crypto.getKeys(secret)
    let address = AschJS.crypto.getAddress(keypair.publicKey)
    return {
      address: address,
      secret: secret
    }
  }
}
```
#### 3. 使用asch-cli，需要手工填写主密码
```
root@asch:~# asch-cli -H 45.32.248.33 -P 4096 openaccount "fault still attack alley expand music basket purse later educate follow ride"
{
  "address": "16723473400748954103",
  "unconfirmedBalance": 20000000000,
  "balance": 20000000000,
  "publicKey": "bd1e78c5a10fbf1eca36b28bbb8ea85f320967659cbf1f7ff1603d0a368867b9",
  "unconfirmedSignature": false,
  "secondSignature": false,
  "secondPublicKey": "",
  "multisignatures": [],
  "u_multisignatures": []
}
```

详细可参考：

API：https://github.com/AschPlatform/asch/blob/master/docs/asch_http_interface.md

Asch-cli: https://github.com/AschPlatform/asch/blob/master/docs/asch_cli_usage.md

Asch-js: https://github.com/AschPlatform/asch-js
