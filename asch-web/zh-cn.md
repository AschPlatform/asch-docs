# AschPay Browser Extension

[Download From Chrome WebStore](https://chrome.google.com/webstore/detail/aschpay/eibepfonpdkkelekmahbbhcfkeijlpop)

AschPay is a Browser Extension for Asch NetWork.  
It can be used to debug smart contract, or play DApps with browser.

## Build

- Install [Node.js](https://nodejs.org/) version 8.9.3 or later.
- Install local dependencies with `npm install`.
- Build with development `npm run dev`.
- Build for Publishing `npm run build`.

Uncompressed builds will found in `./build`

## DApp Developers

When AschPay is installed, AschPay will inject a [AschWeb](https://github.com/AschPlatform/asch-web) object into current document, you can find it in `window.aschPay.aschWeb` or `window.aschWeb`.  
Note that you can use like this to check AschPay environment

```
window.addEventListener('load', function() {

  // Checking if the aschWeb has been injected
  if (typeof aschPay !== 'undefined') {
    aschWeb = aschPay.aschWeb || aschWeb
    if (aschWeb.isAschPay && aschWeb.ready) {
        // Now start you app & access aschWeb
    }
  } else {
    console.log('No aschWeb? You should install AschPay!')
  }
})
```



## Asch智能合约和前端交互


### 安装谷歌AschPay钱包

```javascript
// chrome网上应用店
https://chrome.google.com/webstore/detail/asch-pay/gjdneabihbmcpobmfhcnljaojmgoihfk

// github
https://github.com/AschPlatform/asch-web

```

### 全局声明

```javascript
const aschWeb = window.aschWeb
const contract = await aschWeb.createContractFromName('crowdFundging_v1')
```

### 调用合约方法

```javascript
let result = await contract.call('getXXT', ['233'], 1000000, false)
console.log('testContract result:' + JSON.stringify(result))

```

### 转账到合约

```javascript
  contract.pay('XAS', '12345', contract.name, 1000000, false).
    then(res => {
      if (res.success) {
        alert('调用成功')
        //document.getElementById('result').innerHTML = JSON.stringify(res)
      } else {
       // alert(res.error)
        console.error(res)
      }
    }).catch(err => {
      alert(res.error)
      console.error(err)
    })

```



## License

AschPay is [MIT](./LICENSE) licensed# asch-pay
