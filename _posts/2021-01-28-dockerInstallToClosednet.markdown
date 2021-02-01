---
layout: post
title: "docker install to closednet"
description: 폐쇄망에서의Docker 설치
date: 2021-01-28 13:10:00 +0900
categories: SSH DOCKER CentOS7
---

이번엔 폐쇄망에서의 Docker 구축을 해볼일이생겼다.

1.wget 설치

```
  yum install wget & sudo yum install wget
```

2.버젼의 맞는 파일 다운로드

```
wget --recursive --no-parent http://ftp.kaist.ac.kr/CentOS/7/extras/x86_64/
  --recursive (폴더 하위에 있는 파일들 모두 다운로드)
  --no-parent (상위폴더 무시 다운로드 X)
```

3.다운로드뒤 폐쇄망으로 파일 이전

```
나같은경우에는 SCP 를 이용하였다.
scp -r ./ftp.kaist.ac.kr/CentOS/7/extras/x86_64/ serverName@0.0.0.0:/설치할경로
mv x86_64 kaistrepo
```

4.폐쇄망 작업

```
su
cd /etc/yum.repos.d
vi kaist.repo
그다음 아래의사진과같이 입력한다.
```

![](/capture/closednetDocker/closedDocker.JPG)

5.yum repo reload

```
yum clean all
yum repolist all
```

6.설치 확인
![](/capture/closednetDocker/closedDocker2.JPG)

```
캡쳐를 올렸는대 너무 작아서 다시찍기귀찮아 설명으로함
kaist-repo    kaistrepo enabled:448
본인은 마지막에 enabled 만보고 다되었다고 생각했으나 뒤에 숫자가0일경우에는 제대로 되지않는것이니 숫자도 봐야댐
```

7.docker 설치
yum install -y docker

```
하지만 난바로 설치가 되지 않음.....
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running? 이러한 오류가 떳다..그래서 검색을해보니
systemctl enable docker
systemctl start docker
해결~
이제 폐쇄망에서의 docker 가 가능해졌다~
```

```
2021-02-01 추가
다른 곳의 테스트중 root 권한 일때만 docker 명령어가 실행이 되었다.
#Debian
sudo usermod -a -G docker $USER

#Centos
sudo groupadd docker
sudo chown root:docker /var/run/docker.sock
sudo usermod -aG docker $USER
```
