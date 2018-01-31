---
layout: post
Title: "[Docker] Install Docker in Linux"
Author: bosco lyu
Date: January 26, 2018
Meta: "IT"
---


# Requirement
* os : To install Docker CE, you need a maintained version of CentOS 7
* yum repository : centos-7 - Extras
    * command : yum repolist
    * https://zetawiki.com/wiki/Yum_%EC%A0%80%EC%9E%A5%EC%86%8C_%ED%99%95%EC%9D%B8
# Uninstall
* old version 제거 작업임. 신규 설치면 아래와 같이 지울 것이 없다고 나옴.
[parallels@centos-linux-7 ~]$ sudo yum remove docker docker-common docker-selinux docker-engine
Loaded plugins: fastestmirror, langpacksNo 
Match for argument: docker
No Match for argument: docker-common
No Match for argument: docker-selinux
No Match for argument: docker-engine
No Packages marked for removal
# Install
## install with yum
* 설치 가능한 버전 확인
[parallels@centos-linux-7 ~]$ yum list docker-ce --showduplicates | sort -r
 * updates: mirror.navercorp.com
Loading mirror speeds from cached hostfile
Loaded plugins: fastestmirror, langpacks
 * extras: mirror.navercorp.com
docker-ce.x86_64            17.09.0.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.06.2.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.06.1.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.06.0.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.03.2.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.03.1.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.03.0.ce-1.el7.centos             docker-ce-stable
 * base: mirror.navercorp.comAvailable Packages

* 최신 버전 설치

sudo yum install docker-ce
sudo yum install docker-compose

* 버전별로 설치

sudo yum install <FULLY-QUALIFIED-PACKAGE-NAME>

* check the GPG Key
* check the GPG Key
    * 설치 중간에 이런 거 물어봄 
    * 아래 매뉴얼에 Fingerprint 확인에 대한 내용이 나와있음.
    * 동일하면 Y누르면 됨.
...
Retrieving key from https://download.docker.com/linux/centos/gpg
Importing GPG key 0x621E9F35:
 Userid     : "Docker Release (CE rpm) <docker@docker.com>"
 Fingerprint: 060a 61c5 1b55 8a7f 742b 77aa c52f eb6b 621e 9f35
 From       : https://download.docker.com/linux/centos/gpg
Is this ok [y/N]: y
Running transaction check
...

## install with script
*  매뉴얼 내용 추가함

$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh

## uninstall
* uninstall binary
$ sudo yum remove docker-ce
* To delete all images, containers, and volumes:
$ sudo rm -rf /var/lib/docker

## start the docker
sudo systemctl start docker

## run the docker with sudo
* add group docker
$ sudo grouped docker
* add user to group docker

$ sudo user mod -aG docker $USE
* logout and login
    * you will fail the docker command without logout
## configure Docker to start on boot
* enable
$sudo systemctl enable docker
* disabled

$sudo systemctl disable docker


# reference 
https://docs.docker.com/engine/installation/linux/docker-ce/centos/
https://docs.docker.com/engine/installation/linux/linux-postinstall/