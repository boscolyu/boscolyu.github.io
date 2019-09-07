---
layout: post
Title: "[BlockChain] 일반론"
Author: bosco lyu
Meta: ""
published: false
---

# 사전 리뷰 - 블럭체인 정의 및 특징
### 공개성
* 이전 : 방화벽 뒤쪽의 중앙 데이터베이스에 데이터 저장
* 이후 : P2P 네트워크에 분산된 원장 형태의 데이터베이스 구조

### 신뢰성
* 조작을 어렵게 만들자.
    * 이전 블럭에 해시값을 다음 블럭에 추가한다.
    * 하나를 고치면 이후 블럭을 전부 고쳐야 함.
* 사이닝을 통한 본인 확인
    * private key로 암호화했기 때문에 키가 유출되지 않는 한 본인 확인 가능함. 
* 이중 지불의 방지
    * 없는 돈을 송금할 수 없음.

### 조작방지를 위한 합의
* PoW : 숙제를 먼저 해결한 사람의 블럭을 추가함.

### Smart Contract
* 계약 내용을 프로그래밍 한다.
* 중개자가 필요없음.

### public, private, consortium
* 블럭 생성 권한을 누가 가지고 있는가?


# 목차
## 신뢰
* 이중 지불 Double Spending

## 공유
* P2P

## 거래
* UTXO
    * input(이전 트랜잭션 번호:index) -> function -> output(새로운 output)
    * 
* State

## 저장
* Merkle Tree
* Bloom Filter
* Level DB

## 합의 Consensus 
* PoW
* PoS
* PoA
* PBFT
* LFT

## Smart Contract
* scripting (bitcoin)
* 단점 (by Ethereum)
    * 튜링 불완전성
    * 반복문이 포함되어 있지 않다. 
        * 무한 루프 방지 목적
    * 다양한 상태를 표시할 수 없다.
    * 블럭체인을 해독할 방법이 없다
* smart contract (ethereum solidity)

## Security, Prove
* PrivateKey, PublickKey, Wallet Address
* HD Wallet

## Trend
* Lightening Network
* Plazma

## Term
* Segwit (Segregated Witness)
* CoinBase
* ommers
