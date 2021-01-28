---
layout: post
title: "https & nginx settings"
description: https 인증서 발급 및 적용 + nginx
date: 2021-01-27 09:10:00 +0900
categories: nginx https letsencrypt certbot crontab
---

HTTPS 적용하기!!

step1<br>
CentOS 설치 (CentOS 7 기준)

```
sudo yum install epel-release
```

Ubuntu 설치 (18.04 LTS 기준)

```
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository universe
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
```

step2<br>
Certbot 설치

CentOS

```
sudo yum install certbot
```

Ubuntu

```
apt-get install certbot
```

여기 까지 완료하면 기본적으로 https 발급을 위한 준비 끝 ~

나같은 경우에는 ubuntu 환경에 nginx 를 이용하여 https 를 구성하였다.

step3<br>
인증서 발급및 url 확인

```
sudo certbot certonly --manual --email {email}-d "{domain}"
여기서 유의할점은 밑에 조금더 세팅이 있을예정인대 사진의 마지막 줄에도 보이다 시피
Preess Enter to Continue 즉 엔터를 누르라는건대 엔터를 누르게 대면 바로 유효성검사를 시작하니 셋팅을 다 마친다음에 눌러야된다.
```

![](/capture/https/https.JPG)

```
이런식으로 letsencrypt 에서 입력한 도메인의 유효성을 검사하는 테스트가 나오게된다
영어로 이런저런 쏼라쏼라가 있지만 간단하게 요약을 한다면
http://[도메인]/.well-known/acme-challenge/XFWbgceOCx-3NZc36uRQTtAclpZv9i-yhDyYnhkPR5s5s <-- 이URL 에 접속을하였을때
XFWbgceOCx-3NZc36uRQTtAclpZv9i-yhDyYnhkPR5s.lLIPvOSu22UsRTUocW42u_4Nw4e1n4etHwV71QK3foc 이문구가 뜨면 인증이 완료된다는뜻이다.

```

step4<br>
이제 nginx 설정만질 차례<br>
![](/capture/https/https2.JPG)

```
location에 이렇게 추가 ^~ 이거표시는 패턴이 일치하면 다른패턴 탐색금지인대
왜하는지 모르겠지만 그냥 따라함
```

step5<br>
/usr/share/nginx/html 에 폴더및 파일을 만든다.

```
mkdir .well-known
cd .well-known
mkdir acme-challenge
cd acme-challenge
vi XFWbgceOCx-3NZc36uRQTtAclpZv9i-yhDyYnhkPR5s5s
XFWbgceOCx-3NZc36uRQTtAclpZv9i-yhDyYnhkPR5s.lLIPvOSu22UsRTUocW42u_4Nw4e1n4etHwV71QK3foc 추가한다음 저장하고 나온다.
```

step6<br>
이제 url 실행해볼차례

```
주소창에 http://[도메인]/.well-known/acme-challenge/XFWbgceOCx-3NZc36uRQTtAclpZv9i-yhDyYnhkPR5s5s
입력했을때의 XFWbgceOCx-3NZc36uRQTtAclpZv9i-yhDyYnhkPR5s.가 뜨는지확인 해본다
```

step7<br>
인증받으러 ㄱㄱㄱ

```
값이 표출되는걸 확인후 step3의 엔터버튼을눌러 유효성 검사를 진행한다.
만약 유효성검사가 잘끝났다면 아래와같이 완료 문구가 뜰것임
```

![](/capture/https/https3.JPG)

```
이제 /etc/letsencrypt/live/도메인 <-- 까지 들어가게되면
README
cert.pem
chain.pem
fullchain.pem
privkey.pem
이렇게 파일이 구성되어있을거임
```

step8<br>
자이제 nginx 에 적용을 하러 갑시다.

```
일단 docker-compose 에 volume 을 잡는다
- ./config/ssl:/etc/ssl 이런식으로 볼륨을 잡았다.
혹여나 nginx 볼륨을 모른다면 검색해보시길..
그다음 nginx.conf 설정을 한다. 아래의 사진참고
```

![](/capture/https/https4.JPG)

```
https 인증서를 등록해주는 conf라고 보면된다.
여기까지 설정한다음 docker container 를 restart 하거나
nginx 를 restart 하게된다음 https 로 접속을 시도하게 되면 완료가된걸 볼수있다.
혹시나 https 적용이 안된다면 캐시를 지우고 해보고 그래도 안된다면 잘못설정한 가능성이크다.
```

lastStep<br>
드디어 마지막 https 인증은 90일이므로 일정 주기마다 갱신을 해줘야된다.

```
자동갱신을 위한 crontab 이용하기
대부분 주기적으로 shell script 를 이용하여
    *         *          *           *           *
분(0-59)  시간(0-23)  일(1-31)    월(1-12)    요일(0-7)
순으로 진행하며 활용법은 찾아보세요...예제가 많아요

명령어확인
crontab -e
crontab 실행여부확인 명령어
tail -f /var/log/cron 저는 이게 제일편하더라구요
끝~
```
