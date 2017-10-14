---
layout: post
Title: "Go, Docker, BlockChain, Hyperledger Fabric"
Author: bosco lyu
Date:   September 27, 2017
Meta: "IT"  
---
<img src="/images/fulls/01.jpg" class="fit image">
## site 
* Go 사이트 : https://golang.org/#
* Go 개발 환경 구축 : https://github.com/arahansa/golkorea/wiki/02.-Go%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95_Linux-%ED%8E%B8
* 예제로 배우는 Go 프로그래밍 : http://golang.site/

## Docker
## Site
* https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html
* https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html
* https://subicura.com/2017/02/10/docker-guide-for-beginners-create-image-and-deploy.html
* https://docs.docker.com/machine/overview/#what-is-docker-machine
* https://docs.docker.com/docker-for-mac/
* https://docs.docker.com/get-started/part2/
* https://docs.docker.com/

# blockchain
## site
* https://steemit.com/kr/@maa/pos
* https://steemit.com/kr/@hoonboy21c/pos-vs-pow
* https://www.coindesk.com/ethereums-big-switch-the-new-roadmap-to-proof-of-stake/

# Hyperledger Fabric
## concept
## SDK
* client SDK : 
	* Node.js : Node.js version 7.x is not supported at this time. (2017/09/25)
	* Java : https://github.com/hyperledger/fabric-sdk-java
		* JDK 1.8 or above

## install
### prerequisites
* dependecy : curl, docker, go
* site : https://hyperledger-fabric.readthedocs.io/en/latest/prereqs.html
### install Binaries and Docker Images
* get docker fabric image

```
curl -sSL https://goo.gl/Gci9ZX | bash
```

```
git clone https://github.com/hyperledger/fabric-samples.git
```

```
npm install
```
### run the first network

* generate required certificates and genesis block

```
cd first-network
./byfn.sh -m generate
```

### run the sample application

```
cd fabcar
./startFabric.sh
npm install
```

if you fail to npm install command, check the below document
https://haandol.wordpress.com/2013/10/01/node-gyp-rebuild-%EC%97%90%EB%9F%AC/

```
npm WARN fabcar@1.0.0 No repository field.
npm ERR! Linux 3.10.0-327.28.3.el7.x86_64
npm ERR! argv "/usr/bin/node" "/usr/bin/npm" "install"
npm ERR! node v6.11.4
npm ERR! npm  v3.10.10
npm ERR! code ELIFECYCLE

npm ERR! pkcs11js@1.0.10 install: `node-gyp rebuild`
npm ERR! Exit status 1

```






## application
* update, query
### SDK
* https://hyperledger-fabric.readthedocs.io/en/latest/fabric-sdks.html

# architecture
* https://hyperledger-fabric.readthedocs.io/en/latest/arch-deep-dive.html

## hyperledger fabric basic component
serve as the backbone of network.
### peer node
* maybe save the data, manage the blockchain
* network endpoints
### ordering node
The ordering service will bundle the transaction into a block and then “deliver” the block to all peers on a channel for validation
### Certificate Authority
* http://hyperledger-fabric-ca.readthedocs.io/en/latest/
### CLI Container for a few administrative commands.
command
### chaincode
* https://hyperledger-fabric.readthedocs.io/en/latest/chaincode.html
* https://hyperledger-fabric.readthedocs.io/en/latest/chaincode4noah.html
* https://hyperledger-fabric.readthedocs.io/en/latest/chaincode4ade.html
* chaincode ID (?)


### channel 
* https://hyperledger-fabric.readthedocs.io/en/latest/channels.html
### gossip
* https://hyperledger-fabric.readthedocs.io/en/latest/gossip.html



## Site
* https://developer.ibm.com/kr/developer-%EA%B8%B0%EC%88%A0-%ED%8F%AC%EB%9F%BC/2017/01/15/blockchain-basic-02-hyperledger-fabric-overview/
* https://developer.ibm.com/kr/cloud/bluemix/2017/04/04/starting_blockchain_using_hyperledger_fabric/
* https://github.com/hyperledger/fabric
* https://hyperledger-fabric.readthedocs.io/en/latest/getting_started.html
