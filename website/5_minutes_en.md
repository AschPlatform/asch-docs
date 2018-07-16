ASCH is a blockchain application development platform based on multi-chain architecture. Follow the steps to develop DApps on ASCH Platform:

### What is ASCH?

1.ASCH White Paper: http://asch-public.oss-cn-beijing.aliyuncs.com/asch.io/Asch-whitepaper-en.pdf
2.ASCH official website: https://www.asch.io
3.ASCH blockchain explorer: https://explorer.asch.io
4.ASCH source code repository: https://github.com/AschPlatform/asch
5.ASCH related documentation: https://github.com/AschPlatform/asch/tree/master/docs

### How to develop ASCH DAPP

1.Build local development nodes
2.Start localnet and install asch-cli
3.Locally create a Dapp template
4.Registration is applied to the main chain
5.Deployment of application code and subnetwork
6.Implementation of business logic
Detailed reference：
https://github.com/AschPlatform/asch/blob/master/docs/dapp_docs/1_hello.md


### How to use the development tools

ASCH provides a series of development tools for the blockchain application development, including SDK, a command-line tool as well as a series of REST API interface. Developers can choose the right development tools according to their preferences and environments. The following are the ways to use different tools to create an account, for example:

#### 1.Call API

```
Request：
curl -k -X GET 'http://45.32.248.33:4096/api/accounts/new'

Response JSON：
{    
	success: true,
	secret: "during crush zoo wealth horror left night upset spike iron divert lawn", 
	publicKey: "261fa56f389c324fddbe8777dbc0ef3341ee7b75d1ffdc82192265633b90d503",  
	privateKey: "67c9523b7622704c4bcfe960cb32d7fa04d3eb94e30e7964d3c6a24a3647a0a3261fa56f389c324fddbe8777dbc0ef3341ee7b75d1ffdc82192265633b90d503", 
	address: "ANfXDQUZroMnrQ6vRGR7UXXtbPn3fhEVRJ" 
}
```

#### 2.using asch-js

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


#### 3.using asch-cli,you need to manually fill in the main password.

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


Detailed reference：
API：https://github.com/AschPlatform/asch/blob/master/docs/asch_http_interface.md
ASCH-js:https://github.com/AschPlatform/asch-js
ASCH-cli:https://github.com/AschPlatform/asch/blob/master/docs/asch_cli_usage.md
