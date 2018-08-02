ASCH is a blockchain application development platform based on multi-chain architecture. Follow the steps to develop DApps on the ASCH Platform:

<br/>

<p align="center">
  <img src="./images/asch-wide-logo.png" alt="logo">
</p>

<br/>
<br/>

### What is ASCH?

1.ASCH [White Paper](http://asch-public.oss-cn-beijing.aliyuncs.com/asch.io/Asch-Whitepaper-en.pdf)

2.ASCH [official website](https://www.asch.io)

3.ASCH [blockchain explorer](https://explorer.asch.io)

4.ASCH source code [repository](https://github.com/AschPlatform/asch)

5.ASCH related [documentation](https://github.com/aschplatform/asch-docs)

<br/>

### Get started with Sidechain development (tutorial)

1. Install local ASCH blockchain node  
2. Create new DApp  
3. Register your DApp on your local ASCH blockchain  
4. Start developing the business logic  

All steps are described in detail in the following tutorials:  

#### Part 1
<a href="https://medium.com/aschplatform/develop-blockchain-apps-with-sidechain-technology-part-1-c5aa91c4602f" rel="sidechain tutorial 1">
<img src="https://cdn-images-1.medium.com/max/800/1*70nbCVQ9UMKPXrJ2p90fEg.jpeg" alt="sidechain1" height="200px"/>
</a>

#### Part 2
<a href="https://medium.com/aschplatform/develop-blockchain-apps-with-sidechain-technology-part-2-b241d82f3058" rel="sidechain tutorial ">
<img src="https://cdn-images-1.medium.com/max/800/1*37r9b5DzDELOXc9xuPgpKw.jpeg" alt="sidechain2" height="200px"/>
</a>


<br/>
<br/>


### Hello World (tutorial)

1. Build ASCH [Hello World](https://github.com/AschPlatform/asch-docs/blob/master/dapp/hello_world/en.md) DApp  

3. Build ASCH [Mini DAO](https://github.com/AschPlatform/asch-docs/blob/master/dapp/mini_dao/en.md) DApp  


### ASCH Sample DApps

- CCTime: [Sidechain-Backend](https://github.com/AschPlatform/cctime) and [Sidechain-Frontend](https://github.com/AschPlatform/cctime-frontend)
- Hello-World: [Frontend and Backend](https://github.com/AschPlatform/asch-dapp-helloworld)


### Documentation
- [Dapp Javascript SDK](https://github.com/AschPlatform/asch-docs/blob/master/sdk_api/en.md)
- [Dapp Http API](https://github.com/AschPlatform/asch-docs/blob/master/dapp/api/en.md)
- [ASCH Http API](https://github.com/AschPlatform/asch-docs/blob/master/http_api/en.md)

### Tools  
- asch-js [repository](https://github.com/aschplatform/asch-js), [documentation](https://github.com/AschPlatform/asch-docs/blob/master/js_api/en.md)
- asch-cli [repository](https://github.com/aschplatform/asch-cli), [documentation](https://github.com/AschPlatform/asch-docs/blob/master/cli_usage/en.md)
- asch-redeploy [repository](https://github.com/aschplatform/asch-redeploy), [documentation](https://github.com/AschPlatform/asch-redeploy/blob/master/README.md)

<br/>
<br/>


### Create an Account

ASCH provides a series of development tools for the blockchain application development, including SDK, a command-line tool as well as a series of REST API interfaces. Developers can choose the right development tools according to their preferences and environment.  

The following are ways to use different tools to create an account, for example:  

#### 1. Call API

```bash
Request：
curl -k -X GET 'https://wallet.asch.io/api/accounts/new'

# return value  
Response JSON：
{    
	success: true,
	secret: "during crush zoo wealth horror left night upset spike iron divert lawn", 
	publicKey: "261fa56f389c324fddbe8777dbc0ef3341ee7b75d1ffdc82192265633b90d503",  
	privateKey: "67c9523b7622704c4bcfe960cb32d7fa04d3eb94e30e7964d3c6a24a3647a0a3261fa56f389c324fddbe8777dbc0ef3341ee7b75d1ffdc82192265633b90d503", 
	address: "ANfXDQUZroMnrQ6vRGR7UXXtbPn3fhEVRJ" 
}
```

#### 2. Use npm `asch-js` package

Create new file `account.js`:  

```bash
touch account.js
```

Create a `package.json` file with the following command:  

```bash
npm init --yes
```

Install all needed dependencies:  

```bash
npm install --save asch-js bitcore-mnemonic
```

Paste the following code into the `account.js` file:  

```js
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

Then execute the new code:  

```bash
node -p 'require("./account").createNewAccount()'

# return value:  
{
  address: 'AMD4DNn5fKsnETVUJxBB3RB8nWNxC7goDf',
  secret: 'lecture shed style cake dentist print cool noble cloud safe ozone estate'
}
```


#### 3. Use npm `asch-cli` package  

```bash
./asch-cli crypto --generate
# ? Enter number of accounts to generate // 1

# return value  
[
  { 
    address: 'AP4CiQ7pFaazNfkv8JSqHmM1UmZ4kiqkvY',
    secret: 'glance stand fix dumb lottery exist filter peace donate shed intact cannon',
    publicKey: 'cd3559626060bd232444c3deb2b4a7a3807e7b8cf5a0558a7a0cb0a98a9ea3da'
  }
]
```

