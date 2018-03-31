---
layout: post
Title: "[GO] govendor "
Author: bosco lyu
Date: February 1, 2018
Meta: "IT, GO"
published: false
---

# govendor

# 정의
* url : https://github.com/kardianos/govendor


# trouble shooting

## govendor를 실행할 수 없을 때
### 증상
* govendor를 받았는데 실행이 안됨

```
$go get -u github.com/kardianos/govendor
-bash: govendor: command not found

```

### 원인
* $PATH에 $GOPATH/bin이 추가되어 있지 않아서 그랬음
* go get을 하면 src만이 아니라 bin 디렉토리에도 파일이 다운로드된다는 사실을 몰랐음

### 해결
$PATH에 $GOPATH/bin이 추가함

## github 패키지를 받을 때 계정을 물어볼 때

### 증상 
```
$ govendor fetch github.com/psf13/cobra
Username for 'https://github.com': 
```
### 원인
* 오타로 없는 패키지를 github로 요청하면 발생함.
    * 오타 수정 명령
```
$ govendor fetch github.com/spf13/cobra
```

# reference 
* https://blog.gopheracademy.com/advent-2015/vendor-folder/
* https://zerokspot.com/weblog/2017/04/23/getting-started-with-govendor/



