---
layout: post
title: "other ssh connections"
description: 서로다른 SSH 연결
date: 2020-07-11 13:10:00 +0900
categories: SSH DOCKER
---

두개의 컨테이너 간의 SSH 연결하여 shell 파일을 실행하고자 하였다.
그러기위해 선행 작업으로는 docker container 2개를 생성한다.

```
sudo docker run -itd --name test1 ubuntu:latest /bin/bash

sudo docker run -itd --name test2 ubuntu:latest /bin/bash
```

필요한 만큼의 docker container 생성후 각각의 생성한 컨테이너에 접속한다.

```
sudo docker exec -it test1 /bin/bash

sudo docker exec -it test2 /bin/bash
```

접속후 아래의 명령어를 통해 SSH 연결을 위해 필요한 툴 들을 받는다.

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install openssh-server
```

툴을 받은뒤 본격적으로 원격SSH 접속을 위한 공개키와 개인키를 만든다.
이명령어같은경우 상호간의 접속이 필요한 양쪽모두 명령어를 입력해야한다.

```
rm -f /etc/ssh/ssh_host_dsa_key /etc/ssh/ssh_host_rsa_key /root/.ssh/id_rsa
ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key
ssh-keygen -q -N "" -t rsa -f /root/.ssh/id_rsa
chmod 600 /root/.ssh/authorized_keys
```

입력후 접속을 위해 필요한 public key 를 출력한뒤 복사한다.
컨테이너 접속후 cat/root/.ssh/authorized_keys 명령어를 입력한다.

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDV9dO...
이와비슷한 public key 출력
```

위의 public key 를 복사하여 SSH 접속을 하려는 컨테이너에 /root/.ssh/authorized_keys 경로에
추가 하게되면 이제부터는 명령어를 통해 자유롭게 컨테이너 이동이 가능해진다.

```
test1 컨테이너에 접속한다음 [ssh test2] <-- 명령어를 통해 자유롭게 컨테이너 이동 가능
```

나의경우 컨테이너에서의 shell 실행을 원했기에 나와같은 문제를 해결하고싶은 경우

```
ssh root@{container name} 'sh /path'
```

끝으로 SSH 연결같은경우 서칭을 통해 쉽게 누구든 찾을수있으나,
기록을 남겨 똑같은 상황이 생길경우 간편하게 찾아 해결하고싶어 글남겨봄...
