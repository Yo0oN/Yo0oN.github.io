---
title: Jenkins? CI? CD?
modified: 2021-07-24
author: Yo0oN
categories: [Project, Festa]
tags: [Project]
math: true
---

<hr>

진행중인 프로젝트에서 대부분의 기능을 완성해가고, 서버에 배포하는 작업을 해보기로 하였습니다.    
그러던 중 회사에서 진행했던 프로젝트에서 Jenkins라는 빌드 자동화 툴을 이용하는것이 생각나 이를 이용해보기로 했습니다.

## 1. Jenkins?

Jenkins는 소프트웨어 구축, 테스트, 전달, 배포 등등..여러 작업들을 자동화해주는 도구입니다.



### CI(Continuous Integration)란?

Continuous Integration이란 지속적인 통합이라는 뜻입니다.
개발자들이 코드를 짠 후 Git과 같은 버전관리 툴에 내용을 올리는데, 배포하기 위해서는 여러 내용을 하나로 받아 빌드해야합니다.
하지만, 이런 작업을 사람이 직접 하게된다면 오류가 날 수도 있고, 변경사항이 있을 때마다 같은 작업을 반복하는 일은 귀찮은 작업입니다.
그래서 정기적으로 코드를 통합하는 일을 알아서 해주는 프로그램을 CI tool이라고 부르게 되었습니다.
