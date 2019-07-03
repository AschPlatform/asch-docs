# ASCH HTTP API Documentation

Table of Contents
=================

<!-- TOC -->

- [ASCH HTTP API Documentation](#asch-http-api-documentation)
  - [**1 API instructions**](#1-api-instructions)
  - [**2 Basic interface**](#2-basic-interface)
    - [**2.1 Accounts**](#21-accounts)
      - [**2.1.1 Login**](#211-login)
        - [**2.1.1.1 Login after local encryption (recommended)**](#2111-login-after-local-encryption-recommended)
        - [**2.1.1.2 Login without encryption (not recommended)**](#2112-login-without-encryption-not-recommended)
      - [**2.1.2 Get account information by providing address**](#212-get-account-information-by-providing-address)
      - [**2.1.3 Get account balance**](#213-get-account-balance)
      - [**2.1.4 Get voting list based on the address**](#214-get-voting-list-based-on-the-address)
      - [**2.1.5 Generate new account**](#215-generate-new-account)
      - [**2.1.6 Get the total amount of accounts on the blockchain**](#216-get-the-total-amount-of-accounts-on-the-blockchain)
    - [**2.2 Transactions**](#22-transactions)
      - [**2.2.1 Get transaction information**](#221-get-transaction-information)
      - [**2.2.2 Get the Transaction Detail Information by Transaction ID**](#222-get-the-transaction-detail-information-by-transaction-id)
      - [**2.2.3 Get Transaction Detail by Unconfirmed Transaction ID**](#223-get-transaction-detail-by-unconfirmed-transaction-id)
      - [**2.2.4 Get unconfirmed transaction details [from all network nodes]**](#224-get-unconfirmed-transaction-details-from-all-network-nodes)
      - [**2.2.5 Get transfer history**](#225-get-transfer-history)
    - [**2.3 Blocks**](#23-blocks)
      - [**2.3.1 Get detail of a specified block**](#231-get-detail-of-a-specified-block)
      - [**2.3.2 Get block data**](#232-get-block-data)
      - [**2.3.3 Get blocks by id or height**](#233-get-blocks-by-id-or-height)
      - [**2.3.4 Get current blockchain height**](#234-get-current-blockchain-height)
      - [**2.3.5 Get current Milestone**](#235-get-current-milestone)
      - [**2.3.6 View current block rewards**](#236-view-current-block-rewards)
      - [**2.3.7 Get current supply of XAS**](#237-get-current-supply-of-xas)
      - [**2.3.8 Get the blockchain status**](#238-get-the-blockchain-status)
      - [**2.3.9 Get transaction information for a specific block**](#239-get-transaction-information-for-a-specific-block)
    - [**2.4 Delegates**](#24-delegates)
      - [**2.4.1 Get the total number of delegates**](#241-get-the-total-number-of-delegates)
      - [**2.4.2 Get the voters for a delegate by his name**](#242-get-the-voters-for-a-delegate-by-his-name)
      - [**2.4.3 Get delegate information by public key or username**](#243-get-delegate-information-by-public-key-or-username)
      - [**2.4.4 Get list of delegates**](#244-get-list-of-delegates)
      - [**2.4.5 Delegate forging status**](#245-delegate-forging-status)
    - [**2.5 Peers**](#25-peers)
      - [**2.5.1 Get all peers for a given node**](#251-get-all-peers-for-a-given-node)
      - [**2.5.2 Get version information about an ASCH node**](#252-get-version-information-about-an-asch-node)
      - [**2.5.3 Get the specified ip node information**](#253-get-the-specified-ip-node-information)
    - [**2.6 Sync and load**](#26-sync-and-load)
      - [**2.6.1 View the blockchain loading status**](#261-view-the-blockchain-loading-status)
      - [**2.6.2 View block sync information**](#262-view-block-sync-information)
    - [**2.7 Proposals**](#27-proposals)
      - [**2.7.1 Get a list of proposals**](#271-get-a-list-of-proposals)
      - [**2.7.2 Get Proposal by ID**](#272-get-proposal-by-id)
    - [**2.8 Gateway**](#28-gateway)
      - [**2.8.1 List of gateways**](#281-list-of-gateways)
      - [**2.8.2 Get validators for a specific gateway**](#282-get-validators-for-a-specific-gateway)
      - [**2.8.3 Get all supported cross chain currencies**](#283-get-all-supported-cross-chain-currencies)
      - [**2.8.4 Get the supported currency of the specified gateway**](#284-get-the-supported-currency-of-the-specified-gateway)
      - [**2.8.5 Get a specific account for a specified gateway**](#285-get-a-specific-account-for-a-specified-gateway)
      - [**2.8.6 Get all gateway accounts for the specified user address**](#286-get-all-gateway-accounts-for-the-specified-user-address)
      - [**2.8.7 Get all recharge records for a currency and gateway**](#287-get-all-recharge-records-for-a-currency-and-gateway)
      - [**2.8.8 Get all recharge records for a currency and user address**](#288-get-all-recharge-records-for-a-currency-and-user-address)
    - [**2.9 Agents and Groups**](#29-agents-and-groups)
      - [**2.9.1 Get all agents accounts**](#291-get-all-agents-accounts)
      - [**2.9.2 Get a clientless agent**](#292-get-a-clientless-agent)
      - [**2.9.3 Get Group information**](#293-get-group-information)
    - [**2.10 Sidechain Endpoint**](#210-sidechain-endpoint)
      - [**2.10.1 Get all registered Sidechains**](#2101-get-all-registered-sidechains)
    - [**2.11 User Defined Asset UIA**](#211-user-defined-asset-uia)
      - [**2.11.1 Get all publishers**](#2111-get-all-publishers)
      - [**2.11.2 Query information about a publisher by name**](#2112-query-information-about-a-publisher-by-name)
      - [**2.11.3 View assets of a specified publisher**](#2113-view-assets-of-a-specified-publisher)
      - [**2.11.4 Get all assets**](#2114-get-all-assets)
      - [**2.11.5 Get specified asset information**](#2115-get-specified-asset-information)
      - [**2.11.6 Get the balance of all user created assets for an account**](#2116-get-the-balance-of-all-user-created-assets-for-an-account)
  - [**3. Transaction**](#3-transaction)
    - [**Description of the request process**](#description-of-the-request-process)
    - [**3.1 Basic Contracts**](#31-basic-contracts)
      - [**3.1.1 Transfer**](#311-transfer)
      - [**3.1.2 Set nickname**](#312-set-nickname)
      - [**3.1.3 Set second secret**](#313-set-second-secret)
      - [**3.1.4 Lock account**](#314-lock-account)
      - [**3.1.5 Unlock**](#315-unlock)
      - [**3.1.6 Register Group**](#316-register-group)
      - [**3.1.7 Register Agent**](#317-register-agent)
      - [**3.1.8 Activate agent**](#318-activate-agent)
      - [**3.1.9 Cancel Agent**](#319-cancel-agent)
      - [**3.1.10 Register Delegate**](#3110-register-delegate)
      - [**3.1.11 Vote for Delegate**](#3111-vote-for-delegate)
      - [**3.1.12 Cancel Delegate Vote**](#3112-cancel-delegate-vote)
    - [**3.2 Asset Contracts**](#32-asset-contracts)
      - [**3.2.1 Register publisher**](#321-register-publisher)
      - [**3.2.2 Register Asset**](#322-register-asset)
      - [**3.2.3 Mint Asset tokens**](#323-mint-asset-tokens)
      - [**3.2.4 Asset transfer**](#324-asset-transfer)
    - [**3.3 DApp Contracts**](#33-dapp-contracts)
      - [**3.3.1 Register DApp**](#331-register-dapp)
      - [**3.3.2 Update DApp delegate**](#332-update-dapp-delegate)
      - [**3.3.3 Add DApp delegate**](#333-add-dapp-delegate)
      - [**3.3.4 Delete DApp delegate**](#334-delete-dapp-delegate)
      - [**3.3.5 Transfer money to own DApp account (Refuel Operation)**](#335-transfer-money-to-own-dapp-account-refuel-operation)
      - [**3.3.6 Withdaw from own DApp account to Mainchain acount (Withdraw operation)**](#336-withdaw-from-own-dapp-account-to-mainchain-acount-withdraw-operation)
    - [**3.4 Proposal Contracts**](#34-proposal-contracts)
      - [**3.4.1 Initiate a proposal**](#341-initiate-a-proposal)
      - [**3.4.2 Vote for proposal**](#342-vote-for-proposal)
      - [**3.4.3 Activate Proposal**](#343-activate-proposal)
    - [**3.5 Gateway Contracts**](#35-gateway-contracts)
      - [**3.5.1 Open gateway account**](#351-open-gateway-account)
      - [**3.5.2 Register member**](#352-register-member)
      - [**3.5.3 Recharge the gateway**](#353-recharge-the-gateway)
      - [**3.5.4 Withdraw from the gateway**](#354-withdraw-from-the-gateway)
      - [**3.5.5 Submit a withdrawl transaction**](#355-submit-a-withdrawl-transaction)
      - [**3.5.6 Submit transaction signature**](#356-submit-transaction-signature)
      - [**3.5.7 Submit a transaction agreement**](#357-submit-a-transaction-agreement)
    - [**3.6 Group Contracts**](#36-group-contracts)
      - [**3.6.1 Vote**](#361-vote)
      - [**3.6.2 Activate Group**](#362-activate-group)
      - [**3.6.3 Add member**](#363-add-member)
      - [**3.6.4 Remove Member**](#364-remove-member)

<!-- /TOC -->

Created by [markdown-toc](https://github.com/AlanWalk/Markdown-TOC)


## **1 API instructions**   

1.1 **Generate request data:** The client constructs the data for a signed request using the [asch-js](https://github.com/AschPlatform/asch-js) package. Or the client builds a unsigned transaction, but must later send his secret. The second option is not recommended.  

1.2 **Sending request data:** Transfer the generated data to the ASCH node using HTTP POST/GET/PUT verbs.  

1.3 **ASCH processes the data:** After receiving the data the ASCH node will perform a security check. After the verification passed, the received data will be processed.  

1.4 **ASCH returns the result:** The ASCH node returns the result of the operation as JSON object back to the client. See below in detail which data format and error codes are used. Each response contains a `success` field indicating whether the request was successful. If the request failed, it will also contain an `error` field indicating the reason for the failure.  

1.5 **The client processes the returned data**  


## **2 Basic interface**  

### **2.1 Accounts**   

#### **2.1.1 Login**   

##### **2.1.1.1 Login after local encryption (recommended)** 

API Endpoint: /api/accounts/open2/  
HTTP Verb: POST  
Format: JSON  
Note: Generate a `public Key` on the local client based on the user's secret  

Request Parameter Description:     

|Name	 |Type  |Required  |Description  |
|------  |-----  |---  |----  |
|publicKey  |string  |Y  |The public key of the ASCH account  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------  |-----  |----  |
|success  |boolean  |Whether login was successful  |
|account  |JSON  |Account information  |

Request example:  
```js
// npm install asch-js
const AschJS = require('asch-js');

// account secret
let secret = 'sentence weasel match weather apple onion release keen lens deal fruit matrix';
// Generate the public Key based on the secret
let publicKey = AschJS.crypto.getKeys(secret).publicKey;

// Submit the the data generated above to the ASCH node via HTTP POST  
curl -X POST -H "Content-Type: application/json" -k -d '{"publicKey":"116025d5664ce153b02c69349798ab66144edd2a395e822b13587780ac9c9c09"}' 'http://localhost:4096/api/accounts/open2/'   
```

JSON Response:  

```json
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

##### **2.1.1.2 Login without encryption (not recommended)**  
API Endpoint: /api/accounts/open/  
HTTP Verb: POST  
Format: JSON  
Note: Pass the password to the backend in clear text to query the account information. **Not recommended for use in production environment**

Request Parameter Description:     

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|secret |string |Y    |ASCH Account secret  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |Whether login is successful  |
|account|JSON   |Account information  |

Request example:     
```bash
curl -X POST -H "Content-Type: application/json" -k -d '{"secret":"tunnel hope keep manual balcony quantum phrase deer prefer vivid deer hazard"}' 'http://localhost:4096/api/accounts/open/'   
```

JSON Response:     
```json
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
#### **2.1.2 Get account information by providing address**  

API Endpoint: /api/v2/accounts/:address  
HTTP Verb: GET  
Format: urlencoded  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|:----:  |:---:  |:-: |:--:  |
|address |string |Y  |Account address  |

Request example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/accounts/ABuH9VHV3cFi9UKzcHXGMPGnSC4QqT2cZ5'
```
Response Parameter Description:     

|Name  |Type  |Description  |
|:----: |:---:  |:--:  |
|success|boolean  |Was it successful?      |
|account|string   |Account information          |
|latestBlock|string |Information about last block  |
|version|string |ASCH node version information |

JSON Response:     
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

#### **2.1.3 Get account balance**   

API Endpoint: /api/v2/balances/:address  
HTTP Verb: GET  
Format: urlencoded  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|:----: |:---:  |:-:  |:--:              |
|address |string |Y    |ASCH account address  |

Request example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/balances/A9Evp9iYWtSUSBQc8yuWtBT2ReBkvzXDxB'
```

Response Parameter Description:     

|Name  |Type  |Description  |
|:----: |:---:  |:--:              |
|success|boolean  |true: response data returned successfully  |
|balances|Array  |Array of balance information for the individual assets      |

JSON Response:     
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

#### **2.1.4 Get voting list based on the address**  

API Endpoint: /api/accounts/delegates  
HTTP Verb: GET  
Format: No  

Request parameters:  

|  Name   |  Type  |   Description   |
| :-----: | :----: | :------: |
| address | string | ASCH account address |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/accounts/delegates?adddress=APSu9NhiCTtvRGx1EpkeKNubiApiBWMf7T' 
```

Response Example:  

```js
{
    "success": true,
    "delegates": []    // If someone voted, there will be voting information
}
```

Response Example:  

```json
{
  "success":true,
  "delegates":[
    {
      "address":"A7KTa5k24PTfdmZxAcYiRmHYN94hFLyMvT",
      "tid":"30eae9b5cb385bd86f42baec40ad1635289c24c820f9f97484b0324de8fc1d3e",
      "name":"asch999",
      "publicKey":"581a0ac98a32eaa6011f921c1f7be69b3bf0348c2dee063a73cee134e5e994d2",
      "votes":27395762167634,
      "producedBlocks":null,
      "missedBlocks":0,
      "fees":0,
      "rewards":0,
      "_version_":2,
      "rate":234,
      "approval":0.23042111630911288,
      "productivity":"0.00",
      "vote":27395762167634,
      "missedblocks":0,
      "producedblocks":null
    },
    {
      "address":"A7XBsecVtHEze4Lfrscmg2DEDChETRknZm",
      "tid":"6829b0a158551c55051e6dc5a82220426955985ca26ca483d954dcf0c16b757e",
      "name":"shan078",
      "publicKey":"23bbd81857aa74b4fb67f8e27f86321318c1c50c7c820859a581e75fc1038ac0",
      "votes":1006965261018096,
      "producedBlocks":684,
      "missedBlocks":0,
      "fees":6186533771,
      "rewards":809760000000,
      "_version_":710,
      "rate":91,"approval":8.469414287820324,
      "productivity":"100.00",
      "vote":1006965261018096,
      "missedblocks":0,
      "producedblocks":684
    }
]
```

#### **2.1.5 Generate new account**  
API Endpoint: /api/accounts/new  
HTTP Verb: GET  
Format: No  
Request parameters: No  

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|secret|string  |ASCH account secret  |
|publicKey|string  |ASCH account public Key  |
|privateKey|string  |ASCH account private Key (not often used)  |
|address|string  |ASCH account address  |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/accounts/new'   
```

JSON Response:     
```js  
{
    "success": true,
    "secret": "ginger angle fury grow differ about bamboo swim transfer mixed era radio",
    "publicKey": "bb201d25fae05de56d0450932b0603eb3c6e8b001ea6215a49f392aaa94b241d",
    "privateKey": "026c7eb8876354a9480e1ca1cba4919760d1c1e998830cd66e5e01b6370002f6bb201d25fae05de56d0450932b0603eb3c6e8b001ea6215a49f392aaa94b241d",
    "address": "A3xBcFQHcubF8qUE8mcmFZFN2WdUA8KGvV"
}  
```

#### **2.1.6 Get the total amount of accounts on the blockchain**  
API Endpoint: /api/accounts/count  
HTTP Verb: GET  
Format: No  
Request parameters: No      

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|count|integer  |The total number of accounts on the ASCH blockchain  |

Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/accounts/count'    
```

JSON Response:     
```js   
{
    "success": true,
    "count": 144
}
```

### **2.2 Transactions**  

#### **2.2.1 Get transaction information**   
API Endpoint: /api/v2/transactions  
HTTP Verb: GET  
Format: urlencoded  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|:----: |:---:  |:-:  |:--:              |
|orderBy |string |N    |Sort by  |
|height |number |N |The height of the block where the transaction is included |
|senderId |string |N |The ASCH address of the account that signed this transaction  |
|message |string |N |A transaction note |
|offset |number |N |Offset|
|limit |number |N |Limit |

Request example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/transactions?senderId=A7Vbt5h3WgaXLSJhUeHnRRcwvkGF3ecS7r&orderBy=height:desc&offset=1&limit=3'
```

Response Parameter Description:     

|Name  |Type  |Description  |
|:----: |:---:  |:--:              |
|success|boolean  |Whether the data returned successfully  |
|transactions|Array   |Array of transactions  |

JSON Response:  

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
#### **2.2.2 Get the Transaction Detail Information by Transaction ID**   
API Endpoint: /api/v2/transactions/:tid  
HTTP Verb: GET  
Format: urlencoded  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|:----: |:---:  |:-:  |:--:              |
|tid |JSON |Y    |Transaction ID  |

Request example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/transactions/e19a3ae0090208c3e2e1289d12b80511eca5ceb814d20f0cf37bd2e37942f820'
```

Response Parameter Description:     

|Name  |Type  |Description  |
|:----: |:---:  |:--:              |
|success|boolean  |true: response data returned successfully  |
|transaction|string  |Transaction information     |

JSON Response:     
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

#### **2.2.3 Get Transaction Detail by Unconfirmed Transaction ID**   
API Endpoint: /api/transactions/unconfirmed/get  
HTTP Verb: GET  
Format: urlencoded  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|id|string |Y    |Unconfirmed transaction id  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|transaction|JSON  |Unconfirmed transaction detail  |


Request example:     
```bash  
# Under normal circumstances, the unconfirmed transaction lives for just 0 to 10 seconds
curl -k -X GET 'http://localhost:4096/api/transactions/unconfirmed/get?id=e19a3ae0090208c3e2e1289d12b80511eca5ceb814d20f0cf37bd2e37942f820'   
```

JSON Response:     
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


#### **2.2.4 Get unconfirmed transaction details [from all network nodes]**   
API Endpoint: /api/transactions/unconfirmed  
HTTP Verb: GET  
Format: urlencoded  
Description: If no parameters are added, all unconfirmed transactions on the whole network will be obtained.  

Request Parameter Description:     

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|senderPublicKey |string |N    |ASCH public Key of sender  |
|address |string |N    |ASCH address     |


Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|transactions|Array  |Unconfirmed transaction array  |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/transactions/unconfirmed'   
```

JSON Response:     
```js   
{   
	"success": true,   
	"transactions": []  // There are currently no unconfirmed transactions on all ASCH nodes 
}   
```

#### **2.2.5 Get transfer history**   
API Endpoint: /api/v2/transfers  
HTTP Verb: GET  
Format: urlencoded   

Response Parameters:  

|   Name   |   Type   |   Description   |
| :------: | :----: | :--------------------: |
|  limit   | string | Return limit (default 10) |
|  offset  | string |        Offset          |
| ownerId  | string |    ASCH address of sender or receiver     |
| currency | string |         Currency          |

Response Parameters:  

|   Name   |   Type   |   Description   |
| :-------: | :-----: | :----------------------: |
|  success  | boolean | Whether the request was successful |
| transfers |  Array  |         Array of transfers         |

Request example:  

```bash   
curl -k -X GET 'http://localhost:4096/api/v2/transfers?limit=2'   
```

JSON Response:  

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


### **2.3 Blocks**   

#### **2.3.1 Get detail of a specified block**   

API Endpoint: /api/blocks/get  
HTTP Verb: GET  
Format: urlencoded  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|id |string |Parameter 3 is selected    |Block id      |
|height|string|Parameter 3 is selected  |Block height  |
|hash|string|Parameter 3 is selected   |Block hash  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|block|JSON  |Block details      |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/blocks/get?id=6076474715648888747'   
```

JSON Response:     
```js   
{   
	"success": true,   
	"block": {   
		"id": "6076474715648888747",   
		"version": 0,   
		"timestamp": 4734070,   
		"height": 140538,   
		"previousBlock": "16033230167082515105",    // id of previous block  
		"numberOfTransactions": 0,  // number of transactions  
		"totalAmount": 0,   // total amount of all transactions in this block   
		"totalFee": 0,  // total fee of all transactions in this block 
		"reward": 350000000,    // delegate reward for minting this block   
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

#### **2.3.2 Get block data**   

API Endpoint: /api/v2/blocks   
HTTP Verb: GET      
Format: urlencoded   
Description: Get the first 20 blocks by default without parameters  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|limit |integer |N    |maximum number of records to return, between 0 and 100  |
|offset|integer  |N      |offset, minimum 0  |
|orderBy|string  |N      |Sort by various properties, such es `height:desc`  |
|transactions|string|N   |If this keyword is added with `transactions=true` then the block will be accompanied by transaction information |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|blocks|Array  |Array of blocks  |
|count|integer|The current height of the blockchain (means the number of blocks since block 1)  |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/v2/blocks?limit=2&offset=350'   
```

JSON Response:  
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

#### **2.3.3 Get blocks by id or height**   

API Endpoint: /api/blocks/:IdOrHeight  
HTTP Verb: GET  
Format: No  

Request Parameter Description:   

|Name  |Type  |Description  |
|------ |-----  |----              |
|idOrHeight |String |Block id or height|

Response Parameter Description:  

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|height|integer  |Block chain height      |

Request example:     
```bash   
curl -k -X GET 'http://192.168.1.78:4096/api/v2/blocks/351'
curl -k -X GET 'http://192.168.1.78:4096/api/v2/blocks/426e6b99b7308416d87509da9a485fdbecd61e19fdd139a306ee4938949f1844'
```

JSON Response:     
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

#### **2.3.4 Get current blockchain height**  
API Endpoint: /api/blocks/getHeight   
HTTP Verb: GET      
Format: No  
Request Parameter Description: No  

Response Parmeter Description:  

|Name  |Type   |Description  |
|:----: |:---:  |:--:              |
|success|boolean  |true: response data returned successfully  |
|height|integer|Blockchain height  |

Example:  

```bash
curl -k -X GET 'http://192.168.1.78:4096/api/blocks/getheight'  
```

JSON Response:  

```json
{
    "success": true,
    "height": 31363
}
```

#### **2.3.5 Get current Milestone**   
API Endpoint: /api/blocks/getMilestone   
HTTP Verb: GET      
Format: No  
Request Parameter Description: No  

Response Parameter Description:     

|Name  |Type   |Description  |
|:----: |:---:  |:--:              |
|success|boolean  |true: response data returned successfully  |
|milestone|integer  |Milestones describe certain time periods for delegate forging rewards |

Below you can find the relationship between block height, milestones and delgate reward:  

Milestones `mainnet`:  

| Block height | Milestone | Delegate Reward |
| :--------:  | :-------: | :-------: |
| >= 1 | 0  | 3.5 XAS  |
| >= 3464500 | 1 | 3.0 XAS |
| >= 6464500 | 2 | 2.0 XAS |
| >= 9464500 | 3 | 1.0 XAS |
| >= 12464500 | 4 | 0.5 XAS |

Milestones `localnet` and `testnet`:  

| Block height | Milestone | Delegate Reward |
| :--------:  | :-------: | :------: |
| >= 1 | 0  | 3.5 XAS |
| >= 3000001 | 1 | 3.0 XAS |
| >= 6000001 | 2 | 2.0 XAS |
| >= 9000001 | 3 | 1.0 XAS |
| >= 12000001 | 4 | 0.5 XAS |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/blocks/getMilestone'    
```

JSON Response:     
```js   
{
    "success": true,
    "milestone": 0
}
```

#### **2.3.6 View current block rewards**  

API Endpoint: /api/blocks/getReward   
HTTP Verb: GET   
Format: No  
Request Parameter Description: No  

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|reward|integer  |Delegate block rewards  |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/blocks/getReward'   
```

JSON Response:     
```js   
{
    "success": true,
    "reward": 350000000
} // each delegate gets 3.5 XAS as reward for forging a block
```

#### **2.3.7 Get current supply of XAS**   

API Endpoint: /api/blocks/getSupply   
HTTP Verb: GET      
Format: No  
Request Parameter Description: No  

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|supply|integer  |The number of XAS in the whole network   |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/blocks/getSupply'   
```

JSON Response:     
```js   
{
    "success": true,
    "supply": 10010958150000000
} // current testnet has a total of 100109581.5 XAS  
```

#### **2.3.8 Get the blockchain status**  

API Endpoint: /api/blocks/getStatus   
HTTP Verb: GET   
Format: No  
Request Parameter Description: No  

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|height|integer  |Blockchain height  |
|fee|integer  |Transaction fees      |
|milestone|integer  |More information about milestones can you find [here](#234-get-current-milestone)      |
|reward|integer  |Block reward      |
|supply|integer  |The total XAS supply      |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/blocks/getStatus'   
```

JSON Response:     
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

#### **2.3.9 Get transaction information for a specific block**   

API Endpoint: /api/blocks/full   
HTTP Verb: GET   
Format: No  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |----   |----           |
|id |string |    |Block id  |
|height|string|    |Block height  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|block|JSON  |block details, including transaction information      |

Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/blocks/full?height=34'   
```

JSON Response:     
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


### **2.4 Delegates**   

#### **2.4.1 Get the total number of delegates**   
API Endpoint: /api/delegates/count   
HTTP Verb: GET   
Format: No  
Request Parameter Description: No   

Response Parameter Description:     
    
|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|count|integer   |Total number of delegates  |

Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/delegates/count'   
```

JSON Response:     
```js   
{
    "success": true,
    "count": 106
}   
```

#### **2.4.2 Get the voters for a delegate by his name**   
API Endpoint: /api/delegates/voters   
HTTP Verb: GET   
Format: urlencoded   
Request Parameter Description:     

|Name  |Type  |Required  |Description  |
|:----: |:---:  |:-:  |:--:              |
|name |string |Y    |delegate name  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|accounts|Array  |Array of ASCH accounts  |

Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/delegates/voters?name=asch_g59'   
```

JSON Response:     
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

#### **2.4.3 Get delegate information by public key or username**   
API Endpoint:  /api/delegates/get   
HTTP Verb: GET      
Format: urlencoded   
Note: Get delegate information by public key or username   

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|publicKey |string |pick one of two   |Delegate public key      |
|name  |string |pick one of two    |delegate user name      |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|delegate|JSON  |Delegate information  |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/delegates/get?publicKey=ff6ea4945fee31f64439030f84bac934604468cf5d0b441bec761cfc1911653a'   
curl -k -X GET 'http://localhost:4096/api/delegates/get?name=asch_g59'   
```

JSON Response:     
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

#### **2.4.4 Get list of delegates**   

API Endpoint: /api/delegates   
HTTP Verb: GET   
Format: urlencoded   
Description: If no parameters are specified, a list of all delegates is returned   

Request Parameter Description:     

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----  |
|address |string |N    |delegate address  |
|limit|int  |N       |maximum number of records to return  |
|offset|integer  |N       |Offset, minimum: 0  |
|orderBy|string  |N       |Sort by various properties, such es `height:desc`  |


Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|delegates|Array  |Array of delegates     |

Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/delegates?limit=5'
```

JSON Response:     
```js   
{   
  "success": true,   
  "delegates": [{   
    "username": "wgl_002",  //delegate user name   
    "address": "14636456069025293113",  // delegate address   
    "publicKey": "ae256559d06409435c04bd62628b3e7ea3894c43298556f52b1cfb01fb3e3dc7",  // delegate   public Key   
    "vote": 9901984015600500,   // Number of votes   
    "producedblocks": 1371, // Number of generated blocks  
    "missedblocks": 6,  // Number of missed blocks   
    "fees": 12588514990,       
    "rewards": 276850000000,    // Rewards already received   
    "rate": 1,   
    "approval": 98.54,  // Vote approval   
    "productivity": 99.56,  // Productivity   
    "forged": "289438514990"    // All rewards for forging   
  },
  {
    "address": "ADcPTKHLnDfxBjWyxVVMquPQDjfBNBwnvT",
    "name": "asch_g59",  //delegate name
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
  }],   
  "totalCount": 233   
}
```

#### **2.4.5 Delegate forging status**   

API Endpoint: /api/delegates/forging/status      
HTTP Verb: GET   
Format: urlencoded  

Request Parameter Description:     

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|publicKey|string  |Y      |ASCH public key|


Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|enabled|string  |Whether forging for this delegate is possible  |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/delegates/forging/status?publicKey=fafcd01f6b813fdeb3c086e60bc7fa9bfc8ef70ae7be47ce0ac5d06e7b1a8575'        
```

JSON Response:     
```js   
{
  "success":true,
  "enabled":false
}    
```

### **2.5 Peers**  

#### **2.5.1 Get all peers for a given node**  
API Endpoint: /api/peers   
HTTP Verb: GET   
Format: urlencoded   

Request Parameter Description:     

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|state |integer |N    |Node status: 0, 1, 2, 3  |
|os|string|N|Operating System kernel version |
|version|string|N|ASCH version|
|limit |integer |N    |maximum number of records to return, between 0 and 100  |
|orderBy|string|N|  |
|offset|integer  |N      |Offset, minimum value: 0  |
|port|integer|N|Port: 1~65535|


Response Parameter Description:  

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|peers|Array  |Array of ASCH nodes|
|totalCount|integer|The number of nodes currently running|


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/peers?limit=3'   
```

JSON Response:     
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

#### **2.5.2 Get version information about an ASCH node**   
API Endpoint: /api/peers/version   
HTTP Verb: GET   
Format: No  
Request Parameter Description:  No  

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|version|string  |version number      |
|build  |timestamp |Build time    |
|net    |string  |Main ASCH chain (mainnet) or test ASCH chain (testnet)     |


Request example:     
```bash   
curl -k -X 'GET http://localhost:4096/api/peers/version'   
```

JSON Response:     
```js   
{
    "success": true,
    "version": "1.4.2",
    "build": "21:04:40 09/08/2018",
    "net": "testnet"
}
```

#### **2.5.3 Get the specified ip node information**   

API Endpoint: /api/peers/get   
HTTP Verb: GET      
Format: urlencoded   
Request Parameter Description:     

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|ip |string |Y    |Pending ASCH node IP address  |
|port|integer|Y|Port of ASCH node, 1~65535|


Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|peer|JSON  |      |


Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/peers/get?ip=45.32.248.33&port=4096'   
```

JSON Response:     
```js   
{   
	"success": true,   
}   
```

### **2.6 Sync and load**   
#### **2.6.1 View the blockchain loading status**   
API Endpoint: /api/loader/status  
HTTP Verb: GET  
Format: No   
Request Parameter Description: No  

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|loaded |boolean    |          |
|blocksCount|integer||

Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/loader/status'
```

JSON Response:     
```js   
{   
	"success": true,   
	"loaded": true,   
	"blocksCount": 0   
}   
```

#### **2.6.2 View block sync information**   

API Endpoint: /api/loader/status/sync   
HTTP Verb: GET   
Format: No  
Request Parameter Description: No Parameters    

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |true: response data returned successfully  |
|height |int    |Block height        |

Request example:     
```bash   
curl -k -X GET 'http://localhost:4096/api/loader/status/sync'
```

JSON Response:     
```js   
{
    "success": true,
    "syncing": false,     // No data can be synced, therfore is the value false
    "blocks": 0,
    "height": 31580
} 
```

### **2.7 Proposals**

#### **2.7.1 Get a list of proposals**

API Endpoint: /api/v2/proposals  
HTTP Verb: GET      
Format: urlencoded  

Request parameters:  

|   Name   |   Type   |   Description   |
| :----: | :----: | :------------------------: |
| limit  | string | Return data limit, default 20 |
| offset | string |           Offset           |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/proposals?limit=2'
```

Response Example:  

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

#### **2.7.2 Get Proposal by ID**

API Endpoint: /api/v2/proposals/:id  
HTTP Verb: GET  
Format: urlencoded   

Parameter Description:  

|   Name   |   Type   |   Description   |
| :--: | :----: | :----: |
|  id  | string | Proposal id |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/proposals/c58fbea59446364f1d0f9b780bc7bd5d137746b6e1032e6a2ed4ff4f8cd45a9e'  
```

Response Example:  

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

### **2.8 Gateway**

#### **2.8.1 List of gateways**

API Endpoint: /api/v2/gateways  
HTTP Verb: GET  
Format: urlencoded  

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/gateways?limit=2'
```

Response Example:  

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

#### **2.8.2 Get validators for a specific gateway**

API Endpoint: /api/v2/gateways/:name/validators  
HTTP Verb: GET  
Format: urlencoded  

Response Parameters:  

|   Name   |   Type   |   Description   |
| :--: | :----: | :------: |
| name | string | Gateway name |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/gateways/bitcoin/validators'  
```

Response Example:  

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

#### **2.8.3 Get all supported cross chain currencies**

API Endpoint: /api/v2/gateways/currencies  
HTTP Verb: GET  
Format: urlencoded  
Request Parameter Description: No  

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/gateways/currencies' 
```

Response Example:  

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

#### **2.8.4 Get the supported currency of the specified gateway**

API Endpoint: /api/v2/gateways/:name/currencies  
HTTP Verb: GET  
Format: urlencoded  

Request Parameters:  

|   Name   |   Type   |   Description   |
| :--: | :----: | :------: |
| name | string | Gateway name |

Response Parameters:  

| Name  | Type  | Description  |
| :---: | :---: | :---:        |
| success | boolean   |Whether operation was successful |
| count   |       |      |
| currencies | Array | Array of currencies |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/gateways/bitcoin/currencies'  
```

Response Example:  

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

#### **2.8.5 Get a specific account for a specified gateway**

API Endpoint: /api/v2/gateways/:name/accounts/:address  
HTTP Verb: GET  
Format: urlencoded  

Response Parameters:  

|   Name   |   Type   |   Description   |
| :-----: | :----: | :------: |
|  name   | string | Gateway name |
| address | string | ASCH account address |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/gateways/bitcoin/accounts/AGw5h2cYK2iYGwp8czhn59Dbr8LMz2BaU'   
```

Response Example:  

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

#### **2.8.6 Get all gateway accounts for the specified user address**

API Endpoint: /api/v2/gateways/accounts/:address  
HTTP Verb: GET  
Format: urlencoded  

Request parameters:  

|   Name   |   Type   |   Description   |
| :-----: | :----: | :------: |
| address | string | ASCH account address |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/gateways/accounts/AGw5h2cYK2iYGwp8czhn59Dbr8LMz2BaUC'    
```

Response Example:  

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

#### **2.8.7 Get all recharge records for a currency and gateway**

API Endpoint: /api/v2/gateways/deposits/:address/:currency  
HTTP Verb: GET  
Format: urlencoded  

Request parameters:  

|   Name   |   Type   |   Description   |
| :------: | :----: | :------: |
| address  | string | ASCH account address |
| currency | string |   Currency   |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/gateways/deposits/mvGfGo9YfNiTJK6MDnfwDwr5jTdWR1ovdC/BTC'    
```

Response Example:  

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

#### **2.8.8 Get all recharge records for a currency and user address**

API Endpoint: /api/v2/gateways/withdrawals/:address/:currency  
HTTP Verb: GET  
Format: urlencoded  

Response Parameters:  

|   Name   |   Type   |   Description   |
| :------: | :----: | :------: |
| address  | string | ASCH account address |
| currency | string |   Currency   |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/gateways/withdrawals/APSu9NhiCTtvRGx1EpkeKNubiApiBWMf7T/BTC'   
```

Response Example:  

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
        outTransaction: {
          "txhex":"0100000001f823dd6bec281e20355a4da44221bdd69c089b89e00e7c695e65e9c564366c380100000000ffffffff0210f699000000000017a9144bf1f23966f4f815980e089f18519f1f87d9ae73875847a5060000000017a914aaf52a57317ed5c8f1ccdd80fc3f21f63a9f2cba8700000000",
          "input":[
            "2N8qAZHVsG8yaAyQHCdbry6iHYxCxyMDd6W"
            ]
        },
        signs: 2,
        ready: 1,
        oid: "",
        _version_: 3
    }]
}
```

### **2.9 Agents and Groups**

#### **2.9.1 Get all agents accounts**

API Endpoint: /api/v2/agents  
HTTP Verb: GET   
Format: urlencoded  

Response Parameters:  

|   Name   |   Type   |   Description   |
| :----: | :----: | :--------------------: |
| limit  | string | Return limit (default 20) |
| offset | string |         Offset         |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/agents'      
```

Response Example:  

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

#### **2.9.2 Get a clientless agent**

API Endpoint: /api/v2/agents/:name/clienteles   
HTTP Verb: GET   
Format: urlencoded 

Request parameters:  

|   Name   |   Type   |   Description   |
| :--: | :----: | :--------: |
| name | string | Agent name |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/agents/agent001/clienteles'     
```

Response Example:  

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

#### **2.9.3 Get Group information**

API Endpoint: /api/v2/groups/:address    
HTTP Verb: GET   
Format: urlencoded 

Response Parameters:  

|   Name   |   Type   |   Description   |
| :-----: | :----: | :-------: |
| address | string | Group address |

Request Example:  

```bash
curl -k -X GET 'http://localhost:4096/api/v2/groups/G3sQzuWpvXZjxhoYnvvJvnfUUEo8aNzKdj'     
```

Response Example:  

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

### **2.10 Sidechain Endpoint**

#### **2.10.1 Get all registered Sidechains**

API Endpoint: /api/v2/chains  
HTTP Verb: GET   
Format: urlencoded  

Request Example:  

|   Name   |   Type   |   Description   |
| :----: | :----: | :--------------------: |
| limit  | string | Return limit (default 20) |
| offset | string |         Offset         |


```bash
curl -k -X GET 'http://localhost:4096/api/v2/chains'   
```

Response Example:  

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

###  **2.11 User Defined Asset UIA**  

#### **2.11.1 Get all publishers**  
API Endpoint: /api/v2/uia/issuers  
HTTP Verb: GET   
Format: urlencoded 

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|limit|integer|N|maximum number of records to return, between 0 and 100  |
|offset|integer|N|Offset, minimum 0|

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |Whether operation was successful  |
|issuers|Array|Array of publishers  |
|count|integer|Total number of publishers  |

Request example:     
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://localhost:4096/api/v2/uia/issuers?offset=0&limit=2' && echo
```

JSON Response:  
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

#### **2.11.2 Query information about a publisher by name** 
API Endpoint: /api/v2/uia/issuers/:address  
HTTP Verb: GET  
Format: urlencoded  

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|address|string|Y|Can be the ASCH account address  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |Whether operation was successful  |
|issuers|JSON|Contains the publisher name, description and id (ASCH address)|

Request example:     
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://localhost:4096/api/uia/issuers/ChinaBank' 
```

JSON Response:     
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

#### **2.11.3 View assets of a specified publisher** 
API Endpoint: /api/v2/uia/issuers/:address/assets  
HTTP Verb: GET      
Format: urlencoded 

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|address|string|Y|Can be  ASCH account address |
|limit|integer|N|maximum number of records to return, between 0 and 100  |
|offset|integer|N| Offset, minimum 0  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |Whether operation was successful  |
|assets|Array|Array of assets, each item includes the asset name, description, cap (maximum circulation = true circulation times accuracy), accuracy, strategy, current circulation, release height, publisher Id, acl mode (0: blacklist, 1: whitelist), whether to log off|
|count|interger|The total number of assets registered by the publisher (including those that have been cancelled)  |


Request example:     
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://localhost:4096/api/v2/uia/issuers/CCTime/assets/'
```

JSON Response:     
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

#### **2.11.4 Get all assets** 
API Endpoint: /api/v2/uia/assets  
HTTP Verb: GET   
Format: urlencoded 

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|limit|integer|N|maximum number of records to return, between 0 and 100  |
|offset|integer|N| Offset, minimum 0  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |Whether operation was successful  |
|assets|Array|Array of assets, each item is an asset detail, including asset name, description, cap, precision, strategy, current circulation, issue height, publisher id, acl, whether to log off|
|count|integer|Number of all assets  |

Request example:     
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://localhost:4096/api/uia/assets?offset=0&limit=2' && echo
```

JSON Response:     
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

#### **2.11.5 Get specified asset information** 
API Endpoint: /api/v2/uia/assets/:name  
HTTP Verb: GET   
Format: urlencoded 

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|name|string|Y|Asset name|

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |Whether operation was successful  |
|assets|JSON|Contains asset name, description, cap, precision, current circulation, issue height, publisher id|

Request example:     
```js   
curl -X GET -H "Content-Type: application/JSON"  'http://localhost:4096/api/v2/uia/assets/CCTime.XCT'
```

JSON Response:     
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

#### **2.11.6 Get the balance of all user created assets for an account** 
API Endpoint: /api/uia/balances/:address  
HTTP Verb: GET   
Format: urlencoded 

Request Parameter Description:  

|Name  |Type  |Required  |Description  |
|------ |-----  |---  |----              |
|address  |string  |Y  |ASCH account address  |
|limit  |integer  |N  |maximum number of records to return, between 0 and 100  |
|offset  |integer  |N  | Offset, minimum 0  |

Response Parameter Description:     

|Name  |Type  |Description  |
|------ |-----  |----              |
|success|boolean  |Whether operation was successful  |
|balances|Array|Asset array, details owned, each element is an asset, including asset name, balance, cap, precision, current circulation, whether to cancel (0: not cancelled, 1: cancelled)|
|count|integer|The number of assets currently owned by this address|

Request example:     
```bash  
curl -X GET -H "Content-Type: application/JSON" 'http://localhost:4096/api/uia/balances/AHMCKebuL2nRYDgszf9J2KjVZzAw95WUyB' && echo
```

JSON Response:  

```json
{
  "success":true,
  "count":1,
  "balances":[{
    "address":"AHMCKebuL2nRYDgszf9J2KjVZzAw95WUyB",
    "currency":"CCTime.XCT",
    "balance":"2000000000000",
    "flag":2,
    "_version_":1,
    "name":"CCTime.XCT",
    "desc":"XCT",
    "maximum":"1000000000000000000",
    "precision":8,
    "quantity":"2000000000000",
    "issuerId":"AHMCKebuL2nRYDgszf9J2KjVZzAw95WUyB",
    "writeoff":0,
    "maximumShow":"10000000000",
    "quantityShow":"20000"
  }
  ]
}
```


## **3. Transaction**   

### **Description of the request process**  

Transactions can be locally constructed and signed with the `asch-js` npm package. They are created with a call to `transaction.createTransactionEx(params)`. After that, the transaction can be send with a HTTP POST request to the `/api/peer/transaction` endpoint.

The parameter `params` is an object that needs to be constructed.  

- **type: Contract number**

- **fee: Handling fee**

- **args: Required parameters for the respective contract**

- **message: Remarks**

- **secret: Sender ASCH secret**

- **secondSecret: Sender ASCH 2nd Second**

The parameters, contract numbers and fees are different for each contract.  

Create transaction with `asch-js` (transaction type 1):  

```js
let message = 'Note'  
  amount = 50*100000000,  
  recipient = 'A3w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ',  // this is only a demo address
  mySecret = 'cat craft often annual face marriage lyrics clutch room helmet crowd biology',
  secondSecret = 'abcd12345'
let args = [amount,recipient],  // the first parameter is the transfer amount, and the second parameter is the target address
     
// construct a params object
let params = {
  type: 1, // The contract number for the transfer is 1  
  fee: 0.1*100000000,  // The transfer fee is 0.1  
  args: args,  // this is the array with the required parameters for the contract  
  message,    // A transaction note (not required)  
  secret: mySecret,   // My secret (the secret of the person who is transfering the XAS currency)
  secondSecret: mySecondSecret  // Second secret (not required)
}

// The params object got constructed, let it hand over to the createTransactionEx interface from asch-js
let aschjs = require('asch-js')
// The transaction returned by the following method needs to be submitted to the server
let transaction = aschjs.transaction.createTransactionEx(params)
```


Submit Transaction with Bash:  
```bash
curl -H "Content-Type: application/json" -H "magic:594fe0f3" -H "version:''" -k -X POST -d '{"transaction":transaction}' 'http://localhost:4096/peer/transaction'
```

Submit Transaction with Javsacript:  
```js
axios({
  method: 'post',
  url: 'http://localhost:4096/peer/transactions',
  json:true,
  data:{
      transaction:transaction
  },
  headers:{
      'Content-Type':'application/json',
      'version':'',
      'magic':'594fe0f3'
  }})
    .then(function(response){
        console.log(response.data)
    })
    .catch(function(error){
        console.error(error)
    })
```

JSON Response from the server:  
```js
{
  success: true,
  transactionId: "609074700dcea17b56e5a98bbfeee5f6416935b6b444c0750e5cb319d818a502"
}
```

The whole example above is the process of calling a __contract__. Other contracts require other `args`, `fees` and `type` values.  


The accuracy of XAS is eight decimal places, so you need to multiply by 100000000 when using the XAS coin.

```js
const XAS = 100000000
```


### **3.1 Basic Contracts**   

#### **3.1.1 Transfer**   
- **type: 1**

- **fee:    0.1 XAS**

- **args:  [amount，recipient]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :------: |
  |  amount   | number | Transfer amount |
  | recipient | string | ASCH address of recipient |

  Example:  

  ```js
  let amount =  100*XAS // transfer amount
  let recipient = 'A3w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ' // recipient address
  let args = [amount,recipient]
  
  // Construct params
  let params = {
    type:1,  // the contract number for the transfer is 1  
    fee:0.1*100000000,  // the transfer fee is 0.1 XAS
    args: args,  // required parmaeter for the contract
    message,    // A transaction note (not required)
    secret: mySecret,   // the ASCH account secret of the sender
    secondSecret:mySecondSecret // second secret (only required if set for the respective ASCH account)
  }
  
  // sign the transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.2 Set nickname**

- **type: 2**

- **fee:   1/10/40/80/100/200*XAS**

- **args:  [name]**

  The fee for setting the nickname depends upon the length of it. The longer the nickname gets, the cheaper is it.  

  Nickname-Lenght - Fee

  | len  |   fee   |
  | :--: | :-----: |
  |  2   | 200*XAS |
  |  3   | 100*XAS |
  |  4   | 80*XAS  |
  |  5   | 40*XAS  |
  | 6-10 | 10*XAS  |
  | >10  |  1*XAS  |

  |   Name   |   Type   |   Description   |
  | :--: | :----: | :--: |
  | name | string | nickname |

  Example:  

  ```js
  let name = 'username1'
  let args = [name]
  
  // construct a params object
  let params = {
    type: 2, // the contract number for the nickname is 2  
    fee:10*100000000, // The fee is explained in detail above
    args: args, // required parameter for the contract
    message, // A transaction note (not required)
    secret:mySecret, // the secret of the respective ASCH account
    secondSecret:mySecondSecret // second secret (only required if set for the respective ASCH account)
  }

  // create transaction with asch-js
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.3 Set second secret**   

- **type: 3**

- **fee:    5*XAS**

- **args:  [secondSecret]**

  |   Name   |   Type   |   Description   |
  | :----------: | :----: | :--------------: |
  | secondSecret | string | second secret (IMPORTANT: only after it has been encrypted, see below for an example) |

  ```js
  
  // the second secret will be encrypted
  let password = 'asch123456'
  let hash = sha256Bytes(new Buffer(password))
  let keypair = nacl.sign.keyPair.fromSeed(hash);
  let secondSecret = new Buffer(keypair.publicKey).toString("hex")
  let args = [secondSecret]  

  // construct the params object  
  let params = {
    type:3,  
    fee:5*100000000,    
    args: args,
    message,   
    secret:mySecret,   
    secondSecret:null
  } 
  // use asch-js to generate transaction
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```


#### **3.1.4 Lock account**

- **type: 4**

- **fee:    0.1*XAS**

- **args:  [height,amount]**

  |   Name   |   Type   |   Description   |
  | :----: | :----: | :--------: |
  | height | number | Lock height (height of a future block) |
  | amount | number | Lock amount |

  Example:  	

  ```js
  let height = 64200,
      amount = 20000*XAS
  let args = [height,amount]
  // construct parmas object
  let params = {
    type:4,   
    fee:0.1*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // generate transaction with asch-js
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.5 Unlock**

- **type: 5**

- **fee:   0*XAS**

- **args:  []**

  Example:  

  ```js
  let params = {
    type:5,   
    fee:0*100000000,  
    args: [],
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  }  
  // generate transaction using asch-js
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.6 Register Group**

- **type: 6**

- **fee:    5*XAS**

- **args:  [name,members,min,max,m,updateInterval]**

  |   Name   |   Type   |   Description   |
  | :------------: | :----: | :-----------------: |
  |      name      | string |     Group name      |
  |    members     | array  |       Array of group members  |
  |      min       | number | Minimum number of decisions (minimum of 3) |
  |      max       | number |     Maximum number of decisions      |
  |       m        | number |   Minimum decision weight   |
  | undateInterval | number |      Update interval       |

  Example:  

  ```js
  let name = 'group1'
  let members = [
      {
          name:'asch_g1',      // member name
          weight:2,            // member weight
          address:'ANge1aRG19tdXcFKu8x6mGHg9PgGdXN69L'   // member address
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
    args: [name,members,min,max,m,undateInterval],
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // generate transaction using asch-js
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.7 Register Agent**

- **type: 7**

- **fee:    100*XAS**

- **args:  []**

  This contract doesn't need parameters.  

  Example:  

  ```js
  let params = {
    type:7,   
    fee:100*100000000,  
    args: [],
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.8 Activate agent**

- **type: 8**

- **fee:    0.1*XAS**

- **args:  [agent]**

  |   Name   |   Type   |   Description   |
  | :---: | :----: | :----------: |
  | agent | string | Agent's nickname |

  ```js
  let agent = 'user1'
  let args = [agent]
  
  let params = {
    type:8,   
    fee:0.1*100000000,  
    args: args  
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  }
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.9 Cancel Agent**

- **type: 9**

- **fee:    0*XAS**

- **args:  []**

  Example:  

  ```js
  let params = {
    type:9,   
    fee:0*100000000,  
    args: [],
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.10 Register Delegate**

- **type: 10**

- **fee:    100*XAS**

- **args:  []**

  Example:  

  ```js
  let params = {
    type:10,   
    fee:100*100000000,  
    args: [],
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  }
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.11 Vote for Delegate**

- **type: 11**

- **fee:    0.1*XAS**

- **args:  [delegates]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :--------------: |
  | delegates | string | name of a delegate |

  Example:  

  ```js
  // delegate1,delegate2,delegate3 (names of 3 delegates)
  let delegates = 'delegate1,delegate2,delegate3'   
  let args = [delegates]
  
  let params = {
    type:11,   
    fee:0.1*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.1.12 Cancel Delegate Vote**

- **type: 12**

- **fee:    0.1*XAS**

- **args:  [delegates]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :--------------: |
  | delegates | string | name of delegates |

  Example:  

  ```js
  let delegates = 'delegate1,delegate2'
  let args = [delegates]
  let params = {
    type:12,   
    fee:0.1*100000000,  
    args: args  
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

###  **3.2 Asset Contracts**

#### **3.2.1 Register publisher**

- **type: 100**

- **fee:    100*XAS**

- **args:  [name,desc]**

  |   Name   |   Type   |   Description   |
  | :--: | :----: | :----------: |
  | name | string |  Publisher name  |
  | desc | string | Description of Publisher |

  Example:  

  ```js
  let name = 'TEST'
  let desc = 'my first issuer'
  let args = [name,desc]
  
  let params = {
    type:100,   
    fee:100*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.2.2 Register Asset**

- **type: 101**

- **fee:    500*XAS**

- **args:  [symbol,desc,maximum,precsion]**

  |   Name   |   Type   |   Description   |
  | :------: | :----: | :----------: |
  |  symbol  | string | Asset name |
  |   desc   | string | Asset description |
  | maximum  | string |  Maximum circulation  |
  | precision | number |  Accuracy |

  Example:  

  ```js
  let symbol = 'TXC'
  let desc = 'my first asset'
  let maximum = '100000000000'
  let precision = 1     // possible values are: 1 up to 16
  // construct args array
  let args = [symbol,desc,maximum,precision]
  let params = {
    type:101,   
    fee:500*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.2.3 Mint Asset tokens**

- **type: 102**

- **fee:    0.1*XAS**

- **args:  [name,amount]**

  |   Name   |   Type   |   Description   |
  | :----: | :----: | :------------: |
  |  name  | string | The asset name |
  | amount | string |    number of minted tokens    |

  Example:  

  ```js
  let name = 'TEST.TXC'    // the asset name is composited from "PublisherName.AssetName"
  let amount = '1000000000'
  let args = [name,amount]
  let params = {
    type:102,   
    fee:0.1*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.2.4 Asset transfer**

- **type: 103**

- **fee:    0.1*XAS**

- **args:  [currency,amount,recipient]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :--------: |
  | currency  | string | Asset name |
  |  amount   | string |  Amount to transfer  |
  | recipient | string |  Receiving address  |

  Example:  

  ```js
  let currency = 'TEST.TXC'
  let amount = '10000000'
  let recipient = 'A3w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'
  let args = [currency,amount,recipient]
  let params = {
    type:103,   
    fee:0.1*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

### **3.3 DApp Contracts**

#### **3.3.1 Register DApp**

- **type: 200**

- **fee:    100*XAS**

- **args:  [name,desc,link,icon,delegates,unlockNumber]**

  |   Name   |   Type   |   Description   |
  | :----------: | :----: | :--------: |
  |     name     | string | Dapp name   |
  |     desc     | string | Description    |
  |     link     | string | Link |
  |     icon     | string | Icon |
  |  delegates   | string | Delegates   |
  | unlockNumber | number | Minmum number of delegates that are needed for block production, minimum 3 |

  Example:  

  ```js
  let name = 'dappTest'        // Dapp name
  let desc = 'some description'
  let link = 'http://yourdomain/dapp.zip'     // Zip archive of DApp code
  let icon = 'htpps//yourdomain/logo.png'     // Link to dapp icon
  // Array of the public keys of future DApp delegates
  let delegates = [
    "0352486d87c928918638c8a13c7e4765f2c9fa075318bd680b8d95e1cf1d616f",
    "cbb3671d343628fe03fba2f0139b783a7b86445f79ee55c99bf5bbe380e4fb46",
    "2f23a9659e32032910b8e078c0c980c6cb7c3a052a235a59079bfd6d608ecc95",
    "351c081c470f41620f4709b6b3ca3721dc920d4e528b27b8fa4d88635e53e128",
    "cbd808111a08081f7dc93aafd9fe26a70216e3f42d927660ab8d15b7bdf8998c"
  ]
  // minimum number of delegates that are needed for block production
  let unlockNumber = 3
  //构建args
  let args = [name,desc,link,icon,delegates,unlockNumber]
  
  let params = {
    type:200,   
    fee:100*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.3.2 Update DApp delegate**

- **type: 201**
- **fee:    1*XAS**
- **args:  [chain,from,to]**

#### **3.3.3 Add DApp delegate**

- **type: 202**
- **fee:    1*XAS**
- **args:  [chain,key]**

#### **3.3.4 Delete DApp delegate**

- **type: 203**
- **fee:    1*XAS**
- **args:  [chain,key]**

#### **3.3.5 Transfer money to own DApp account (Refuel Operation)**

- **type: 204**

- **fee:    0.1*XAS**

- **args:  [chainName,currency,amount]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :------------: |
  | chainName | string | Dapp name |
  | currency  | string | Asset name |
  |  amount   | string | Amount to transfer  |

  Example:  

  ```js
  let chainName = 'dappTest'
  let currency = 'XAS'   // Can also be an asset like CCTime.XCT
  let amount = '1000000000'
  //args构造
  let args = [chainName,currency,amount]
  let params = {
    type:204,   
    fee:0.1*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.3.6 Withdaw from own DApp account to Mainchain acount (Withdraw operation)**

- **type: 205**

- **fee:    0.1*XAS**

- **args:  [chainName,recipient,currency,amount,oid,seq]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :------: |
  | chainName | string |  Chain name  |
  | recipient | string | Receiving address |
  | currency  | string |  Asset name  |
  |  amount   | string | Amount to withdraw |
  |    oid    | string | The corresponding transactionId on the sidechain |
  |    seq    | string | A sequence of numbers in the sidechain `withdrawals` table starting at 1 |

  **Note**: Developers shouldn't call this contract. This contract is called by the ASCH sandbox if the user initiates a [DApp withdrawal contract call](https://github.com/AschPlatform/asch-docs/blob/master/dapp/api/en.md#3112-dapp-withdraw-money-type2). 

### **3.4 Proposal Contracts**

#### **3.4.1 Initiate a proposal**

- **type: 300**

- **fee:    10*XAS**

- **args:  [title,desc,topic,content,endHeight]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :----------: |
  |   title   | string |   Propose title   |
  |   desc    | string |   Description    |
  |   topic   | string |   Proposal type  |
  |  content  | string |     Content     |
  | endHeight | string | Proposal end date (valid until a certain block height) |

  Example:  

  ```js
  let title = 'title fo propose'     //  length: 10-100
  let desc = 'some describes of this propose'
  let topic = 'type of proposal (details below)'
  let content = 'required parameter (details below)'
  let endHeight = 50000     // end height
  // construct args array
  let args = [title,desc,topic,content,endHeight]
  let params = {
    type:300,   
    fee:10*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

  Provide different parameters for different proposal types:  

  1. Add a new gateway

  ```js
  // proposal type
  let topic = 'gateway_register'
  // The content is constructed below. For the new gateway proposal, the name, description, minimum member, update interval, asset information, etc. of the proposal need to be provided.
  let name = 'aschCoin'   // name can be from 3-16 characters long, alphanumeric
  let desc = 'aschyu: test the gateway register'
  let minimumMembers = 3      // The minimum number of members for this gateway. The range of this value should be an integer between 3 and 33.
  let updateInterval = 8640   // Update frequency, this value should be greater than 8640
  
  let symbol = 'TEC'   // For example, the issued currency is called TEC
  let currencyDesc = 'some describes of currency'    // Asset description
  let precsion = 1      // Asset currency
  let currency = {
    symbol:symbol,
    desc:currencyDesc,
    precision:precision
  }
  // construct the content
  let content = {
    name:name,
    desc:desc,
    minimumMembers:minimumMembers,
    updateInterval:updateInterval,
    currency:currency
  }
  ```

  2. Gateway initialization  

  ```js
  // proposal type
  let topic = 'gateway_init'
  // construct content below
  let gateway = 'bitcoin' // gateway name
  let members = [ // Members of the initial gateway
    'A5eTVn2Mz5p2j6SjGKdgvmUc2vMsSvKzuy',
    'A3SmW61ZwxmNc26BbfKLbHkaNbmUQzexuj',
    'A4ncaYtKRrD8YS2Mi82HbwGEE9DxqsbEr9'
  ]
  // construct the content
  let content = {
    gateway:gateway,
    members:members
  }
  ```

  3. Update Gateway Member  

  ```js
  // proposal type
  let topic = 'gateway_update_member'
  // construct content below
  let gateway = 'bitcoin' // gateway name
  let form = 'A3SmW61ZwxmNc26BbfKLbHkaNbmUQzexuj' // member address to revoke
  let to = 'A7w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'     // member address to be added
  // construct the content
  let content = {
    gateway:gateway,
    from:from,
    to:to
  }
  ```

  4. Gateway Revocation

  ```js
  // proposal type
  let topic = 'gateway_revoke'
  // gateway name
  let gateway = 'bitcoin' // gateway name
  // construct content
  let content = {
    gateway:gateway
  }
  ```

#### **3.4.2 Vote for proposal**

- **type: 301**

- **fee:    0.1*XAS**

- **args:  [pid]**

  |   Name   |   Type   |   Description   |
  | :--: | :----: | :--------: |
  | pid  | string | Proposal number |

  Example:  

  ```js
  // the transaction id of the proposal
  let pid = 'aer074700dcea17b56e5a98bbfeee5f6416935b6b444c0750e5cb319d818a502'
  let args = [pid]
  let params = {
    type:301,
    fee:0.1*100000000,
    args: args,
    message,
    secret:mySecret,
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.4.3 Activate Proposal**

- **type: 302**

- **fee:    0*XAS**

- **args:  [pid]**

  |   Name   |   Type   |   Description   |
  | :--: | :----: | :--------: |
  | pid  | string | Proposal id |

  Example:  

  ```js
  let pid = 'aer074700dcea17b56e5a98bbfeee5f6416935b6b444c0750e5cb319d818a502' // transaction id of proposal
  let args = [pid]
  let params = {
    type:303,   
    fee:0*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  }
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

### **3.5 Gateway Contracts**

#### **3.5.1 Open gateway account**

- **type: 400**

- **fee:    0.1*XAS**

- **args:  [gateway]**

  |   Name   |   Type   |   Description   |
  | :-----: | :----: | :--------: |
  | gateway | string | Gateway name |

  Example:  

  ```js
  // gateway name
  let gateway = 'bitcoin'
  let args = [gateway]
  let params = {
    type:400,   
    fee:0.1*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  }
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.5.2 Register member**

- **type: 401**

- **fee:    100*XAS**

- **args:  [pid]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :------: |
  |  gateway  | string | Gateway name |
  | publicKey | string | Public key of member |
  |   desc    | string | Description   |

  Example:  

  ```js
  let gateway = 'bitcoin'
  let publicKey = 'c03e43c7e8aefe3b5a83e02a7b4dc8cce84bb787202650338e85d1b7758065d6'
  let desc = 'aschyu: some describes of resgiter member'
  let args = [gateway,publicKey,desc]
  
  let params = {
    type:401,   
    fee:100*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.5.3 Recharge the gateway**

- **type: 402**

- **fee:    0.01*XAS**

- **args:  [gateway,address,currency,amount,oid]**

  |   Name   |   Type   |   Description   |
  | :------: | :----: | :------: |
  | gateway  | string | Gateway name |
  | address  | string | Deposit address |
  | currency | string | Currency |
  |  amount  | string | Amount |
  |   oid    | string |   |

  Example:  

  ```js
  let gateway = 'bitcoin'
  let address = 'A7w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'
  let currency = 'BTC'
  let amount = '100000000000'
  let oid = ''
  let args = [gateway,address,currency,amount,oid]
  let params = {
    type:402,   
    fee:0.01*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.5.4 Withdraw from the gateway**

- **type: 403**

- **fee:    0*XAS**

- **args:  [address,gateway,currency,amount,fee]**

  |   Name   |   Type   |   Description   |
  | :------: | :----: | :------: |
  | address  | string | Withdraw address |
  | gateway  | string | Gateway name |
  | currency | string | Currency   |
  |  amount  | string |  Amount  |
  |   fee    | string |  Fee  |

  Example:  

  ```js
  let gateway = 'bitcoin'
  let address = 'A7w7Rx5bCerJFbfG5BKdQ77bPqfWeyrmgJ'
  let currency = 'BTC'
  let amount = '100000000000' // amount to transfer
  let fee = '200000000' // gateway fee
  // construct args
  let args = [address,gateway,currency,amount,fee]
  let params = {
    type:403,   
    fee:0*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.5.5 Submit a withdrawl transaction**

- **type: 404**

- **fee:    0.01*XAS**

- **args:  [wid,ot,ots]**

  |   Name   |   Type   |   Description   |
  | :--: | :----: | :------: |
  | wid  | string |  Withdraw id  |
  |  ot  | string | Transaction data |
  | ots  | string |    |

**Note**: This operation is done automatically by the system and is not initiated by the user or developer


#### **3.5.6 Submit transaction signature**

- **type: 405**

- **fee:    0.01*XAS**

- **args:  [wid,signature]**

  |   Name   |   Type   |   Description   |
  | :-------: | :----: | :----: |
  |    wid    | string | Withdraw id |
  | signature | string |  signature  |

**Note**: This operation is done automatically by the system and is not initiated by the user or developer.


#### **3.5.7 Submit a transaction agreement**

- **type: 406**

- **fee:    0.01*XAS**

- **args:  [wid,oid]**

  |   Name   |   Type   |   Description   |
  | :--: | :----: | :----: |
  | wid  | string | Withdraw id |
  | oid  | string |        |


### **3.6 Group Contracts**

#### **3.6.1 Vote**

- **type: 500**

- **fee:    0*XAS**

- **args:  [targetId]**

  |   Name   |   Type   |   Description   |
  | :------: | :----: | :----: |
  | targetId | string | Target Id |

  Example:  

  ```js
  // transaction id
  let targetId = 'f80dcf3d520cc14e963ddf4aedd6ae42db92795fc80ac3738c2be5b3aa5c9238'
  let args = [targetId]
  let params = {
    type:500,
    fee:0*100000000,
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.6.2 Activate Group**

- **type: 501**

- **fee:    0*XAS**

- **args:  [targetId]**

  |   Name   |   Type   |   Description   |
  | :------: | :----: | :----: |
  | targetId | string | 目标ID |

  Example:  

  ```js
  let targetId = 'f80dcf3d520cc14e963ddf4aedd6ae42db92795fc80ac3738c2be5b3aa5c9238' // transaction id
  let args = [targetId]
  let params = {
    type:501,
    fee:0*100000000,
    args: args,
    message,
    secret:mySecret,
    secondSecret:mySecondSecret
  }
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.6.3 Add member**

- **type: 502**

- **fee:   1*XAS**

- **args:  [address,weight,m]**

  |   Name   |   Type   |   Description   |
  | :-----: | :----: | :------: |
  | address | string | 成员地址 |
  | weight  | string |   权重   |
  |    m    | number |          |

  Example:  

  ```js
  let address = 'AMySpLqC4bEgQ8VoYK1iWNEEuhRtjS59Bt'  
  let weight = ''
  let m = 1
  let args = [address,weight,m]
  let params = {
    type:502,
    fee:1*100000000,
    args: args,
    message,
    secret:mySecret,
    secondSecret:mySecondSecret
  }
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```

#### **3.6.4 Remove Member**

- **type: 503**

- **fee:    1*XAS**

- **args:  [address,m]**

  |   Name   |   Type   |   Description   |
  | :-----: | :----: | -------- |
  | address | string | Member address |
  |    m    | number |          |

  Example:  

  ```js
  let address = 'AMySpLqC4bEgQ8VoYK1iWNEEuhRtjS59Bt'  
  let m = 1
  let args = [address,m]
  let params = {
    type:503,   
    fee:1*100000000,  
    args: args,
    message, 
    secret:mySecret,  
    secondSecret:mySecondSecret
  } 
  // create transaction using the asch-js package
  let trs = AschJS.transaction.createTransactionEx(params)
  http.POST(trs)  // see the description of the request process for detail
  ```
