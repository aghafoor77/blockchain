<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">Ethereum Private Network Deployment</h3>
</div>

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#directory-structure">Directory structure</a></li>
         <li><a href="#install-ethereum-geth">Install ethereum geth</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>  
       <ul>
        <li><a href="#create-boot-key">Create boot key</a></li>
        <li><a href="#create-node-accounts">Create Node Accounts</a></li>
        <li><a href="#create-genesis-block">Create genesis block</a></li>   
        <li><a href="#initialize-ethereum-nodes">Initialize Ethereum Nodes</a></li>
         <li><a href="#deployment-of-ethereum-private-network">Deployment of Ethereum Private Network</a></li>
      </ul>
    </li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

In this tutorial Ethereum private blockchain will be created. It will run four nodes (boot, minner, node1, node2) on same computer. I used Ubuntu 18.04.3 LTS but ican also run on higher version of Ubuntu

<p align="right">(<a href="#readme-top">back to top</a>)</p>



### Directory structure
To deply private network, you need to create folloiwng directory structure.
* Create root directory 
```
$mkdir etherprivatentk
```
```
cd etherprivatentk
```

* Create directory for each node
```
/etherprivatentk$ mkdir boot
```
```
/etherprivatentk$ mkdir minner
```
```
/etherprivatentk$ mkdir node1
```
```
/etherprivatentk$ mkdir node2
```


<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Install ethereum geth
```
$ sudo apt-get -y install software-properties-common
```
```
$ sudo add-apt-repository -y ppa:ethereum/ethereum
```
```
$ sudo apt-get update
```
```
$ sudo apt-get -y install ethereum
```

<!-- GETTING STARTED -->
## Getting Started

### Create boot key
Create boot key for boot node by running following commands.

```
$cd boot
```
```
/boot$ bootnode -genkey boot.key
```

### Create Node Accounts
Create eth account for minner, node1, node2:
* Create eth account for minner account
Execute following commands and it will ask for password. Create minnerpass.txt file in the same fodler and paste password in that.
```
cd minner
```
```
/minner$ geth --datadir ./data account new
```

After creation minner account, you need to save following data which is displayed on terminal.

Public address of the key:   0x6F93Bb12D5Eec64edF36F081d6Ec5d6DD5ABe1a0

Path of the secret key file: data/keystore/UTC--2022-12-22T12-11-28.556147252Z--6f93bb12d5eec64edf36f081d6ec5d6dd5abe1a0

* Create eth account for node1
Execute following commands and it will ask for password. keep it for future use.
```
cd ..
```
```
cd node1
```
```
$ geth --datadir ./data account new
```
It it will display folloiwng informaton on termal. please keep it save for future use.

Public address of the key:   0xCACD7e341bD0F629aC22D6Fb067aAd380000F8C8

Path of the secret key file: data/keystore/UTC--2022-12-22T12-12-51.178534386Z--cacd7e341bd0f629ac22d6fb067aad380000f8c8


* Create eth account for node2
Execute following commands and it will ask for password. keep it for future use.
```
cd ..
```
```
cd  node2
```
```
$ geth --datadir ./data account new
```

Public address of the key:   0x3E8Be83e729282c25dDf95B715d97b7b07724e8e

Path of the secret key file: data/keystore/UTC--2022-12-22T12-13-38.477210329Z--3e8be83e729282c25ddf95b715d97b7b07724e8e

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Create genesis block
For creating genesis block, run following command. Please note when you execute this command, it will ask for various options in sequence and in each option, please provide recommended input.

Open a new Terminal and then execute folloiwng command 

```
$ puppet
```

Please specify a network name to administer (no spaces, hyphens or capital letters please)

Enter >admin

Sweet, you can set this via --network=admin next time!

INFO [12-23|13:14:05.896] Administering Ethereum network           name=admin

WARN [12-23|13:14:05.901] No previous configurations found         path=/home/vmc/.puppeth/admin

Enter >2

What would you like to do? (default = create)

 1. Create new genesis from scratch
 2. Import already existing genesis

Enter >1

Which consensus engine to use? (default = clique)

 1. Ethash - proof-of-work
 2. Clique - proof-of-authority
 
Enter >1

Which accounts should be pre-funded? (advisable at least one)

 Enter > 0x<Public address of the key (remove 0x which are the starting two character of address)>
 
 Enter > 0x<Public address of the key (remove 0x which are the starting two character of address)>
 
 . 0x

Like following 

Enter > 0xCACD7e341bD0F629aC22D6Fb067aAd380000F8C8

Enter > 0x3E8Be83e729282c25dDf95B715d97b7b07724e8e

Enter > 0x<press-enter>
  
Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? (advisable yes)
  
Enter >yes
  
Specify your chain/network ID if you want an explicit one (default = random)
  
Enter >94321701

Also save network ID: 94321701
  
What would you like to do? (default = stats)
 1. Show network stats
 2. Manage existing genesis
 3. Track new remote server
 4. Deploy network components
  
Enter >2
  
1. Modify existing configurations
2. Export genesis configurations
3. Remove genesis configuration
  
Enter >2
  
Which folder to save the genesis spec into? (default = current)
  Will create admin.json
  
Enter >/home/<host-name>/Desktop/etherprivatentk
  
INFO [12-23|13:25:01.582] Saved native genesis chain spec          path=/home/<host-name>/Desktop/etherprivatentk/admin.json

Note: Close terminal and you can find the admin.json (genesis) is in the =/home/<host-name>/Desktop/etherprivatentk/ folder. 

<p align="right">(<a href="#readme-top">back to top</a>)</p>


### Initialize Ethereum Nodes
 
Run following command on each node [minner, node1, node2, no need on bootnode]
```  
cd ..
```
```
cd minner
```
```
geth --datadir ./data init /home/<host-name>/Desktop/etherprivatentk/admin.json 
```
```  
cd ..
```
```
cd node1
```
```
geth --datadir ./data init /home/<host-name>/Desktop/etherprivatentk/admin.json 
```

```  
cd ..
```
```
cd node2
```
```
geth --datadir ./data init /home/<host-name>/Desktop/etherprivatentk/admin.json 
```
### Deployment of Ethereum Private Network
  
* Deploy bootnode:

  Open Terminal and current directory should be etherprivatentk and run following command:

```
cd boot
```
```
/boot$ bootnode -nodekey ./boot.key -verbosity 7 -addr "127.0.0.1:30301"
```

  It will display following data on terminal 

  enode://eaedc775ab59e41657b78225cb26f3d6c7470ab1af63382c5c53e385aa5bb5531e3370748cb2afdc22e3538cc686a20ee5ce8ab2f816a917eb9ddc197161307b@127.0.0.1:0?discport=30301
  
  Note: you're using cmd/bootnode, a developer tool.
  We recommend using a regular node as bootstrap node for production deployments.
  INFO [12-23|13:30:30.297] New local node record                    seq=1,671,798,630,296 id=08ccf1b133843096 ip=<nil> udp=0 tcp=0

Keep above data in a file for future usage which is the boot node address started from enode:// 
 
* Run minner:

  You need to create following command by replacing <parameters>

geth --networkid <networkid> --datadir "./data" --bootnodes <change-with-boot-address> --port 30303 --ipcdisable --syncmode full  --unlock <minner-address> --password <minner-pass-file> --mine console

Open Terminal and current directory should be etherprivatentk. Run following command:

```
cd minner
```
```
/ minner$ geth --networkid 94321701 --datadir "./data" --bootnodes enode://eaedc775ab59e41657b78225cb26f3d6c7470ab1af63382c5c53e385aa5bb5531e3370748cb2afdc22e3538cc686a20ee5ce8ab2f816a917eb9ddc197161307b@127.0.0.1:0?discport=30301 --port 30303 --ipcdisable --syncmode full  --unlock 0x6F93Bb12D5Eec64edF36F081d6Ec5d6DD5ABe1a0 --password minnerpass.txt --mine console
```
  
It will connect with boot node and will start Looking for peers

* Running Node 1: 

You need to create following command by replacing <parameters>
  
/node1$ geth --networkid <networkid> --datadir "./data" --bootnodes <boot-node-address> --port <port-eth-network> --ipcdisable --syncmode full --rpc.allow-unprotected-txs --authrpc.port <rpc-port> --allow-insecure-unlock --http --http.addr 0.0.0.0 --http.api personal,eth,net,web3 --http.port <http-port> console

Note: Ports should be unique and different from the minner and boot node ports

Open Terminal and current directory should be etherprivatentk. Run following command:
```
cd node1
```
```
/node1$ geth --networkid 94321701 --datadir "./data" --bootnodes enode://eaedc775ab59e41657b78225cb26f3d6c7470ab1af63382c5c53e385aa5bb5531e3370748cb2afdc22e3538cc686a20ee5ce8ab2f816a917eb9ddc197161307b@127.0.0.1:0?discport=30301 --port 30305 --ipcdisable --syncmode full --rpc.allow-unprotected-txs --authrpc.port 8585 --allow-insecure-unlock --http --http.addr 0.0.0.0 --http.api personal,eth,net,web3 --http.port 8586 console

You can view minner terminal and it start showing following information 
  
INFO [12-23|13:40:15.641] Looking for peers                        peercount=1 tried=0 static=0


* Running Node 2: 

You need to create following command by replacing <parameters>
geth --networkid <networkid> --datadir "./data" --bootnodes <boot-node-address> --port <port-eth-network> --ipcdisable --syncmode full --rpc.allow-unprotected-txs --authrpc.port <rpc-port> --allow-insecure-unlock --http --http.addr 0.0.0.0 --http.api personal,eth,net,web3 --http.port <http-port> console
Note: Ports should be unique and different from the minner, boot and node1 ports

Open Terminal and current directory should be etherprivatentk. Run following command:
```
cd node2
```
```
/node2$geth --networkid 94321701 --datadir "./data" --bootnodes enode://eaedc775ab59e41657b78225cb26f3d6c7470ab1af63382c5c53e385aa5bb5531e3370748cb2afdc22e3538cc686a20ee5ce8ab2f816a917eb9ddc197161307b@127.0.0.1:0?discport=30301 --port 30307 --ipcdisable --syncmode full --rpc.allow-unprotected-txs --authrpc.port 8587 --allow-insecure-unlock  --http --http.addr 0.0.0.0 --http.api personal,eth,net,web3 --http.port 8588 console
```
  
After this you can check the minner node and it start displaying following information where peercount=2
  
INFO [12-23|13:51:08.742] Looking for peers                        peercount=2 tried=0 static=0


<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



## Contact

Abdul Ghafoor Abbasi -aghafoor77@gmail.com

Project Link: [https://github.com/aghafoor77/selectivedisclouser](https://github.com/aghafoor77/selectivedisclouser)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

