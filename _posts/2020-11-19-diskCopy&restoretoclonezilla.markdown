---
layout: post
title: "diskCopy&restore to clonezilla"
description: 클론질라 를 이용한 디스크 전체 카피 및 복구
date: 2020-11-19 09:10:00 +0900
categories: Clonezilla
---

디스크 완전 복제 프로그램인 클론질라 USB 만들기부터 백업및 복구까지 ~

https://clonezilla.org/downloads/download.php?branch=stable
요기 들어간다음 다운을 zip 형태로 받은후 USB나 어딘가에 압축푸시고~

![](/capture/diskCopy/usb.PNG)
utils 클릭
![](/capture/diskCopy/usb2.PNG)
자신의 맞는 운영체제 초이스!
![](/capture/diskCopy/usb3.PNG)
기다리거나 엔터키
![](/capture/diskCopy/usb4.PNG)
기다리거나 엔터키2
![](/capture/diskCopy/usb5.PNG)
기다리거나 엔터키3

이렇게 하시면 USB 만들기끝~

이제 본론으로 쫌 넘어가볼까요...

![](/capture/diskCopy/KakaoTalk_20201119_104134509.jpg)
클론질라로 부팅했을때의 첫화면 이며 <br>
제일 상단의 Clonezilla live (Default settings , VGA 800 X 600) 버튼을 누른다.

![](/capture/diskCopy/KakaoTalk_20201119_104134509_01.jpg)
로딩중..............
![](/capture/diskCopy/KakaoTalk_20201119_104134509_02.jpg)
로딩이 끝나면 이와같이 언어선택이 나온다.<br>
한국어가 있기는 하지만 개발자라면 영어로...?
![](/capture/diskCopy/KakaoTalk_20201119_104134509_03.jpg)
키보드 레이아웃은 표준으로
![](/capture/diskCopy/KakaoTalk_20201119_104134509_04.jpg)
기본적인 환경세팅은끝났다.<br>
이제 본격적으로 시작 Start_Clonezilla 선택
![](/capture/diskCopy/KakaoTalk_20201119_104134509_05.jpg)
device-image 선택!
![](/capture/diskCopy/KakaoTalk_20201119_104134509_06.jpg)
당연히 복사할 hard나 ssd는 연결했을테니 local_dev ㄱㄱ
![](/capture/diskCopy/KakaoTalk_20201119_104134509_07.jpg)
기다리다 보면 자동적으로 셋팅하고 Enter 키 버튼을 누르라한다.
![](/capture/diskCopy/KakaoTalk_20201119_104134509_08.jpg)
Enter 버튼누른후 또다시 조금기다리다보면 위와같은화면이나오며
Ctrl-C 를 누르라는 문구가나오면 누르세여~
![](/capture/diskCopy/KakaoTalk_20201119_104134509_09.jpg)
그담엔 image 복사할 hard 및 ssd 선택
![](/capture/diskCopy/KakaoTalk_20201119_104134509_10.jpg)
이미지 디렉토리 어쩌고 하라고하지만 그냥 가볍게 무시 Done 누르면된다.
필자는 모르고 생각없이 엔터키를 눌러 이상한화면으로 넘어간다...
![](/capture/diskCopy/KakaoTalk_20201119_104134509_11.jpg)
가볍게 NO 디렉토리 설정 화면일때 Done 누르면 이화면은 안뜹니다.
![](/capture/diskCopy/KakaoTalk_20201119_104134509_13.jpg)
Beginner 클릭 expert 는 옵션및 기타등등 세부적으로 셋팅할수있지만<br>
뭐굳이 할필요있나요?
![](/capture/diskCopy/KakaoTalk_20201119_104134509_14.jpg)
savadisk 선택
![](/capture/diskCopy/KakaoTalk_20201119_104134509_15.jpg)
이미지명 설정 default 값이 있으니 편하신대로~
![](/capture/diskCopy/KakaoTalk_20201119_104134509_16.jpg)
복사할 disk 선택
![](/capture/diskCopy/KakaoTalk_20201119_104134509_17.jpg)
image 만들때의 뭐 짜잘한설정....
![](/capture/diskCopy/KakaoTalk_20201119_104134509_18.jpg)
image 만들때의 뭐 짜잘한설정....2
![](/capture/diskCopy/KakaoTalk_20201119_104134509_19.jpg)
image 만들때의 뭐 짜잘한설정....3
![](/capture/diskCopy/KakaoTalk_20201119_104134509_20.jpg)
image 만들때의 뭐 짜잘한설정....4
![](/capture/diskCopy/KakaoTalk_20201119_104134509_21.jpg)
image 만들때의 뭐 짜잘한설정....5
![](/capture/diskCopy/KakaoTalk_20201119_104134509_22.jpg)
image 만들때의 뭐 짜잘한설정....6
까지 그냥 생각없이 Enter 키만 죽어라누르다보면 약간의 로딩과 한번더 Enter 버튼을 누르라는 문구가 나옵니다.
![](/capture/diskCopy/KakaoTalk_20201119_104134509_23.jpg)
partition 체크후 진행할꺼냐라는 질문 ( 당연히 Y!!!)
![](/capture/diskCopy/KakaoTalk_20201119_104134509_24.jpg)
image 만드는중~
![](/capture/diskCopy/KakaoTalk_20201119_104134509_25.jpg)
완료했답니다~ Enter 키 누르세여~
![](/capture/diskCopy/KakaoTalk_20201119_104134509_26.jpg)
power off 후 image 복사가 잘되었나 체크~!

복구 방법은

![](/capture/diskCopy/KakaoTalk_20201119_104134509_13.jpg)
여기까지는 동일하게 진행

![](/capture/diskCopy/aaaa.PNG)<br>
여기에서 restore disk 하신다음 진행하시면됩니다~
