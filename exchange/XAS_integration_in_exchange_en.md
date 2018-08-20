# The docking documentation between XAS and the trading platform

## 1. Basic information of Asch

Token name: XAS<br>
Main network launch time: August 16, 2016<br>
Total issuance: 100 million, the current total supply is 111 million XAS (with a dynamic inflation rate, the longer the issuance, the lower the inflation rate)<br>
Consensus algorithm: DPoS + PBFT<br>
Trading mode: account balance mode, non-UTXO<br>
Official website: https://www.asch.io<br>
Online wallet: https://mainnet.asch.io, basic features can be experienced here<br>
Blockchain explorer: https://explorer.asch.io/<br>
Address format: alphanumeric, base58 format and starting with a capital letter A with a length of not less than 10,such as A7RD9YP37iUnYZ1SFnmAp6ySHUx3msC4r5

Asch is not a copy of BTC source code, but is newly developed with Node.js. It is currently a pure HTTP API, so don't use the BTC template's trading platform code to create a hard copy when docking. Currently there are SDK versions of Java and node.js, which can be used by trading platform directly. As for other development languages, you need to encapsulate the HTTP API.

Asch does not have the concept of wallet. Each password corresponds to an account address. That is to say, a "wallet" contains only one address (essentially a computer wallet), which is quite different from BTC and ETH.

Asch's precision is 8 digits after the decimal point, but the background processing is handled by integers. For example, if you want to transfer 0.1XAS, the actual processing in the background is 0.1 * 100000000. <br>
Asch http interface documentation-Chinese version: https://github.com/AschPlatform/asch-docs/blob/master/http_api/zh-cn.md<br>
Asch http interface documentation - English version: https://github.com/AschPlatform/asch-docs/blob/master/http_api/en.md<br>
This document contains most of the Asch interfaces, such as query balance, transfer, transaction details, etc., and calling api will return the result in JSON format.

## 2. It is recommended that the trading platform build an Asch full node in the LAN

Node installation document:<br>
Chinese: https://github.com/AschPlatform/asch-docs/blob/master/install/zh-cn.md<br>
English: https://github.com/AschPlatform/asch-docs/blob/master/install/en.md <br>

## 3. Deposit XAS

Asch supports transfer notes, so the trading platform can have the following two deposit options.<br>
a)Generate a deposit address for each user<br>
b)Generate the same deposit address for all users, and determine which user is depositing according to the note of transfer<br>

### 3.1 option 1- generate a deposit address for each user

At present, the trading platforms early listing XAS such as bit-z.com, chaoex.com, coinegg.com and okex.com adopt this method.

#### 3.1.1 Generate deposit address for users

User UserA logs into the trading platform and enters the XAS deposit page. The platform generates a deposit address by calling the following code, writes it to the database, and displays it on the page. Use the following code to generate an Asch deposit address for UserA: ALU3f2GaGrWzG4iczamDmGKr4YsbMFCdxB, the password for the deposit address is 'latin december swing love square parade era fuel circle over hub spy', here is just an example, and the data is not real.

##### 3.1.1.1 Calling the HTTP Interface to generate an address

```bash
> curl -k -X GET 'http://192.168.1.100:8192/api/accounts/new'
// The JSON example returned is shown below
{
    success: true,
    secret: "during crush zoo wealth horror left night upset spike iron divert lawn", // secret
    publicKey: "261fa56f389c324fddbe8777dbc0ef3341ee7b75d1ffdc82192265633b90d503", // publicKey
    privateKey: "67c9523b7622704c4bcfe960cb32d7fa04d3eb94e30e7964d3c6a24a3647a0a3261fa56f389c324fddbe8777dbc0ef3341ee7b75d1ffdc82192265633b90d503", // privateKey
    address: "ANfXDQUZroMnrQ6vRGR7UXXtbPn3fhEVRJ" // address
}
```

##### 3.1.1.2 Generate address in batches using the asch-cli command line tool 

If you use other programming languages and feel that it is difficult to generate account addresses in batches, you can use the asch-cli command line tool to generate wallet addresses (including passwords, addresses, and public keys) in batches. Generate multiple addresses, and save them to a database or other place, then the program can use them directly.

```bash
// install asch-cli tool
> npm install -g asch-cli
// generate address in batches
// you need the nodejs version to be 8.x，use command node ––version to see the version of node
> asch-cli crypto -g
? Enter number of accounts to generate 1 // The 1 entered here means to generate an address; you can fill in numbers such as 10, 100 or 1000. 
[ { address: 'AAW3Bh86U8RdHryp86KN19ScSVLpr2x6J4',
	secret: 'actress south egg hen neutral salute section sign truck produce agent daughter',
	publicKey: 'fd86a5bb9e06bd3a0555e27402f90b565300b0a7a6fb42ee4269aae0cfca60c6' } ]
Done
```

##### 3.1.1.3 Generate address with nodejs code

```bash
// the following is the demo of the nodejs programming language (currently the Asch SDK supports nodejs and java, and other languages ​​will be supported later. Currently, developers need to code themselves).
// It is recommended to use ubuntu 16.04, latest version of nodejs 8.x 
// Install nvm, the version management tool of nodejs 
> curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
// after the above command is executed, open another os shell window and execute the following command to install nodejs 8.x.
> nvm install node 8

// Install the dependency libraries (asch-js, bitcore-mnemonic) and run it in the os shell
> npm install asch-js bitcore-mnemonic

// the following is running in node
var Mnemonic = require('bitcore-mnemonic');
var secret = new Mnemonic(Mnemonic.Words.ENGLISH).toString();	// Generate password
console.log(secret);	     // print password，'latin december swing love square parade era fuel circle over hub spy'
Mnemonic.isValid(secret);   // Verify that the password complies with the bip39 specification
var AschJS = require('asch-js');
var publicKey = AschJS.crypto.getKeys(secret).publicKey;  // Generate public key based on password
var address = AschJS.crypto.getAddress(publicKey);  // Generate address based on public key
console.log(address);	// print address，ALu3f2GaGrWzG4iczamDmGKr4YsbMFCdxB
restore user name, address, and encrypted password to database or file to complete the binding of the user and the deposit address, and then the deposit address is displayed on the front page.
```

#### 3.1.2 Deposit by users

User UserA transfers to the deposit address in Asch wallet (such as mainnet.asch.io), such as 0.8xas. 

#### 3.1.3 Trading platform confirms user deposit 

The trading platform detects each new block, and can detect it every 10 seconds (or 30 seconds or one minute, technically it is no problem, but the user experience is different). The height of the block is increased by 1 each time. It is highly recommended to persist the height and add a flag bit "checked". If the receipt address of the transaction details in the block is the deposit address of the platform, the deposit record needs to be displayed on the front page and stored into the database.

##### 3.1.3.1 Check whether the latest block contains transactions

```
/ / Use the block height to check whether the block contains transaction and get the block id, each new block must be checked
// height=3183940 indicates the height of the block 
> curl -k -X GET 'http://mainnet.asch.io/api/blocks/get?height=3183940'
/ / Return the result as follows, save it to the variable res, which will be used later 
{
	"success": true,
	"block": {
		"id": "951e14ef5100a9724a133f74e8f5c35e0d872aee654e7ea5323e57cd1c7b004e",	// block id
		"version": 0,
		"timestamp": 36252710,
		"height": 3183940,
		"previousBlock": "5dbf4b80063153e3bb66b46b27f9041955d308c47d57e51b4934952591519589",
		"numberOfTransactions": 1,  // the number of transactions included in the block
		"totalAmount": 80000000,
		"totalFee": 10000000,
		"reward": 350000000,
		"payloadLength": 143,
		"payloadHash": "5a61b58b75a70a42a6d51deba4dba560c78b2d671dfac68d37984eb464421d81",
		"generatorPublicKey": "65e318f0022e3a05cc1603610125cf42af6772ac1afed657eec44bb3f8b02e64",
		"generatorId": "9537352069871373416",
		"blockSignature": "7b26571e3a55798d83e531817a5971ebdca59b4cfbb1edd182aff3b25c31578356b3a8992714b543f004cd7b362d7069f5dd426f411caacf06659747de1e580e",
		"confirmations": "17", // the number of confirmations for this block		"totalForged": 360000000
	}
}
```

##### 3.1.3.2 Search transaction details according to block id

```
// If res.block.numberOfTransactions > 0, then the block contains the transaction.
// Then use the following interface to query the transaction details contained in the block based on res.block.id 
> curl -k -X GET 'http://mainnet.asch.io/api/transactions?blockId=951e14ef5100a9724a133f74e8f5c35e0d872aee654e7ea5323e57cd1c7b004e'
// return the result as follows, save as variable trs 
{	
	"success": true,
	"transactions": [{
		"id": "5a61b58b75a70a42a6d51deba4dba560c78b2d671dfac68d37984eb464421d81", // transaction id
		"height": "3183940",    //block height
		"blockId": "951e14ef5100a9724a133f74e8f5c35e0d872aee654e7ea5323e57cd1c7b004e",  //block id
		"type": 0, // transaction type，0：XAS ordinary transfer
		"timestamp": 36252686,  // transaction timestamp, Asch time, can be converted to real-world time
		"senderPublicKey": "40e322be1ec9084f48a17b5fecf88d59d0c70ce7ab06b1c4f6d285acfa3b0525",
		"senderId": "AC4i4srjg1TyW24p8M4B8NTcYApUgvTpkd",   // send address
		"recipientId": "ALu3f2GaGrWzG4iczamDmGKr4YsbMFCdxB", // receipt address, if it is a platform address, it needs to be processed
		"amount": 80000000, // ​​transfer amount, divided by 100000000 is the actual number of XAS, here 0.8XAS
		"fee": 10000000,
		"signature": "08a97ba29f7db324b31f782272e17c048f4b99d1761830bd7f541c484c28fcf14b1ee0dbbdd05ab2e80d186473e67d9bfed8e27b8c5e096d29a7f521236d8900",
		"signSignature": "",
		"signatures": null,
		"confirmations": "20",  // the number of block confirmations
		"args": [],
		"message": "",  // transfer notes
		"asset": {
			
		}
	}],
	"count": 1  // the number of transactions in this block
}

// If the array trs.transactions.length>0, loop through trs.transactions to get element i, if (i.type == 0 and i.recipientId is the address of the platform), then the front page will display the reposit record and write the record (deposit id, deposit address, quantity, confirmation number, send time, deposit status, transaction id) to the local database.

// the deposit status is determined by the confirmation number. Specifically, it is determined by the platform itself. If the confirmation number does not meet the platform requirements when entering the database, the deposit status is “unconfirmed”, otherwise it is “confirmed”. (Currently Asch network believes that the six confirmations are safe, and the trading platform can increase the value appropriately.)

// Reconfirm all "unconfirmed" deposit records in the local database every 1 minute. Use the following interface to check transaction details according to the "transaction id" in the database. 
> curl -k -X GET 'http://mainnet.asch.io/api/transactions/get?id=5a61b58b75a70a42a6d51deba4dba560c78b2d671dfac68d37984eb464421d81'
{
	"success": true,
	"transaction": {
		"id": "5a61b58b75a70a42a6d51deba4dba560c78b2d671dfac68d37984eb464421d81",
		"height": "3183940",
		"blockId": "951e14ef5100a9724a133f74e8f5c35e0d872aee654e7ea5323e57cd1c7b004e",
		"type": 0,
		"timestamp": 36252686,
		"senderPublicKey": "40e322be1ec9084f48a17b5fecf88d59d0c70ce7ab06b1c4f6d285acfa3b0525",
		"senderId": "AC4i4srjg1TyW24p8M4B8NTcYApUgvTpkd",
		"recipientId": "ALu3f2GaGrWzG4iczamDmGKr4YsbMFCdxB",    //receipt address
		"amount": 80000000, // amount
		"fee": 10000000,
		"signature": "08a97ba29f7db324b31f782272e17c048f4b99d1761830bd7f541c484c28fcf14b1ee0dbbdd05ab2e80d186473e67d9bfed8e27b8c5e096d29a7f521236d8900",
		"signSignature": "",
		"signatures": null,
		"confirmations": "7837",    // confirmation number
		"args": [],
		"message": "",  // transfer notes
		"asset": {
			
		}
	}
}
// When "confirmations" meets the platform requirements, update the "deposit status" in the database to "confirmed" and display it on the front-end page. Finally, the UserA's XAS balance is increased accordingly.
```

At this point, user UserA has completed the deposit process.

#### 3.1.4 Trading platform transfers the user's deposited XAS to a total account

After the deposit is completed, the trading platform will transfer these scattered XAS to the trading platform's own total account (please save the password).
Total account: It can be used as Asch cold wallet or hot wallet for users to withdraw.
For example, the XAS total account address of platform: 
A7RD9YP37iUnYZ1SFnmAp6ySHUx3msC4r5
Asch offers the following two ways to transfer.

##### 3.1.4.1 Transfer through an unsafe API

This method is to put the key into the request and send it to the server in clear text for the generation and signature of the transaction. It is not safe and is not recommended. If you want to use this method, be sure to set up an Asch node server in the LAN to provide API services.
1) Find the accounts with the XAS balance greater than 0 by querying the local database before summarizing. 
2) You can use the following api to transfer the deposited XAS to the platform's total account, which consumes 0.1XAS fee.

```
> curl -k -H "Content-Type: application/json" -X PUT -d '{"secret":"latin december swing love square parade era fuel circle over hub spy","amount":70000000,"recipientId":"A7RD9YP37iUnYZ1SFnmAp6ySHUx3msC4r5","message":"beizhu"}' 'http://192.168.1.100:8192/api/transactions' && echo // 70000000 means 0.7 XAS, because the network needs to charge a fixed 0.1XAS fee, so UserA's deposit address can only be transferred out of 0.7 XAS 
// return the result as follows 
{
	"success": true,    // transfer status, success
	"transactionId": "6d9b9338ea71ca74a41995458959250e16e49f52b31f4887ac28d3cc3586b1a1" // transaction id
}
```

##### 3.1.4.2 Transfer through a secure API

It is recommended to use such a secure method to transfer, which is to generate transaction information locally and sign it, then broadcast it to the blockchain network, where there is no security requirement for Asch Server.

```javascript
var asch = require('asch-js');
var targetAddress = "A7RD9YP37iUnYZ1SFnmAp6ySHUx3msC4r5";   // receipt address
var amount = 0.7*100000000;   // 0.7 XAS
var message = 'beizhuxinxi'; // transfer notes
var password = 'latin december swing love square parade era fuel circle over hub spy'; // sender master password
var secondPassword=null; // sender secondary password, null if not set 
// generate transaction information and signature 
var transaction = asch.transaction.createTransaction(targetAddress, amount, message, password, secondPassword || undefined);  
JSON.stringify({"transaction":transaction})
'{"transaction":{"type":0,"amount":70000000,"fee":10000000,"recipientId":"A7RD9YP37iUnYZ1SFnmAp6ySHUx3msC4r5","message":"beizhuxinxi","timestamp":43831575,"asset":{},"senderPublicKey":"d1cda821c7f98436f0c7824b96e9fe4dba50d54ed8fd69a92752cd923e416fc2","signature":"005e529e580010398424dbbd65b9c154b37f6cd575010a4f6d9396594311c1ef62487f1040a2cba1dd16a5dba3d12605d211fa08171967886ce9ef301ae82f05","id":"0f28435e9c395dd6b825bda167359bc23d41b5fc632afb59fedfafa298c27cde"}}'

// submit the transaction data of the transfer operation generated above to the asch server via post 
curl -H "Content-Type: application/json" -H "magic:5f5b3cf5" -H "version:''" -k -X POST -d '{"transaction":{"type":0,"amount":70000000,"fee":10000000,"recipientId":"A7RD9YP37iUnYZ1SFnmAp6ySHUx3msC4r5","message":"beizhuxinxi","timestamp":43831575,"asset":{},"senderPublicKey":"d1cda821c7f98436f0c7824b96e9fe4dba50d54ed8fd69a92752cd923e416fc2","signature":"005e529e580010398424dbbd65b9c154b37f6cd575010a4f6d9396594311c1ef62487f1040a2cba1dd16a5dba3d12605d211fa08171967886ce9ef301ae82f05","id":"0f28435e9c395dd6b825bda167359bc23d41b5fc632afb59fedfafa298c27cde"}}' http://192.168.1.100:8192/peer/transactions
```

### 3.2 option 2- generate the same deposit address for all users

All users share an Asch deposit address. When depositing, fill in the username or id on the trading platform as the note, so that there is no need to generate multiple Asch deposit addresses. But it is more troublesome if the user fills in the incorrect notes, which needs to be handled by special customer service staff. In this way, the general process is consistent with option 1, and will not be described here. 

## 4.	Withdraw XAS

The withdrawal operation is to transfer the platform token to the user. 

### 4.1 The user binds the withdrawal address 

The user logs into Asch's withdrawal page and refers to other tokens, allowing the user to bind the withdrawal address on their own. 

### 4.2 Withdraw by users

Enter the amount of withdrawal, SMS verification, and click ok.

### 4.3 The platform shall carry out the operations of token withdrawal

Refer to section 3.1.4. There are two ways to transfer. Please decide which one to use. The interface will return the transaction id of the withdrawal, restore it in the database and display it on the front-end page, and update the withdrawal status as "success".

### 4.4 user confirm

Users can verify the result of the withdrawal by themselves. If in doubt, they can come to the platform with the transaction id for query verification.
