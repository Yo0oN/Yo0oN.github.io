---
layout: post
title: Network 01. Web과 WAS?
modified: 2020-06-30
author: Yo0oN
categories: [Network, Web]
tags: [Network, web]
comments: true
published : true
---

* Table of Contents
{:toc}

내용에서 잘못된 점이 있다면 댓글을 남겨주세요.

## 1. Web 서버와 WAS

<cite>**Web 서버**</cite>는 정적인 컨텐츠(HTML, CSS, JS)를 제공해주는 서버로, 사용자가 누구이던 정해진 요청에 정해진 응답을 해주는 서버이다.

그래서 내가 언제 어디서나 A라는 것을 Web 서버에 요청하면 서버는 A로 응답해준다.

내가 아닌 다른 사람이, 다른곳에서 요청해도 마찬가지다.

<br>

반대로 <cite>**WAS (Web Application Server)**</cite>는 동적인 컨텐츠를 제공해주는 서버이다.

동적인 컨텐츠는 코드(ex.JSP)를 포함해서 누가 언제, 어떻게 요청했는지에 따라 응답해주는 것이 달라진다.

요청하는 상태에 따라 응답해주는 것이 달라지기 때문에 서버는 미리 HTML문장을 만들어 놓지 않고 동적 컨텐츠에 대한 요청이 들어오면 그때마다 HTML 문장을 만들어낸다.

요청에 따라 응답을 다르게 할 수 있는 이유는 페이지 내부에는 상황에 따라 HTML 문장을 만들어 주는 코드(JSP, PHP, Node.js 등등..)가 있기 때문이다.

그러면 정말 그런지 사이트에 들어가서 확인해보자.

<br>

마이페이지는 나만이 볼 수 있고, 사용자에 따라 다른 화면을 보여주는 동적페이지이다.

![텀블벅](/images/posts/Network/01.webWAS/webwas01.jpg "텀블벅 마이페이지")

그러면 개발자도구나 소스보기를 이용하여 이 화면이 어떻게 작성되었는지, 어떤 코드가 이 페이지의 HTML들을 만들어 주고 있는지 살펴보자.

![텀블벅](/images/posts/Network/01.webWAS/webwas02.jpg "텀블벅 마이페이지2")

사진에는 초반부분만 있지만 아래의 다른 부분을 보아도 HTML 문장을 만들어 주는 코드는 보이지 않는다.

모두 만들어진 문장들만 들어있다.

HTML을 만들어 주는 코드들은 어디 있을까? WAS는 어떻게 동적인 컨텐츠를 제공해주고 있을까?

<hr>

## 2. WAS의 동적 컨텐츠 처리

브라우저(크롬, 엣지, 사파리 등등..)는 정적 콘텐츠인 HTML, CSS, JS만 해석을 할 수 있다.

그래서 동적 컨텐츠인 HTML을 만들어주는 코드들은 브라우저가 읽을 수 없기 때문에, 브라우저는 알아서 코드를 읽어다가 페이지를 만들 수 없다.

이때 WAS는 동적 컨텐츠 요청이 들어오면 코드들을 읽어 정적 컨텐츠로 바꿔준다.

요청을 보고 사용자에 맞게 코드로 HTML을 만들어서 정적 컨텐츠로 만든 후 정적인 콘텐츠로 응답을 해주는 것이다.

<br>

![WAS](/images/posts/Network/01.webWAS/webwas03.png "WAS 구조")

사진처럼 WAS 내부에는 웹서버와 웹 컨테이너(=서블릿 컨테이너 = 컨테이너)가 들어있는데

웹 컨테이너는 .jsp파일을 Servlet으로 변환하여 컴파일한 후 동적컨텐츠를 정적컨텐츠로 바꿔서 웹 서버에게 전달해준다.

그래서 사용자마다 요청에 대한 응답을 다르게 해줄 수 있고, 동적 컨텐츠를 제공해 준다는 뜻이다.

대표적인 WAS로는 Tomcat, JBoss, WebLogic, Jetty 등이, Web에는 Apache, Nginx, IIS 등이 있다.

<hr>

### 2-1. WAS의 동적 컨텐츠 처리 순서

1. 웹서버에 동적 요청이 오면 웹 컨테이너가 해당 요청을 처리한다.
2. 웹 컨테이너는 설정이 적혀있는 web.xml을 참조하여 스레드를 생성하고 httpServletRequest와 httpServletResponse 객체를 생성하여 전달한다.
3. 웹 컨테이너는 서블릿을 호출한다.
4. 호출된 서블릿의 작업을 담당하게된 2번의 스레드는 doPost() 또는 doGet()을 호출한다.
5. 호출된 doPost(), doGet() 메소드는 생성된 동적 페이지를 Response 객체에 담아 웹 컨테이너에 전달한다.
6. 웹 컨테이너는 전달 받은 Response 객체를 HTTPResponse 형태로 바꿔 웹 서버에 전달하고, 생성되었던 스레드를 종료한다.
7. 생성되었던 httpServletRequest, httpServletResponse 객체를 소멸한다.


