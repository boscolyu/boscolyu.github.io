---
layout: post
Title: "[GO] golang"
Author: bosco lyu
Date: February 1, 2018
Meta: "IT, GO"
---

# go version mismatch error

## 증상
어느 날 갑자기 go build 명령의 결과에 에러가 발생함.
에러 로그는 아래와 같음.

```
compile: version "go1.9" does not match go tool version "go1.9.3"
```

## 원인
$GOROOT에 설정된 go 와 실제 $PATH에 잡힌 go의 버전이 달라서 발생한 문제

```
$echo $GOROOT
/usr/local/go

$which go
/usr/local/bin/go
```

나도 모르게 go를 하나더 설치한 듯..

## 해결
brew uninstall 로 추가 설치된 go를 삭제함.

```
$brew list
autoconf	coreutils	gnu-tar		libksba		libyaml		pkg-config	ruby
automake	gdb		go		libgpg-error	libtool		openssl		readline
```

```
$brew uninstall go
```


