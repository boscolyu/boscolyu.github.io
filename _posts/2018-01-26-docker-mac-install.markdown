---
layout: post
Title: "[Docker] Install Docker in Mac"
Author: bosco lyu
Date: January 26, 2018
Meta: "IT"
---

<img src="/images/fulls/docker.png" class="fit image">

## 개요
* docker는 리눅스 컨테이너임. 그래서 docker for mac의 경우에는 VM 기반위에서 동작함.
* 관련 문서 : https://docs.docker.com/docker-for-mac/

## 설치
다운로드 받아서 일반적인 맥 프로그램 설치하듯이 설치할 수 있음.
매뉴얼이 잘 되어 있음

install manual : https://docs.docker.com/docker-for-mac/install/

* 설치 후 화면


## 설치 확인

* docker 설치 위치

```
MacBook-Pro:fabcar nhnent$ which docker
/usr/local/bin/docker
```

* docker 버전 확인 명령

```
MacBook-Pro:fabcar nhnent$ docker --version
Docker version 17.06.2-ce, build cec0b72
```