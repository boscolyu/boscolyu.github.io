---
layout: post
Title: "docker command"
Author: bosco lyu
Date:   September 24, 2017
Meta: "IT"
published: false
---
<img src="/images/fulls/02.jpg" class="fit image">
## docker 프로세스 확인하기
### 명령어 : docker ps 

* 도움말

```
MacBook-Pro:fabcar$ docker ps --help

Usage:    docker ps [OPTIONS]

List containers

Options:
  -a, --all             Show all containers (default shows just running)
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print containers using a Go template
      --help            Print usage
  -n, --last int        Show n last created containers (includes all states) (default -1)
  -l, --latest          Show the latest created container (includes all states)
      --no-trunc        Don't truncate output
  -q, --quiet           Only display numeric IDs
  -s, --size            Display total file sizes
```

* 옵션 설명

```
  -a, —all             모든 컨테이너 정보를 보여줌 (종료된 것도 같이 보여줌. -a 옵션이 없으면 현재 실행중인 컨테이너 정보를 보여줌) 
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print containers using a Go template
      —help            사용법 확인
  -n, --last int        상태와 상관없이 마지막에 생성된 n개의 컨테이너 정보를 보여줌. 
  -l, —latest          상태와 상관없이 맨 마지막에 생성된 컨테이너 정보를 보여줌.
      --no-trunc      output을 자르지 않고 다 보여주기. container id의 전체값이 보여짐.
  -q, —quiet         컨테이너 아이디만 보여주기 
  -s, —size           맨 마지막 컬럼에 파일 사이즈를 추가해서 보여줌.
```
결과물 

```
MacBook-Pro:fabcar$ docker ps
CONTAINER ID        IMAGE                                                   COMMAND                  CREATED             STATUS              PORTS                       NAMES
1997e0354b69        hyperledger/fabric-tools                                          "/bin/bash"              2 days ago          Up 2 days                                                            cli
2b45c86b7f12        hyperledger/fabric-peer                                            "peer node start"        2 days ago          Up 2 days           0.0.0.0:7051->7051/tcp, 0.0.0.0:7053->7053/tcp   peer0.org1.example.com
06f8fd6a9aee        hyperledger/fabric-orderer                                         "orderer"                2 days ago          Up 2 days           0.0.0.0:7050->7050/tcp                           orderer.example.com
bb27a74c7355        hyperledger/fabric-ca                                               "sh -c 'fabric-ca-..."   2 days ago          Up 2 days           0.0.0.0:7054->7054/tcp                           ca.example.com
```
## docker 에 쉘로 접속하기

### 명령어 : docker exec
 
* 도움말

```
MacBook-Pro:fabcar$ docker exec --help

Usage:    docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

Run a command in a running container

Options:
  -d, --detach               Detached mode: run command in the background
      --detach-keys string   Override the key sequence for detaching a container
  -e, --env list             Set environment variables
      --help                 Print usage
  -i, --interactive          Keep STDIN open even if not attached
      --privileged           Give extended privileges to the command
  -t, --tty                  Allocate a pseudo-TTY
  -u, --user string          Username or UID (format: <name|uid>[:<group|gid>])
```

* 옵션 설명

```
  -d, --detach               Detached mode: run command in the background
      --detach-keys string   Override the key sequence for detaching a container
  -e, --env list             Set environment variables
      --help                 Print usage
  -i, --interactive          Keep STDIN open even if not attached
      --privileged           Give extended privileges to the command
  -t, --tty                  Allocate a pseudo-TTY
  -u, --user string          Username or UID (format: <name|uid>[:<group|gid>])

```

```
MacBook-Pro:fabcar$ docker exec -it 2b45c86b7f12 /bin/bash
root@2b45c86b7f12:/opt/gopath/src/github.com/hyperledger/fabric#
```
