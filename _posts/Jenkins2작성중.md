---
title: Jenkins 사용해서 배포하기 (Jenkins - 2편)
modified: 2021-08-02
author: Yo0oN
categories: [Project, festa]
tags: [DevOps, Project, Jenkins]
math: true
---

<hr>

이 글은 이전 글인 [CI란?(Jenkins - 1편)](https://yo0on.github.io/posts/Jenkins1편/)에서 이어지는 글로, 젠킨스를 적용하는 방법에 대해 설명하고 있습니다.    
현재 프로젝트에서 서버의 운영체제는 Debian을 이용합니다.

## 1. Jenkins 설치하기

> 아래의 내용은 이전 글에서 말했던 CI 사용에 필요한 것들 (ex.빌드툴, JDK 등..)이 설치되어있다는 가정 하에 진행합니다.    


- 파일을 받아온 후, 젠킨스를 설치합니다.    

```
wget https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get install jenkins
```
<br>
<br>

- 포트번호를 변경합니다. (기본 포트번호는 8080으로, 중복되는 어플리케이션이 없다면 그대로 진행해도 됩니다.)    
Debian의 경우 `/etc/default/jenkins`의 설정 파일에서 변경하면 됩니다.

> 만약 해당 경로가 존재하지 않는다면 `/etc/systemctl/jenkins`를 확인해 보는걸 추천드립니다.    

```
JENKINS_PORT="변경을 원하는 포트번호 입력"
```

<br>
<br>

- 방화벽 설정    

```
ufw allow 포트번호
```

![image](https://user-images.githubusercontent.com/53729311/128366908-e6916a3e-6d17-4ead-a962-bc17e2c53b3e.png)

참고로 GCP를 이용하고 있다면 VPC network > Firewall 항목에서 쉽게 설정할수도 있습니다.

<br>
<br>

- Jenkins 실행    

```
systemctl start jenkins
```



## 2. Jenkins 실행해보기




<hr>

**참고**
- [초보자를 위한 젠킨스 2 활용 가이드](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791161752143&orderClick=LEa&Kc=)
- [Jenkins doc](https://www.jenkins.io/doc/book/installing/)

**관련 프로젝트**
- [event-recommender-festa](https://github.com/f-lab-edu/event-recommender-festa)
