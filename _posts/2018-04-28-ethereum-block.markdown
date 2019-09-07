---
layout: post
Title: "Ethereum Block"
Author: bosco lyu
Meta: ""
published: false
---


# BlockHeader
* parentHash : 이전 브럭의 해시값
* ommersHash : 자기 블럭에 포함된 ommers list에서 추출한 해시값
    * 모든 데이터의 해시값?
    * 머클 트리형태의 해시값?
* beneficiary : 성공적으로 마이닝한 트랙잭션의 수수료의 합계? 160 bit address
* stateRoot : world state trie root
* transactionRoot : transaction trie root
* receiptsRoot : transactio receipt trie root
* logsBloom : bloom filter
* difficulty : 
* number : block의 높이 (the numbers of ancestor block)
* gasLimit : block당 소모한 gas의 현재 한계값
* gasUsed :
* timestamp : 
* extraData :
* mixHash :
* nonce :
* transaction List :
* ommers List :



# How to make the ehtereum block chain


