   * [Asch Full Node Installation](#asch-full-node-installation)
      * [1. System Requirements and dependencies](#1-system-requirements-and-dependencies)
         * [1.1 System Requirements](#11-system-requirements)
         * [1.2 Install dependencies](#12-install-dependencies)
         * [1.3 Install Node.js](#13-install-nodejs)
      * [2. Install Asch Mainnet Full Node](#2-install-asch-mainnet-full-node)
         * [2.1 Download installation package](#21-download-installation-package)
         * [2.2 Modify config.json](#22-modify-configjson)
         * [2.3 Download database snapshot](#23-download-database-snapshot)
         * [2.4 Start the node](#24-start-the-node)
      * [3. Install Asch Testnet Full Node](#3-install-asch-testnet-full-node)
         * [3.1 Download installation package](#31-download-installation-package)
         * [3.2 Modify config.json](#32-modify-configjson)
         * [3.3 Download database snapshot](#33-download-database-snapshot)
         * [3.4 Start the node](#34-start-the-node)
      * [4. Install Asch Localnet Full Node](#4-install-asch-localnet-full-node)
         * [4.1 Download installation package](#41-download-installation-package)
         * [4.2 Modify config.json](#42-modify-configjson)
         * [4.3 Start the node](#43-start-the-node)
         * [4.4 Genesis account](#44-genesis-account)
      * [5. Install from source code](#5-install-from-source-code)
         * [5.1 Clone the code](#51-clone-the-code)
         * [5.2 Install dependencies](#52-install-dependencies)
         * [5.3 Modify app.js](#53-modify-appjs)
         * [5.4 Replace config.json](#54-replace-configjson)
         * [5.5 Create relevent folders](#55-create-relevent-folders)
         * [5.6 Configure frontend](#56-configure-frontend)
         * [5.7 Download database snapshot](#57-download-database-snapshot)
         * [5.8 Start the node](#58-start-the-node)
      * [6. Common errors and solutions](#6-common-errors-and-solutions)
         * [6.1 Cannot access wallet webpage](#61-cannot-access-wallet-webpage)
         * [6.2 Delegates node can not forge new blocks](#62-delegates-node-can-not-forge-new-blocks)
         * [6.3 Cannot sync blocks](#63-cannot-sync-blocks)
      * [7. Upgrade](#7-upgrade)
      * [8. Frequently used commands](#8-frequently-used-commands)
      * [9. Configure delegate](#9-configure-delegate)


# Asch Full Node Installation

## 1. System Requirements and dependencies

### 1.1 System Requirements

- Must be a linux os, recommend Ubuntu 14.04+
- Must have a public IP address
- CPU > 2 cores
- Memory > 2G
- Bandwidth > 2Mbps
- Hard disk > 30 GB

### 1.2 Install dependencies

```
# Install dependency package
sudo apt-get install curl sqlite3 ntp wget git libssl-dev openssl make gcc g++ autoconf automake python build-essential -y
# libsodium for ubuntu 14.04
sudo apt-get install libtool -y
# libsodium for ubuntu 16.04
sudo apt-get install libtool libtool-bin -y
```

### 1.3 Install Node.js

Asch support the latest LTS version of Node.js(current version is v8.11.3). Please make sure that you install the right version.

```
# Install nvm
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash

# This loads nvm
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" 
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# Install node and npm for current user.
nvm install v8

# check node version and it should be v8.x.x
node --version
```

## 2. Install Asch Mainnet Full Node

Default port for mainnet is 8192, P2P port is 8193. If you change the default port, please make sure `P2P port = default port + 1`

### 2.1 Download installation package

```
wget https://downloads.asch.cn/package/asch-linux-latest-mainnet.tar.gz
tar zxvf asch-linux-latest-mainnet.tar.gz
cd asch-linux-1.4.2-mainnet // This version varies in different time 
```

### 2.2 Modify config.json 

```
vim config.json

add your IP address to the field publicIp
```

### 2.3 Download database snapshot

Download the database snapshot and then unpack it. Replace the original data folder.

```
wget https://downloads.asch.cn/package/blockchain-mainnet-snapshot.tar.gz
tar zvxf blockchain-mainnet-snapshot.tar.gz
```

### 2.4 Start the node
execute 
`./aschd start`

Check your height from `logs/debug.2018xxxx.log` or `http://yourip:8192/api/blocks/getHeight`


## 3. Install Asch Testnet Full Node

Default port for testnet is 4096, P2P port is 4097. If you change the default port, please make sure `P2P port = default port + 1`


### 3.1 Download installation package

```
wget https://downloads.asch.cn/package/asch-linux-latest-testnet.tar.gz
tar zxvf asch-linux-latest-testnet.tar.gz
cd asch-linux-1.4.2-testnet // This version varies in different time 
```

### 3.2 Modify config.json 

```
vim config.json

add your IP address to the field publicIp
```

### 3.3 Download database snapshot

Download the database snapshot and then unpack it. Replace the original data folder.

```
wget https://downloads.asch.cn/package/blockchain-testnet-snapshot.tar.gz
tar zvxf blockchain-testnet-snapshot.tar.gz
```

### 3.4 Start the node

execute `./aschd start`

Check your height from `logs/debug.2018xxxx.log` or `http://yourip:8192/api/blocks/getHeight`

## 4. Install Asch Localnet Full Node

Default port for localnet is 4096, P2P port is 4097. If you change the default port, please make sure `P2P port = default port + 1`

### 4.1 Download installation package

```
wget https://downloads.asch.cn/package/asch-linux-latest-localnet.tar.gz
tar zxvf asch-linux-latest-localnet.tar.gz
cd asch-linux-1.4.2-localnet // This version varies in different time
```

### 4.2 Modify config.json 

```
vim config.json

add your IP address to the field publicIp
```

### 4.3 Start the node

execute `./aschd start`

Check your height from `logs/debug.2018xxxx.log` or `http://yourip:8192/api/blocks/getHeight`

### 4.4 Genesis account

There are 100,000,000 XAS in the genesis account, the password is 

`stone elephant caught wrong spend traffic success fetch inside blush virtual element`

## 5. Install from source code

We will install mainnet from source code here.

### 5.1 Clone the code
```
git clone https://github.com/AschPlatform/asch
```

### 5.2 Install dependencies

```
npm install
```

### 5.3 Modify app.js

```
search for testnet and modify it to mainnet。Result：

appConfig.netVersion = process.env.NET_VERSION || 'mainnet'
```

### 5.4 Replace config.json

```
cp config-mainnet.json config.json
```

Add you IP address to the publicIp field.

### 5.5 Create relevent folders

```
mkdir -p public/dist
mkdir chains
```

### 5.6 Configure frontend

```
cd public/dist
wget https://downloads.asch.cn/package/frontend-mainnet-5f5b3cf5.zip
unzip frontend-mainnet-5f5b3cf5.zip
```

### 5.7 Download database snapshot

```
cd asch
wget http://47.75.26.122/blockchain-mainnet-snapshot.tar.gz
tar zvxf blockchain-mainnet-snapshot.tar.gz
```

### 5.8 Start the node

```
./aschd start
```

## 6. Common errors and solutions

### 6.1 Cannot access wallet webpage

The url of wallet is  http://your_ip:your_port, Mainnet default port is 8192， Testnet and Localnet are both 4096.

Steps：

1. Check the port in config.json
2. Check your firewall
3. Check the node status executing `./aschd status`. If not started, please run `./aschd start`.

### 6.2 Delegates node can not forge new blocks

Steps：

1. Check your ranking (should be in the top 101)
2. Seach the log by executing `grep Failed logs/debug.log`. If you found errors like `Failed to get public ip, block forging MAY not work!`, please config your publicIp in config.json
3. Search the log by executing `grep error logs/debug.log`. If you found errors like `Failed to load delegates: Account xxxxxxxxx not found`, please register your account to a delegate first.

If your node is syncing blocks, please wait the server to finish syncing and then restart.

```
./aschd restart
```
If you found these logs, then your node is worked!
```
grep Forging logs/debug.log
Forging enabled on account: xxxxxxxxxxxxxx
```

### 6.3 Cannot sync blocks

Check your node's block height with the latest block height(can be found on https://wallet.asch.cn/api/blocks/getHeight). If you found your node's height is not increasing, please check the follow steps:

1. Update to the latest version and restart
```
./aschd upgrade
./aschd start
```

2. rebuild
```
./aschd rebuild
```

## 7. Upgrade

After installing the node, upgrade is easy by executing `./aschd upgrade`.

Go to the asch folder and run:
```
./aschd upgrade
./aschd start
```

## 8. Frequently used commands

```
# start node 
./aschd start

# stop node
./aschd stop

# check node status
./aschd status

# restart node
./aschd restart

# upgrade node
./aschd upgrade

# rebuild the blocks
./aschd rebuild

# check node version
./aschd version

# enable forging blocks(only used for delegates)
./aschd enable "your sercret"

# check node log
tail -f logs/debug.201xxxxx.log
```

## 9. Configure delegate

Open config.json and fill in your master secret to the secret field.

Note: Please don't configure the same delegate on different servers!

run following commands：
```
// restart node
./aschd restart

// enable forging
./aschd enable "your sercret"
```
