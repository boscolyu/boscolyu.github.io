---
layout: post
Title: "Ethereum Modified Merkle Patricia Trie"
Author: bosco lyu
Meta: ""
published: false
---
# Background
## Bitcoin Bloom Filter, Merkle Tree
블록체인의 개념이 처음에는 많이 생소했지만 이제는 많은 개발자분들이 알고 계신 것같습니다. Oracle, My-SQL처럼 중앙 데이터베이스에 값을 저장하는 대신에 블록체인에 값을 저장하면서 데이터 조작이 매우 힘들다는 것은 개선된 점이지만 반대로 Primary Key, Index가 없기 때문에 특정 키에 대한 조회 성능은 현저하게 떨어집니다. 다른 한 편으로는 데이터에 대한 변경이 이루어지지 않았고 유효하다는 것을 검증하는 방법도 데이터에 대한 조회도 상대적으로 조작의 위험성은 많이 블록이 해시값을 이용한 체인으로 연결되어 있습니다. 비트코인에서 내부적으로 2가지 자료 구조를 사용합니다. Merkel Tree

### Merkle Tree
* 블록 1개에 포함되어 있는 트랜잭션들이 조작없이 포함되어 있음을 최대한 빠른 시간에 확인하기 위해서 만든 자료 구조.
* 이미 트랜잭션 조작이 불가능한 상태에서 

# Why ethereum make the Merkle Patricia Trie

# How to make?

# Trie

# Patricia Trie

# reference

* https://github.com/ethereum/wiki/wiki/Patricia-Tree
